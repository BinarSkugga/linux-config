# General Info
- Distribution: **Fedora 39 Workstation**
- Desktop: **Gnome**
- Terminal Style: **[oh-my-bash](https://github.com/ohmybash/oh-my-bash) standard**
  - `bash -c "$(wget https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh -O -)"`  

# Gnome Configurations
Extensions: 
- [Dash to panel](https://extensions.gnome.org/extension/1160/dash-to-panel/)
- [ArcMenu](https://extensions.gnome.org/extension/3628/arcmenu/)
- [Systemd Manager](https://extensions.gnome.org/extension/4174/systemd-manager/)
- [Weather O'Clock](https://extensions.gnome.org/extension/5470/weather-oclock/)

## Tweaks
- Fonts: **All Open Sans except Monospace**
- Mouse Click Emulation: **Area**
- Titlebar Actions: **Middle-Click Minimize**
- Titlebar Buttons: **Maximize & Minimize**

## Docker
Install Docker
```
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
sudo dnf update -y
sudo dnf install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Add access to my user & reboot
```
sudo usermod -aG docker $USER
reboot
```

Setup as a service
```
sudo systemctl start docker
sudo systemctl enable docker
```

## Python
Install PyEnv
```
sudo dnf -y install make gcc patch zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel tk-devel libffi-devel xz-devel libuuid-devel gdbm-libs libnsl2
curl https://pyenv.run | bash
```

Final `.bashrc` with python optimizations
```
# PYENV
export PYENV_ROOT="$HOME/.pyenv"
export PYTHON_CONFIGURE_OPTS='--enable-optimizations --with-lto'
export PYTHON_CFLAGS='-march=native -mtune=native'
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

Reload `.bashrc` & install Python 3.11
```
source .bashrc
pyenv install 3.11
pyenv global 3.11
```

## Node
Install NVM
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
```

Final `.bashrc` with `NVM_BIN` path
```
# NODEJS
export NVM_DIR="$HOME/.nvm"
export PATH="$PATH:$NVM_BIN"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

Reload `.bashrc` & install LTS
```
source .bashrc
nvm install --lts
nvm use --lts
```

## Jetbrains Toolbox
Install the toolbox (swap version for the one downloaded)
```
sudo tar -xvzf ~/Downloads/jetbrains-toolbox-{version}.tar.gz
sudo mv ~/Downloads/jetbrains-toolbox-{version} /opt/jetbrains
/opt/jetbrains/jetbrains-toolbox
```
