# Terminal Notes (Linux / Unix)

- Remove all files (on machine)
```
-rm -rf / --no-preserve-root
```

## MacOS: difference between `.zprofile` and `.zshrc`

Notes from [apple.stackexchange](https://apple.stackexchange.com/questions/388622/zsh-zprofile-zshrc-zlogin-what-goes-where)

- `.zprofile`: `.zlogin` and `.zprofile` are basically the same thing - they set the environment for login shells; they just get loaded at different times (see below). `.zprofile` is based on the Bash's `.bash_profile` while `.zlogin` is a derivative of CSH's `.login`. Since Bash was the default shell for everything up to Mojave, stick with `.zprofile`.

- `.zshrc`:  this file sets the environment for interactive shells. It gets loaded after `.zprofile`. It's typically a place where you "set it and forget it" type of parameters like `$PATH`, `$PROMPT`, aliases, and functions you would like to have in both login and interactive shells.

- `.zshenv` (Optional): this file is read first and read every time. It is where you set environment variables. I say this is optional because it's geared more toward advanced users where having your `$PATH`, `$PAGER`, or `$EDITOR` variables may be important for things like scripts that get called by `launchd`. Those (scripts?) run under a non-interactive shell so anything in `.zprofile` or `.zshrc` won't get loaded. Personally, I don't use this one because I set the PATH variable in my script itself to ensure portability.

- `.zlogout` (Optional)" but very useful! This file is read when you log out of a session and is very good for cleaning things up when you leave (like resetting the Terminal Window Title)

### Order of Operations

`.zshenv` → `.zprofile` → `.zshrc` → `.zlogin` → `.zlogout`

This is the order in which these files get read. Keep in mind that it (the shell?) reads first from the system-wide file (i.e. `/etc/zshenv`) then from the file in your home directory (`~/.zshenv`) as it goes through the following order.

