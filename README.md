# gtkmm-msvc

A project to package up gtkmm and its dependencies for use in an MSVC development environment.

## Prelude

Along with the GPL license on this work -- which is only repackaging other OpenSource packages, some of which are themselves under GPL -- please accept this blessing (acknowledging SQLite, from their [`LICENSE.md`](https://github.com/sqlite/sqlite/blob/master/LICENSE.md?plain=1#L37-L39)):

* May you do good and not evil.
* May you find forgiveness for yourself and forgive others.
* May you share freely, never taking more than you give.

## Intro

A collection of build drivers to get `gtkmm` and its dependencies into a coherent place in a Windows Development Environment.
It depends on `gtk-msvc` which packages the C-dependencies `gtkmm` needs.

As has been done with `ansak-string`, `ansak-lib`, and `sqlite_msvc_packager`, this build driver enables an environment where
* all headers associated with `gtkmm` and its dependencies are placed in `C:\ProgramData\include`
* all link libraries, whether static-link or stub libraries to link to a `DLL` are placed in `C:\ProgramData\lib`
   * with separate sub-directories from `Release`, `Debug`, `RelWithDebInfo` and `MinSizeRel` where appropriate.

It uses python scripts, `configure.py` and `make.py` to simulate only loosely the standard commands and targets used in a typical `autoconf`/`automake`-driven build setup, selecting only to run python3. (`python2` is beyond deprecation now)

## Prerequisites

* A python interpreter. The one from [python.org](https://python.org) is recommended.
* Turn off Windows auto-redirect from `python` and `python3` to the app store ([here's how](https://stackoverflow.com/questions/58754860/cmd-opens-windows-store-when-i-type-python) -- find the "App Execution Alias" image, should be in most-popular answer)
* update pip and install tools:
    * `python --version` -- to verify you have a "latest"-ish python3 installed
    * `python -m ensurepip --default-pip` -- to make sure pip is there
    * `python -m pip install --upgrade pip setuptools wheel` -- to make sure the pip system is up to date
    * `python -m pip install patch pyyaml` -- to bring in a couple of tools the scripts depend on
* install gendef: it creates stub libraries for `.DLL` components whose build process doesn't itself produce `.LIB` files as part of their build. Recommendation is the [ansak packaged version](https://github.com/ANSAKsoftware/gendef-msvc) but any version of the GPL tool will do.
* if you use the ansak version of gendef, per sé, you will want your `PATH` variable to include `C:\ProgramData\bin` -- or copy `gendef.exe` produced there to a `tools` directory on your system, whatever you happen to call it.

For build systems, you may want to do these inside a python virtual environment (`venv` -- iykyk). If you have no idea what I'm talking about there, you're probably okay just doing the above for now.
