# linux-command-collection

## Install pyenv python 3.6.2 & 2.7.13 on deepin linux
```bash
$ sudo apt install libbz2-dev libreadline-dev libssl-dev libsqlite3-dev
$ pyenv install 3.6.2
```

## Make sure your .ssh private key file has chmod 400
```bash
$ chmod 400 ~/.ssh/id_rsa
```

## Install nodejs > 6.x on deepin linux
[Credits](https://github.com/nodesource/distributions/issues/442#issuecomment-295227771)
```bash
$ curl -o install_nodejs_8x.sh https://deb.nodesource.com/setup_8.x

# Replace DISTRO=$(lsb_release -c -s) to DISTRO="jessie" within the file

$ cat install_nodejs_8x.sh | sudo -E bash -
$ sudo apt install nodejs
```

## Install solr together with Java
```bash
$ sudo apt install default-jre
$ curl -LO https://archive.apache.org/dist/lucene/solr/6.0.0/solr-6.0.0.tgz
$ tar -C solr -xf solr-6.0.0.tgz --strip-components=1

# Create a new core
$ ./bin/solr start
$ ./bin/solr create -c tester -n basic_config
```

## Set vim to default editor
```bash
$ sudo update-alternatives --config editor
# Enter ID of vim.basic and press enter
```

## Add file to global gitignore
```bash
$ git config --global core.excludesfile ~/.gitignore_global
```
