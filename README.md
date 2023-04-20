# my-mac-setup

mac tools for a windows/linux origin developer

# Basic tools

| name                 | link                                                                                  | note                        |
|----------------------|---------------------------------------------------------------------------------------|-----------------------------|
| Firefox              | https://www.mozilla.org/fr/firefox/new/                                               |                             |
| Bitwarden            | https://bitwarden.com/download/                                                       | also available in mac store |
| Yubiko Authenticator | https://www.yubico.com/products/yubico-authenticator/#h-download-yubico-authenticator | also available in mac store |
| Discord              | https://discord.com/                                                                  |                             |
| Telegram Lite        | https://desktop.telegram.org/                                                         | available in mac store      |

## Firefox extensions

| name                             | link                                                                      | note                                                 |
|----------------------------------|---------------------------------------------------------------------------|------------------------------------------------------|
| uBlock Origin                    | https://addons.mozilla.org/fr/firefox/addon/ublock-origin/                | Block Ads                                            |
| Consent-O-Matic                  | https://addons.mozilla.org/en-US/firefox/addon/consent-o-matic/           | refuse all tracking cookies, hide banner             |
| SponsorBlock                     | https://addons.mozilla.org/fr/firefox/addon/sponsorblock/                 | Skip sponsor in videos                               |
| Return YouTube Dislike           | https://addons.mozilla.org/en-US/firefox/addon/return-youtube-dislikes/   |                                                      |
| Firefox Multi-Account Containers | https://addons.mozilla.org/fr/firefox/addon/multi-account-containers/     | usefull to manage different identities on same sites |
| Bitwarden                        | https://addons.mozilla.org/fr/firefox/addon/bitwarden-password-manager/   |                                                      |
| FreshRSS-Notify                  | https://addons.mozilla.org/fr/firefox/addon/freshrss-notify-webextension/ | Get notifications of my rss feeds                    |
| React Developer Tools            | https://addons.mozilla.org/en-US/firefox/addon/react-devtools/            |                                                      |
| JSON Lite                        | https://addons.mozilla.org/en-US/firefox/addon/json-lite/                 | view json file in browser                            |
| XML Viewer Plus                  | https://addons.mozilla.org/fr/firefox/addon/xml-viewer/                   | View XML in browser                                  |

# Utils tools

| name                 | link                                                    | note                                                                                      |
|----------------------|---------------------------------------------------------|-------------------------------------------------------------------------------------------|
| french-nf-azerty-mac | https://github.com/cyril-L/french-nf-azerty-mac         | French NF Z 71‐300 Layout                                                                 |
| Karabiner-Elements   | https://karabiner-elements.pqrs.org/                    | A powerful and stable keyboard customizer for macOS. To combine with `PC-Style Shortcuts` |
| PC-Style Shortcuts   | https://ke-complex-modifications.pqrs.org/#pc_shortcuts | allow to use classical Windows/Linux Shortcuts style                                      |
| BetterDisplay        | https://github.com/waydabber/BetterDisplay#readme       | I used it to have HiDPI FHD resolution on my external screen                              |
| Rectangle            | https://rectangleapp.com/                               | intuitive tiling snaps                                                                    |

Thanks
to [@JonathanReez](https://apple.stackexchange.com/questions/312656/how-can-i-reprogram-osx-to-use-windows-style-shortcuts-for-all-operations/312864#312864)
for Karabiner and Shortcuts tip.
Also about karabiner > Settings > Simple Modifications > LDLC AZERTY+ (A4Tech)

- keypad_period > m (like that numpad dot will input a dot instead comma)
- non_us_backslash > grave_accent_and_tilde (because my `@` and `<` key are inverted)
- grave_accent_and_tilde > non_us_backslash

# Dev tools

| name              | link                                         | note                               |
|-------------------|----------------------------------------------|------------------------------------|
| Homebrew          | https://brew.sh/index_fr                     | MacOS Package manager              |
| git               | https://git-scm.com/download/mac             | `brew install git`                 |
| gpg               | https://gnupg.org/                           | `brew install gpg`                 |
| pinentry          | https://github.com/GPGTools/pinentry         | `brew install pinentry-mac`        |
| volta             | https://volta.sh/                            | Node.js version manager            |
| Jetbrains Toolbox | https://www.jetbrains.com/fr-fr/toolbox-app/ | IDE Installer tool from jetbrains  |
| WebStorm          | https://www.jetbrains.com/fr-fr/webstorm/    | HTML - CSS - JS IDE from Jetbrains |
| Zed               | https://zed.dev/download                     | lightweight text editor            |
| iTerm2            | https://iterm2.com/downloads.html            | better terminal                    |

## git setup

```zsh
echo '.idea' >> ~/.gitignore
git config --global user.name 'tpoisseau'
git config --global user.email '22891227+tpoisseau@users.noreply.github.com'
git config --global core.excludesfile /Users/tpoisseau/.gitignore
git config --global init.defaultBranch main
```

### git ssh setup

Generate https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key

```zsh
ssh-keygen -t ed25519 -C "22891227+tpoisseau@users.noreply.github.com" -f ~/.ssh/id_ed25519_tpoisseau_github
touch ~/.ssh/config
open ~/.ssh/config
```

with content

```
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519_tpoisseau_github
```

Add in GH
account https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account#adding-a-new-ssh-key-to-your-account

```zsh
pbcopy < ~/.ssh/id_ed25519_tpoisseau_github
```

https://github.com/settings/ssh/new

```zsh
ssh -T git@github.com
```

### git gpg setup

Genrate https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key#generating-a-gpg-key

```zsh
gpg --full-generate-key
# use 22891227+tpoisseau@users.noreply.github.com as email
gpg --list-secret-keys --keyid-format=long
gpg --armor --export <sec>
```

https://github.com/settings/gpg/new

```zsh
git config --global --unset gpg.format
git config --global user.signingkey <sec>
git config --global commit.gpgsign true

if [ -r ~/.zshrc ]; then echo 'export GPG_TTY=$(tty)' >> ~/.zshrc; \
  else echo 'export GPG_TTY=$(tty)' >> ~/.zprofile; fi

if [ -r ~/.bash_profile ]; then echo 'export GPG_TTY=$(tty)' >> ~/.bash_profile; \
  else echo 'export GPG_TTY=$(tty)' >> ~/.profile; fi

echo "pinentry-program $(which pinentry-mac)" >> ~/.gnupg/gpg-agent.conf
killall gpg-agent
```
