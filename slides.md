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

 1. What is Nix and Where did it come from<br>
    1.1 How and Why Nix was created<br>
    1.2 Nix (Package Manager)<br>
 2. How to integrate Nix into your workflow<br>
    2.1 Nix (DSL)<br>
    2.2 Using The Nix Package Manager<br>
    2.3 Using NixOS and Home Manager<br>
    2.4 Using Nix Shells<br>
    2.5 Using Nix Flakes<br>
---
layout: default
---

<div class="grid grid-cols-[30%_70%] gap-8 h-full items-center">

<div class="flex flex-col justify-center">

<img src="./resources/pfp.jpg" class="w-full object-cover rounded-lg shadow-lg mb-4" />

<div style="font-size: 27px; font-weight: bold;">Farbod Khalili Khoshehmehr</div>

Computer Engineering Student at University of Guilan

- [Github](https://github.com/thecosmomancer)
- [LinkedIn](https://www.linkedin.com/in/farbodkhalilikhoshehmehr/)

</div>

<div class="flex flex-col justify-top">

## Why should you listen to me

<v-clicks>

- I've been using NixOS for more than a year

- I've read the original 250+ page paper that documenting Nix

- I'm wearing a NixOS T-shirt

- I've wrote a poem for NixOS (available for reading at the end of the slides)

   So yeah I'm **VERY** interested in Nix and NixOS
</v-clicks>

</div>
</div>
---
---
<div class="relative h-full flex items-center justify-center">
  <h1 class="text-5xl font-bold text-white drop-shadow-lg" style="font-size: 70px;">1. What is Nix and <br><br> Where did it come from</h1>
</div>
---
---
# The How:
The Nix Package Manager
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
# The How:
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

Going back to Nix, it started as a way to improve the consistency of software deployment.
Before Nix there were two main ways to deploy software: using a compiling a binary file from its source code, or getting a copy of the binary compiled by the distributor.

The issues with the latter were that: 1. The binary each is only compatible with the CPU architecture and operating system of the platform it was compiled on. 2. The exact version of the libraries that the binary depends on at runtime are not always available on the User's machine or are not available at all.

As for the former, its core issues were: 1. It was unusable for closed-source software. 2. The correct version of tools and libraries needed to compile the software and run the software needed to be available on the User's machine. 3. The compilation process was a massive waste of time and resources.

As you can see, software deployment had a lot to be improved; And improving software deployment is exactly what Nix did.
---
---
# How Nix Works
isolation and reproducibility


---
---
<div class="relative h-full flex items-center justify-center">
  <h1 class="text-5xl font-bold text-white drop-shadow-lg" style="font-size: 70px;">2. How to integrate Nix<br><br> into your workflow</h1>
</div>
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
 - [Nix Packages](https://search.nixos.org/packages)
 - [NixOS Options](https://search.nixos.org/options)
 - [NixOS Wiki](https://nixos.wiki/wiki/Main_Page)
 - [NixOS Forums](https://discourse.nixos.org/)
 - [Nix Package Repository](https://github.com/NixOS/nixpkgs)
 - [Claude](https://claude.ai/) and many more ...