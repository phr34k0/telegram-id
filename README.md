# How to get an id to use on Telegram Messenger

###### The ultimate guide

## Telegram-CLI

The best way I found to get ids is using Telegram-CLI. 

It's available on https://github.com/vysheng/tg 

Install and run it. I recommend using bot mode `-b`, but it's optional.

Run `Telegram CLI`:

```
bin/telegram-cli -k tg-server.pub -b
```

Wait for it do load and then paste a bot token.

The output must be similar to this:

```
root@prod:/usr/src/tg# bin/telegram-cli -k tg-server.pub -b
change_user_group: can't find the user telegramd to switch to
Telegram-cli version 1.4.0, Copyright (C) 2013-2015 Vitaly Valtman
Telegram-cli comes with ABSOLUTELY NO WARRANTY; for details type `show_license'.
This is free software, and you are welcome to redistribute it
under certain conditions; type `show_license' for details.
Telegram-cli uses libtgl version 2.1.0
Telegram-cli includes software developed by the OpenSSL Project
for use in the OpenSSL Toolkit. (http://www.openssl.org/)
I: config dir=[/root/.telegram-cli]
[/root/.telegram-cli] created
[/root/.telegram-cli/downloads] created
hash: 
```

## User ID

To get a user id, ask the user to send any message do the bot and observe it on `Telegram CLI` window.

The message must appear similar to this:

```
[11:07]  Gabriel R F »»» /start
```

Then, on `Telegram CLI`, type:

```
user_info Gabriel_R_F
```

Note that spaces are replaced by `_`.

The output will be something like this:

```
User Gabriel R F @GabrielRF (#9083329):
        phone: (null)
        offline (was online recently)
```

There you go! The user id, on this example, is `9083329`.

## Group ID

Add the bot to the group. On `Telegram CLI`, a message will be printed.

```
[11:12]  test Gabriel R F added user test
```

Then, on `Telegram CLI`, type

```
chat_info test
```

Where `test` is the group's name. Note that spaces are replaced by `_`.

The output on `Telegram CLI` will be similar to:

```
Chat test updated admin members
Chat test (id 148228539) members:
                test invited by Gabriel R F at [2016/03/29 11:12:30]
                Gabriel R F invited by Gabriel R F at [2016/03/29 11:11:18] admin
```

So, the id for the example group is `-148228539`. 

Group ids are always a __negative integer__, so remember to add the `-` while using it on the Telegram API.

## Channel ID

Finally, to get a channel id, add the bot as a channel `administrator`.

On `Telegram CLI` type:

```
channel_info test
```

where `test` is the channel's name. The output must be like this:

```
Channel test (id 1035716040):
                2 participants, 2 admins, 0 kicked
```

Here is the trick. Every channel id is a __13 characters negative integer__. So the id for this channel is `-1001035716040` and not `1035716040` as printed.
