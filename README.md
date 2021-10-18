# Coq Platform 2021.09.0

The [Coq interactive prover](https://coq.inria.fr) provides a formal language
to write mathematical definitions, executable algorithms, and theorems, together
with an environment for semi-interactive development of machine-checked proofs.

The **Coq Platform** is a distribution of the Coq interactive prover together
with a selection of Coq libraries and plugins.
The main goal of the Coq Platform is to provide a system independent, dependable
and easy to install platform for developments based on the Coq proof assistant
and for teaching Coq.
See [Charter](charter.md) for the coq platform concept.

The Coq Platform is based on the OCaml package manager **Opam** and provides a set
of scripts to compile and install OPAM, Coq and the platform contents on macOS,
Windows and many Linux distributions in a reliable way with consistent results.
In addition **pre-compiled binary packages** or **installers** are provided for **macOS**,
**Windows** and **Snap** for Linux (Docker is in preparation).

The Coq Platform supports to install several versions of Coq - also in parallel,
e.g. for porting developments from one version of Coq to another.
The table below contains links to the ReadMe files for the supported versions
of Coq and libraries. Each ReadMe file contains a list of included packages with
detailed information for each package.

- [Coq 8.13.2 04/2021 with updated/extended package pick 09/2021](doc/ReadMe_2021.09.0_8.13.md)
- [Coq 8.13.2 04/2021 with original package pick 02/2021](doc/ReadMe_2021.09.0_8.13~2021.02.md)
- [Coq 8.12.2 12/2020 (previous release version)](doc/ReadMe_2021.09.0_8.12.md)
- [Coq 8.14+rc1 with a beta package pick](doc/ReadMe_2021.09.0_8.14+beta1.md)

It is an intended use case of the Coq Platform to create custom variants, e.g.
for projects or lectures, by creating additional files in the [versions](versions)
folder.
The scripts for creating binary packages and installers should be able to
handle such variants, so that it should be easy to create a custom installer
e.g. for a lecture.

## Usage of the Coq Platform

Please refer to the ReadMe file for your OS.

- macOS: see [README_macOS](doc/README_macOS.md).
- Windows: see [README_Windows](doc/README_Windows.md)
- Linux: see [README_Linux](doc/README_Linux.md).

## Additional information

<details><summary><font size="+1">Licenses</font></summary>

The Coq platform setup scripts and the selection of packages and patches are licensed Creative Commons CC0.
This license does **not** apply to the packages installed by the Coq platform.
The ReadMe files linked above provide license information for each package.
This information is also available as .CSV files here [doc](doc).
Please note that the license information is obtianed from opam.
The Coq Platform team does no double check this information.

</details>

<details><summary><font size="+1">Release notes / change lists</font></summary>

## Changes in 2021.09.0

- support for multiple versions of Coq (currently 8.12.2, 8.13.2, 8.14+rc1, dev)
- parallel installation of several versions of Coq is possible - each version creates a separate opam switch
- new substantially extended package pick for Coq 8.13.2 (the original pick from 2021.02 is also available)
- new beta pick for Coq 8.14+rc1 - as close as possible to the updated pick for Coq 8.13.2

## Changes in 2021.02.2

- support for opam 2.1.0 (which integrates the opam system dependency manager *depext* - this needed a few adjustments)
- fix issues with Cygwin binutils
- various minor fixes for the Snap package (support gappa, clightgen, ...)
- various minor fixes to the Windows installer (add icon for CoqIDE, ...)
- minor cleanup and improvements of the Coq Platform scripts
- the versions of provided Coq packages are identical to 2021.09.0

## Changes in 2021.02.1

- added DMG package / installer for macOS
- Coq and CoqIDE update to version 8.13.2 (bugfix release)
- VST updated to version 2.7.1 (bugfix release)
- new package `coq-hott` *The Homotopy Type Theory library*

</details>

<details><summary><font size="+1">Features of the Coq Platform</font></summary>

- fully Opam based, also on Windows
- single script call to install system dependencies, Opam (if not there), a fresh Opam switch and the Coq Platform
- interactive (well script based) guidance of the user through the few parameters
- one unified setup script for Windows, macOS and Linux with few OS dependent sections only
- for Windows there is an additional wrapper batch script to setup Cygwin as build and working environment
- for Windows there is in addition a classic Windows installer mostly intended for quick installation by beginners
- for macOS a signed (but currently not yet notarized) DMG package is provided, also mostly intended for beginners
- for Linux Snap packages are provided via the snap store
- it is easy to build variants of the provided installers with modified content
- it is supported to install several versions of Coq in parallel - each will create a separate opam switch - this is intended e.g. for porting Coq developments from older versions of Coq
- system prerequisites are installed using opam depext in a system independent manner
- the script should be fairly robust and safe - it will immediately abort an all errors not explicitly handled
- the script can be restarted if it fails - e.g cause of internet or memory issues - it will not redo things it already did

</details>

<details><summary><font size="+1">Installation of additional packages or package variants</font></summary>

## CompCert and VST variants

For some packages, notably CompCert and VST (the Princeton tool-chain for verification of C code), exist various variants.

By default the 64 bit variant of CompCert and the 64 bit variant of VST are installed.

You can install the 32 bit variants in addition any time later by issuing `opam install` commands, e.g.
```
opam install coq-compcert-32.3.9
opam install coq-vst-32.2.8
```
Please note that since both variants can be installed in parallel, only one, the 64 bit variant, is immediately available to Coq
without -Q and -R options.
If you want to work with the 32 bit variants, please use these options in your Coq project:
```
-Q $(coqc -where)/../coq-variant/compcert32/compcert compcert
-Q $(coqc -where)/../coq-variant/VST32/VST VST
```

**Important note:** CompCert is **not** free / open source software, but may be used for research and evaluation purposes.
Please clarify the license at [CompCert License](https://github.com/AbsInt/CompCert/blob/master/LICENSE).

## Installation of other packages

- On Windows open a shell with `C:\<your_coq_platform_cygwin_path>\cygwin.bat`.
- On Linux or macOS open a shell in the usual way.
- Run the command `opam switch` which will show the list of available switches:
    ```
    #   switch                                 compiler                    description
        __coq-platform.2021.09.0~8.12          ocaml-base-compiler.4.10.0  __coq-platform.2021.09.0~8.12
        __coq-platform.2021.09.0~8.13          ocaml-base-compiler.4.10.0  __coq-platform.2021.09.0~8.13
        __coq-platform.2021.09.0~8.13~2021.02  ocaml-base-compiler.4.10.0  __coq-platform.2021.09.0~8.13~2021.02
    ->  __coq-platform.2021.09.0~8.14+beta1    ocaml-base-compiler.4.10.0  __coq-platform.2021.09.0~8.14+beta1
        _coq-platform_.2021.02.1               ocaml-base-compiler.4.07.1  _coq-platform_.2021.02.1
    ```
- Choose the switch you want to change with this command (example):
    ```
    opam switch __coq-platform.2021.09.0~8.13
    eval $(opam env)
    ```
- Install additional packages with `opam install "package"`
- You can find packages with `opam list --all | grep "some keyword"`

</details>
