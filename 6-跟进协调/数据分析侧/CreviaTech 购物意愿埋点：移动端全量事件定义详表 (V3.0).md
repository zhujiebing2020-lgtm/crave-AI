# CreviaTech 购物意愿埋点：移动端全量事件定义详表 (V3.0)

**版本：** v3.0 (Mobile Optimized & Refuted)  
**目标：** 适配移动端生理交互（点击、长按、滑动、缩放），剔除误触噪声，量化真实购买意图。

---

## 1. 核心事件定义清单 (Core Event Specs)

| 所属组件 (Component) | 触发时机 (Mobile Trigger) | 事件名称 (eventName) | 具体上报字段 (Fields) | 业务价值 (Insight) |
| :--- | :--- | :--- | :--- | :--- |
| **Buy Now 按钮** | 按钮在屏幕中心区域停留 > 2s | `buy_button_dwell` | `product_id`, `dwell_duration`, `viewport_pos` | **潜在意向**：用户在浏览时被吸引，但未采取行动。 |
| **Buy Now 按钮** | 用户长按按钮且无位移 | `buy_button_long_press` | `product_id`, `press_duration`, `is_intentional` | **深度审视**：用户在进行心理博弈或寻找更多信息。 |
| **Buy Now 按钮** | 3s 内连续点击 > 2次且有反馈 | `buy_button_multi_tap` | `product_id`, `tap_count`, `has_ui_feedback` | **冲动购买**：极高意向信号（需区分系统响应慢导致的焦虑）。 |
| **产品图片** | 用户双指缩放产品图 > 3s | `product_image_zoom` | `product_id`, `zoom_scale`, `zoom_duration` | **细节审视**：对产品材质、形态、细节的极度关注。 |
| **产品详情页** | 用户慢速滚动 (Velocity < 0.5) | `detail_slow_scroll` | `product_id`, `scroll_depth`, `scroll_velocity` | **有效阅读**：用户在认真研读产品文案或评价。 |
| **结账表单** | 输入框获得焦点且保持 > 5s | `checkout_form_focus` | `field_name` (如 address, phone), `focus_duration` | **隐私顾虑**：用户在犹豫是否要填写敏感隐私信息。 |
| **结账表单** | 输入内容校验失败报错 | `checkout_form_error` | `field_name`, `error_type`, `error_msg` | **技术摩擦**：导致用户流失的最直接原因。 |
| **结账流程** | 用户在结账页截屏 | `checkout_screenshot` | `current_step`, `timestamp`, `cart_value` | **极高意向**：保存隐私信息或寻求他人意见的物理证据。 |
| **结账流程** | 离开结账页且未完成支付 | `checkout_abandon` | `last_filled_field`, `abandon_reason`, `visibility_state` | **流失归因**：识别环境干扰或最终决策放弃。 |

---

## 2. 移动端“隐藏意图”高级埋点 (Advanced Intent)

| 所属组件 | 触发时机 | 事件名称 (eventName) | 具体上报字段 (Fields) | 业务价值 |
| :--- | :--- | :--- | :--- | :--- |
| **全局** | 用户从竖屏切换为横屏 | `screen_orientation_change` | `from_orientation`, `to_orientation`, `page_url` | **深度沉浸**：用户想在大屏下完整观看视频或故事。 |
| **全局** | 页面可见性改变 (切出后台) | `visibility_change` | `is_hidden`, `hidden_duration`, `current_step` | **环境干扰/比价**：识别用户是否因外部消息或比价流失。 |
| **全局** | 用户摇晃手机 (加速计触发) | `user_shake_detected` | `shake_intensity`, `page_url`, `timestamp` | **操作焦虑**：用户在遇到卡顿或支付失败时的物理反应。 |

---

## 3. 移动端上报通用公共字段 (Mobile Common Fields)

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
**版本：** v3.0 (Mobile Optimized & Refuted)
