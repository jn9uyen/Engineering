# VS Code Notes

### To fix the issue that the terminal shell doesn't read `.bash_profile` (Linux environment)

Update the linux terminal setting.json to the below (This can be found in ~/.local/share/code-server/User/settings.json in your VScode console)
```
{
    "terminal.integrated.automationShell.linux": "",
    "terminal.integrated.shell.linux": "/bin/bash",
    "terminal.integrated.shellArgs.linux": [ "-l" ]
}
```

### Run code-server specifying port
```
code-server --auth none --port 8082
```

or set alias in `~/.bash_aliases`
```
alias vscode='code-server --auth none --port 8082'
```
