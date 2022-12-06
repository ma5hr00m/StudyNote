---
title: 使用Go开发telegramBot初尝试
time: 2022-11-25
update: 2022-11-25
---

<div align=center>

# Go开发telegramBot

</div>

<div align=center>

## 申请telegramBot账号

</div>

1. telegram内搜索`BotFather`，发起对话。

   ```
   Client: /newbot
   Botfather: Alright, a new bot. How are we going to call it? Please choose a name for your bot.
   ```

2. 发送机器人`ID`，建议和机器人的用途有关。

   ```
   Client: testGear
   BotFather: Good. Now let's choose a username for your bot. It must end in `bot`. Like this, for example: TetrisBot or tetris_bot.
   ```

3. 发送机器人`username`，要求是以`bot`结尾。

   可能会出现`username`已被申请或者命名不规范的情况，改改就行。

   ```
   Sorry, this username is already taken. Please try something different.
   OR
   Sorry, this username is invalid.
   ```

   ```
   // Successfully applied for an bot account
   Client: 20221126gear_bot
   BotFather: Done! Congratulations on your new bot. You will find it at t.me/gear20221126_bot. You can now add a description, about section and profile picture for your bot, see /help for a list of commands. By the way, when you've finished creating your cool bot, ping our Bot Support if you want a better username for it. Just make sure the bot is fully operational before you do this.
   
   Use this token to access the HTTP API:
   Keep your token secure and store it safely, it can be used by anyone to control your bot.
   
   For a description of the Bot API, see this page: https://core.telegram.org/bots/api
   ```

<div align=center>

## 测试运行

</div>

1. 在`github`新创建了一个仓库，`clone`到本地后进入本地仓库，编译安装`Golang`版本的`telegram bot api`。

   ```
   go get -u github.com/go-telegram-bot-api/telegram-bot-api
   ```

2. 创建一个`bot.go`文件，写入`github`提供的复读机`Demo`。

   ```go
   //记得将 YourBotTOKEN 换成你自己的token
   package main
   
   import (
   	"log"
   
   	tgbotapi "github.com/go-telegram-bot-api/telegram-bot-api/v5"
   )
   
   func main() {
   	bot, err := tgbotapi.NewBotAPI("YourBotTOKEN")
   	if err != nil {
   		log.Panic(err)
   	}
   
   	bot.Debug = true
   
   	log.Printf("Authorized on account %s", bot.Self.UserName)
   
   	u := tgbotapi.NewUpdate(0)
   	u.Timeout = 60
   
   	updates := bot.GetUpdatesChan(u)
   
   	for update := range updates {
   		if update.Message != nil { // If we got a message
   			log.Printf("[%s] %s", update.Message.From.UserName, update.Message.Text)
   
   			msg := tgbotapi.NewMessage(update.Message.Chat.ID, update.Message.Text)
   			msg.ReplyToMessageID = update.Message.MessageID
   
   			bot.Send(msg)
   		}
   	}
   }
   ```

3. `Terminal`中运行该文件，然后在`telegram`中向你的机器人发送一条信息，可以看见机器人成功复读你的信息。

   ```shell
   go run bot.go
   ```

<br>
