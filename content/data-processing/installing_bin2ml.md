---
section: Data Processing
nav_order: 1
title: Installing bin2ml
topics: Data Processing, Intermediate to Processed
---

# Verify you have `bin2ml` installed

`bin2ml` should have already been installed during the setup/pre-reqs. In order to check it is present
you can execute the following and get the following back:
```
> bin2ml --version
bin2ml 0.4.0
```

If you get `bin2ml 0.4.0` outputed, you can skip the rest of this!

# Help, it is not working!

If the above command does not work, use the following steps to work out what has gone wrong.

## Option 1: Non-container

The following steps assume that you have already got a valid install of the `rust` toolchain `cargo`. 
If not, please refer to google for how to install `rust` for the platform you want to run this workshop on. 
You will also need a working install of `radare2` within your `PATH` environment variable.

This is fairly straightforward and can be done using the following commands:
```
git clone https://github.com/br0kej/bin2ml
cd bin2ml
cargo install --path .
```
This will take a bit of time if this is your first time installing a rust project using `cargo` but 
should complete without a hitch. The `bin2ml` binary will be installed into `~/.cargo/bin/`. This *should* 
have been added to your `PATH` environment variable when installing `rust` but if not you may have to 
edit your terminal dot file (`.bashrc`/`.zshrc` etc). 

To test that it's working and installed execute:
```
> bin2ml --version
bin2ml 0.4.0
```

## Option 2: Docker Container

The `bin2ml` repo comes with a `Dockerfile` which can be used to build a dockerized version of `bin2ml` as well
as handling the installation of `radare2`. The steps to build this are as follows:

```
git clone https://github.com/br0kej/bin2ml
cd bin2ml
docker build -t bin2ml-44con .
```

To test that it's working and built correctly:
```
> docker run --rm bin2ml-44con bin2ml --version
bin2ml 0.3.1
```

If you see the above, we are ready to rock and roll! 