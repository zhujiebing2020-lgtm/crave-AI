# CreviaTech 购物意愿埋点：移动端全量事件定义详表 (Mobile Optimized)

**版本：** v2.0 (Mobile Optimized)  
**目标：** 适配移动端/App 手势交互特性，量化用户在小屏幕上的感官偏好与购买意愿。

---

## A. 故事交互埋点 (Mobile Story Interaction)

| 所属组件 | 触发时机 (Mobile Trigger) | 事件名称 (eventName) | 具体上报字段 (Fields) |
| :--- | :--- | :--- | :--- |
| **故事卡片** | 故事卡片在屏幕停留 > 1 秒 | `story_card_dwell` | `story_id`, `dwell_time`, `viewport_position` |
| **故事卡片** | 用户长按故事卡片 | `story_card_long_press` | `story_id`, `press_duration`, `timestamp` |
| **故事卡片** | 用户点击故事卡片进入详情 | `story_card_tap` | `story_id`, `source_page`, `timestamp` |
| **故事详情** | 用户重复点击查看同一故事 | `story_rewatch` | `story_id`, `view_count`, `time_since_last_view` |
| **故事详情** | 用户在故事详情页单指滑动 | `story_content_swipe` | `story_id`, `swipe_direction`, `swipe_velocity` |
| **故事文本** | 用户长按/高亮故事文本 | `story_text_highlight` | `story_id`, `highlighted_text`, `highlight_duration` |

---

## B. 产品交互埋点 (Mobile Product Interaction)

| 所属组件 | 触发时机 (Mobile Trigger) | 事件名称 (eventName) | 具体上报字段 (Fields) |
| :--- | :--- | :--- | :--- |
| **产品卡片** | 产品卡片在屏幕停留 > 1 秒 | `product_card_dwell` | `product_id`, `dwell_time`, `timestamp` |
| **产品卡片** | 用户长按产品卡片 | `product_card_long_press` | `product_id`, `press_duration`, `haptic_feedback_flag` |
| **产品图片** | 用户双指缩放 (Pinch) 产品图像 | `product_image_zoom` | `product_id`, `max_zoom_scale`, `zoom_duration` |
| **产品轮播** | 用户在产品轮播中左右滑动 | `product_carousel_swipe` | `product_id_from`, `product_id_to`, `swipe_index` |
| **产品信息** | 用户点击查看价格/规格信息 | `product_info_tap` | `product_id`, `info_type` (price/size), `timestamp` |
| **产品标签** | 用户点击产品标签 (如 #Car Sex) | `product_tag_tap` | `product_id`, `tag_name`, `timestamp` |
| **产品详情** | 用户在产品详情页快速滚动 | `product_detail_flick` | `product_id`, `flick_velocity`, `scroll_depth` |

---

## D. 感官反应埋点 (Mobile Sensory Reaction)

| 所属组件 | 触发时机 (Mobile Trigger) | 事件名称 (eventName) | 具体上报字段 (Fields) |
| :--- | :--- | :--- | :--- |
| **话题标签** | 用户点击话题标签 | `hashtag_tap` | `tag_name`, `tag_category`, `timestamp` |
| **标签区域** | 用户在标签列表滑动浏览 | `hashtag_list_scroll` | `tags_viewed_count`, `scroll_duration`, `user_segment` |
| **女性专栏** | 用户点击“女性专栏”文章 | `article_tap` | `article_id`, `article_title`, `article_category` |
| **专栏文章** | 用户阅读文章的时间 (停留时长) | `article_dwell_time` | `article_id`, `read_time`, `max_scroll_depth` |
| **App 演示** | 用户滑动查看 App 演示步骤 | `app_flow_swipe` | `step_number`, `step_name`, `view_duration` |
| **App 演示** | 用户点击 App 演示中的交互点 | `app_flow_tap` | `step_number`, `action_name`, `next_step` |
| **订阅组件** | 用户点击订阅并提交 | `newsletter_submit` | `email_domain`, `signup_source`, `timestamp` |
| **Ask AI** | 用户点击打开 Ask AI 浮窗 | `ai_chat_tap` | `chat_session_id`, `entry_point`, `timestamp` |
| **Ask AI** | 用户在虚拟键盘输入并发送消息 | `ai_chat_message` | `chat_session_id`, `message_length`, `input_method` |
| **Ask AI** | 用户保持聊天窗口活跃时长 | `ai_chat_active_time` | `chat_session_id`, `message_count`, `active_duration` |

---

## E. 移动端通用环境字段 (Mobile Common Fields)

*所有移动端事件均需携带以下字段，以便进行多端归因分析：*

*   **`session_id`**: 当前会话唯一标识。
*   **`user_id`**: 用户 ID / 游客 ID。
*   **`os_type`**: 操作系统 (`iOS` / `Android`)。
*   **`os_version`**: 系统版本号。
*   **`network_type`**: 网络环境 (`WiFi` / `5G` / `4G`)。
*   **`screen_size`**: 屏幕分辨率 (如 `1170x2532`)。
*   **`timestamp`**: 事件触发的精确时间戳。

---
**日期：** 2026-03-16  
**版本：** v2.0 (Mobile Optimized)
