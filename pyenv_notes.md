# "Pyenv Virtualenv Virtualenvwrapper" Notes

Instructions from [Svi Scripts](https://alysivji.github.io/setting-up-pyenv-virtualenvwrapper.html):

When we install `pyenv`, we add an additional directory of shims to the front of our `$PATH`. Each shim intercepts commands (python, pip, etc) and redirects them to the appropriate location.

- A [shim](https://stackoverflow.com/questions/2116142/what-is-a-shim/51646150) is a library that transparently intercepts commands / arguments / API calls to change the arguments passed, and handles the operation itself or redirects the operation elsewhere

## Installation (MacOS Homebrew)

Instructions following [pyenv github](https://github.com/pyenv/pyenv#installation):
```
brew update
brew install pyenv
```

- Using `Zsh`:
```
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
echo 'eval "$(pyenv init -)"' >> ~/.zshrc

source ~/.zprofile
source ~/.zshrc

echo $PATH
```
`/Users/joe/google-cloud-sdk/bin:/Users/joe/miniconda3/bin:/Users/joe/miniconda3/condabin:/Users/joe/.pyenv/shims:/usr/local/bin:/usr/local/sbin:/Users/joe/Documents/c01_wxds:/usr/bin:/bin:/usr/sbin:/sbin:~/.local/bin:/Users/joe/Documents/c01_wxds`
-> Note that `/Users/joe/.pyenv/shims` has been added (3rd element in `$PATH`)


### Commands

- List available Python versions
```
pyenv install --list
```

- Install a few Python versions to see how `pyevn` works
```
pyenv install 2.7.13
pyenv install pypy-5.7.1
pyenv install 3.6.2
pyenv install 3.7-dev
pyenv install 3.10.1
```

- If installation fails due to `BUILD FAILED (OS X 11.5.2 using python-build 20180424)`, first install the `Xcode Command Line Tools` beta version (https://emilwypych.com/2020/11/23/pyenv-problem-macosx_deployment_target11-0/?cn-reloaded=1)
```
xcode-select --install
softwareupdate --list

xcode-select --switch /Applications/Xcode-beta.app

```


- View `pyevn` versions
```
pyenv versions
```





https://github.com/pyenv/pyenv#installation
https://github.com/pyenv/pyenv#basic-github-checkout
