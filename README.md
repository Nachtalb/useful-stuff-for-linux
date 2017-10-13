# linux-command-collection

<!-- toc -->

- [Installations](#installations)
  * [Pyenv installation](#pyenv-installation)
  * [Install nodejs > 6.x on Deepin Linux](#install-nodejs--6x-on-deepin-linux)
  * [Install solr together with Java](#install-solr-together-with-java)
- [Python](#python)
  * [Pyenv on Deepin Linux](#pyenv-on-deepin-linux)
- [Git](#git)
  * [Add file to global git ignore](#add-file-to-global-git-ignore)
- [Misc](#misc)
  * [Make sure your .ssh private key file has chmod 400](#make-sure-your-ssh-private-key-file-has-chmod-400)
  * [Set vim to default editor](#set-vim-to-default-editor)

<!-- tocstop -->

## Installations

### Pyenv installation
The easiest way is to install [pyenv](https://github.com/pyenv/pyenv) via it's 
installer. This installer also installs the most common pyenv plugins: 
[pyenv-doctor](https://github.com/pyenv/pyenv-doctor), 
[pyenv-installer](https://github.com/pyenv/pyenv-installer), 
[pyenv-update](https://github.com/pyenv/pyenv-update), 
[pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv) and 
[pyenv-which-ext](https://github.com/pyenv/pyenv-which-ext)
```bash
$ curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
``` 
Additional information on how to install new python versions on Deepin Linux 
take a look at the [Pyenv on Deepin Linux](#pyenv-on-deepin-linux) section.


### Install nodejs > 6.x on Deepin Linux
Deepin Linux is not added in the supported list of the newer nodejs version. 
The used workaround here is to tell the setup that you are another linux 
distribution. [Credits](https://github.com/nodesource/distributions/issues/442#issuecomment-295227771)
```bash
$ curl -o install_nodejs_8x.sh https://deb.nodesource.com/setup_8.x

# Replace DISTRO=$(lsb_release -c -s) to DISTRO="jessie" within the file

$ cat install_nodejs_8x.sh | sudo -E bash -
$ sudo apt install nodejs
```

### Install solr together with Java
Install [solr](http://lucene.apache.org/solr/) and add a tester core.  
Replace `x.x.x` with the version you want. Eg. `6.0.0` or `7.0.1`. All versions
can be found [here](https://archive.apache.org/dist/lucene/solr/). Also do not 
forget to change the path `/path/to/solr`.
```bash
$ sudo apt install default-jre
$ curl -LO https://archive.apache.org/dist/lucene/solr/x.x.x/solr-x.x.x.tgz
# $_is a special parameter that holds the last argument of the previous command
$ mkdir -P "/path/to/solr" && cd "$_"
$ tar -C . -xf solr-x.x.x.tgz --strip-components=1

# Create a new core
$ ./bin/solr start
$ ./bin/solr create -c tester -n basic_config
```

## Python

### Pyenv on Deepin Linux
On a default Deepin Linux some dev packages, which pyenv's python versions need,
are missing. These dev packages are `bzip2`, `readline`, `openssl` and 
`sqlite3`. Not all of them are mandatory but it is recommended to install them 
all. Install those and then install your python versions.
 
```bash
$ sudo apt install libbz2-dev libreadline-dev libssl-dev libsqlite3-dev
$ pyenv install 3.6.2
```

## Git

### Add file to global git ignore
Add a global gitignore file. 
```bash
$ git config --global core.excludesfile "/path/to/gitignore"
```

Mine contains this: 
```git
# Jetbrains
.idea

# Python Related
ENV
venv
.envrc
.Python

# System artefacts
Thumbs.db
desktop.ini
.DS_Store

# Misc
.coverage
*-COPY
TEMP-*
*.OLD
```

## Misc

### Make sure your .ssh private key file has chmod 400
```bash
$ chmod 400 ~/.ssh/id_rsa
```

### Set vim to default editor
If you use my [zsh configuration](https://github.com/Nachtalb/zsh_configuration.linux/)
the first part of the configuration is already done and you only have to use the
`update-alternatives` command. 
```bash
# Put this in your shells rc file
export VISUAL=vim
export EDITOR="$VISUAL"

# Not every program uses the variables above. Set this as well. 
$ sudo update-alternatives --config editor
```
