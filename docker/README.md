# Docker
Software which deals with operating-system-level virtualization.

## Starting Docker CE on Debian 9

Remove older versions, than install the right package. 

```bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

Now obtain dependency packages to install docker from PPA repo.

```bash
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common
$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
$ sudo apt-key fingerprint <last 8 characters of the fingerprint>
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
$ sudo apt-get update
```

The finally install docker.

```bash
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## Installing Docker on Debian 10

Start by checking if there is none older version of Docker installed on your machine.

```bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

Now you have a few options to go on:

I - Install by the convinient way  by adding the PPA repository from Docker official GPG key  
II - Install from a `.deb` package and update it manually after each new release  
III - Install by running a convenience script provided by the Docker-CE team (not recommend for production env)

Here I choose to demonstrate the second option. You can explore the other options [here](https://docs-stage.docker.com/engine/install/debian/).

First you need to access the [Docker for Debian download page](https://download.docker.com/linux/debian/dists/buster/). Once there navigate to `pool/`, then `nightly/`, and finally choose the link correspondent to your [instruction set architecture](https://en.wikipedia.org/wiki/Comparison_of_instruction_set_architectures#Instruction_sets). The url will look like this:

```html
https://download.docker.com/linux/debian/dists/buster/pool/nightly/amd64/
```

Once there, you will find several packages, different versions of the following packages:

* __containerd.io__ - daemon to interface with the OS API (in this case, LXC - Linux Containers), essentially decouples Docker from the OS, also provides container services for non-Docker container managers
* __docker-ce__ - Docker daemon, this is the part that does all the management work, requires the other two on Linux
* __docker-ce-cli__ - CLI tools to control the daemon, you can install them on their own if you want to control a remote Docker daemon

You must download a version of each of these three. I recommend the latest ones.

Therefore, you must have downloaded three files with names similar to:

* `containerd.io_1.2.6-3_amd64.deb`
* `docker-ce_0.0.0-20190727010531-15bdbd76a5-0_debian-buster_amd64.deb`
* `docker-ce-cli_0.0.0-20190727010531-15bdbd76a5-0_debian-buster_amd64.deb`

Now things get easier. Go to the directory where the files are stored and install them using the `dpkg` tool.

```bash
$ cd Downloads/
$ sudo dpkg -i containerd.io_1.2.6-3_amd64.deb docker-ce_0.0.0-20190727010531-15bdbd76a5-0_debian-buster_amd64.deb docker-ce-cli_0.0.0-20190727010531-15bdbd76a5-0_debian-buster_amd64.deb
```

Check that everything has been set up correctly by running the `hello-world` container image.

```bash
$ sudo docker run hello-world
```

Keep in mind that to upgrade Docker Engine, you will have to download the newer package file and repeat the installation procedure, pointing to the new file.

Docker has a experimental feature called [Rootless mode](https://docs-stage.docker.com/engine/security/rootless/). But here I stick with the standard procedure of adding existing users to the `docker` group.

Just execute the given commands:

```bash
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
$ newgrp docker
```

First we create the `docker` group (which must have already been created when we installed the Docker Engine), then we add the current logged-in user to this group and force the activation of the changes we made in this group. To test that everything was set up correctly, run:

```bash
docker run hello-world
```

## License

The softwares stored in this repository aren't covered by any license yet.
