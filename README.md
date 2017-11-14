
# **BotKit Starter for Cisco Jabber**

This repo contains everything you need to get started building a Cisco Spark bot with [Botkit](https://botkit.ai/).

Botkit is designed to ease the process of designing and running useful, creative bots that live inside Cisco Jabber.
Botkit features a comprehensive set of tools to deal with Cisco Jabber, and allows developers to build interactive bots and applications that send and receive messages just like real humans.
This document covers the Cisco Jabber-specific implementation details only.

## **Getting Started**

-Install Botkit

-Ask admin to create a Jabber user for the bot in either Cisco IM&Presence Server (on-premise deployment) or Cisco Webex Messenger (cloud deployment), then get the jid and password from the admin.

Jabber bots can send and receive messages, and in many cases, appear alongside their human counterparts as normal Jabber users.

## **Working with Cisco Jabber**
Jabber bot uses node-xmpp to connect to Cisco Unified IM & Presence server or Cisco WebEx Messenger and can only use the password authentication methods. Cisco Jabber bot can take part in 1-1 chat or group chat conversations and can provide information or other services for the conversations. It’s better to use persist store for the Botkit controller, otherwise when restart the bot, it will lose the group information and cannot received the message from a group chat.

The full code for a simple Cisco Jabber bot is as below:

const Botkit = require('./lib/Xmppbot.js');

var controller = Botkit({

    json_file_store: './bot_store/'   
});

var bot = controller.spawn({
    
    client: {  
        jid: ‘john@alpha-cup.cisco.com',
        
        password: *,
        
        host: "shn-alpha-cup011.cisco.com",
        
        port: 5222
        
    }  
});


controller.hears(\['hello'\], \['direct_mention', 'direct_message'\], function (bot, message) {

    bot.reply(message, 'Hi');
    
});

controller.on('direct_mention', function (bot, message) {

    bot.reply(message, 'You mentioned me in a group and said, "' + message.text + '"');
});

controller.on('direct_message', function (bot, message) {

    bot.reply(message, 'I got your direct message. You said, "' + message.text + '"');  
});
