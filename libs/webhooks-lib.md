# Webhooks lib

![](<../.gitbook/assets/image (43).png>)

Integration with external services can be possible with webhooks notifications. This lib generate url for webhooks.

## Example bot

See [example bot](https://t.me/BBWebhookBot)

{% hint style="info" %}
From [wikipedia](https://en.wikipedia.org/wiki/Webhook): a **webhook** is a method of augmenting or altering the behavior of bot, with custom [callbacks](https://en.wikipedia.org/wiki/Callback_\(computer_programming\)).

These callbacks may be maintained, modified, and managed by third-party users and developers who may not necessarily be affiliated with the originating website or application.

 The term "webhook" was coined by Jeff Lindsay in 2007 from the computer programming term [hook](https://en.wikipedia.org/wiki/Hooking).
{% endhint %}

Webhooks is more simple way for integration. Other libs also use webhooks notifications already: CoinPayments, FreeKassa.

## Get Webhook Url

```javascript
// user's webhook
let webhookUrl = Libs.Webhooks.getUrlFor({
  // this command will be runned on webhook
  command: "/onWebhook",
  // this text will be passed to command
  content: "Did you see the cat?",
  // execute for this (current) user
  user_id: user.id,
  // redirect to page with cat after calling webhook
  // you need remove this for external service
  redirect_to: "https://cataas.com/cat"
})

Bot.inspect(webhookUrl);
```

This code will generate Webhook url. 

After loading page via this url:

* web page with cat will be loaded (Thank for cat to [https://cataas.com](https://cataas.com/cat))
* command `/onWebhook` will be execute on Bot for user with user.id
* content "Did you see the cat?" will be passed for command `/onWebhook`

###  More useful for external services

As a rule, the webhook URL must be set from the admin panel on the external service. So we can not set it for just one user: 

```javascript
// global bot webhook
let webhookUrl = Libs.Webhooks.getUrlFor({
  // this command will be runned on webhook
  command: "/onWebhook"
})
```

{% hint style="warning" %}
Webhooks can be with GET and POST methods only. All passed data contains on content variable
{% endhint %}

On command `/onWebhook` we can get posted content from external service

```javascript
// for user's webhook
Bot.sendMessage(inspect(content))
// also you can read data with Bot.getProperty - you need store it before
```

As a rule, external service must pass useful data on webhook. For example info about payments: order_id, user_id. Use it!

On command `/onWebhook` for bot's webhook we do not have user:

```javascript
// for bot's webhook

// this is not worked - because no current user on bot's webhook
// Bot.sendMessage(inspect(content))

// make any not specific user code
// ...

// We can pass user_id in content (it is depend from external service)
Bot.run({ command: "/userCommand", user_id: JSON.parse(content).user_id })

// in /userCommand we can now use Bot.sendMessage function

```

