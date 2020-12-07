# Python dev env setup with pyenv on macOS

Possibly the best way to manage and switch between multiple Python versions as of today.

I prefer `brew install` over [pyenv-installer](https://github.com/pyenv/pyenv-installer) script, where I can choose what will be installed.

```
$ brew install pyenv pyenv-virtualenv
```

To finish the instalation and disable pip (you have to toggle this later for pipx installation) outside venvs, your `~/.zshrc` or `~/.bash_profile` in my case should contain these:

```
# pyenv
export PIP_REQUIRE_VIRTUALENV=true
if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init -)"
fi

# pyenv-virtualenv
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi

# 'brew install tcl-tk' if you want to run idle, I prefer 'IPython' more lately.
export PATH="/usr/local/opt/tcl-tk/bin:$PATH"
export LDFLAGS="-L/usr/local/opt/tcl-tk/lib"
export CPPFLAGS="-I/usr/local/opt/tcl-tk/include"
export PKG_CONFIG_PATH="/usr/local/opt/tcl-tk/lib/pkgconfig"
export PYTHON_CONFIGURE_OPTS="--with-tcltk-includes='-I/usr/local/opt/tcl-tk/include' --with-tcltk-libs='-L/usr/local/opt/tcl-tk/lib -ltcl8.6 -ltk8.6'"

# pipx path
export PATH="$PATH:/Users/novakjan/.local/bin"

# pipx shell completions (pipx up<tab> packag<tab>)
eval "$(register-python-argcomplete pipx)"
```


Reload your shell, restart Terminal or open a new tab to refresh your paths, in my case:

```
$ source ~/.bash_profile
```



Then you can manage many Python versions using command-line, choose which one to use globally or locally in one directory.

```  
pyenv install --list | grep " 3\.[678]"
pyenv install 3.6.12
pyenv versions

pyenv global 3.x.x
pyenv local 3.x.x
pyenv shell 3.x.x

# create, activate venv for projects
pyenv virtualenv 3.x.x project_name
pyenv activate project_name

# list venvs
pyenv virtualenvs

# pyenv will automatically load venv after entering directory
pyenv local project_name

# check $ which python
python --version

# by using the Python Interpreter $ python
>>> import sys
>>> print(sys.executable)
```



## pipx - formatter and linter installation

With pipx you can do `pipx install package` instead of `pip install package` to install a Python package on your computer (outside of virtual environment specific to a project) - without those package dependencies messing up your <u>global Python</u> and be accessible throught all virtual environments.

```
python -m pip install pipx
pipx ensurepath

pipx install black
pipx install flake8
pipx install ipython
pipx list
pipx upgrade-all

# to run package once & delete afterwards (--skip-string-normalization or -S, skips '=>")
pipx run black -S test.py
```

```
# your paths to set in vscode are
"python.linting.flake8Path": "~/.local/bin/flake8",
"python.formatting.blackPath": "~/.local/bin/black"
```



###### obsolete

```
# python builtin venv management
python -m venv ~/envs/env
source ~/envs/env/bin/activate venv
deactivate

# while pgzero has older pygame version in dependencies
python -m pip install pygame==2.0.0.dev8
pip install pgzero --ignore-installed pygame
```

