---
title: bashからzshに鞍替え
tags:
  - Zsh
private: false
updated_at: '2024-10-29T11:42:48+09:00'
id: 16c0e03b601d7f062702
organization_url_name: null
slide: false
ignorePublish: false
---
## 環境

- ubuntu22.04

## zshのインストール

```zsh:bash
sudo apt update
sudo apt install zsh
```

## ログインシェルの変更

```zsh:zsh
zsh
chsh -s $(which zsh)
```

できたら

```
echo $SHELL
```

でログインシェルが変更できているか確認する。

`/usr/bin/zsh`と出力されればOK。



余談だが、
```
echo $0
```
で現在使用しているシェルを確認できる。

## preztoを設定

### インストール

クローンする

```zsh:zsh
git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"
```

### 設定ファイル作る

```zsh:zsh
setopt EXTENDED_GLOB
for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
  ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
done
```

root直下に
.zlogin
.zlogout
.zpreztorc
.zprofile
.zshenv
.zshrc
ができていることを確認する.
ファイルがすでにあるとエラーが出ます.

### 設定

`.zpreztorc`の30行目らへんにこんなのがある

```diff_batchfile:.zpreztorc
# Set the Prezto modules to load (browse modules).
# The order matters.

zstyle ':prezto:load' pmodule \
  'environment' \
  'terminal' \
  'editor' \
  'history' \
  'directory' \
  'spectrum' \
  'utility' \
  'completion' \
  'prompt'
```

それにちょびっと付け加える

```diff_batchfile:.zpreztorc
zstyle ':prezto:load' pmodule \
  'environment' \
  'terminal' \
  'editor' \
  'history' \
  'directory' \
  'spectrum' \
  'utility' \
  'completion' \
+ 'git' \
+ 'syntax-highlighting' \
+ 'autosuggestions' \
  'prompt'
```

### テーマの変更

https://qiita.com/abirutakayuki/items/4e04114b702f8e36def7#cloud

これを見たらたぶんわかる.
`.zpreztorc`の115行目とかそのくらいにある、
`zstyle ':prezto:module:prompt' theme 'sorin'`
のsorinのとこを好きなやつに変えてください。
僕はcloudが好きなので

```
zstyle ':prezto:module:prompt' theme 'cloud'
```

としてください.

## ターミナル再起動

おしまい
