```
                            .--~~~~~~~~~~~~~------.
                           /--===============------\
                           | |```````````````|     |
                           | |               |     |
                           | |      >_<      |     |
                           | |               |     |
                           | |_______________|     |
                           |                   ::::|
                           '======================='
                           //-"-"-"-"-"-"-"-"-"-"-\\
                          //_"_"_"_"_"_"_"_"_"_"_"_\\
                          [-------------------------]
                          \_________________________/


                          Secure Shell Developer Guide
```

# Introduction

Secure Shell is a Chrome App (currently a "v1.5" app, soon to become a "v2" or
Platform App) that combines hterm with a NaCl build of OpenSSH to provide
a PuTTY-like app for Chrome users.

See [/HACK.md](/HACK.md) for general information about working with the source
control setup.

# Building the dependencies.

The Secure Shell app depends on some library code from
[libapps/libdot/](/libdot/) and the hterm terminal emulator from in
[libapps/hterm/](/hterm/).  To build these external dependencies, run...

    nassh$ ./bin/mkdeps.sh

This will create the `nassh/js/nassh_deps.concat.js` file containing all of the
necessary libdot and hterm source.  If you find yourself changing a lot of
libdot or hterm code and testing those changes in Secure Shell you can run this
script with the "--forever" (aka -f) option.  When run in this manner it will
automatically re-create nassh_deps.concat.js file whenever one of the source
files is changed.

# The NaCl plugin dependency

Secure Shell depends on a NaCl (Native Client) plugin to function.  This plugin
is a port of OpenSSH.  You'll have to find or create a version of this plugin,
and copy it into `libapps/nassh/plugin/`.

Your options are:

1. Build it yourself from https://chromium.googlesource.com/chromiumos/platform/assets/+/master/chromeapps/ssh_client

2. Copy it from `plugin/` directory of the latest version of Secure Shell.
If you have Secure Shell installed, the plugin can be found in your profile
directory, under
`Default/Extensions/pnhechapfaindjhompbnflcldabbghjo/<version>/plugin/`.

# Dev-Test cycle.

The `./bin/run_local.sh` script can be used to launch a new instance of Chrome
in an isolated profile, with the necessary command line arguments, and launch
the Secure Shell app.  You can run this script again to rebuild dependencies
and relaunch the Secure Shell app.
