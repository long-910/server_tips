---
Copyright: (C) 2023 long-910
marp: true
theme: 
paginate: true

---
<!--
headingDivider: 2
-->
# server_tips

[Ubuntu Server 22.04.2 LTS](https://ubuntu.com/download/raspberry-pi/thank-you?version=22.04.2&architecture=server-arm64+raspi)をインストール後の設定を残す。

## Add User

### Add New User

```bash
$ sudo adduser User_Name
$ ls -l /home
$ sudo gpasswd -a User_Name sudo
```

### Delete ubuntu user

```bash
$ sudo userdel -r ubuntu
```

## Install Apps

### tmux

```bash
$ sudo apt install tmux
$ which tmux
$ curl https://raw.githubusercontent.com/long-910/home/main/.tmux.conf > .tmux.conf
```
---
### zsh

```bash
$ sudo apt install zsh
$ which zsh
$ chsh
Changing the login shell for long910
Enter the new value, or press ENTER for the default
	Login Shell [/bin/bash]: /usr/bin/zsh
#Logout/Login
$ echo $SHELL
/usr/bin/zsh
$ curl https://raw.githubusercontent.com/long-910/home/main/.zshrc > .zshrc
$ source .zshrc
```
---
### emacs

```bash
$ sudo apt install emacs
$ which emacs
$ curl https://raw.githubusercontent.com/long-910/home/main/.emacs.el > .emacs.el
```

## Setting SSH

### 公開鍵を Ubuntu に SCP で送付,登録

```bash
# SCPでサーバーに公開鍵を送付
$ mkdir .ssh
$ cat id_rsa.pub > ~/.ssh/authorized_keys
$ chmod 600 .ssh/authorized_keys
```
---
### Config設定
```bash
$ sudo emacs /etc/ssh/sshd_config
```

```diff
-#Port 22
+Port 2222

-#PermitRootLogin prohibit-password
+PermitRootLogin no

-#PubkeyAuthentication yes
+PubkeyAuthentication yes

-#PermitEmptyPasswords no
+PermitEmptyPasswords no
```
### sshdを再起動
```bash
$ sudo service ssh restart
```
## ufw

```bash
$ sudo apt-get install ufw
$ sudo ufw allow 2222/tcp
$ sudo ufw enable
```

