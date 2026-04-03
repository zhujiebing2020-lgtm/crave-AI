# CreviaTech 购物意愿埋点：事件定义详表

**目标：** 通过微观交互追踪量化用户购买意向，赋能 AI 实时意图预测。

---

## 核心事件定义清单

| 所属组件 (Component) | 触发时机 (Trigger) | 事件名称 (eventName) | 具体上报字段 (Fields) |
| :--- | :--- | :--- | :--- |
| **Buy Now 按钮** | 鼠标悬停按钮时长 > 1s | `buy_button_hover` | `product_id`, `hover_duration`, `hesitation_flag: true` |
| **Buy Now 按钮** | 3s 内连续点击按钮 > 2次 | `buy_button_multi_click` | `product_id`, `click_count`, `time_between_clicks` |
| **购物车组件** | 点击加入购物车成功 | `cart_add` | `product_id`, `quantity`, `price`, `currency` |
| **购物车组件** | 点击从购物车移除商品 | `cart_remove` | `product_id`, `item_index`, `reason_category` |
| **购物车组件** | 修改商品购买数量 | `cart_quantity_change` | `product_id`, `before_qty`, `after_qty` |
| **结账流程** | 点击“结账”按钮跳转页面 | `checkout_start` | `cart_total_value`, `item_count`, `currency` |
| **结账表单** | 表单输入框获得焦点 (Focus) | `checkout_form_focus` | `field_name` (如 address, phone), `focus_order` |
| **结账表单** | 输入内容校验失败 (Validation Error) | `checkout_form_error` | `field_name`, `error_type`, `error_msg` |
| **结账流程** | 离开结账页且未完成支付 | `checkout_abandon` | `last_filled_field`, `abandon_reason`, `cart_value` |

---

## 上报通用公共字段 (Common Fields)

*所有事件均需携带以下字段，以便后端进行路径还原：*

*   **`session_id`**: 当前会话唯一标识（单次访问内保持不变）。
*   **`user_id`**: 用户 ID（游客状态下可为空或生成临时 ID）。
*   **`page_url`**: 触发事件的当前页面 URL。
*   **`timestamp`**: 事件触发的具体 ISO 时间戳（如 `2026-03-16T10:00:00Z`）。
*   **`device_type`**: 设备类型（`mobile` / `desktop`）。

---
**日期：** 2026-03-16  
**版本：** v1.0
