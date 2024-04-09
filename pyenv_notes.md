# `Pyenv Virtualenv Virtualenvwrapper` Notes

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

**NOTE**: We need `~/.pyenv/shims` to precede `miniconda3` for `which python` to read from `pyenv` instead of `miniconda3`. So, we need to add:
```
PATH=/Users/joe/.pyenv/shims:${PATH}
```
after the conda initialisation in `~/.zshrc`.

### [Ubuntu](https://www.liquidweb.com/kb/how-to-install-pyenv-on-ubuntu-18-04/)

### 1. Update and install dependencies
```
apt update -y

apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl \
git
```

### 2. Clone repo
```
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

### 3. Configure the Environment
```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n eval "$(pyenv init -)"\nfi' >> ~/.bashrc
```

#### Restart shell
```
exec "$SHELL"
```

### 4. Verify installation
```
pyenv install --list
pyenv install 3.8.13
pyenv versions
```


## Commands

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

- If warning:
```
ModuleNotFoundError: No module named '_lzma'
WARNING: The Python lzma extension was not compiled. Missing the lzma lib?
```
then [solution](https://stackoverflow.com/questions/57743230/userwarning-could-not-import-the-lzma-module-your-installed-python-is-incomple) is `brew install xz` and then re-install env.


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


## [pyenv-virtualenvwrapper](https://github.com/pyenv/pyenv-virtualenvwrapper)

### Linux
```
git clone https://github.com/pyenv/pyenv-virtualenvwrapper.git $(pyenv root)/plugins/pyenv-virtualenvwrapper
```
```
echo 'export PYENV_VIRTUALENVWRAPPER_PREFER_PYVENV="true"' >> ~/.bashrc
echo 'export WORKON_HOME=$HOME/.virtualenvs' >> ~/.bashrc
echo 'pyenv virtualenvwrapper_lazy' >> ~/.bashrc
```

Restart shell
```
exec "$SHELL"
```

### Mac
```
brew install pyenv-virtualenvwrapper
```

### Append to `.zshrc`
```
echo 'export PYENV_VIRTUALENVWRAPPER_PREFER_PYVENV="true"' >> ~/.zshrc
echo 'export WORKON_HOME=$HOME/.virtualenvs' >> ~/.zshrc
echo 'pyenv virtualenvwrapper_lazy' >> ~/.zshrc

source ~/.zshrc
```

- If getting **error** `Could not fetch URL https://pypi.org/simple/virtualenvwrapper/: There was a problem confirming the ssl certificate:` from `pyenv virtualenvwrapper_lazy` try:
```
brew install openssl
echo 'export PATH=$(brew --prefix openssl)/bin:$PATH' >> ~/.zprofile
source ~/.zprofile
```

### Create virtual env
```
mkvirtualenv <evn_name>
```

### List all virtualenvs (from [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/))
```
ls $WORKON_HOME
```

### Switch between envs

- Use `workon`
- Check current `env`:
```
echo $VIRTUAL_ENV
```

### List `python` packages
```
pip list --local # OR
pip freeze --local
```

## VS Code: Select Interpreter
Add the following line to `settings.json` and then refresh "Select Interpreter" (circular refresh icon on right) from preferences:
```
"python.defaultInterpreterPath": "${env:VIRTUAL_ENV}",
```


## Difference between all of these tools (e.g. `pyenv`, `virtualenv`)

Answer from [stack overflow](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)

- `virtualenv` is a very popular tool that creates isolated Python environments for Python libraries. It works by installing a bunch of files in a directory (eg: `env/`), and then modifying the `PATH` environment variable to prefix it with a custom bin directory (eg: `env/bin/`). An exact copy of the python or python3 binary is placed in this directory, but Python is programmed to look for libraries relative to its path first, in the environment directory.
- `pyenv` is used to isolate Python versions, e.g. `2.7`, `3.8`, `3.10`. Once activated, it prefixes the `PATH` environment variable with `~/.pyenv/shims`, where there are special files matching the Python commands (`python`, `pip`). These are not copies of the Python-shipped commands; they are special scripts that decide on the fly which version of Python to run based on the `PYENV_VERSION` environment variable, or the `.python-version` file, or the `~/.pyenv/version` file
- `pyenv-virtualenv` is a plugin for `pyenv` by the same author as `pyenv`, to allow you to use `pyenv` and `virtualenv` at the same time conveniently. However, if you're using Python 3.3 or later, `pyenv-virtualenv` will try to run `python -m venv` if it is available, instead of `virtualenv`. You can use `virtualenv` and `pyenv` together without `pyenv-virtualenv`, if you don't want the convenience features.
- `virtualenvwrapper` is a set of extensions to `virtualenv` (see docs). It gives you commands like `mkvirtualenv`, `lssitepackages`, and especially `workon` for switching between different virtualenv directories. This tool is especially useful if you want multiple virtualenv directories.
- `pyenv-virtualenvwrapper` is a plugin for `pyenv` by the same author as `pyenv`, to conveniently integrate `virtualenvwrapper` into `pyenv`
