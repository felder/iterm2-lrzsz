# iterm2-lrzsz

There are a mess of troubles in sending and receiving files from my macbook to dev server, since I had no permission to excute command scp on dev server.
Here is a lightweight, quick, and convenience tools which related with ssh, called lrzsz. lrzsz is a unix communication package providing the XMODEM, YMODEM, ZMODEM file transefer protocol which usually has been already installed in most of servers.

For more information see:
https://www.ohse.de/uwe/software/lrzsz.html

Prerequisites
---

- iTerm2 is necessary. [Here][] is the official website.
- Install lrzsz on your mac:

```shell
sudo brew install lrzsz
```

Set trigger for iTerm2
---

- First you should download the scripts from [ZModem integration for iTerm 2][], and save them in /Users/{USERNAME}/.local/bin
- Set up two triggers in iTerm2's [preference] -> [profile] -> [advanced] -> [triggers] -> [edit]

```
	Regular expression: rz waiting to receive.\*\*B0100
	Action: Run Silent Coprocess
	Parameters: /Users/{USERNAME}/.local/bin/iterm2-send-zmodem.sh

	Regular expression: \*\*B00000000000000
	Action: Run Silent Coprocess
	Parameters: /Users/{USERNAME}/.local/bin/iterm2-recv-zmodem.sh
```

How to use it
---
Note the first time you try this, iterm2 may indicate there was an error.  In my experience it works fine and you can simply click the option in the popup to ignore errors.

### rz

- Run "rz" on dev server. Then it would prompt that something like "rz waiting to receive." and create a new window titled "choose a file to send".
- Choose the file you need to receive from your laptop.

### sz

- run "sz /path/file" to send server's file to your laptop.
