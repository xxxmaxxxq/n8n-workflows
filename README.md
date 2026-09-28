# n8n workflows

Коллекция моих автоматизаций на self-hosted n8n: приём и квалификация заявок,
контент-пайплайны, AI-агенты с Telegram-интерфейсом, работа с отзывами маркетплейсов.
Один JSON — один воркфлоу, импортируется в n8n как есть.

## Что здесь показано

- Сквозные пайплайны «вход → AI-обработка → выдача → эскалация человеку».
- LangChain-агенты n8n: tools, structured output parser, память диалога.
- Интеграции: Telegram, Google Sheets/Docs, Wildberries API, Airtable, Baserow, OpenAI, Anthropic, VK, Blotato.
- Ветвления, ожидания, повторные попытки и модерация негатива перед публикацией ответа.

## Воркфлоу

| Название | Файл | Узлов | Основные типы узлов |
|---|---|---|---|
| Angie, personal AI assistant with Telegram voice and text | [`angie-personal-ai-assistant-with-telegram-voice-and-text.json`](workflows/angie-personal-ai-assistant-with-telegram-voice-and-text.json) | 15 | agent, baserowTool, gmailTool, googleCalendarTool, if |
| Create vertical AI videos from web articles with OpenAI, Seedance and Blotato | [`create-vertical-ai-videos-from-web-articles-with-openai-seed.json`](workflows/create-vertical-ai-videos-from-web-articles-with-openai-seed.json) | 20 | agent, code, httpRequest, if, lmChatOpenAi |
| ДЕМО 1 — Заявки в Telegram + таблица + эскалация | [`demo-1-zayavki-v-telegram-tablica-eskalaciya.json`](workflows/demo-1-zayavki-v-telegram-tablica-eskalaciya.json) | 9 | code, googleSheets, if, respondToWebhook, telegram |
| ДЕМО 2 — Отзывы WB: ИИ-ответ с модерацией негатива | [`demo-2-otzyvy-wb-ii-otvet-s-moderaciey-negativa.json`](workflows/demo-2-otzyvy-wb-ii-otvet-s-moderaciey-negativa.json) | 9 | code, httpRequest, if, scheduleTrigger, splitOut |
| Generate AI viral videos with NanoBanana & VEO3, shared on socials via Blotato | [`generate-ai-viral-videos-with-nanobanana-veo3-shared-on-soci.json`](workflows/generate-ai-viral-videos-with-nanobanana-veo3-shared-on-soci.json) | 47 | agent, blotato, code, googleDrive, googleSheets |
| Multi-agent SEO optimized blog writing system with hyperlinks for E-Commmerce | [`multi-agent-seo-optimized-blog-writing-system-with-hyperlink.json`](workflows/multi-agent-seo-optimized-blog-writing-system-with-hyperlink.json) | 75 | agent, aggregate, airtable, code, googleDocs |
| My 1 workflow | [`my-1-workflow.json`](workflows/my-1-workflow.json) | 6 | code, openAi, telegram, telegramTrigger |
| PP_work — 2 пост Дзен | [`pp-work-2-post-dzen.json`](workflows/pp-work-2-post-dzen.json) | 31 | code, httpRequest, if, merge, openAi |
| PP_work — 3. Maintenance metrics + rewrites + crosspost | [`pp-work-3-maintenance-metrics-rewrites-crosspost.json`](workflows/pp-work-3-maintenance-metrics-rewrites-crosspost.json) | 31 | code, httpRequest, manualTrigger, merge, openAi |
| PP_work MVP - Main | [`pp-work-mvp-main.json`](workflows/pp-work-mvp-main.json) | 32 | code, executeWorkflow, httpRequest, if, openAi |
| PP_work Optional - Media Agent | [`pp-work-optional-media-agent.json`](workflows/pp-work-optional-media-agent.json) | 4 | code, executeWorkflowTrigger, httpRequest |
| PP_work Optional - Trend Sources | [`pp-work-optional-trend-sources.json`](workflows/pp-work-optional-trend-sources.json) | 7 | code, executeWorkflowTrigger, httpRequest, merge, openAi |
| СТО - MVP Заявки | [`sto-mvp-zayavki.json`](workflows/sto-mvp-zayavki.json) | 1 | webhook |
| Telegram Anatomical | [`telegram-anatomical.json`](workflows/telegram-anatomical.json) | 5 | code, httpRequest, scheduleTrigger, telegram |

## Локальные заготовки (`local/`)

| Файл | Что это |
|---|---|
| `03-ai-konsultant-telegram.json` | AI-консультант в Telegram с передачей менеджеру |
| `PP_work_n8n_full_automation.json` | Полная сборка контент-пайплайна PP_work |
| `workflow_1_lead_capture.json` | Приём лида с формы лендинга |
| `workflow_2_buttons.json` | Квалификация лида кнопками в Telegram |

## Импорт

1. n8n → **Workflows → Import from File** → выбрать JSON.
2. Подключить свои креды: в файлах оставлены только названия подключений, без идентификаторов и секретов.
3. Заменить плейсхолдеры на свои значения и включить воркфлоу.

| Плейсхолдер | Чем заменить |
|---|---|
| `YOUR_TELEGRAM_CHAT_ID` | ID чата или канала Telegram |
| `YOUR_GOOGLE_SHEET_ID` | ID Google-таблицы |
| `YOUR_AIRTABLE_BASE` / `YOUR_AIRTABLE_VIEW` | База и вид Airtable |
| `YOUR_DZEN_ID` | ID канала на Дзене |
| `@your_channel` | Ваш Telegram-канал |
| `<N8N_HOST>` | Адрес вашего n8n |
| `REDACTED_GOOGLE_API_KEY` | Свой ключ, и только через credentials n8n |

## Приватность

Репозиторий публичный, поэтому из файлов убраны адреса серверов, chat_id, идентификаторы таблиц,
внутренние ID воркфлоу и кредов, а также ключи. Секреты в n8n хранятся отдельно и в экспорт не попадают.
