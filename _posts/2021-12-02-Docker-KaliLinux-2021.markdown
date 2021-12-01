---
  layout: post
  title: Docker Installation (KaliLinux:2021)
  date: 2021-12-02 1:25:00 +0530
  image: docker.jpg
  tags: [docker]
---

Follow these step-by-step commands to install docker in kali linux machine (also virtual machine)

##Why use Docker?

When you are working, you most likely won’t only be using the tools that are included with Kali Linux, but you are using a lot of different tools that you find on Github. The classic way of installing those tools was to git clone the repository and then using install scripts to locally install them in your /opt/ folder on Kali Linux.
Recent trend that more and more Git Repositories are offering a pre-configured Docker file that you just need download and run, without the need of installing anything at all. (Except, of course, the only thing is that you need to install Docker on Kali Linux).

---

##Installation

Configuring APT & Keys
First, as always, update APT:
```bash
sudo apt update
```

Then we need to add the official Docker PGP key like so:
```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
```

Next, we configure APT so we will be able to download, install and update Docker.
```bash
echo 'deb [arch=amd64] https://download.docker.com/linux/debian buster stable' | sudo tee /etc/apt/sources.list.d/docker.list
```

After adding Docker to APT, we need to update apt once more so we will be able to install Docker on Kali Linux:
```bash
sudo apt update
```

In case you have any old and/or outdated versions of Docker installed on your system, we make sure to get rid of them first:
```bash
sudo apt remove docker docker-engine docker.io
```

Once this is done, we are ready to install Docker on Kali Linux:
```bash
sudo apt install docker-ce -y
```

Finally, starting Docker:
```bash
sudo systemctl start docker
```

---

##Verifying the Installation

```bash
sudo docker run hello-world
```
