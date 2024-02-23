# General Info
- Distribution: **Fedora 39 Workstation**
- Desktop: **Gnome**
- Terminal Style: **[oh-my-bash](https://github.com/ohmybash/oh-my-bash) standard**
  - `bash -c "$(wget https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh -O -)"`

## Preview
![image](https://github.com/BinarSkugga/linux-config/assets/7575628/cd3a64cf-8d1d-491b-aa9c-8a28e9d4158f)


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
- Execute `gnome-terminal` on `CTRL+SHIFT+T`
- Execute `flameshot gui` on `SHIFT+PRTSRC`

# DNF Config
Find the config file
```
sudo find / -name dnf.conf
```

```
[main]
gpgcheck=True
installonly_limit=2
clean_requirements_on_remove=True
best=False
skip_if_unavailable=True
max_parallel_downloads=10
fastestmirror=True
```

## Misc Packages
```
sudo dnf install neofetch
```

# Docker
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

# Python
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

# Node
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

# Jetbrains Toolbox
Install the toolbox (swap version for the one downloaded)
```
sudo tar -xvzf ~/Downloads/jetbrains-toolbox-{version}.tar.gz
sudo mv ~/Downloads/jetbrains-toolbox-{version} /opt/jetbrains
/opt/jetbrains/jetbrains-toolbox
```

# Chrome Tweaks
Channel: **unstable**

Find `.desktop` file
```
sudo find / -name *chrome*.desktop
```

Create a new one with with
```
[Desktop Entry]
Version=1.0
Name=Google Chrome (Clean)
Exec=/usr/bin/google-chrome-stable --disable-session-crashed-bubble --hide-crash-restore-bubble --disable-default-apps --disable-sync %U
StartupNotify=true
Terminal=false
Icon=google-chrome-stable
Type=Application
Categories=Network;WebBrowser;
MimeType=application/pdf;application/rdf+xml;application/rss+xml;application/xhtml+xml;application/xhtml_xml;application/xml;image/gif;image/jpeg;image/png;image/webp;text/html;text/xml;x-scheme-handler/http;x-scheme-handler/https;
Actions=new-window;new-private-window;

[Desktop Action new-window]
Name=New Window
Exec=/usr/bin/google-chrome-stable --disable-session-crashed-bubble --hide-crash-restore-bubble --disable-default-apps --disable-sync

[Desktop Action new-private-window]
Name=New Incognito Window
Exec=/usr/bin/google-chrome-stable --incognito --disable-session-crashed-bubble --hide-crash-restore-bubble --disable-default-apps --disable-sync
```
Add the following policies in `/etc/opt/chrome/policies/managed/00_gssapi.json`:
```
{
        "DefaultNotificationsSetting": 2,
        "DefaultGeolocationSetting": 2,
        "HttpsOnlyMode": "force_enabled",
        "AutoplayAllowed": false,
        "SyncDisabled": true,
        "ClearBrowsingDataOnExitList": [
                "browsing_history",
                "cookies_and_other_site_data",
                "cached_images_and_files",
                "autofill",
                "site_settings",
                "download_history"
        ]
}
```

What it does:
- **Disables sync with google account**
- **Disables session restore**
- **Disables default applications**

Manual Steps:
- **Disable password manager**
- **Disable payment methods**
- **Disable addresses**
- **Don't allow notifications and locations**
- **Enable memory saver**
- **Remove all search engines except Google**
- **Always show bookmark bar**
- **Extensions:**
  - **[Tabby Cat](https://chromewebstore.google.com/detail/tabby-cat/mefhakmgclhhfbdadeojlkbllmecialg?hl=en)**
  - **[LastPass](https://chromewebstore.google.com/detail/lastpass-free-password-ma/hdokiejnpimakedhajhdlcegeplioahd?hl=en)**
  - **[Ghostery](https://chromewebstore.google.com/detail/ghostery-%E2%80%93-privacy-ad-blo/mlomiejdfkolichcflejclcbmpeaniij?hl=en)**
  - **[WebSocket King](https://chromewebstore.google.com/detail/websocket-king-client/cbcbkhdmedgianpaifchdaddpnmgnknn)**

Favorites:
- **[CyberChef](https://gchq.github.io/CyberChef/)**
- **[Gitlab](https://gitlab.com/dashboard)**
- **[Miro](https://miro.com/app/dashboard/)**

# General Applications
- **[Spotify](https://open.spotify.com/)**
- **[MQTTX](https://mqttx.app/)**
- **[Insomnia](https://insomnia.rest/)**
- **[Flameshot](https://flameshot.org/)**
