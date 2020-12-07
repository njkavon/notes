# Various little notes...

...and bits of knowledge gathered around topics below.

- [python development environment setup](devsetup.md)
- [clean macOS ~Mojave tweaks](systemsetup.md)
- [raspberry pi projects](rpi.md)

Maybe you'll find something helpful here, but you will most likely find something ridiculous :)



##### random command-line snippets

```
pyenv virtualenv 3.6.12 django2-app
pyenv activate django2-app
pip install Django==2.2

# to list|install packages with version specified
pip freeze > requirements.txt
pip install -r requirements.txt

# to see dependencies & details
pip show pygame
```

------



```
$ subl ~/.gitignore_global
```

```
# pyenv
.python-version

# Django stuff
*.log
local_settings.py
db.sqlite3
db.sqlite3-journal

# Flask stuff
instance/
.webassets-cache

# macOS
.DS_Store
.AppleDouble
.LSOverride
```

```
$ git config --global core.excludesfile ~/.gitignore_global
```

------



```
git init
git add .
git status
git commit -m 'initial commit'

git log --oneline
git reset 0dbebc9  // 'commit hash' to revert to
git reset HEAD~1  // revert last commit 

git branch -M main  // rename master
git remote add origin ...  // add remote
git push -u origin main  // then just 'git push'

git branch new_feature | git checkout -b new_feature
git add README.md
git commit -m 'added README.md'

git checkout main
git diff new_feature
git merge new_feature  // locally
git push

git push --set-upstream origin new_feature  // then compare&pullreq on the web
git checkout main
git pull origin  // update local main
git branch -d new_feature  // rm merged branch

git remote -v
```

```
git clone ...
git clone ... --depth 1 --branch=main

# just check to see if there are any changes available
git fetch ...
git diff main origin/main
git merge origin/main  // merge with local

# check and update (fetch & merge) your current HEAD branch, tries to merge local/remote
git pull ...
git diff 37b431a..b2615b4
```

------



- great vscode plugin to mount a remote folder over SSH as a local Workspace https://github.com/SchoofsKelvin/vscode-sshfs

```
# scp (secure cp), so You can also rename the files
scp co2data.py pi@192.168.1.241:'/home/pi'

# '.' == the current working directory instead of path
scp pi@192.168.1.241:'/home/pi/co2.csv' .

# '-r' option to copy all the contents of a directory
scp -r pi@192.168.1.241:'/home/pi '~/Downloads/pi'
```

```
# vscodium install ext from file
$ code --install-extension Downloads/ms-vscode-remote.remote-ssh-0.56.0.vsix
```

------



```
# caffeinate keeps mac awake as long as the script is running
# or without args - until you stop it
caffeinate python script.py
```

```
# edit crontab file, if sudo not needed by script
$ crontab -e

# use absolute path to venv to use env modules
@hourly /usr/bin/python /home/pi/test.py >> ~/cron.log 2>&1

# execute on system @reboot

┌───────────── minute (0 - 59)
│ ┌───────────── hour (0 - 23) 
│ │ ┌───────────── day of month (1 - 31)
│ │ │ ┌───────────── month (1 - 12)
│ │ │ │ ┌───────────── day of week (0 - 6) (Sunday to Saturday)
* * * * *

# execute every 10 minutes
*/10 * * * * /usr/bin/python /home/pi/test.py >> ~/cron.log 2>&1

# at 6 AM and 6 PM daily
0 5,17 * * * /usr/bin/python /home/pi/test.py >> ~/cron.log 2>&1
```

------



###### obsolete

```
# while pgzero has older pygame version in dependencies
$ python -m pip install pygame==2.0.0.dev8
$ pip install pgzero --ignore-installed pygame

# put into pygame project .py file to hide linter warnings
pylint: disable=undefined-variable
pylint: disable=undefined-variable, no-member

# or with vscode settings
"python.linting.pylintArgs": [
        "--extension-pkg-whitelist=pygame",
        //"--erros-only",
        "--disable=W,C",
    ]
```