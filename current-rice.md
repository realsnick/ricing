# Welcome to my Stream!

## Current Rice - QHY_CCD SDK NixOS Package

- [ ] setup obs on laptop and stream directly from laptop. 

- [ ] development enviornment for nixpkgs
  
  - [x] nix build -A qhyccd_sdk

- [x] QHY SDK package
  
  - [x] build the package for x86_64 - device should be detected by `lsusb
  - [x] helptest the package locally
  - [ ] build the package for arm64
  - [ ] test the packapge ont he rpi-5+
    - [ ] clone the sky360 repository and use nixos-rebuild
  - [x] submit PR
    - [ ] PR Accepted
  - [ ] Release SD Images automatically
    - [ ] orange pi 5
    - [ ] orange pi 5 plus
    - [ ] rk3588
    - [ ] raspberry pi 4 

## stretch

- [ ] sort google drive

- [ ] sort one drive

- [ ] sort apple icloud drive

- [ ] setup netboot to boot nixos-installer 

- [ ]...

## notes

need to fix DMCA Music on twitch...

for udev rules this is the option. 

require the user of the package to add the following line in configuration.nix

```nix
services.udev.packages = [ pkgs.qhyccd_sdk ];
```

1. # open bugs
- [x] /sbin/fxload not found/installed 
  
  fixed substituteInPlace --replace

- [x] ldconfig: Can't create temporary cache file /nix/store/lqz6hmd86viw83f9qll2ip87jhb7p1ah-glibc-2.35-224/etc/ld.so.cache~: Permission denied
  
  this is related to not running udev rules... 

- [ ] stylix - broken due to fonts

- [ ] hyprland broken - error: attribute 'gcc13Stdenv' missing
  
  this is due update the local flake with recent nixpkgs which seems broken...will investigate this issue
  
  [error: attribute 'gcc13Stdenv' missing · Issue #92 · hyprwm/xdg-desktop-portal-hyprland (github.com)](https://github.com/hyprwm/xdg-desktop-portal-hyprland/issues/92)

- [x] /sbin/fxload is called in udev rules but is not executable or does not exist
  
  had to patch the udev rules files to find fxload in nix store

- [x] /bin/sleep is called in udev rules but is not executable or does not exist

- [x] camera firmware isn't being uploaded - udev rules issue
  
  more patched to the udev-rules, looks like the qhy ccd has a built in fxload that has different parameters then the libusb1 fxload (-d on libusb1 required vendor:product, -D on qhyccd sdk requires -D DEVNAME)

## followers request

## need to learn

- [ ] helix editor

- [ ] git branch work - sync from remote / master

## future

- [ ] support unstable channel - currently default one is stable, only reason for stable is nvidia

- [ ] use nix flake https://github.com/NixOS/templates

- [ ] repl development for nix, C++, Rust

- [ ] secrets and full disk encryption
    https://github.com/numtide/nixos-anywhere/blob/main/docs/howtos.md#secrets-and-full-disk-encryption

- [ ] Using your own kexec image
    https://github.com/numtide/nixos-anywhere/blob/main/docs/howtos.md#using-your-own-kexec-image

- [ ] nix build / nix shell / nix develop

- [ ] look at this flake structure for multiple machines: https://github.com/baetheus/.nix

- [ ] look at aya ebpf in rust = https://github.com/aya-rs/aya

- [ ] look at https://www.omg.org/about/index.htm

# contribution