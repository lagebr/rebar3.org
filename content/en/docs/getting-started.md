---
title: "Getting Started"
weight: 1
excerpt: ""
---

Rebar3 is the standard build tool within the Erlang community. It essentially integrates many of the other tools shipping with Erlang along with a few open-source ones, and makes them all work under a unified project structure.

## Installing Erlang

Rebar3 relies on Erlang already being present on your system in order to run. If Erlang runs there, Rebar3 should run there as well.

See the [Adopting Erlang](https://adoptingerlang.org/) section [Installing Erlang/OTP](https://adoptingerlang.org/docs/development/setup/#installing-erlang-otp) for detailed steps of installing Erlang for Windows, Mac, Linux and FreeBSD.

## Installing from the Rebar3 escript

[Download the latest stable release](https://s3.amazonaws.com/rebar3/rebar3) as an executable [escript](https://erlang.org/doc/man/escript.html). While the script version of Rebar3 is portable and usable from anywhere, it is advised not to keep it in your project's repository and to install it once for your entire system. Regardless of which recent Erlang version you have installed, it should be fully compatible with all of them.

One downside of the escript however is that it is a bit slower than a regular Erlang program. We recommend to install a fully compiled form of rebar3, which rebar3 can do for you:

```shell
$ ./rebar3 local install
===> Extracting rebar3 libs to ~/.cache/rebar3/lib...
===> Writing rebar3 run script ~/.cache/rebar3/bin/rebar3...
===> Add to $PATH for use: export PATH=$PATH:~/.cache/rebar3/bin
```

Be sure to follow the instructions the command outputs and add the executable to your systems `$PATH`, such as calling `export PATH=$PATH:~/.cache/rebar3/bin`. You can then delete the `rebar3` escript you used to run `local install`.

When a new stable release of `rebar3` is available, you can simply run `rebar3 local upgrade` and the new version will fetched and installed the same way:

```shell
$ rebar3 local upgrade
===> Extracting rebar3 libs to ~/.cache/rebar3/lib...
===> Writing rebar3 run script ~/.cache/rebar3/bin/rebar3...
===> Add to $PATH for use: export PATH=$PATH:~/.cache/rebar3/bin 
```

### Windows

Windows users who want to use the code from PowerShell or cmd.exe (rather than a terminal emulator) must ensure that a `rebar3.cmd` file is added:

   ```
   @echo off
   setlocal
   set rebarscript=%~f0
   escript.exe "%rebarscript:.cmd=%" %*
   ```

Then add the directory where the file has been saved to the system `PATH`.

If you want to change the default path (`C:\Users\<user>`) you can set an ENV var for `REBAR_CACHE_DIR` pointing to the directory of your liking.

## Installing from Source

The `rebar3` project's repo is hosted on Github and comes with a `bootstrap` script for building from source. This form is likely to cause fewer issues to Windows users, since building from source will generate the wrapper scripts required to work well in both CMD and powershell environments:

```shell
$ git clone https://github.com/erlang/rebar3.git
$ cd rebar3
$ ./bootstrap
```

This will compile a `rebar3` escript to the top level of the `rebar3` directory which you can then install globally:

```shell
$ ./rebar3 local install
```

Do note that if you are planning to work with multiple Erlang versions on the same machine, you will want to build Rebar3 with the oldest one of them. The five newest major Erlang releases are supported at any given time: if the newest version is OTP-23, building with versions as old as OTP-19 will be supported, and produce an executable that will work with those that follow.

## Creating a New Project

Rebar3 offers templates that will ensure your Erlang project fits into a regular OTP structure:

```shell
$ rebar3 new umbrella myproj
===> Writing apps/myproj/src/myproj_app.erl
===> Writing apps/myproj/src/myproj_sup.erl
===> Writing apps/myproj/src/myproj.app.src
===> Writing rebar.config
===> Writing config/sys.config
===> Writing config/vm.args
===> Writing .gitignore
===> Writing LICENSE
===> Writing README.md 
```

The OTP structure is part of the basic contract Rebar3 expects; following it will guarantee a much better time than doing otherwise.

You can see [Basic Usage](/docs/basic_usage) to learn more on how to use `rebar3`, and follow it with [Workflow](/docs/workflow/) for broader usage.
