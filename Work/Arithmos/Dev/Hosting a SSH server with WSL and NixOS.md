- Secure Shell Protocol (SSH) enables a client to get a command line interface on a server.
- Windows Subsystem for Linux (WSL) allows you to run a Linux environment on a Windows machine.
- NixOS is a declarative Linux distribution that makes it easy to deploy servers.
### SSH Server
Should be a Windows (11) computer.
#### Installing WSL
1. Enable WSL: `wsl --install --no-distribution`
2. Download `nixos.wsl` from [NixOS-WSL](https://github.com/nix-community/NixOS-WSL/releases/tag/2605.7.2)
3. Double click `nixos.wsl` to install the NixOS instance

`wsl -d NixOS` to launch/enter NixOS
`wsl --shutdown` to close NixOS

#### Configuring NixOS
Keep in mind that this server will be run headlessly and relies on WSL. Any GUIs, window managers, and hardware configuration can 

#### `ssh-server.nix`:
```nix
{
  config,
  pkgs,
  ...
}: let
  username = config.var.username;
in {
  services.openssh = {
    enable = true;
    openFirewall = true;
    settings = {
      PasswordAuthentication = false;
      KbdInteractiveAuthentication = false;
      PermitRootLogin = "no";
      AllowUsers = ["vlee"];
    };
  };

  users.users.${username} = {
    isNormalUser = true;
    openssh.authorizedKeys.keys = [
	  # Client public SSH keys go here
      "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMw7rODwcEweRCCb89gX7P6hwI+0o5zcdt5gx9/aVgGb ${username}@laptop"
    ];
  };
}

```

### `nix-ld.nix`
```nix
{pkgs, ...}: {
  environment = {
    localBinInPath = true;
  };

  programs.nix-ld = {
    enable = true;
    libraries = with pkgs; [
      # Standard C/C++ Libraries & Build Tools
      stdenv.cc.cc.lib
      gcc
      gnumake
      cmake
      pkg-config

      # System C Libraries
      zlib
      glib
      libffi
      openssl
      readline
      sqlite
      ncurses
      bzip2
      xz

      # Graphics & Image Libraries
      libGL
      libx11
      libxext
      libxrender
      libxi
      libxcb
      libpng
      libjpeg
      freetype
      fontconfig
      lcms2

      # Performance & Math
      openblas
      lapack

      # NVIDIA CUDA Support
      linuxPackages.nvidia_x11 # nvidia-smi for 1050 ti
      linuxPackages.nvidiaPackages.stable
      cudaPackages.cudatoolkit
      cudaPackages.cuda_cudart
      cudaPackages.libcublas
      cudaPackages.libcufft
      cudaPackages.libcurand
      cudaPackages.libcusparse
      cudaPackages.cudnn
    ];
  };
}

```
Installs common C++/Nvidia dependencies with a shim layer to spoof FHS compliance. Note that some additional packages may be necessary depending on GPU.

#### `wsl.nix`
```nix
{pkgs, ...}: {
  wsl.enable = true;
  wsl.defaultUser = "vlee";
}

```
Configures NixOS to be WSL ready.
### SSH Client
Should be a NixOS computer