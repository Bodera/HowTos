# Docker
Software which deals with operating-system-level virtualization.

## Download
You can download Docker Community Edition for Debian by clicking  [here](https://docs.docker.com/install/linux/docker-ce/debian/).

## Starting Docker CE on Debian 9
Remove older versions, than install the right package. 
```bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
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
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## License
The softwares stored in this repository aren't covered by any license yet.
