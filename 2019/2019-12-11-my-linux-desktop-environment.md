# My Linux Desktop Environment

**2019-12-11 POST IN PROGRESS**

I have used Linux as a desktop environment since about 2006, mostly with Gnome or Cinnamon.

Around 2016 I got bored of the general direction that most desktop environment ("DE" for short) were taking (what I would call "Apple-ization") and decided to tailor, hand craft, optimize and automate my Linux DE.

By no way the aim was to make it sexy, but rather making it more efficient, distraction-free, fast, favoring keyboard usage, using as much display estate as possible.

Look how boring it is:

![Boring](https://blog.wains.be/images/desktop/boring.png)

**Please tell me what would be your first answer if I told you to reformat your computer right now?**

Those questions are certainly popping up in most people head:

- do I actually have all my data backed up?
- I should save that very useful git config somewhere before reformatting!
- and how many hours would it take to get your working environment back to what it was, installing the OS, installing the right packages, reconfiguring options in app X and Y, etc.

I no longer have those concerns, and I will describe all the bits and pieces of my current DE that makes my life easier and probably a bit less stressful.

## Disclaimer

Part of my job is to automate many different stuff for my customers. I enjoy automating all the things (even has a hobby) and I understand many people are not interested in spending time automating their DE.

I still believe, though, that with little efforts, one can improve their desktop experience tremendously.

## This Desktop Environment is Probably not for You

The DE matches my work environment and my own workflows, at this point in time.

I don't expect anyone to think this DE is the absolute best approach to desktops.

I just want to share what I came up with and that give you ideas.

## Computer

A Lenovo Thinkpad T480s with 24GB of RAM and 1TB of SSD, currently running a regular and non customized Fedora Workstation 30 with Libvirt as virtualization layer.

![Thinkpad](https://blog.wains.be/images/desktop/thinkpad.png)

## Virtual Machines (VM)

I almost exclusively work inside Libvirt virtual machines and barely install anything on the host. I use `virt-manager` on the host to access the VM.

I have worked in VM's for the past 3 years.

Advantages:

- VM snapshots
- easy backups of VM on external disk
- easy migration/restore of VM if laptop fails
- thanks to virtual hardware, VM is "portable" from one laptop to another, I don't have to think about different chipsets or such
- I have two almost similar VM: **personal** and **work**. The personal VM acts as "staging" for the work VM. If I'm trying to improve something in my DE, it is first tested on the personal VM, then it is promoted to "production" on the work VM, if the feature is stable/useful/etc.
- I have always split work and personal stuff. I don't see why customer should see private bookmarks when I demo something for them.
- with the QEMU agent, performances can be close to native for a development or sysadmin machine
- Multi-screen is managed by the Fedora host and never caused any problem

Disadvantages:

- you have to install the QEMU agent on the VM
- you have to pause the VM before closing the lid
- changing brightness/volume/etc requires you to get out of the VM (moving the mouse cursor at the top center to collapse the "Leave fullscreen" menu is enough)
- AFAIK multi screen is still not yet available inside a VM, if you must present something on a projector, you have to mirror your host and project your VM
- most audio/video applications perform poorly: video conference, Discord, VLC
- don't expect to play games inside a VM
- when resuming the VM, the clock is not syncing automatically

## My Data

I make sure that all data produced on my VM are backed up on a self-hosted cloud solution. My solution allows _very fast_ restoration, which is crucial.

I don't fret about losing any data.

## VM Installation

I install a minimal Fedora Workstation in latest version.

I can PXE boot from my host machine but usually don't bother with it, installing Fedora is only a few clicks anyway.

## VM post provisioning

Once my OS is up and running, I install Ansible on it (`sudo dnf install ansible`) and run my `guest.yml` playbook.

The playbook takes care of:

- installing packages
- starting services
- creating user
- creating directories
- configuring firewall
- etc.

**IMPORTANT: anything that I do on the VM (such as installing a package) always ends up inside the Ansible playbook. Do _NOT_ be lazy about this or you will quickly lose track of what's installed. Updating the playbook should become a reflex which can be difficult to acquire in the beginning.**

Ansible actions are tagged for either personal machine, work machine or both.

Example of a tagged action:

```
  - name: install pip packages for work
    pip:
      name:
        - td-watson # time tracker
    tags: ['work']
```

Executing the playbook is done like this:

`ansible-playbook -b guest.yml --tags work`

## Dotfiles Management with Stow

The Ansible playbook takes care of installing applications.

I use `stow` to manage most applications configurations.

How does it work?

Basically you create a `dotfiles` directory in your `$HOME` folder.

Say that you want to manage your ZSH configuration (located under `$HOME/.zshrc`). You simply need to create a folder `$HOME/dotfiles/zsh/` and move your `.zshrc` in the folder. Then from the dotfiles folder run `stow zsh`.

A symling has been created:

![Stow](https://blog.wains.be/images/desktop/stow_link.png)

The beauty of this is that your `dotfiles` folder can be a git repository. You can easily keep track of changes in your configurations, revert them or commit them.

![Stow](https://blog.wains.be/images/desktop/stow.png)

### Personal vs Work configurations

There are some application configurations that I want a bit different between the work VM and personal VM.

When the application doesn't support conditions in its config files, you should create (and maintain) two separate configuration files (eg: config-work and config-personal).

In the case I have to figure out how to start the application with a different configuration file. My i3 configuration is one of those and I created a GDM service that starts i3 with `config-personal`:

```
[Desktop Entry]
Name=i3 Personal
Comment=improved dynamic tiling window manager
Exec=i3 -c /home/sw/.i3/config-personal
TryExec=i3
Type=Application
X-LightDM-DesktopName=i3 Personal
DesktopNames=i3 Personal
Keywords=tiling;wm;windowmanager;window;manager;
```

**NOTE:** Some dotfiles managers can generate configuration files based on templates. This comes with the limitation that if you change something in the application GUI, the change would be overwritten the next time the configuration is rebuilt.

<!-- ## i3wm

- tiling windows manager
- monitor resolution
- floating
- scratchpad

### i3blocks

scripts -->

## Terminator

My terminal emulator of choice since 2010.

Terminator comes with cool plugins such as "Watch for activity" or "Watch for silence". When there's activity or silence, you get a notification.

![Terminator](https://blog.wains.be/images/desktop/terminator.gif)

[Plugins](https://terminator-gtk3.readthedocs.io/en/latest/plugins.html) are easily written in Python.

## Fonts

As seen in the GIF above, for the past couple of years, my font of choice for my DE has been Terminus (TTF version since bitmap is no longer supported in recent Pango releases).

## Autokey

[Autokey](https://github.com/autokey/autokey) is a desktop automation utility.

It allows to create keyboard shortcuts for phrases that you type often and even scripts.

This is a keyword for a simple phrase:

![Autokey](https://blog.wains.be/images/desktop/autokey.gif)

And here's a keyword triggering a Python script!

![Autokey Script](https://blog.wains.be/images/desktop/autokey_date.gif)

## Clipit

[Clipit](https://github.com/CristianHenzel/ClipIt) is a lightweight clipboard manager.

This tool obviously implies that any sensitive data is kept for a while. You can filter out some content with regex rules.

## task.sh

For tasks/todo list, I use a tool I wrote myself.

I couldn't find a simple and lightweight task app that integrates well with i3wm, so I wrote my own.

![](https://raw.githubusercontent.com/sebw/task.sh/master/demo.gif)

Download [task.sh](https://github.com/sebw/task.sh)

## Zsh

I use [powerlevel10k](https://github.com/romkatv/powerlevel10k) as my ZSH theme.

I use the following ZSH plugins:

- git
- sudo
- tmux
- k
- dirhistory
- z 
- zsh-autosuggestions
- zsh-syntax-highlighting

<!-- TODO detail what plugins do -->

This is my configuration (be very careful, the order of options in your config is important):

```
export ZSH="${HOME}/.oh-my-zsh"
export TERM="xterm-256color"

ZSH_THEME="powerlevel10k/powerlevel10k"

CASE_SENSITIVE="false"
HYPHEN_INSENSITIVE="true"

POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(context dir dir_writable vcs)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status root_indicator background_jobs history time)

POWERLEVEL9K_BACKGROUND_JOBS_VERBOSE="true"
POWERLEVEL9K_BACKGROUND_JOBS_BACKGROUND="yellow"
POWERLEVEL9K_BACKGROUND_JOBS_FOREGROUND="black"

POWERLEVEL9K_DIR_HOME_BACKGROUND="032"
POWERLEVEL9K_DIR_HOME_SUBFOLDER_BACKGROUND="032"
POWERLEVEL9K_DIR_DEFAULT_BACKGROUND="244"
POWERLEVEL9K_DIR_ETC_BACKGROUND="202"

POWERLEVEL9K_VCS_CLEAN_BACKGROUND="green"
POWERLEVEL9K_VCS_MODIFIED_BACKGROUND="yellow"
POWERLEVEL9K_VCS_UNTRACKED_BACKGROUND="red"

POWERLEVEL9K_STATUS_ERROR_BACKGROUND="red"
POWERLEVEL9K_STATUS_OK_BACKGROUND="green"
POWERLEVEL9K_STATUS_OK_FOREGROUND="black"

POWERLEVEL9K_DIR_PATH_SEPARATOR="%F{black} $(print $'\uE0B1') %F{black}"
POWERLEVEL9K_DIR_PATH_ABSOLUTE=true
POWERLEVEL9K_DIR_OMIT_FIRST_CHARACTER=true

POWERLEVEL9K_HOME_ICON=''
POWERLEVEL9K_HOME_SUB_ICON=''
POWERLEVEL9K_FOLDER_ICON=''
POWERLEVEL9K_ETC_ICON=''

# Plugins
plugins=(git sudo tmux k dirhistory z zsh-autosuggestions)

# Do not start Tmux, otherwise this would mess up vscode terminal and also on Mac
ZSH_TMUX_AUTOSTART=false

# Buffer
ZSH_AUTOSUGGEST_BUFFER_MAX_SIZE=50

# Editor
export EDITOR='vim'

# Custom alias zsh
# Execute commands
alias -s {yml,yaml}=ansible-playbook
alias -s {conf,adoc,md}=code

# cd will show dotfiles
# BUT will not suggest . and ..
_comp_options+=(globdots)
zstyle ':completion:*' special-dirs false

# Mimicking fg behavior from bash (fg 1 instead of fg %1)
# https://stackoverflow.com/questions/32614648/weird-jobs-behavior-within-zsh
fg() {
    if [[ $# -eq 1 && $1 = - ]]; then
        builtin fg %-
    else
        builtin fg %"$@"
    fi
}

# Oh my zsh stuff
source $ZSH/oh-my-zsh.sh

# Ctrl+Space to accept suggestion (MUST come after sourcing oh my zsh stuff see https://github.com/zsh-users/zsh-autosuggestions/issues/471#issuecomment-573500890)
bindkey '^ ' autosuggest-accept

# Syntax highlighting comes as RPM in Fedora. Must be sourced at the end
if [ -f /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh ]; then
	source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
elif [ -f $HOME/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh ]; then
	source $HOME/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
fi

# Custom aliases bash/zsh, must be at the end to override some stuff sourced before by zsh
if [ -f ${HOME}/.bash_aliases ]; then
	source ${HOME}/.bash_aliases
fi
```

## VS Code Editor

My editor of choice is vscode.

I use the following plugins:

![code1](https://blog.wains.be/images/desktop/vscode1.png)

![code2](https://blog.wains.be/images/desktop/vscode2.png)

The most interesting ones are:

- Project Manager: allows to open project directories very easily. Ulauncher also has a plugin using the same database.
- Settings Sync: allows to sync your vscode settings in a Github gist

## Ulauncher

My launcher of choice is Ulauncher, it used to be Alfred but development slowed down.

Ulauncher comes with a ton of nice plugins available at [https://ext.ulauncher.io](https://ext.ulauncher.io).

I wrote and open sourced two plugins to manage [TPLink smart plugs](https://ext.ulauncher.io/-/github-sebw-ulauncher-tplink-home-manager) and another one to [search in my self hosted bookmarks](https://ext.ulauncher.io/-/github-sebw-ulauncher-shaarli).

![](https://raw.githubusercontent.com/sebw/ulauncher-tplink-home-manager/master/demo/demo.gif)

![](https://raw.githubusercontent.com/sebw/ulauncher-shaarli/master/demo.gif)

<!-- 

## Thunar

Custom actions

## Taking notes

xpad

config + notes in cloud (not dotfiles)



## Git

Self hosted Gogs
Git all the things

## Desktop Screenshots and GIF Recording

Script
Flameshot

## Custom Actions with Thunar

gitg
terminator
vscode

## Firefox

Power Tabs

## Bookmarks

Shaarli

## Tmux

## DNF / Flatpak / Snap / Pip -->