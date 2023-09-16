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
    
    - [x] orange pi 5 plus
    - [ ] orange pi 5
    - [x] Rock 5A - not tested
    - [x] Raspberry pi 4 - not tested
    - [ ] x86_64-linux - require restructure the NUC PR,
  - [x] Release SD Images automatically  - build currently fails due to not having aarch64 host
    - [x] setup cacheix for sky360 builds - [sky360 | Cachix
    - [x] CI using github actions - [Continuous Integration with GitHub Actions — nix.dev documentation](https://nix.dev/tutorials/nixos/continuous-integration-github-actions) 

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

- [x] nix switch case statement 
  
  ```nix
     sytem =
      {
        aarch64-linux = "Arm64";
        x86_64-linux = "linux64";
      }
      .${stdenv.system}
      or (throw "Unsupported system: ${stdenv.system}");
  
  ```

# issues

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

- [x] fixed qhyccd sdk package PR - [qhyccd_sdk: init at 23.09.06 by realsnick · Pull Request #254714 · NixOS/nixpkgs · GitHub](https://github.com/NixOS/nixpkgs/pull/254714)

- [ ] sd image not booting for orange pi 5
  
  - [x] testing orange pi 5 plus
  
  - [ ] testing orange pi 5 
    
    github issue : [orange pi 5 image fails to boot · Issue #8 · ryan4yin/nixos-rk3588 (github.com)](https://github.com/ryan4yin/nixos-rk3588/issues/8)

- [ ] github-runner jobs require node 16 which has a security risk and the nix package of github-runner uses node 20, there is an option to override it though due to security risk i didn't run it

- [ ] SD Image issues
  
  - [ ] open ssh should be disabled and utilize ssh with GPG
    
    [Setting up GnuPG + Yubikey on NixOS for SSH authentication (rzetterberg.github.io)](https://rzetterberg.github.io/yubikey-gpg-nixos.html)
    
    ```nix
    { config, lib, pkgs, ... }:
    
    {
      programs.ssh.startAgent = false;
    
      services.pcscd.enable = true;
    
      environment.systemPackages = with pkgs; [
        gnupg
        yubikey-personalization
      ];
    
      environment.shellInit = ''
        gpg-connect-agent /bye
        export SSH_AUTH_SOCK=$(gpgconf --list-dirs agent-ssh-socket)
      '';
    
      services.udev.packages = with pkgs; [
        yubikey-personalization
      ];
    }
    ```
  
  - [ ] setup ~/.secrets to use ubikey and remove the age key
  
  - [x] disable sky360 user sudo access
  
  - [x] auto sudo to snick - remove the need for password

## followers request

## need to learn

- [ ] helix editor

- [ ] git branch work - sync from remote / master

## future

- [ ] setup laptop
  
  - [ ] rofi
  
  - [ ] overlay window:

- [ ] prompt
  
  - [ ] [Starship: Cross-Shell Prompt](https://starship.rs/)

- [ ] file system encryption 
  
  - [ ] [NixOS/disko.nix at main - NixOS - Codeberg.org](https://codeberg.org/lutzgo/NixOS/src/branch/main/hosts/flores/disko.nix)

- [ ] git as storage recorder 
  
  - [ ] github/git-sizer: Compute various size metrics for a Git repository, flagging those that might cause problems](https://github.com/github/git-sizer)

- [x] setup secrets - require for the github-runner..
  
  - [x] [nixpkgs/pkgs/development/tools/continuous-integration/github-runner/default.nix at nixos-23.05 · NixOS/nixpkgs](https://github.com/NixOS/nixpkgs/blob/nixos-23.05/pkgs/development/tools/continuous-integration/github-runner/default.nix#L296)
    
    ```nix
     services.github-runner.enable = true;
      services.github-runner.url = "https://github.com/ORG_NAME";
      services.github-runner.tokenFile = config.sops.secrets."github-runner/token".path;
      services.github-runner.extraPackages = with pkgs; [ config.virtualisation.docker.package ];
    
      virtualisation.docker.enable = true;
    
      systemd.services.github-runner.serviceConfig.SupplementaryGroups = [ "docker" ]; ```
    ```
  
  - [x] research [Comparison of secret managing schemes - NixOS Wiki](https://nixos.wiki/wiki/Comparison_of_secret_managing_schemes)
  
  - [x] research nixos recommendations
  
  - [x] YUBIKEY - GPG [Setting up GnuPG + Yubikey on NixOS for SSH authentication (rzetterberg.github.io)](https://rzetterberg.github.io/yubikey-gpg-nixos.html)
  
  - [x] package sops-nix [Mic92/sops-nix: Atomic secret provisioning for NixOS based on sops (github.com)](https://github.com/Mic92/sops-nix)
  
  - [x] how to manage secrets with nixos anywhere [nixos-anywhere/docs/howtos.md at main · numtide/nixos-anywhere (github.com)](https://github.com/numtide/nixos-anywhere/blob/main/docs/howtos.md#secrets-and-full-disk-encryption)
  
  - [x] to setup github-action-runner 
    
    - [x] [numtide/srvos: NixOS profiles for servers (github.com)](https://github.com/numtide/srvos)
  
  - [x] setup 1password - manual
  
  - [ ] setup gpg ssh 
  
  - [x] setup github secrets - sign commits

- [ ] Themes 
  
  - [ ] nix-colors [http://github/misterio77/nix-colors](http://github/misterio77/nix-colors)  
  
  - [ ] services.rgbdaemon 
    
    - [ ] [NixOS/default.nix at 3a12352bdfb775f0316637de70db5c2a98e4046d - NixOS - Codeberg.org](https://codeberg.org/lutzgo/NixOS/src/commit/3a12352bdfb775f0316637de70db5c2a98e4046d/home/lgo/features/rgb/default.nix)
    
    - [ ] [Misterio77/flavours: 🎨💧 An easy to use base16 scheme manager that integrates with any workflow. (github.com)](https://github.com/Misterio77/flavours)
    
    - [ ] 
  
  - [ ] 

- [ ] nixosConfiguration - minimize and break into files
  
  ```nix
    nixosConfigurations = {
      # Lenovo Thinpad X1-Tablet
      your_host =  lib.nixosSystem {
        modules = [ ./hosts/your_host ];
        specialArgs = { inherit inputs outputs; };
      };
    };
  ```

- [ ] mutable OS state 
  
  - [ ] root '/' on tmpfs - github:nix-community/impermanence

- [x] CI

- [ ] setup development enviornment 
  
  - [ ] use nix flake [GitHub - NixOS/templates: Flake templates](https://github.com/NixOS/templates)
  
  - [ ] [NixOS/templates at main - NixOS - Codeberg.org](https://codeberg.org/lutzgo/NixOS/src/branch/main/templates)
  
  - [ ] research using - http://devenv.sh 
  
  - [ ] research [Set up a development environment — nix.dev documentation](https://nix.dev/tutorials/first-steps/dev-environment) 
  
  - [ ] research [Development Environments on NixOS | NixOS & Flakes Book (thiscute.world)](https://nixos-and-flakes.thiscute.world/development/intro) 
  
  - [ ] ros2
  
  - [ ] C++
  
  - [ ] Rust

- [ ] support unstable channel - currently default one is stable, only reason for stable is nvidia

- [ ] repl development for nix, C++, Rust

- [ ] secrets and full disk encryption
    https://github.com/numtide/nixos-anywhere/blob/main/docs/howtos.md#secrets-and-full-disk-encryption

- [ ] Using your own kexec image
    https://github.com/numtide/nixos-anywhere/blob/main/docs/howtos.md#using-your-own-kexec-image

- [ ] nix build / nix shell / nix develop

- [ ] look at this flake structure for multiple machines: https://github.com/baetheus/.nix

- [ ] look at aya ebpf in rust = https://github.com/aya-rs/aya

- [ ] look at https://www.omg.org/about/index.html

# contribution