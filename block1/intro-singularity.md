
# Introduction to Singularity

## Docker and Singularity

#### Important: 
Docker and [Singularity](http://singularity.lbl.gov/docs-docker) are friends but they have distinct differences.

#### Docker:

* Inside a Docker container the user has escalated privileges, effectively making them root on the host system. This is not supported by most administrators of High Performance Computing (HPC) centers.

#### Singularity:

* Works on HPC systems
* Same user inside and outside the container
* User only has root privileges if elevated with `sudo`
* Run (and modify!) existing Docker containers

Singularity uses a 'flow' whereby you can (1) create and modify images on your dev system, (2) build containers using recipes or pulling from repositories, and (3) execute containers on production systems.

The workflow we recommend for most researchers is to create Docker containers of their software and then run them on HPC and shared resources with Singularity using Singularity's ability to convert the Docker image to a Singularity image. Docker is simpler to install on most modern operating systems that are on a laptop or desktop.

## Machine Learning App with Singularity Runtime
In this tutorial, we will run a Machine Learning Image Classifier app that uses Singularity Runtime. You are not required to install Singularity today. Rest of this page can be completed as a self exercise.
You may now navigate to [Intro to Tapis Systems](https://tacc-cloud.github.io/gateways21-portable-computing-cloud-hpc/block3/tapis-systems/)


## Further Reading: (Not Needed For the Tutorial Today - Use At Home)

Singularity homepage: [http://sylabs.io](http://sylabs.io/)

While Singularity is more likely to be used on a remote system, e.g. HPC or cloud, you may want to develop your own containers first on a local machine.

## Setting up your Laptop

To Install Singularity on your laptop or desktop PC follow the instructions from Singularity: [Install Singularity Windows or Mac ](https://sylabs.io/guides/3.2/user-guide/installation.html#install-on-windows-or-mac) or [Install Singularity on Linux](https://sylabs.io/guides/3.2/user-guide/installation.html#install-on-linux)

## HPC

Load the Singularity module on a HPC

If you are interested in working on HPC, you may need to contact your systems administrator and request they install [Singularity](https://sylabs.io/guides/3.2/user-guide/installation.html#installationrequest).

Most HPC systems are running Environment Modules with the simple command `module`. You can check to see what is available:

```
  $ module avail
```

If Singularity is installed:

```
  $ module load singularity
    
```

## XSEDE Jetstream Cloud

We have already installed Singularity for you on your Jestream VM but in the future if you need to you can do the following:

Jetstream staff have deployed an Ansible playbooks called `ez` installation which includes [Singularity](https://cyverse-ez-quickstart.readthedocs-hosted.com/en/latest/#) that only requires you to type a short line of code.

Start a featured instance on Atmosphere or Jetstream.

Type in the following:

```
    $ ezs

    * Updating ez singularity and installing singularity (this may take a few minutes, coffee break!)
    Cloning into '/opt/cyverse-ez-singularity'...
    remote: Counting objects: 11, done.
    remote: Total 11 (delta 0), reused 0 (delta 0), pack-reused 11
    Unpacking objects: 100% (11/11), done.
    Checking connectivity... done.
```


## Check Installation

Singularity should now be installed on your laptop or VM, or loaded on the HPC, you can check the installation with:

```
>singularity --help
USAGE: singularity [global options...] <command> [command options...] ...

GLOBAL OPTIONS:
    -d|--debug    Print debugging information
    -h|--help     Display usage summary
    -s|--silent   Only print errors
    -q|--quiet    Suppress all normal output
       --version  Show application version
    -v|--verbose  Increase verbosity +1
    -x|--sh-debug Print shell wrapper debugging information

GENERAL COMMANDS:
    help       Show additional help for a command or container
    selftest   Run some self tests for singularity install

CONTAINER USAGE COMMANDS:
    exec       Execute a command within container
    run        Launch a runscript within container
    shell      Run a Bourne shell within container
    test       Launch a testscript within container

CONTAINER MANAGEMENT COMMANDS:
    apps       List available apps within a container
    bootstrap  *Deprecated* use build instead
    build      Build a new Singularity container
    check      Perform container lint checks
    inspect    Display container's metadata
    mount      Mount a Singularity container image
    pull       Pull a Singularity/Docker container to $PWD

COMMAND GROUPS:
    image      Container image command group
    instance   Persistent instance command group


CONTAINER USAGE OPTIONS:
    see singularity help <command>

For any additional help or support visit the Singularity
website: http://singularity.lbl.gov/
```


## Downloading Singularity containers

The easiest way to use a Singularity container is to `pull` an existing container from one of the Container Registries maintained by the Singularity group or from Docker Hub.  There are ways to build a container with a recipe similar to how you create a Dockerfile - see [Singulairty Recipe Documentation](https://sylabs.io/guides/2.6/user-guide/quick_start.html#singularity-recipes)

## Exercise

### Pulling a Container

You can use the `pull` command to download pre-built images from a number of Container Registries, here we'll be focusing on the [DockerHub](https://hub.docker.com/).

Container Registries:

* `shub` - images hosted on Singularity Hub 
* `library` - *this is only accessible on Singularity 3 or greater
* `docker` - images hosted on Docker Hub

This example pulls a Ubuntu 16.04 container from DockerHub

Build to your container by pulling an image from Docker:

```
	$ singularity pull docker://ubuntu:16.04
	WARNING: pull for Docker Hub is not guaranteed to produce the
	WARNING: same image on repeated pull. Use Singularity Registry
	WARNING: (shub://) to pull exactly equivalent images.
	Docker image path: index.docker.io/library/ubuntu:16.04
	Cache folder set to /home/.../.singularity/docker
	[5/5] |===================================| 100.0%
	Importing: base Singularity environment
	Importing: /home/.../.singularity/docker/sha256:1be7f2b886e89a58e59c4e685fcc5905a26ddef3201f290b96f1eff7d778e122.tar.gz
	Importing: /home/.../.singularity/docker/sha256:6fbc4a21b806838b63b774b338c6ad19d696a9e655f50b4e358cc4006c3baa79.tar.gz
	Importing: /home/.../.singularity/docker/sha256:c71a6f8e13782fed125f2247931c3eb20cc0e6428a5d79edb546f1f1405f0e49.tar.gz
	Importing: /home/.../.singularity/docker/sha256:4be3072e5a37392e32f632bb234c0b461ff5675ab7e362afad6359fbd36884af.tar.gz
	Importing: /home/.../.singularity/docker/sha256:06c6d2f5970057aef3aef6da60f0fde280db1c077f0cd88ca33ec1a70a9c7b58.tar.gz
	Importing: /home/.../.singularity/metadata/sha256:c6a9ef4b9995d615851d7786fbc2fe72f72321bee1a87d66919b881a0336525a.tar.gz
	WARNING: Building container as an unprivileged user. If you run this container as root
	WARNING: it may be missing some functionality.
	Building Singularity image...
	Singularity container built: ./ubuntu-16.04.simg
	Cleaning up...
	Done. Container is at: ./ubuntu-16.04.simg
```

Note, there are some Warning messages concerning the build from Docker.

The example below does the same as above, but renames the image.

```
	$ singularity pull --name ubuntu_docker.simg docker://ubuntu:16.04
   	Importing: /home/***/.singularity/docker/sha256:c71a6f8e13782fed125f2247931c3eb20cc0e6428a5d79edb546f1f1405f0e49.tar.gz
	Importing: /home/***/.singularity/docker/sha256:4be3072e5a37392e32f632bb234c0b461ff5675ab7e362afad6359fbd36884af.tar.gz
	Importing: /home/***/.singularity/docker/sha256:06c6d2f5970057aef3aef6da60f0fde280db1c077f0cd88ca33ec1a70a9c7b58.tar.gz
	Importing: /home/***/.singularity/metadata/sha256:c6a9ef4b9995d615851d7786fbc2fe72f72321bee1a87d66919b881a0336525a.tar.gz
	WARNING: Building container as an unprivileged user. If you run this container as root
	WARNING: it may be missing some functionality.
	Building Singularity image...
	Singularity container built: ./ubuntu_docker.simg
	Cleaning up...
	Done. Container is at: ./ubuntu_docker.simg
```

When we run this particular Docker container without any runtime arguments, it does not return any notifications, and the Bash prompt does not change the prompt.

```
	$ singularity run ubuntu_docker.simg
	$ cat /etc/*release
	DISTRIB_ID=Ubuntu
	DISTRIB_RELEASE=16.04
	DISTRIB_CODENAME=xenial
	DISTRIB_DESCRIPTION="Ubuntu 16.04.3 LTS"
	NAME="Ubuntu"
	VERSION="16.04.3 LTS (Xenial Xerus)"
	ID=ubuntu
	ID_LIKE=debian
	PRETTY_NAME="Ubuntu 16.04.3 LTS"
	VERSION_ID="16.04"
	HOME_URL="http://www.ubuntu.com/"
	SUPPORT_URL="http://help.ubuntu.com/"
	BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
	VERSION_CODENAME=xenial
	UBUNTU_CODENAME=xenial
```

Whoa, we're inside a container!?!

This is the OS on the VM I tested this on:

```
> exit
> cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=18.04
DISTRIB_CODENAME=bionic
DISTRIB_DESCRIPTION="Ubuntu 18.04.2 LTS"
NAME="Ubuntu"
VERSION="18.04.2 LTS (Bionic Beaver)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 18.04.2 LTS"
VERSION_ID="18.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=bionic
UBUNTU_CODENAME=bionic
```

Here we are back in the container:

```
	$ singularity shell ubuntu_docker.simg
	Singularity: Invoking an interactive shell within container...

	Singularity ubuntu_docker.simg:~> cat /etc/*release
	DISTRIB_ID=Ubuntu
	DISTRIB_RELEASE=16.04
	DISTRIB_CODENAME=xenial
	DISTRIB_DESCRIPTION="Ubuntu 16.04.3 LTS"
	NAME="Ubuntu"
	VERSION="16.04.3 LTS (Xenial Xerus)"
	ID=ubuntu
	ID_LIKE=debian
	PRETTY_NAME="Ubuntu 16.04.3 LTS"
	VERSION_ID="16.04"
	HOME_URL="http://www.ubuntu.com/"
	SUPPORT_URL="http://help.ubuntu.com/"
	BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
	VERSION_CODENAME=xenial
	UBUNTU_CODENAME=xenial
	Singularity ubuntu_docker.simg:~>
```

When invoking a container, make sure it executes and exits, or notifies you it is running.

Keeping track of downloaded images may be necessary if space is a concern.

By default, Singularity uses a temporary cache to hold Docker tarballs:

```
  $ ls ~/.singularity
```

You can change these by specifying the location of the cache and temporary directory on your localhost:

```
  $ mkdir tmp
  $ mkdir scratch

  $ SINGULARITY_TMPDIR=$PWD/scratch SINGULARITY_CACHEDIR=$PWD/tmp singularity --debug pull --name ubuntu-tmpdir.simg docker://ubuntu
```

## Running Singularity Containers

Commands:

`exec` - command allows you to execute a custom command within a container by specifying the image file.

`shell` - command allows you to spawn a new shell within your container and interact with it.

`run` - assumes your container is set up with "runscripts" triggered with the `run` command, or simply by calling the container as though it were an executable.

`inspect` - inspects the container.

`--writable` - creates a writable container that you can edit interactively and save on exit. (requires sudo permissions)

`--sandbox` - copies the guts of the container into a directory structure.

## Exercise

### Using the `exec` command


```
    $ singularity exec ubuntu_docker.simg cat /etc/os-release
```

###  Using the `shell` command

```
    $ singularity shell ubuntu_docker.simg
```

### Using the `run` command

```
    $ singularity run ubuntu_docker.simg
```

###  Using the `inspect` command

You can inspect the build of your container using the `inspect` command

```
    $ singularity inspect ubuntu_docker.simg

```

### Using the `--sandbox` and `--writable` commands

As of Singularity v2.4 by default `build` produces immutable images in the 'squashfs' file format. This ensures reproducible and verifiable images.

Creating a `--writable` image must use the `sudo` command, thus the owner of the container is `root`

```
   	$ sudo singularity build --writable ubuntu-master.simg docker://ubuntu
```

You can convert these images to writable versions using the `--writable` and `--sandbox` commands.

When you use the `--sandbox` the container is written into a directory structure. Sandbox folders can be created without the `sudo` command.

```
    	$ singularity build --sandbox lolcow/ docker://ubuntu
	@vm142-73:~$ cd lolcow/
	@vm142-73:~/lolcow$ ls
	bin  boot  dev  environment  etc  home  lib  lib64  media  mnt  opt  proc  run  sbin  singularity  srv  sys  tmp  usr  var
```

### Bind Paths

When Singularity creates the new file system inside a container it ignores directories that are not part of the standard kernel, e.g. `/scratch`, `/xdisk`, `/global`, etc. These paths can be added back into the container by binding them when the container is run.

```
	$ sudo mkdir /xdisk
	$ sudo touch /xdisk/atest.txt
	$ singularity shell --bind /xdisk ubuntu-16.04.simg
	Singularity: Invoking an interactive shell within container...
	$Singularity ubuntu-16.04.simg:~> ls /xdisk
	atest.txt
	
```
The above commands - you create a "xdisk" folder at the root space and then we bind it to the container so it is available inside the container and start the container and go inside the container and then list the files from inside the container in "xdisk" - note that the file from the host we made "atest.txt" is in the container.

The system administrator can also define what is added to a container. This is important on campus HPC systems that often have a `/scratch` or `/xdisk` directory structure. By editing the `/etc/singularity/singularity.conf` a new path can be added to the system containers.


## Singularity Related Resources

We have only scratched the surface of using Singularity. For more information and resources see the links below.

[Singularity Homepage](https://sylabs.io/)

[Singularity Hub](https://www.singularity-hub.org/)

[University of Arizona Singularity Tutorials](https://docs.hpc.arizona.edu/display/UAHPC/Singularity+Tutorials)

[NIH HPC](https://hpc.nih.gov/apps/singularity.html)

## Singularity Talks

Gregory Kurtzer, creator of Singularity has provided two good talks online:

[Introduction to Singularity](https://wilsonweb.fnal.gov/slides/hpc-containers-singularity-introductory.pdf)

[Advanced Singularity](https://www.intel.com/content/dam/www/public/us/en/documents/presentation/hpc-containers-singularity-advanced.pdf)

Vanessa Sochat, lead developer of Singularity Hub, also has given a great talk on:

[Singularity](https://docs.google.com/presentation/d/14-iKKUpGJC_1qpVFVUyUaitc8xFSw9Rp3v_UE9IGgjM/pub?start=false&loop=false&delayms=3000&slide=id.g1c1cec989b_0_154)


## Additional Resources

For a deeper dive into building and using containers, especially in an HPC environment:

[Containers at TACC](https://containers-at-tacc.readthedocs.io/en/latest/)

