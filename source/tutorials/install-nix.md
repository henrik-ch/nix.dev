(install-nix)=

# Install Nix

:::::{tab-set}

::::{tab-item} Linux

Install Nix via the recommended [multi-user installation]:

```shell-session
$ curl -L https://nixos.org/nix/install | sh -s -- --daemon
```

::::

::::{tab-item} macOS

Install Nix via the recommended [multi-user installation]:

```shell-session
$ curl -L https://nixos.org/nix/install | sh
```

::::

::::{tab-item} Windows (WSL2)

Install Nix via the recommended [single-user installation]:

```shell-session
$ curl -L https://nixos.org/nix/install | sh -s -- --no-daemon
```

However, if you have [systemd support] enabled, install Nix via the recommended [multi-user installation]:

```shell-session
$ curl -L https://nixos.org/nix/install | sh -s -- --daemon
```

[systemd support]: https://learn.microsoft.com/en-us/windows/wsl/wsl-config#systemd-support

::::

::::{tab-item} Docker

Start a Docker shell with Nix:

```shell-session
$ docker run -it --rm nixos/nix
```

Or start a Docker shell with Nix exposing a `workdir` directory:

```shell-session
$ mkdir workdir
$ docker run -it -v $(pwd)/workdir:/workdir nixos/nix
```

The `workdir` example from above can be also used to start hacking on Nixpkgs:

```shell-session
$ git clone git@github.com:NixOS/nixpkgs
$ docker run --name nixpkgs_experiment -it -v $(pwd)/nixpkgs:/nixpkgs nixos/nix
bash-5.1# cd nixpkgs/
bash-5.1# nix-build -I nixpkgs=/nixpkgs -A hello
bash-5.1# find ./result # this symlink points to the build package
bash-5.1# exit
```
and to restart after first init:
```shell-session
$ docker start -i nixpkgs_experiment
```

::::

:::::

## Verify installation

Check the installation by opening **a new terminal** and typing:

```shell-session
$ nix --version
nix (Nix) 2.11.1
```

[multi-user installation]: https://nixos.org/manual/nix/stable/installation/multi-user.html
[single-user installation]: https://nixos.org/manual/nix/stable/installation/single-user.html
