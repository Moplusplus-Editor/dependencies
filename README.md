# Mo++ Dependencies

All 3rd-party dependencies needed to build Mo++ from scratch.

## Overview

Mo++ relies on a large number of dependencies with specific versions for each, and building all of them locally can take a lot of time and effort. To simplify the process, we ship pre-compiled libraries that contain everything necessary for building and developing Mo++. This repo hosts the build scripts that download the source code of the libraries and package them.

## Exigence

We decided to create this repo after we realized there were major issues with existing build tools:

- Some require installing dependencies globally, which can mess up system libraries, and fail on systems that had their environment tweaked or setup differently, not to mention the need for unsafe root permissions
- Some require a lot of installation, heavy tweaking, and a large number of configuration files to work
- Some cannot handle the large amount of libraries that Mo++ requires, especially with the number of tweaks and differing configurations each library often requires in our use-case
- Some are not portable and cannot make a build from scratch, but instead need many prerequisites to be installed, and throw errors constantly that prerequisites are missing
- Some depend too heavily on an internet connection and rapidly degrade ungracefully if the internet connection drops during a build
- Some are extremely fragile, host huge dependency trees, and add a huge amount of size to the final binary

Instead, we settled on a custom build system that combines aspects of both Blender's build bootstrapper and Gaffer's dependencies library. Here is a basic explanation of how it works:

- Each library's source code is downloaded (with git) and compiled
- The compiled library is placed in a local folder relative to the root of Mo++'s sources
- As Mo++ is compiled, it references the local compiled library to static-link to them correctly

## Usage

In Mo++'s main repo, this directory should be a submodule. If that is the case, just run `python mbuilder.py` which should automatically download the pre-compiled binaries generated from this dependency repo.

If you're not planning on downloading the pre-complied libaries, you can build the libraries like so...

## Thanks

We owe a thank you to the [Gaffer](https://gafferhq.org) team and [Blender](https://blender.org) for coming up with the original version of this idea. See [Gaffer's dependencies repo](https://github.com/GafferHQ/dependencies) for more detail on how they implemented this.
