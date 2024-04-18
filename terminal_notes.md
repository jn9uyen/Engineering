# Terminal Notes (Linux / Unix)

## Nice rendering
Install "oh my zsh" from [ohmyzsh github](https://github.com/ohmyzsh/ohmyzsh). Also install [homebrew fonts](https://github.com/ryanoasis/nerd-fonts?tab=readme-ov-file#option-2-homebrew-fonts)
```
brew tap homebrew/cask-fonts
brew install font-hack-nerd-font
```

## Commands

### Remove all files (on machine)
```
-rm -rf / --no-preserve-root
```

### View lines of file
```
cat <file>
less <file>
more <file>

# Top n rows (e.g. top 100 rows)
head -n <n> <file>
head -n 100 <file>

# Save top 100 rows of file to another file
head -n 100 file.csv > file_top100.csv
```

### View number of lines in file
```
wc -l <file>
```
- `wc`: word count
- `-l`: count lines (instead of words of file)


### [Get public and local IP addresses (Mac)](https://constellix.com/news/what-is-my-ip-address)

- `ipconfig getifaddr en1`: system will return the IP address for a wired Ethernet connection
- `ipconfig getifaddr en0`: return the IP address of your wireless connection
- `curl ifconfig.me`: returns the public IP address of the Mac Terminal

- local IP address is from "wireless connection" when connected on wifi

### [Listening on TCP port (MacOS)](https://stackoverflow.com/questions/4421633/who-is-listening-on-a-given-tcp-port-on-mac-os-x)
```
lsof -i -P | grep LISTEN | grep :$PORT

# Just IP4
lsof -i 4 -P | grep LISTEN | grep :$PORT
```

### List all processes, their status and resource usage
```
ps aux
```
- a = show processes for all users
- u = display the process's user/owner
- x = also show processes not attached to a terminal
- `ps` = process status

List processes on port
```
ps aux | grep node
```

### To kill port ID (PID)
```
sudo kill -9 <PID>
```

### Restart shell
```
exec "$SHELL"
```

### Set and unset env variables
```
export VAR=test_string
echo $VAR
unset VAR
echo $VAR
```

### [List files ordered by file size](https://unix.stackexchange.com/questions/53737/how-to-list-all-files-ordered-by-size)
```
find . -type f -ls | sort -r -n -k7
```

## MacOS: difference between `.zprofile` and `.zshrc`

Notes from [apple.stackexchange](https://apple.stackexchange.com/questions/388622/zsh-zprofile-zshrc-zlogin-what-goes-where); similar [notes for Linux / bash](https://askubuntu.com/questions/121073/why-bash-profile-is-not-getting-sourced-when-opening-a-terminal)

- `.zprofile`: `.zlogin` and `.zprofile` are basically the same thing - they set the environment for login shells; they just get loaded at different times (see below). `.zprofile` is based on the Bash's `.bash_profile` while `.zlogin` is a derivative of CSH's `.login`. Since Bash was the default shell for everything up to Mojave, stick with `.zprofile`.

- `.zshrc`:  this file sets the environment for interactive shells. It gets loaded after `.zprofile`. It's typically a place where you "set it and forget it" type of parameters like `$PATH`, `$PROMPT`, aliases, and functions you would like to have in both login and interactive shells.

- `.zshenv` (Optional): this file is read first and read every time. It is where you set environment variables. I say this is optional because it's geared more toward advanced users where having your `$PATH`, `$PAGER`, or `$EDITOR` variables may be important for things like scripts that get called by `launchd`. Those (scripts?) run under a non-interactive shell so anything in `.zprofile` or `.zshrc` won't get loaded. Personally, I don't use this one because I set the PATH variable in my script itself to ensure portability.

- `.zlogout` (Optional)" but very useful! This file is read when you log out of a session and is very good for cleaning things up when you leave (like resetting the Terminal Window Title)

### Order of Operations

`.zshenv` → `.zprofile` → `.zshrc` → `.zlogin` → `.zlogout`

This is the order in which these files get read. Keep in mind that it (the shell?) reads first from the system-wide file (i.e. `/etc/zshenv`) then from the file in your home directory (`~/.zshenv`) as it goes through the following order.

### `source .bashrc` in `.bash_profile`

In linux env, if a `.bash_profile` is created, then `.bashrc` will not be sourced when logging into the machine (or VM). Add lines to the `.bash_profile` (which is read first before `.bashrc`):
```
# The following sources ~/.bashrc in the interactive login case,
# because .bashrc isn't sourced for interactive login shells:
case "$-" in *i*) if [ -r ~/.bashrc ]; then . ~/.bashrc; fi;; esac
```

#### Note:

- `rc`: stands for run commands/control

