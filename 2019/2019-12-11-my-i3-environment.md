# My Linux Desktop Environment

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

Part of my job is to automate stuff for my customers. I enjoy automating all the things and I understand many people are not interested in spending time automating their DE.

This post is here to give you ideas and would never be the _best_ DE for anyone. It's the one that works for me at this point in time, and I'm bringing changes and improvements to it on a very regular basis. NB: expect this post to be updated.

## Computer

A Lenovo Thinkpad T480s with 24GB of RAM and 1TB of SSD.

![Thinkpad](https://blog.wains.be/images/desktop/thinkpad.png)

It currently runs a Fedora 30 minimal with Libvirt as virtualization layer.

## Virtual Machines

I work inside Libvirt virtual machines and barely install anything on the host. I use `virt-manager` on the host to access the VM.

Advantages:

- VM snapshots
- easy backups of VM on external disk
- easy migration/restore of VM if laptop fails
- VM is "portable" (should I change from Lenovo to a HP laptop wouldn't be a problem)
- I have two almost similar VM: personal and work. The personal VM acts as "staging" for the work VM. If I'm trying to improve something in my DE, it is tested on the personal VM first, then is promoted to "production" on the work VM.
- splitting personal and work in two VM prevents being tracked from social media in the work VM, for example
- with the QEMU agent, performances are close to native (excluding video playing)

Disadvantages:

- you have to install the QEMU agent on the VM
- you have to pause the VM before closing the lid
- changing brightness/volume/etc requires you to get out of the VM
- AFAIK multi screen is still not yet available in a VM, if you must present something on a projector, you have to project your VM
- applications like video conference might act up or perform poorly, I install my work video conference app on the host
- when resuming the VM, the clock is not syncing automatically

## My Data

I make sure that all data produced on my VM are backed up on a self-hosted cloud solution. My solution allows _very fast_ restoration, which is crucial.

I don't fret about losing any data.

## VM Installation

I install a minimal Fedora Workstation in latest version.

## VM Provisioning

Once my OS is up and running, I install Ansible on it and run my `guest.yml` playbook.

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

## i3wm

- tiling windows manager
- monitor resolution
- floating
- scratchpad

### i3blocks

scripts

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

<!-- ## Zsh

## VS Code Editor

Plugins:

- Sync Settings
- Project Manager

## Ulauncher

Desktop shortcuts

- extensions

## Thunar

Custom actions

## Taking notes

xpad

config + notes in cloud (not dotfiles)

## Desktop Screenshots and GIF Recording

Script
Flameshot

## Custom Actions with Thunar

gitg
terminator
vscode

## DNF / Flatpak / Snap / Pip -->