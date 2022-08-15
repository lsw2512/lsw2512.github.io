---
title: "Kali initial setup"
permalink: /Kali/
layout: single
author-profile: true
---


## This page will guide you through my initial configuration of kali. This will be some tools i use alot and some personal configuration changes.

1) The first thing I do is make sure the default kali installation is fully up to date

`sudo apt update && sudo apt full-upgrade -y && sudo apt auto-remove -y && sudo apt auto-clean -y`

2) Now I use an amazing script by Dewalt-Arch

[Dewalt-Arch - Pimp my kali](https://github.com/Dewalt-arch/pimpmykali)

Simply run the script and in the option menu select 'N' for new setup.

3) Next I install brave browser.

```
sudo apt install apt-transport-https curl

sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list

sudo apt update

sudo apt install brave-browser

```

4) install terminator

`sudo apt install terminator`

5) install powerline fonts

`Git clone https://github.com/powerline/fonts.git`

5) install rust tool chain

`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`

6) install rustscan 

`cargo install rustscan`

7) install feroxbuster

`cargo install feroxbuster`

