# Variables

| Variable                 | Description                                                                                                                                                                                       |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| request                  | it is JSON collection with a lot of data. You can see it by `Bot.sendMessage( inspect(request) )`                                                                                                 |
| message                  | current message from user - string                                                                                                                                                                |
| content                  | downloaded content (if there was a URL for loading in the scenario) - text                                                                                                                        |
| user                     | user who sent a command or text. Fields: `id`, `first_name`, `last_name`, `username`, `telegramid`, `created_at`, `updated_at`                                                                    |
| chat                     | data for current chat. Fields: `id`, `chatid`, `title`, `chat_type` (can be: "private", "group", "supergroup"), user_id, created_at, updated_at, bot_id                                           |
| bot                      | data for bot. Fields: `id`, `name`, `token`, `created_at`, `updated_at`, `csv_url`, `botan_token`, `last_run_at`, `store_bot_id`, `status`                                                        |
| params                   | command parameters - text                                                                                                                                                                         |
| completed_commands_count | the count of previously completed commands on `Bot.runCommand` calls. Can be used for [security](https://help.bots.business/scenarios-and-bjs/bjs-security#use-completed_commands_count-variable) |

### You can inspect any variable for debug

```
Bot.sendMessage( inspect(user) )
Bot.sendMessage( inspect(chat) )
```
