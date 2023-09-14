# Welcome to my Stream!

## Current Rice - QHY_CCD SDK NixOS Package

- [x] setup obs on laptop.

- [x] development enviornment for nixpkgs
  
  - [x] nix build -A qhyccd_sdk

- [x] QHY SDK package
  
  - [x] build the package for x86_64 - device should be detected by `lsusb
  
  - [x] helptest the package locally
  
  - [x] build the package for arm64
  
  - [x] test the packapge on the rpi-5+
    
    - [x] clone the sky360 repository and use nixos-rebuild
  
  - [x] submit PR
    
    - [ ] PR Accepted
  
  - [x] Release Manual SD Images - and here is https://github.com/Sky360-Repository/sky360/releases/tag/alpha-2
    
    - [ ] orange pi 5 plus
    - [ ] orange pi 5
    - [ ] Rock 5A
    - [ ] Raspberry pi 4
    - [ ] x86_64-linux
  
  - [ ] Release SD Images automatically 
    
    - [ ] setup secrets - require for the github-runner..
      
      - [ ] research [Comparison of secret managing schemes - NixOS Wiki](https://nixos.wiki/wiki/Comparison_of_secret_managing_schemes)
      
      - [ ] research nixos recommendations
      
      - [ ] package sops-nix [Mic92/sops-nix: Atomic secret provisioning for NixOS based on sops (github.com)](https://github.com/Mic92/sops-nix)
      
      - [ ] how to manage secrets with nixos anywhere [nixos-anywhere/docs/howtos.md at main · numtide/nixos-anywhere (github.com)](https://github.com/numtide/nixos-anywhere/blob/main/docs/howtos.md#secrets-and-full-disk-encryption)
    
    - [ ] [nixpkgs/pkgs/development/tools/continuous-integration/github-runner/default.nix at nixos-23.05 · NixOS/nixpkgs](https://github.com/NixOS/nixpkgs/blob/nixos-23.05/pkgs/development/tools/continuous-integration/github-runner/default.nix#L296)
      
      ```nix
       services.github-runner.enable = true;
        services.github-runner.url = "https://github.com/ORG_NAME";
        services.github-runner.tokenFile = config.sops.secrets."github-runner/token".path;
        services.github-runner.extraPackages = with pkgs; [ config.virtualisation.docker.package ];
      
        virtualisation.docker.enable = true;
      
        systemd.services.github-runner.serviceConfig.SupplementaryGroups = [ "docker" ];
      ```
    
    - [ ] CI using github actions - [Continuous Integration with GitHub Actions — nix.dev documentation](https://nix.dev/tutorials/nixos/continuous-integration-github-actions) 

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

- [x] stylix - broken due to fonts

- [x] hyprland broken - error: attribute 'gcc13Stdenv' missing
  
  this is due update the local flake with recent nixpkgs which seems broken...will investigate this issue
  
  [error: attribute 'gcc13Stdenv' missing · Issue #92 · hyprwm/xdg-desktop-portal-hyprland (github.com)](https://github.com/hyprwm/xdg-desktop-portal-hyprland/issues/92)

- [x] /sbin/fxload is called in udev rules but is not executable or does not exist
  
  had to patch the udev rules files to find fxload in nix store

- [x] /bin/sleep is called in udev rules but is not executable or does not exist

- [x] camera firmware isn't being uploaded - udev rules issue
  
  more patched to the udev-rules, looks like the qhy ccd has a built in fxload that has different parameters then the libusb1 fxload (-d on libusb1 required vendor:product, -D on qhyccd sdk requires -D DEVNAME)

- [ ] trace: warning: mdadm: Neither MAILADDR nor PROGRAM has been set. This will cause the `mdmon` service to crash.
  
  [trace: warning: mdadm: Neither MAILADDR nor PROGRAM has been set. This will cause the `mdmon` service to crash. · Issue #254807 · NixOS/nixpkgs (github.com)](https://github.com/NixOS/nixpkgs/issues/254807)

- [ ] fixed qhyccd sdk package PR - [qhyccd_sdk: init at 23.09.06 by realsnick · Pull Request #254714 · NixOS/nixpkgs · GitHub](https://github.com/NixOS/nixpkgs/pull/254714)

- [ ] sd image not booting for orange pi 5
  
  - [ ] testing orange pi 5 plus
  
  - [ ] testing orange pi 5

- [ ] no Window Capture in OBS Studio 

## followers request

## need to learn

- [ ] helix editor

- [ ] git branch work - sync from remote / master

## future

- [ ] setup laptop
  
  - [ ] rofi
  
  - [ ] overlay window:

- [ ] setup development enviornment 
  
  - [ ] research using - http://devenv.sh 
  
  - [ ] research [Set up a development environment — nix.dev documentation](https://nix.dev/tutorials/first-steps/dev-environment) 
  
  - [ ] research [Development Environments on NixOS | NixOS & Flakes Book (thiscute.world)](https://nixos-and-flakes.thiscute.world/development/intro) 
  
  - [ ] ros2
  
  - [ ] C++
  
  - [ ] Rust

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