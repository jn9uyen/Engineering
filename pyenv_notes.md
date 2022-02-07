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
clang --version
xcode-select --install

# Remove xcode to update version
sudo rm -rf /Library/Developer/CommandLineTools
xcode-select --install
# softwareupdate --list
# xcode-select --switch /Applications/Xcode-beta.app
```
-> Output of `clang --version`
```
Apple clang version 13.0.0 (clang-1300.0.27.3)
Target: x86_64-apple-darwin21.2.0
Thread model: posix
```

- If `pyenv install xxx` does not work here for MacOS, perform these steps
```
brew install openssl
brew reinstall pyenv
pyenv init  # initialise inside your project directory
pyenv install xxx
pyenv local xxx  # activate python version inside your project directory
```

- If needed, modify `.zshrc` file so that `.pyenv shims` is at the start of the `$PATH`
`PATH=/Users/joe/.pyenv/shims:${PATH}`
`source .zshrc`


#### View `pyevn` versions
```
pyenv versions
pyenv global 3.10.1
pyenv versions
```

- Activate different versions of Python using the `pyenv shell [version]`; e.g.
```
which python  # /Users/joe/.pyenv/shims/python
python
pyenv shell 3.10.1
python
```
-> `.pyenv/shims` takes care of everything


## pyenv-virtualenvwrapper

```
brew install pyenv-virtualenvwrapper
```


https://github.com/pyenv/pyenv#installation
https://github.com/pyenv/pyenv#basic-github-checkout
