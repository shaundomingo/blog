title: "The pain of switching from *nix to Windows for the simplest 'devops'"
date: 2016-05-29 21:38:32
tags:
 - windows
 - devops
excerpt: Back in 2016, switching from *nix to Windows for simple DevOps was hard.
---

## Scene setting

Shifting from a great dev environment to a poor one can be particularly infuriating. I wanted to discuss some frustrations I've had shifting a dev environment from Linux/OSX (+ Vagrant + Chef) to Windows.

First up, context. I have a small dev team. They code, they don't dev the ops. They will, just not yet.

So I wanted to make it as simple as possible for them to get going. Trick is, like many big companies the SOE is Windows and the budget for alternate hardware & software is lean.

In open source we trust. Should be easy right, even if it is Windows.

The easiest and obvious solution would be to run a guest Linux VM of choice and have vagrant fire from within. Due to the cost constraint we're not buying VMWare workstation and my Devs don't have a masters in KVM or Xen. Apparently Hyper-V supports nested virt in [early preview](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/nesting) in 2016 but our Windows aren’t that shiny yet. To VirtualBox we turn.

Except, VirtualBox doesn't support nested virtualisation either. Well it sort of does if you run a 32 bit OS on a single CPU without VT-x, but damn, that's slow.

What are we left with? Well we need to break the layers of nesting by shifting the dev environment up a level to the native OS. Argh Windows. Ok if we have to. Again most open source implementations worth their salt are Windows compatible, right? In this case, it was hard going.

## Command line git = git scm / Git bash
Cmd.exe looks like a virus, and as far as I care, it is. So [git-scm](https://git-scm.com/) wraps a mingw64 abstraction to provide Git Bash. Surprisingly it does an ok job. You at least get some history and can change the size of the terminal easily.

## ChefDK
Installs gracefully, works successfully. We just wanted it so we could use knife and berkshelf, the rest was superfluous.

## Vagrant and VirtualBox
Both install perfectly fine. However my first instinct was to use cygwin with vagrant and chef instead of Git scm. In summary, don't. Git-scm seems to set up paths correctly (unlike Cygwin). Embedded ruby gets set up correctly too.

## Git Deploy Keys
A piece of cake on *nix, but Windows? Puttygen? Damn, is that still around? Rather, use Git bash & ssh-keygen to do it a better way.

## Summary
It took me close to a day to figure out how to replicate a simple, semi-sensible development environment in Windows.

Why didn't I just get the Devs to install Ubuntu? Well they probably should, but the corporate world is still bound to MS Office. Furthermore, since they are web Devs they need access to a local version of the Adobe Creative Cloud suite. They can’t fire up windows VMs from *nix because they don’t have access to those images.

(F) Would not recommend.