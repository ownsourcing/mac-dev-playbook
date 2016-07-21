# Mac Development Ansible Playbook

We're adapting this playbook to install and configure most of the software our team uses on Macs for web and software development. It's forked directly from and periodically gets updates from [continue edits that give credit and explain]...

Some things in OS X are difficult to automate (notably, the Mac App Store and certain tools from Apple), so we still have some manual installation steps, but at least it's all documented here.

This is a work in progress, and is mostly a means for us to document our preferred Mac setup from a clean install. We'll sync this repo with GeerlingGuy's as he and we add settings and packages to this set of playbooks over time.

## Installation

  1. Install Ansible with the following commands
    - sudo easy_install pip
    - sudo pip install ansible
    - xcode-select --install
  2. Ensure Apple's command line tools are installed (`xcode-select --install` to launch the installer).
  3. Clone this repository to your local drive.
  4. Run the command `$ ansible-galaxy install -r requirements.yml` inside this directory to install required Ansible roles.
  5. Run `ansible-playbook main.yml -i inventory -u [username] -U [username] --ask-sudo-pass` from the same directory as this README file (substitute `[username]` for your macOS account username). Enter your account password when prompted.

## Included Applications / Configuration

Applications (installed with Homebrew Cask):

  - Adium
  - BetterTouchTool
  - Google Chrome
  - Dropbox
  - Firefox
  - Handbrake
  - Homebrew
  - Karabiner
  - LICEcap
  - MacVim
  - Menu Meters
  - nvALT
  - Sequel Pro (MySQL client)
  - Skype
  - Skitch
  - Slack
  - Seil
  - Sublime Text
  - TextMate
  - TimeMachineEditor
  - Tower (Git client)
  - Transmit (S/FTP client)
  - Vagrant (+ Vagrant Manager)
  - VirtualBox
  - VLC
  -

Packages (installed with Homebrew):

  - ansible
  - atom
  - autoconf
  - gettext
  - libevent
  - packer
  - python
  - sqlite
  - mysql
  - php56 (+ php56-xdebug)
  - ssh-copy-id
  - cowsay
  - ios-sim
  - readline
  - subversion
  - kdiff3
  - openssl
  - pv
  - drush
  - wget
  - brew-cask

OwnSourcing [dotfiles](https://github.com/ownsourcing/dotfiles) (derived from work by [GeerlingGuy](https://github.com/gerlingguy/dotfiles), as is the rest of this playbook) are also installed into the current user's home directory (@TODO - confirm this location is in fact being used), including the `.osx` dotfile for configuring many aspects of Mac OS X for better performance and ease of use.

Finally, there are a few other preferences and settings added on for various apps and services.

## Future additions

### Things that still need to be done manually

It's my hope that I can get the rest of these things wrapped up into Ansible playbooks soon, but for now, these steps need to be completed manually (assuming you already have Xcode and Ansible installed, and have run this playbook).

  1. Set JJG-Term as the default Terminal theme (it's installed, but not set as default automatically).
  2. Install [Sublime Package Manager](http://sublime.wbond.net/installation).
  3. Install all the Mac App Store Apps (see below).
  4. Install all the apps that aren't yet in this setup (see below).
  5. Remap Caps Lock to Escape (keycode 53), using [Seil](https://pqrs.org/osx/karabiner/seil.html.en).
  6. Set trackpad tracking rate.
  7. Set mouse tracking rate.
  8. Configure extra Mail and/or Calendar accounts (e.g. Google, Exchange, etc.).

### Applications/packages to be added:

These are mostly direct download links, some are more difficult to install because of custom installers or other nonstandard install quirks:

  - [iShowU HD](http://downloads.shinywhitebox.com/iShowU_HD_Pro_2.3.7.dmg)
  - xquartz

### Configuration to be added:

  - I have vim configuration in the repo, but I still need to add the actual installation:
    ```
    mkdir -p ~/.vim/autoload
    mkdir -p ~/.vim/bundle
    cd ~/.vim/autoload
    curl https://raw.githubusercontent.com/tpope/vim-pathogen/master/autoload/pathogen.vim > pathogen.vim
    cd ~/.vim/bundle
    git clone git://github.com/scrooloose/nerdtree.git
    ```

  - in order to have all apps appear in /Applications vs ~/Applications, use
    ```
    export HOMEBREW_CASK_OPTS="--appdir=/Applications"
    ```

  - to have git ignore certain files globally, use  
    ```
    printf '.DS_Store\n' > .gitignore_global
    git config --global core.excludesfile ~/.gitignore_global
    ```

  - to have git include standing aliases and upstreams, use (?)


### Apps only available via the App Store

I also use the following apps at least once or twice per week, but unfortunately, as the Mac App Store is not able to be controlled via CLI, or any other way I can find (so far), I have to manually install all of these apps from within the App Store application.

  - Tweetbot
  - RadarScope
  - Pixelmator
  - Quick Resizer
  - 1Password
  - DaisyDisk
  - Byword
  - Aperture
  - Pages
  - Keynote
  - Numbers

There are a couple other apps I'm leaving out of the list, like Microsoft Word, because I normally don't install them unless/until I need them.

## Testing the Playbook

Many people have asked me if I often wipe my entire workstation and start from scratch just to test changes to the playbook. Nope! Instead, I posted instructions for how I build a [Mac OS X VirtualBox VM](https://github.com/geerlingguy/mac-osx-virtualbox-vm), on which I can continually run and re-run this playbook to test changes and make sure things work correctly.

## Ansible for DevOps

Check out [Ansible for DevOps](http://www.ansiblefordevops.com/), which will teach you how to do some other amazing things with Ansible.

## Author

[Jeff Geerling](http://jeffgeerling.com/), 2014 (originally inspired by [MWGriffin/ansible-playbooks](https://github.com/MWGriffin/ansible-playbooks)).
