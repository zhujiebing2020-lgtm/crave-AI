# CreviaTech 购物意愿埋点：全量事件定义详表

**版本：** v1.0  
**目标：** 通过全方位的微观交互追踪，构建用户意图画像，赋能 AI 深度路径分析。

---

## A. 故事交互埋点 (Story Interaction)

| 所属组件 | 触发时机 | 事件名称 (eventName) | 具体上报字段 (Fields) |
| :--- | :--- | :--- | :--- |
| **故事卡片** | 用户悬停故事卡片 > 1 秒 | `story_card_hover` | `story_id`, `hover_duration`, `timestamp` |
| **故事卡片** | 用户在故事卡片停留 > 3 秒 | `story_card_dwell` | `story_id`, `dwell_time`, `user_segment` |
| **故事卡片** | 用户点击故事卡片进入详情 | `story_card_click` | `story_id`, `source_page`, `timestamp` |
| **故事详情** | 用户重复查看同一故事 | `story_rewatch` | `story_id`, `view_count`, `time_between_views` |
| **故事详情** | 用户在故事详情页滚动 | `story_content_scroll` | `story_id`, `scroll_depth`, `scroll_speed` |
| **故事文本** | 用户长按/高亮故事文本 | `story_text_highlight` | `story_id`, `highlighted_text`, `highlight_duration` |

---

## B. 产品交互埋点 (Product Interaction)

| 所属组件 | 触发时机 | 事件名称 (eventName) | 具体上报字段 (Fields) |
| :--- | :--- | :--- | :--- |
| **产品卡片** | 用户悬停产品卡片 > 1 秒 | `product_card_hover` | `product_id`, `hover_duration`, `timestamp` |
| **产品卡片** | 用户长按产品卡片 > 2 秒 | `product_card_long_press` | `product_id`, `press_duration`, `device_type` |
| **产品图片** | 用户放大产品图像 | `product_image_zoom` | `product_id`, `zoom_level`, `zoom_duration` |
| **产品轮播** | 用户在产品轮播中滑动 | `product_carousel_swipe` | `product_id_from`, `product_id_to`, `swipe_count` |
| **产品信息** | 用户查看价格信息 | `product_price_view` | `product_id`, `original_price`, `discount_price` |
| **产品标签** | 用户点击产品标签 (如 #Car Sex) | `product_tag_click` | `product_id`, `tag_name`, `timestamp` |
| **产品详情** | 用户在产品详情页滚动 | `product_detail_scroll` | `product_id`, `scroll_depth`, `scroll_speed` |

---

## D. 感官反应埋点 (Sensory Reaction)

| 所属组件 | 触发时机 | 事件名称 (eventName) | 具体上报字段 (Fields) |
| :--- | :--- | :--- | :--- |
| **话题标签** | 用户点击话题标签 | `hashtag_click` | `tag_name`, `tag_category`, `timestamp` |
| **标签区域** | 用户在标签区域停留 > 3 秒 | `hashtag_dwell` | `tag_count_viewed`, `dwell_time`, `user_segment` |
| **女性专栏** | 用户点击“女性专栏”文章 | `article_click` | `article_id`, `article_title`, `article_category` |
| **专栏文章** | 用户阅读文章的时间 | `article_read_time` | `article_id`, `read_time`, `scroll_depth` |
| **App 演示** | 用户查看 CRAVE+ App 演示的某一步 | `app_flow_step_view` | `step_number`, `step_name`, `view_duration` |
| **App 演示** | 用户点击 App 演示的某一步 | `app_flow_step_click` | `step_number`, `next_action` |
| **订阅组件** | 用户订阅邮件 | `newsletter_signup` | `email_domain`, `signup_source`, `timestamp` |
| **Ask AI** | 用户打开 Ask AI 浮窗 | `ai_chat_open` | `chat_session_id`, `page_context`, `timestamp` |
| **Ask AI** | 用户在 AI 聊天中发送消息 | `ai_chat_message` | `chat_session_id`, `message_content`, `message_type` |
| **Ask AI** | 用户与 AI 聊天的时长 | `ai_chat_duration` | `chat_session_id`, `message_count`, `chat_duration` |

---

## E. 用户会话埋点 (User Session)

| 所属组件 | 触发时机 | 事件名称 (eventName) | 具体上报字段 (Fields) |
| :--- | :--- | :--- | :--- |
| **全局** | 用户开始新会话 | `session_start` | `session_id`, `device_type`, `traffic_source`, `user_segment` |
| **全局** | 用户结束会话 | `session_end` | `session_id`, `session_duration`, `last_action`, `exit_reason` |
| **全局** | 用户访问页面的顺序 | `page_sequence` | `session_id`, `page_sequence`, `time_on_each_page` |
| **页面** | 用户在页面上的滚动深度 | `scroll_depth_tracking` | `page_url`, `scroll_percentage`, `max_scroll_depth` |
| **页面** | 用户在页面停留的时间 | `time_on_page` | `page_url`, `time_on_page`, `user_segment` |

---
**日期：** 2026-03-16  
**制作人：** Manus AI 团队
