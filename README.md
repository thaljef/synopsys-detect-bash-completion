# Bash Completion For Synopsys (Black Duck) Detect

Suggests options and parameters to complete Synopsys (Black Duck) Detect
commands.

# Installation

In all cases, you simply need to install the appropriate bash completion
package (if not already installed) and then copy the `detect` completion
script from this repository into the right directory for your system.
For example:

```bash
sudo apt install bash-completion
sudo curl -sL https://raw.githubusercontent.com/thaljef/synopsys-detect-bash-completion/master/detect > /etc/bash_completion.d/detect
bash -l; # To start new shell
```

In some cases, you may need to explicitly load the completion framework into
your shell. This is usually done by adding something like `source
/etc/bash_completion` to your `~\.bashrc` file.

The actual directory for your bash completion scripts and the exact command to
load them into your shell will vary by Linux distro and version. The above is
just an example; consult your distro docs for more specific guidance.

# Usage

The bash completion mechanism relies on having a _named command_ to bind the
completions to. However, it is customary to execute Detect via a remote
bootstrapping script. This execution process cannot be used with bash
completion.

Therefore, it is necessary to do that bootstrapping in a named command in
order to use these completions for Detect. The following must be placed in an
executable file named `detect` and that file should be in a directory that is
in your `$PATH`:

```bash
#!/bin/bash

bash <(curl -s -L https://detect.synopsys.com/detect.sh) $*
```
# Examples

Option names:
```
$> detect --detect.docker.[TAB][TAB]
--detect.docker.image=                   --detect.docker.inspector.version=    --detect.docker.tar=
--detect.docker.inspector.air.gap.path=  --detect.docker.path.required=
--detect.docker.inspector.path=          --detect.docker.path=
```

Option parameters:
```
$> detect --detect.project.tier=[TAB][TAB]
1  2  3  4  5

$> detect --detect.trust.cert=[TAB][TAB]
false  true
```

Option parameter lists:
```
$> detect --detect.project.tools=[TAB][TAB]
ALL             BINARY_SCAN     DOCKER          POLARIS
BAZEL           DETECTOR        NONE            SIGNATURE_SCAN

$> detect --detect.project.tools=DOCKER,[TAB][TAB]
DOCKER,BAZEL           DOCKER,DETECTOR        DOCKER,SIGNATURE_SCAN
DOCKER,BINARY_SCAN     DOCKER,POLARIS
```

# Compatibility

This completion script is known to work with bash 4.x or 5.x which is found in
any recent Linux distro. It will probably work with recent versions of zsh
too. It will probably *not* work with bash 3.x or older. For Windows, use
either Cygwin or the Linux Subsytem for Windows 10 to get a compatible shell.
MacOS has an ancient version of bash, so you'll probably need to install
homebrew and install both the `bash` and `bash-completion2` brews.

# Caveats

* The completions are derived from the documentation for Detect. But the
options described in the documentation don't always agree with the
implementation. So you may encounter options that are not correctly completed,
or completed options that are not supported.

* At present this script is hard-coded to look for version `5.5.0` of Detect,
so you will need to hack that if you are using a different version or change
versions down the road. In the future, I will improve this.

* The Detect bootstrapping optionally uses certain environment variables.
Ideally, those same variables should be used here too. But at the moment, they
are not. So if you use those variables, it may affect the completions.

# Author

Jeffrey Ryan Thalhammer <jeff@thaljef.org>

# Copyright

2019 (C) Jeffrey Ryan Thalhammer
