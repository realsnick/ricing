# Welcome to my Stream!

## still to do from QHY SDK Rice

- [ ] QHYCCD_SDK PR Accepted

- [x] Release Manual SD Images - and here is https://github.com/Sky360-Repository/sky360/releases/tag/alpha-2
  - [x] orange pi 5 plus
  - [ ] orange pi 5
  - [x] Rock 5A - not tested
  - [x] Raspberry pi 4 - not tested
  - [ ] x86_64-linux - require restructure the NUC PR,

## Current Rice - ROS2

- [ ] setup ros2 nix dev env 

- [ ] run talker as a service in nixos

- [ ] create a heartbeat node 
  
  - [ ] run as a service in nixos



## research
- [ ] buildRosPackage nix function from nix-ros-overlay
      example at https://github.com/realsnick/nix-ros-overlay/blob/develop/distros/iron/rosbag2-cpp/default.nix
- [ ] talker/listener
  - [ ] develop
    - [ ] C++
    - [ ] Rust
  - [ ] build
    - [ ] C++
    - [ ] Rust
  - [ ] run as service
- [ ] recorder proof of concept
  
  - [ ] In memory 
    
    - [x] Git Commiter
    
    - [x] Monitor
    
    - [x] Generate Sample Sensor Data
    
    - [ ] Cleanup/Prune

## stretch

- [ ] sort google drive

- [ ] sort one drive

- [ ] sort apple icloud drive

- [ ] setup netboot to boot nixos-installer 

- [ ]...

## notes

# issues

- [ ] trace: warning: mdadm: Neither MAILADDR nor PROGRAM has been set. This will cause the `mdmon` service to crash.
  
  [trace: warning: mdadm: Neither MAILADDR nor PROGRAM has been set. This will cause the `mdmon` service to crash. · Issue #254807 · NixOS/nixpkgs (github.com)](https://github.com/NixOS/nixpkgs/issues/254807)

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
  
  - [ ] setup gpg ssh 

- [ ] Themes 
  
  - [ ] nix-colors [http://github/misterio77/nix-colors](http://github/misterio77/nix-colors)  
  
  - [ ] services.rgbdaemon 
    
    - [ ] [NixOS/default.nix at 3a12352bdfb775f0316637de70db5c2a98e4046d - NixOS - Codeberg.org](https://codeberg.org/lutzgo/NixOS/src/commit/3a12352bdfb775f0316637de70db5c2a98e4046d/home/lgo/features/rgb/default.nix)
    
    - [ ] [Misterio77/flavours: 🎨💧 An easy to use base16 scheme manager that integrates with any workflow. (github.com)](https://github.com/Misterio77/flavours)

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