---
theme: seriph
background: ./resources/nixwall.png
class: text-center
highlighter: shiki
lineNumbers: false
title: Nix Deep Dive
info: |
  A Deep Dive into Nix and How to Use it
drawings:
  persist: false
transition: slide-left
mdc: true
---

# A Deep Dive into Nix and How to Use it<br><br>
Declarative, Reproducible, Immutable, and Reliable Package Management with Nix

University of Guilan, Rasht, Iran, 2025

---
---
# Table of Contents
<ol>
<v-click>
<li>What is Nix ?<br>
    1.1 How and Why Nix was created<br>
    1.2 Nix Language Crash Course<br>
    1.3 How The Nix Package Manager Works<br></li></v-click>
<v-click>
<li>How to integrate Nix into your workflow<br>
    2.1 Using NixOS<br>
    2.2 Using Nix Shells<br>
    2.3 Using Nix Flakes<br>
    2.4 Using Home Manager<br>
    2.5 Using The Nix Package Manager<br></li>
</v-click>
</ol>
---
layout: default
---

<div class="grid grid-cols-[30%_70%] gap-8 h-full items-center">

<div class="flex flex-col justify-center">

<img src="./resources/pfp.jpg" class="w-full object-cover rounded-lg shadow-lg mb-4" />

<div style="font-size: 27px; font-weight: bold;">Farbod Khalili Khoshehmehr</div>

Computer Engineering Student at University of Guilan

</div>

<div class="flex flex-col justify-top">

## Why should you listen to me

<v-clicks>

- I've been using NixOS for more than a year

- I've read the 250+ page PhD thesis documenting the inner workings of Nix titled: "The Purely Functional Software Deployment Model"

- I've wrote a poem for NixOS (available for reading at the end of the slides)

   So yeah I'm **VERY** interested in Nix and NixOS
</v-clicks>

</div>
</div>
---
---
<div class="relative h-full flex items-center justify-center">
  <h1 class="text-5xl font-bold text-white drop-shadow-lg" style="font-size: 70px;">1. What is Nix ?</h1>
</div>
---
---
# The How
Nix
<div class="grid grid-cols-[70%_30%] gap-8 h-full items-center">

<div class="flex flex-col justify-center">
  The creation of Nix started in 2003 by Eelco Dolstra as an academic research project. The foundational concepts were introduced to the world in 2004 through the paper "Nix: A Safe and Policy-Free System for Software Deployment" which laid out its revolutionary purely functional model. This theoretical foundation was then expanded into a comprehensive framework in Dolstra's 2006 PhD dissertation, "The Purely Functional Software Deployment Model." From these robust academic roots, the project grew steadily in the open-source world, reaching its stable 1.0 release in 2012.
</div>
<div class="flex flex-col justify-top">
<img src="./resources/Eelco-Dolstra.jpg" class="w-full object-cover rounded-lg shadow-lg mb-4" />
<p style="position: relative; left: 30%;">Eelco Dolstra</p>
</div>
</div>
---
---
# The How
NixOS
<div class="grid grid-cols-[70%_30%] gap-8 h-full items-center">

<div class="flex flex-col justify-center">
The first NixOS prototype was created by Armijn Hemel in 2006 as part of his Master's thesis "NixOS: The Nix Based Operating System", which explored applying Nix and its principles to a Linux distribution. Hemel demonstrated the application of package management, system services, kernel management, and other principles that defined NixOS. After continued development, NixOS issued its first stable release, version 13.10, in 2013.

A Dutch non-profit foundation, named The NixOS Foundation, was established in 2015 to support the development and community infrastructure of NixOS and related Nix projects
</div>
<div class="flex flex-col justify-top">
<img src="./resources/Armijn-Hemel.jpg" class="w-full object-cover rounded-lg shadow-lg mb-4" />
<p style="position: relative; left: 30%;">Armijn Hemel</p>
</div>
</div>
---
---
# The Why
reliable software deployment

Going back to Nix, it was made to adress a lot of issues that plagued how software deployment worked back then; and to this day (aside from Nix itself) all software deployment systems include some or all of the following (shortend) list of issues:

 - Dependency specifications are not validated, leading to incomplete deployment.
 - Dependency specifications are inexact (e.g., nominal).
 - It is not possible to deploy multiple versions or variants of a component side-by-side.
 - Components can interfere with each other.
 - It is not possible to roll back to previous configurations.
 - Upgrade actions are not atomic.
 - Applications must be monolithic, i.e., they must statically contain all their dependencies.
 - Deployment actions can only be performed by administrators, not by unprivileged users.
---
---
<div class="relative h-full flex items-center justify-center">
  <h1 class="text-5xl font-bold text-white drop-shadow-lg" style="font-size: 50px;">Nix Language Crash Course</h1>
</div>
---
layout: center
---

<div class="text-center text-6xl font-bold leading-tight">
  <span class="relative inline-block">
    <svg v-click="['+1', '+1']" class="absolute pointer-events-none" style="left: -30px; top: -30px; width: calc(100% + 60px); height: calc(100% + 60px);">
      <ellipse cx="50%" cy="60%" rx="48%" ry="35%" fill="none" stroke="#ba5c3dff" stroke-width="6"
        transform="rotate(-3 50 50)" style="stroke-linecap: round;" pathLength="100"
        stroke-dasharray="100" stroke-dashoffset="0" />
    </svg>
    <span class="relative z-10">Purely Functional</span>
  </span>
  <span class="relative inline-block ml-4">
    <svg v-click="['+0', '+1']" class="absolute pointer-events-none" style="left: -30px; top: -30px; width: calc(100% + 60px); height: calc(100% + 60px);">
      <ellipse cx="50%" cy="58%" rx="48%" ry="35%" fill="none" stroke="#4a70c0ff" stroke-width="6"
        transform="rotate(-2 50 50)" style="stroke-linecap: round;" />
    </svg>
    <span class="relative z-10">Domain-specific</span>
  </span>
  <span class="relative inline-block ml-4">
    <svg v-click="['+0', '+1']" class="absolute pointer-events-none" style="left: -30px; top: -30px; width: calc(100% + 60px); height: calc(100% + 60px);">
      <ellipse cx="50%" cy="45%" rx="48%" ry="36%" fill="none" stroke="#42a165ff" stroke-width="6"
        transform="rotate(3 50 50)" style="stroke-linecap: round;" />
    </svg>
    <span class="relative z-10">Turing Compelete</span>
  </span>
  Programming language
</div>

<style>
.slidev-vclick-hidden {
  opacity: 0;
}

.slidev-vclick-fade {
  transition: opacity 0.3s ease;
}
</style>

---
layout: center
class: text-center
---

<div  class="relative h-full flex items-center justify-center">
<h1 class="text-5xl font-bold text-white drop-shadow-lg" style="font-size: 40px;">Data Types in Nix</h1></div>
<div class="grid-container">
  <div v-click class="grid-item top-left">
    <div class="content">
      <strong>Int: <code>4</code><br>Float: <code>4.1</code></strong>
    </div>
  </div>
  
  <div v-click class="grid-item top-center">
    <div class="content">
      <strong>Boolean:<br><code>true / false</code></strong>
    </div>
  </div>
  
  <div v-click class="grid-item top-right">
    <div class="content">
      <strong>String:<br><code>"1line"<br>''multi<br>line''</code></strong>
    </div>
  </div>
  
  <div v-click class="grid-item bottom-left">
    <div class="content">
      <strong>Path:<br><code>./rel/path<br>/absolute/path</code></strong>
    </div>
  </div>
  
  <div v-click class="grid-item bottom-center">
    <div class="content">
      <strong>List:<br><code>[./one "2" 3]</code></strong>
    </div>
  </div>
  
  <div v-click class="grid-item bottom-right">
    <div class="content">
      <strong>Attribute Set:</strong><br/>
      <code>{a = "hello";<br/>
      b = false;}</code>
    </div>
  </div>
</div>

<style>
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, 1fr);
  width: 100%;
  height: 90%;
  margin: 0 auto;
  border: 0px solid #333;
}

.grid-item {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  font-size: 1.2rem;
  text-align: center;
}

.top-left {
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 2px solid #333;
  border-top: 2px solid #333;
}

.top-center {
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 0px solid #333;
  border-top: 2px solid #333;
}

.top-right {
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 0px solid #333;
  border-top: 2px solid #333;
}

.bottom-left {
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 2px solid #333;
  border-top: 0px solid #333;
}

.bottom-center {
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 0px solid #333;
  border-top: 0px solid #333;
}

.bottom-right{
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 0px solid #333;
  border-top: 0px solid #333;
}

.content {
  line-height: 1.6;
}
</style>

---
layout: center
class: text-center
---

<div  class="relative h-full flex items-center justify-center">
<h1 class="text-5xl font-bold text-white drop-shadow-lg" style="font-size: 40px;">Functions in Nix</h1></div>
<div class="grid-container">
  <div v-click class="grid-item top-left">
    <div class="content">
      <strong>Defining a Function<br><code>f = a : a + 2;<br>f 1 <span style="color: #6a737d; font-style: italic;">//3</span></code></strong>
    </div>
  </div>
<!-- f = a: a+2;f = (a,b): a+b; Xf = {a,b}: a+b;f {a=1; b=2;} == 3f {a=5;} Xf = {a,b ? 50}: a+b -->
  <div v-click class="grid-item top-right">
    <div class="content">
      <strong><s>Multiple Arguments</s><br><s><code>f = (a, b): a + b;</code></s></strong>
    </div>
  </div>
  
  <div v-click class="grid-item bottom-left">
    <div class="content">
      <strong>Attribute Sets as Args<br><code>f = {a, b}: a + b;<br>f {a = 1; b = 2;} <span style="color: #6a737d; font-style: italic;">//3</span></code></strong>
    </div>
  </div>
  
  <div v-click class="grid-item bottom-right">
    <div class="content">
      <strong>Optional Arguments<br><code>f ={a,b?2}: a+b;<br>f {a=1;} <span style="color: #6a737d; font-style: italic;">//3</span></code></strong>
    </div>
  </div>
</div>

<style>
.grid-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  width: 100%;
  height: 90%;
  margin: 0 auto;
  border: 0px solid #333;
}

.grid-item {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  font-size: 1.2rem;
  text-align: center;
}

.top-left {
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 2px solid #333;
  border-top: 2px solid #333;
}

.top-center {
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 0px solid #333;
  border-top: 2px solid #333;
}

.top-right {
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 0px solid #333;
  border-top: 2px solid #333;
}

.bottom-left {
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 2px solid #333;
  border-top: 0px solid #333;
}

.bottom-center {
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 0px solid #333;
  border-top: 0px solid #333;
}

.bottom-right{
  border-right: 2px solid #333;
  border-bottom: 2px solid #333;
  border-left: 0px solid #333;
  border-top: 0px solid #333;
}

.content {
  line-height: 1.6;
}
</style>
---
---
<div class="relative h-full flex items-center justify-center">
  <h1 class="text-5xl font-bold text-white drop-shadow-lg" style="font-size: 50px;">How Nix manages packages</h1>
</div>
---
---
<div class="relative h-full flex items-center justify-center">
  <h1 class="text-5xl font-bold text-white drop-shadow-lg" style="font-size: 70px;">2. How to integrate Nix<br><br> into your workflow</h1>
</div>
---
---
# Using NixOS
System Configuration

You can get the ISO image for NixOS from https://nixos.org/download/. After proceeding with the installation, you can find your configuration file at ```/etc/nixos/configuration.nix``` which allows you to:
 - Manage packages and services
 - Edit system settings
 - Change desktop enviroments and window managers
 - Set environment variables
 - Configure bootloaders
 - Select your kernel package
 - Install drivers

Also since on NixOS everything is handeled by Nix, you get the benefits of atomic upgrades and full system rollbacks down to the kernel itself.

---
---
Now Let's look at a simple ```configuration.nix``` file:
```nix

{ config, pkgs, ... }:
{  imports = [./hardware-configuration.nix];
  boot.loader.systemd-boot.enable = true;
  boot.kernelPackages = pkgs.linuxPackages_latest;
  networking.hostName = "nixos";
  networking.networkmanager.enable = true;
  time.timeZone = "Asia/Tehran";
  i18n.defaultLocale = "en_US.UTF-8";
  services.displayManager.sddm.enable = true;
  services.desktopManager.plasma6.enable = true
  services.pipewire.enable = true;
  environment.systemPackages = [pkgs.nano];
  users.users.myuser = {
    extraGroups = [ "networkmanager" "wheel" ];
    packages = [pkgs.firefox];
  };
}
```
Configuration files can be shared across multiple devices and thanks to the declarative nature of Nix a fresh install of NixOS can be turned into a fully configured workstation in a matter of minutes.
---
---
# Using Nix Shells
Reproducable Developer Enviroments

Nix Shells are Nix's way of handeling developer enviroments. They offer all the benefits of Nix in places wheere they are needed the most:
 - Declarativity for ease of sharing and setup
 - Reproducability for consistancy across the team
 - Seamless conflict management across otherwise incompatible software
 - By far the largest software repository in the world at 120 000+ packages

Here is what a simple ```shell.nix``` looks like:
```nix
{ pkgs ? import <nixpkgs> {} }:
pkgs.mkShell {
  buildInputs = [
    pkgs.hello
  ];
}
```
---
---
Running nix-shell in a directory with a ```shell.nix``` file will launch a dev shell for you with the provided configurations. 
And while getting access to GNU Hello is nice we can do so much more here; So lets have a look at a more compelete shell:

```nix
{ pkgs ? import <nixpkgs> {} }:
pkgs.mkShell {
  
  buildInputs = [
    vscode
    (pkgs.python312.withPackages (
            python-pkgs: [
              python-pkgs.numpy
              python-pkgs.pygame
              python-pkgs.fastapi
              python-pkgs.pytest]))
  ];

  LD_LIBRARY_PATH = "${pkgs.stdenv.cc.cc.lib}/lib";

  shellHook = ''
    fastapi run main.py
    '';
}
```
---
---
# Using Nix Flakes
Deterministic Inputs

To get started add ```nix.settings.experimental-features = ["nix-command" "flakes"];``` to your configuration and rebuild.
then you can run ```nix flake init``` to get a very basic flake to use. lets have a look at it:

```nix
{
  description = "A very basic flake";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs?ref=nixos-unstable";
  };

  outputs = { self, nixpkgs }: {

    packages.x86_64-linux.hello = nixpkgs.legacyPackages.x86_64-linux.hello;

    packages.x86_64-linux.default = self.packages.x86_64-linux.hello;

  };
}
```
---
---
We can build the provided package (GNU Hello) by running ```nix build``` and here are the results of doing so.
```
./test
├── flake.lock
├── flake.nix
└── result -> /nix/store/2bcv91i8fahqghn8dmyr791iaycbsjdd-hello-2.12.2
    ├── bin
    │   └── hello
    └── share
        └── ...
```

As you can see a ```flake.lock``` file is created which pins inputs to exact revisions allowing for complete reproducability.
 Furthermore flakes can also be used as inputs for:
 - Nix and NixOS configurations
 - Home manager inputs (coming up)
 - Nix shells
---
---
# Using Home manager
User Configuration

...
---
---
# Using Nix on Mac, Linux, and WSL
Take Nix with you; Anywhere.

You can also install Nix on other platforms (including other Linux distros and Windows via WSL) by running

```sh <(curl --proto '=https' --tlsv1.2 -L https://nixos.org/nix/install) --daemon``` in the terminal.
By installing nix this way you can access:

 - Some limited configurations
 - Home manager
 - Nix Shells
 - Nix Flakes

Without having to fully commit to NixOS and some of its more challanging aspects like immutability and on places where it would be otherwise impossible to
such as on Apple computers.

---
---
# Sources and Resources
Not all resources listed were directly used in the making of this presentation; But all of them are great resources I've found useful throughout my journey with Nix and NixOS.
 - [The Purely Functional Software
Deployment Model](https://edolstra.github.io/pubs/phd-thesis.pdf) by [Eelco Dolstra](https://github.com/edolstra)
 - Many helpful videos by [Vimjoyer](https://www.youtube.com/@vimjoyer)
 - [Nix explained from the ground up](https://www.youtube.com/watch?v=5D3nUU1OVx8&t=45s) by [Surma](https://www.youtube.com/@dassurma)
 - [NixOS Official Website](https://nixos.org/)
 - [NixOS Manual](https://nixos.org/manual/nixos/stable/)
 - [Nix Package and Option Search](https://search.nixos.org/packages)
 - [Nix Pills](https://nixos.org/guides/nix-pills/)
 - [NixOS Wiki](https://nixos.wiki/wiki/Main_Page)
 - [NixOS Forums](https://discourse.nixos.org/)
 - [Nix Package Repository](https://github.com/NixOS/nixpkgs)
 - and many more ...