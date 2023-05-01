---
title: Telegram Bot
description: How to build a simple Telegram bot with Python
author: jose
language: en
layout: post
date: 2023-05-01 10:00 +0300
proglang: Python
math: true
mermaid: true
pin: true
image:
  path: https://flowxo.com/wp-content/uploads/2021/03/The-Botfather-512x512.png
  alt: BotFather.
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---
**Building a Telegram bot with Python** is a simple task, in this case we will use the [**python-telegram-bot**](https://docs.python-telegram-bot.org/en/stable/) library that makes thing even simpler. We also need to register our bot in order to get a Telegram API Key for our bot. Once completed, you can have your bot up and running on your local machine, or in a dedicated server for it.

## Getting The Telegram Bot API Key
---
To create a Telegram bot, you need to contact the [**BotFather**](https://telegram.me/BotFather), which is essentially a bot used to create other bots.

After starting the conversation with BotFather, the command you need is `/newbot` which leads to the following steps to create your bot:

<img src="https://assets.toptal.io/images?url=https://bs-uploads.toptal.io/blackfish-uploads/uploaded_file/file/27074/image-1562742442995-6474e4cf4325101c9b5656e36ca84658.png" width="70%"/>

Your bot should have two attributes: a `name` and a `username`. The `name` will show up for your bot, while the `username` will be used for mentions and sharing.

After choosing your bot name and username, which must end with **bot**, you will get a message containing your **token**.

## Preparing Your Environment
---
I'm using **Python 3**, you can use the same, this are the instructions to install in a Linux machine:  
```bash
$ apt-get update
$ apt-get install -y python3 python3-pip python-dev build-essential python3-venv
$ pip3 install python-telegram-bot
```

Once completed, it is time to create the bot.

### Bot Code
---
There are three main parts of the bot code,
  1. Initialization of the bot (`run_bot()` method).
    * Here we use our Telegram token to register our bot.
    * We can add handlers for different events/commands, in this case, we are two handlers:
      1. For the `/start` command.
      2. For when a message is received.
  2. Handling the start of the bot (`start_handler(...)` method).
  3. Handling the messages (`message_handler(...)` method).

```python
import telegram
from telegram import (
    Update
)

from telegram.ext import (
    ApplicationBuilder,
    CallbackContext,
    CommandHandler,
    MessageHandler,
    filters
)

# Replace YOUR_TOKEN_HERE with your own Telegram bot token
TOKEN = '1234567890:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
                    

async def start_handler(update: Update, context: CallbackContext):
    # Handle /start command (When the user starts the bot)
    await context.bot.send_message(chat_id=update.effective_chat.id,
                                   text="Hello! I'm a bot. What can I do for you?")


async def message_handler(update, context):
    # Here you will decide what to do with the received message.
    # For this example, we just reply to the user with the exact same
    # message.
    await context.bot.send_message(
        chat_id=update.effective_chat.id, text=update.message.text)


def run_bot() -> None:
    # Create and configure the bot
    application = (
        ApplicationBuilder()
        .token(TOKEN)
        .concurrent_updates(True)
        .build()
    )

    # Add handlers for /start and messages
    application.add_handler(CommandHandler('start', start_handler))
    application.add_handler(MessageHandler(
        filters.TEXT & (~filters.COMMAND), message_handler))

    # Start the bot
    application.run_polling()


# Entry point
if __name__ == '__main__':
    run_bot()
```