#linux 

# How to install and configure Zsh on Linux

This tutorial will guide you through steps to install Zsh on Linux and Configure it to suit your needs.

**Definition of shell from Wikipedia:** A Unix shell is a command-line interpreter or shell that provides a traditional user interface for the Unix operating system and for Unix-like systems. Users direct the operation of the computer by entering commands as a text for a command line interpreter to execute or by creating text scripts of one or more such commands.

Most fresh installation of Linux comes pre-loaded with a Bash shell. Personally, I like zsh, and it’s my favorite shell that I use all the time.

## Why Zsh?

Zsh does a bunch of other useful things that bash alone won’t accomplish. Apart from being a powerful scripting language, Zsh is a shell designed for interactive use. It incorporates into it many useful features of Bash, ksh, and tcsh. Other additional features provided by zsh are:

1.  Auto Completions are case insensitive much faster than bash.
2.  All sorts of bells and whistles made possible by a community-driven framework like oh-my-zsh.
3.  Support multi-line editing
4.  Recursive file globbing
5.  Highly compatible with ksh.
6.  Zsh has a huge collection of better themes.
7.  Simple configuration style
8.  Output redirection to multiple destinations

And many more, do some googling to learn more. Here you’ll Install Zsh on Linux.

##  Install Zsh Shell on Linux Distributions

Install zsh on ***Arch based*** systems:

```
sudo pacman -S zsh
```

How to install Zsh on ***Gentoo***

```
emerge --ask zsh
```

Install Zsh on Debian based systems such as Ubuntu:

```
sudo apt update
sudo apt install zsh
```

Install Zsh on Fedora / CentOS / Rocky / RHEL:

```
# Fedora / RHEL 8 based sudo dnf install zsh

# CentOS 7 / RHEL 7
sudo yum install zsh
```

## Check and Change shell to Zsh

Confirm it’s installed and see a list of installed shells. After you successfully install Zsh on Linux, you should see version displayed.

```
$ ==zsh --version== 
zsh 5.8 (x86_64-ubuntu-linux-gnu)
```

After you’ve installed it, we need to make it our default shell and customize it to get extra eye-candy. You can change the shell for both root and standard user accounts.

**Non-root account,**

```
sudo usermod ==$USER== -s /usr/bin/zsh
# OR sudo chsh -s /usr/bin/zsh ====$USER====
```

The command above will change shell for current logged in user. You can also specify username:

```
sudo usermod ==username== -s /usr/bin/zsh
# OR sudo chsh -s /usr/bin/zsh ======username======
```

Logout after the change to start using new shell:

```
logout
```

Confirm if current shell is set to Zsh

```
$ ==echo $SHELL==
/usr/bin/zsh
```

If the default Zsh configuration file was not created, manually create empty one:

```
touch ~/.zshrc
```

## Install Oh My Zsh (framework for managing your zsh configuration)

The easiest way to customize zsh is to install Oh My Zsh to set zsh theme. Oh My Zsh is an open source, a community-driven framework for managing your zsh configuration. It comes with a load of plugins and themes to take advantage of. Install it as below.
Prerequisites:

1.  wget
2.  curl
3.  git

Make sure you have all above prerequisites installed on your system.

```
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

New look after install Oh My Zsh framework.

[![install zsh linux](https://computingforgeeks.com/wp-content/uploads/2022/03/install-zsh-linux-1024x501.png?ezimgfmt=rs:696x341/rscb23/ng:webp/ngcb23 "How to install and configure Zsh on Linux 1")](data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20width=%221024%22%20height=%22501%22%3E%3C/svg%3E)

Once installed, you’ll get a bundle of themes that comes with it, located at ~/.oh-my-zsh/themes/

```
$ ==ls -l ~/.oh-my-zsh/themes/==
....omitted output ... -rw-r--r-- 1 ubuntu ubuntu  661 Mar 14 20:46 suvash.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  788 Mar 14 20:46 takashiyoshida.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  356 Mar 14 20:46 terminalparty.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  579 Mar 14 20:46 theunraveler.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  516 Mar 14 20:46 tjkirch.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  514 Mar 14 20:46 tjkirch_mod.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu 1214 Mar 14 20:46 tonotdo.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu 3642 Mar 14 20:46 trapd00r.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu 4379 Mar 14 20:46 wedisagree.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  443 Mar 14 20:46 wezm+.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  366 Mar 14 20:46 wezm.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  333 Mar 14 20:46 wuffers.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  574 Mar 14 20:46 xiong-chiamiov-plus.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  554 Mar 14 20:46 xiong-chiamiov.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu 2426 Mar 14 20:46 ys.zsh-theme
-rw-r--r-- 1 ubuntu ubuntu  727 Mar 14 20:46 zhann.zsh-theme
```

You can also take a look in the plugins directory to see all plugins available.

```
$ ==ls -lh ~/.oh-my-zsh/plugins==
....omitted output ...
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 vscode
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 vundle
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 wakeonlan
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 wd
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 web-search
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 wp-cli
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 xcode
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 yarn
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 yii
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 yii2
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 yum
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 z
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 zbell
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 zeus
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 zoxide
drwxr-xr-x 2 ubuntu ubuntu 4.0K Mar 14 20:46 zsh-interactive-cd
drwxr-xr-x 4 ubuntu ubuntu 4.0K Mar 14 20:46 zsh-navigation-tools
```

### Install Oh My Zsh themes for Zsh

You can install custom themes to ***~/.oh-my-zsh/themes/*** and configure `~/.zshrc` to use it.

- [Best Terminal Shell Prompts for Zsh, Bash and Fish](https://computingforgeeks.com/best-terminal-shell-prompts-for-zsh-bash-fish/)

Modify theme variable name to **ZSH_THEME** in ~/.zshrc. See example below:

```
$ ==vim ~/.zshrc==
ZSH_THEME="==spaceship=="
```

Save changes and exit. Type CTRL+X, Then Y. Source **~/.zshrc** file

```
source ~/.zshrc
```

#### Configure Help command.

```
vim ~/.zshrc
```

Add the following lines to the end.

```
autoload -U run-help
autoload run-help-git
autoload run-help-svn
autoload run-help-svk
alias help=run-help
```

Source it and you’re good to go.

```
source ~/.zshrc
```

#### Fish-like syntax highlighting (Optional)

Clone code to plugins folder:

```
cd ~/.oh-my-zsh/plugins 
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git 
vim ~/.zshrc
```

Add below the line at the end,

```
source ~/.oh-my-zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

Then source zshrc file

```
source ~/.zshrc
```

Persistent rehash: This allows compinit to automatically find new executables in the $PATH.

```
vim ~/.zshrc
```

Add line:

```
zstyle ':completion:*' rehash true
```

Save and exit, the source it.

```
source ~/.zshrc
```

#### zsh-completions

Configure additional zsh-completions, applicable to all Linux systems. I will assume you already installed oh-my-zsh, if not refer to it above.

```
git clone https://github.com/zsh-users/zsh-completions ~/.oh-my-zsh/custom/plugins/zsh-completions
```

Then enable it in your .zshrc

```
vim ~/.zshrc
```

Add the lines below:

```
plugins+=(zsh-completions)
autoload -U compinit && compinit
```

#### zsh tab-completion system

To enable the famous zsh tab-completion system, you need to add above commands ( **autoload -U compinit && compinit**).
If you are running [Arch Linux](https://computingforgeeks.com/category/arch-linux/), you can install it using Pacman package manager. This has an advantage of getting updates for it automatically.

```
pacman -S zsh-completions
```

Installing  zsh-completions on Gentoo

```
emerge --ask zsh-completions
```

Install zsh-completions on Fedora / CentOS / RHEL / Scientific Linux:

```
cd /etc/yum.repos.d/
wget https://download.opensuse.org/repositories/shells:zsh-users:zsh-completions/RHEL_7/shells:zsh-users:zsh-completions.repo
yum install zsh-completions
```

Also, check [Configure Zsh syntax highlighting on Linux / macOS](https://computingforgeeks.com/how-to-configure-zsh-syntax-highlighting-on-linux-macos/)

## Conclusion

We’ve covered how to Install Zsh on Linux and configuring Zsh environment on your system. Zsh is the most customizable shell I have ever used. It’s easy to install and customize with more than 100 themes. There are plenty of plugins to extend its functionality with frameworks like oh-my-zsh.