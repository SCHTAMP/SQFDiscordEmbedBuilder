# SQF Discord Embed Builder
![](https://github.com/ConnorAU/SQFDiscordEmbedBuilder/blob/master/SQFDiscordEmbedBuilder.png)

[![GitHub license](https://img.shields.io/github/license/ConnorAU/SQFDiscordEmbedBuilder.svg)](https://github.com/ConnorAU/SQFDiscordEmbedBuilder/blob/master/LICENSE)

A discord webhook addon using basic SQF/Arma configs so even beginners can easily send webhook messages directly from an Arma 3 Server.

## Features
- 2-step installation
- Design embeds how **you** want in Arma config format
- Use SQF parameters for dynamic text content

## Note
- You may need to install [.NET Framework 4.5.2](https://www.microsoft.com/en-au/download/details.aspx?id=42642).
- The extensions were built and tested on Arma 3 Dedicated Server.
- This addon does work on Arma client however the extensions are **NOT** BattlEye whitelisted. 

# Setup
The following instructions are for an Arma 3 Server using the latest [release](https://github.com/ConnorAU/SQFDiscordEmbedBuilder/releases).
1. Place `@DiscordEmbedBuilder` in your server root folder
2. Add the mod to your command line `-serverMod=@DiscordEmbedBuilder`

# Make your own embeds

## Config
The config is where you design your messages. There are quite a few settings for the each message which are explained below.

### Basic settings
[Example.cpp](https://github.com/ConnorAU/SQFDiscordEmbedBuilder/blob/master/addon/embeds/Example.cpp)

- `webhookurl` - Unique URL provided by Discord. It determines what channel your message will send to.
- `message` - The text content of your message. This example uses `This is an example message`.<br/>![](https://i.imgur.com/x80hA14.png)
- `username` - The name of the bot when it sends the message. If this is not set Discord will use the name set in the webhook settings.
- `avatar` - The avatar of the bot when it sends the message. If this is not set Discord will use the image set in the webhook settings.
- `tts` - [Text to speech](https://support.discordapp.com/hc/en-us/articles/212517297-Text-to-Speech-101). 

That's all you need to send a simple text message, however there are more settings to configure embeds.

### Embed settings
Messages can contain up to 10 embeds. These embeds must be defined inside the `Embeds` subclass.
[CfgDiscordEmbedTemplate](https://github.com/ConnorAU/SQFDiscordEmbedBuilder/blob/master/addon/config.cpp)<br/>
[Example2.cpp](https://github.com/ConnorAU/SQFDiscordEmbedBuilder/blob/master/addon/embeds/Example2.cpp)
- `title` - Embed title text.
- `description` - Description text, located under the title.
- `url` - Link opened when you click the title text.
- `color` - RGB color code. eg: Red FF0000.
- `timestamp` - Show timestamp in the embed footer.
- `thumbnail` - Image shown in the top right corner of the embed.
- `image` - Full embed width image shown at the bottom of the embed under all fields.
- `fields` - Array of embed fields. Maximum of 25 fields per embed.

#### Author (Subclass)
- `name` - Author name, located above the title text.
- `url` - Link opened when you click the author name.
- `image` - Tiny image shown to the left of the author name.

#### Footer (Subclass)
- `text` - Footer text, shown to the left of the timestamp (if enabled).
- `image` - Small image shown to the left of the footer text.

## SQF 
The SQF side of this mod is very minimal. You don't need to edit the sqf files in the mod pbo at all as the customization is all done in the config file. 

What you do need to know is how to execute the webhook, which is very simple.
```sqf
[type,parameters] call DiscordEmbedBuilder_fnc_send;
```

1. Type: STRING - The name of the config class in `CfgDiscordEmbedBuilder` you wish to use.
2. Parameters: ARRAY (optional) - Any value you want to use in the embed. 

Parameters are used in `message`, `username`, `embed title`, `embed description`, `author name`, `footer text`, `field name` and `field content` with the `format` command: 
```sqf
format([string]+parameters);
```

## Connecting your message to the webhook
1. Open your Discord client and open the settings of the channel you want your message to send to.<br/>![Step 1](https://i.imgur.com/hFZ2bHw.png)
2. Click `Webhooks` on the left panel, then click `Create Webhook`.<br/>![Step 2](https://i.imgur.com/8KJXkl4.png)
3. Scroll down to `Webhook URL`, click `Copy`.<br/>![Step 3](https://i.imgur.com/l4gpTxP.png)
4. Paste the URL in your `webhookurl` config property and remove the base URL.<br/>~~https://discordapp.com/api/webhooks/~~<br/>00000000000000000/XXXXXXX_XXXXXXXXXXXXXXX_XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

### Video tutorial
Here is a video tutorial showing how to set up your webhook. There is no audio to it but it shows you exactly what to do.<br/>
https://www.youtube.com/watch?v=yF0UEiUnL9E