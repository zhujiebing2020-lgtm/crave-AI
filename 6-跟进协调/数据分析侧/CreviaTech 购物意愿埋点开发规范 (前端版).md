# CreviaTech 购物意愿埋点开发规范 (前端版)

**版本：** v1.0  
**目标：** 通过追踪用户微观交互，量化“购买意愿”与“决策犹豫”，赋能 AI 意图预测。

---

## 1. 统一上报接口规范

前端应封装统一的 `trackEvent` 函数，确保所有埋点数据结构一致。

```typescript
/**
 * @param eventName 事件名称
 * @param params 业务参数
 */
function trackEvent(eventName: string, params: Record<string, any>) {
  const commonParams = {
    session_id: getSessionId(), // 当前会话唯一标识
    user_id: getUserId() || 'guest', // 已登录用户ID或游客标识
    page_url: window.location.href,
    referrer: document.referrer,
    timestamp: new Date().toISOString(),
    device_type: /Mobi|Android|iPhone/i.test(navigator.userAgent) ? 'mobile' : 'desktop',
    screen_resolution: `${window.screen.width}x${window.screen.height}`
  };

  const payload = { ...commonParams, ...params };
  
  // 建议使用 navigator.sendBeacon 以确保在页面跳转时数据不丢失
  if (navigator.sendBeacon) {
    navigator.sendBeacon('/api/v1/collect', JSON.stringify({ event: eventName, data: payload }));
  } else {
    fetch('/api/v1/collect', { method: 'POST', body: JSON.stringify({ event: eventName, data: payload }) });
  }
}
```

---

## 2. 核心埋点事件清单

### C. 购买意愿信号埋点 (Purchase Intent Signals)

| 事件名称 (eventName) | 触发条件 (Trigger) | 业务参数 (Params) | 埋点意义 |
| :--- | :--- | :--- | :--- |
| `buy_button_hover` | 鼠标悬停 "Buy Now" 按钮 > 1s | `product_id`, `hover_duration`, `hesitation_flag: true` | **识别犹豫**：用户在心理博弈。 |
| `buy_button_multi_click` | 3s 内连续点击按钮 > 2次 | `product_id`, `click_count`, `time_between_clicks` | **强意向**：用户极度渴望或操作急躁。 |
| `cart_add` | 点击加入购物车成功 | `product_id`, `quantity`, `price` | **确定意向**：进入实质转化。 |
| `cart_remove` | 从购物车移除商品 | `product_id`, `reason_category` | **流失预警**：用户在进行欲望清理。 |
| `cart_quantity_change` | 修改购物车商品数量 | `product_id`, `before_qty`, `after_qty` | **决策波动**：对购买量产生犹豫。 |
| `checkout_start` | 点击结账按钮进入结账页 | `cart_total_value`, `item_count` | **高价值动作**：转化漏斗关键步。 |
| `checkout_form_focus` | 结账表单字段获得焦点 | `field_name`, `focus_order` | **决策审视**：用户在关注特定隐私项。 |
| `checkout_form_error` | 表单校验失败 | `field_name`, `error_type`, `error_msg` | **技术摩擦**：导致流失的核心原因。 |
| `checkout_abandon` | 离开结账页面 (未支付) | `last_filled_field`, `abandon_reason` | **流失归因**：识别最后一次摩擦点。 |

---

## 3. 代码实现逻辑示例

### 3.1 犹豫追踪 (Hover Logic)
```javascript
let hoverTimer = null;
let hoverStartTime = 0;

const btn = document.querySelector('.buy-now-btn');
btn.addEventListener('mouseenter', () => {
  hoverStartTime = Date.now();
  hoverTimer = setTimeout(() => {
    // 悬停超过1秒触发
    trackEvent('buy_button_hover', {
      product_id: btn.dataset.productId,
      hover_duration: 1, // 已达标
      hesitation_flag: true
    });
  }, 1000);
});

btn.addEventListener('mouseleave', () => {
  clearTimeout(hoverTimer);
  const totalDuration = (Date.now() - hoverStartTime) / 1000;
  if (totalDuration > 1) {
    // 补报实际总时长
    trackEvent('buy_button_hover_complete', {
      product_id: btn.dataset.productId,
      total_duration: totalDuration.toFixed(2)
    });
  }
});
```

### 3.2 结账摩擦追踪 (Form Friction)
```javascript
// 监听结账表单的焦点流转
const fields = document.querySelectorAll('.checkout-input');
fields.forEach((field, index) => {
  field.addEventListener('focus', () => {
    trackEvent('checkout_form_focus', {
      field_name: field.name,
      focus_order: index + 1
    });
  });
  
  // 监听校验错误
  field.addEventListener('blur', () => {
    if (!field.validity.valid) {
      trackEvent('checkout_form_error', {
        field_name: field.name,
        error_type: field.validationMessage
      });
    }
  });
});
```

---

## 4. 开发注意事项 (QA Checklist)

1.  **数据脱敏**：严禁上报用户的具体输入内容（如真实姓名、地址、卡号），仅上报字段名称 (`field_name`)。
2.  **性能优化**：`hover` 等高频事件需做防抖/节流处理，避免阻塞主线程。
3.  **唯一标识**：确保 `session_id` 在单次会话内全局一致，方便后端进行路径还原。
4.  **离线补报**：如遇网络波动，建议将关键转化事件（如 `cart_add`）暂存至 `localStorage`，待网络恢复后补报。

---
**技术对接人：** [您的姓名/Manus]  
**日期：** 2026-03-16
