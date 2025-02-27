# iterm2-lrzsz

This document describes how to configure iterm2 on your Mac to be able to use rz and sz for file transfers through the terminal.

lrzsz is a unix communication package providing the XMODEM, YMODEM, ZMODEM file transfer protocol.  Most distros provide a system package for lrzsz and lrzsz is provided by homebrew for installation on your Mac.

For more information see:
- https://www.ohse.de/uwe/software/lrzsz.html
- https://iterm2.com/
- https://brew.sh/

Prerequisites
---
- iTerm2
- homebrew
- lrzsz package installed on the remote host.  On Ubuntu 24.04:
  - ```shell
    sudo apt install lrzsz
    ```
   
Install lrzsz on your mac:
---
```shell
brew install lrzsz
```

Set trigger for iTerm2
---

- Clone this repo and copy the two shell scripts somewhere.  I chose: /Users/felder/.local/bin/
- Make sure they're executable:
	- chmod 755 /Users/felder/.local/bin/iterm2-send-zmodem.sh
	- chmod 755 /Users/felder/.local/bin/iterm2-recv-zmodem.sh
- On my system, homebrew installs sz and rz to /opt/homebrew/bin/ and the scripts are written accordingly.  If your rz and sz live somewhere else, modify the scripts.
- Set up two triggers in iTerm2's [preference] -> [profile] -> [advanced] -> [triggers] -> [edit]

```
	Regular expression: rz waiting to receive.\*\*B0100
	Action: Run Silent Coprocess
	Parameters: /Users/felder/.local/bin/iterm2-send-zmodem.sh

	Regular expression: \*\*B00000000000000
	Action: Run Silent Coprocess
	Parameters: /Users/felder/.local/bin/iterm2-recv-zmodem.sh
```

How to use it
---
Note the first time you try this, iterm2 may indicate there was an error.  In my experience it works fine and you can simply click the option in the popup to ignore errors.

### rz

- Run "rz" on the remote server. If everything is setup correctly, iterm2 should prompt you to choose a file to send from your Mac.

### sz

- Run "sz /path/to/file" on the remote server. If everything is setup correctly, iterm2 should prompt you to choose a location for saving the file to your Mac.
