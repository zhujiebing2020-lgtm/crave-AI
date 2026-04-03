# CreviaTech 购物意愿埋点：事件定义详表 (移动端适配版)

**版本：** v2.0 (Mobile Optimized)  
**目标：** 适配移动端交互特性（点击、长按、滑动），量化用户购买意向，赋能 AI 实时意图预测。

---

## 核心事件定义清单

| 所属组件 (Component) | 触发时机 (Mobile Trigger) | 事件名称 (eventName) | 具体上报字段 (Fields) |
| :--- | :--- | :--- | :--- |
| **Buy Now 按钮** | 按钮在屏幕可见区域停留 > 1s | `buy_button_dwell` | `product_id`, `dwell_duration`, `hesitation_flag: true` |
| **Buy Now 按钮** | 用户长按按钮 | `buy_button_long_press` | `product_id`, `press_duration`, `timestamp` |
| **Buy Now 按钮** | 3s 内连续点击 (Tap) 按钮 > 2次 | `buy_button_multi_tap` | `product_id`, `tap_count`, `time_between_taps` |
| **购物车组件** | 点击 (Tap) 加入购物车成功 | `cart_add` | `product_id`, `quantity`, `price`, `currency` |
| **购物车组件** | 点击 (Tap) 从购物车移除商品 | `cart_remove` | `product_id`, `item_index`, `reason_category` |
| **购物车组件** | 修改商品购买数量 | `cart_quantity_change` | `product_id`, `before_qty`, `after_qty` |
| **结账流程** | 点击 (Tap) “结账”按钮跳转页面 | `checkout_start` | `cart_total_value`, `item_count`, `currency` |
| **结账表单** | 输入框获得焦点 (Focus/Keyboard Open) | `checkout_form_focus` | `field_name` (如 address, phone), `focus_order` |
| **结账表单** | 输入内容校验失败 (Validation Error) | `checkout_form_error` | `field_name`, `error_type`, `error_msg` |
| **结账流程** | 离开结账页且未完成支付 (如 App 后台/关闭) | `checkout_abandon` | `last_filled_field`, `abandon_reason`, `cart_value` |

---

## 移动端上报通用公共字段 (Common Fields)

*所有事件均需携带以下字段，以便进行多端归因分析：*

*   **`session_id`**: 当前会话唯一标识（单次访问内保持不变）。
*   **`user_id`**: 用户 ID / 游客 ID。
*   **`os_type`**: 操作系统 (`iOS` / `Android`)。
*   **`os_version`**: 系统版本号。
*   **`network_type`**: 网络环境 (`WiFi` / `5G` / `4G`)。
*   **`screen_size`**: 屏幕分辨率 (如 `1170x2532`)。
*   **`timestamp`**: 事件触发的精确时间戳。

---
**日期：** 2026-03-16  
**版本：** v2.0 (Mobile Optimized)
