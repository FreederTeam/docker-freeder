# Dockerfile for Freeder

Based on [Dockerfile for FreshRSS](https://github.com/marienfressinaud/docker-freshrss).

This file is destined to configure a virtual environment for Freeeder. It's
based on Centos 6 as it is shipped with PHP 5.3.

**Please note it's only for developers or testing!** It's assumed you know Docker and you have already installed it on your computer. If it's not, please refer to [the official website](http://www.docker.com/).

If you have troubles to use this image and **answer is NOT in this document**, feel free to contact me at
phyks@phyks.me (or any member of the FreederTeam).


## In details
### Get the Freeder image

First get the Docker image on your PC:
```
$ git clone https://github.com/FreederTeam/docker-freeder.git docker-freeder
$ docker build -t freederteam/freeder docker-freeder
```

### Get Freeder

Note image does NOT include Freeder source code! You should first get the code
from Github:

```
$ git clone https://github.com/FreederTeam/Freeder.git Freeder
```

### Run a Freeder container

To use Freeder image, you should run it and mount your local Freeder
directory in the corresponding running container. Do not forgive to map port
```8080``` (or anyone else) on port ```80```:

```
$ docker run -t -i -v /path/to/Freeder:/var/www/html/Freeder -p 8080:80 freederteam/freeder
```

Now, you have access to a shell where you can do whatever you want (you have a
root access!). In a basic usage, you should not have need of this shell. Just
keep it open and read the next section :)

- apache UID is 1000 and GID is 100. Note that you can have to change these
  values to match with owner of source code. To do that: ```usermod -u NEW_UID
  -g NEW_GID apache```
- You have access to Freeder source code in ```/var/www/html``` (be careful, if you
  change it, it is changed on the host OS too)
- If you want to install new packages, remember you use a Centos: ```yum
  install``` command is your friend…


## Install Freeder
Last step is to install Freeder. Don't worry, you will not have to do that
next time.

1. Open a web browser on [127.0.0.1:8080/Freeder](http://127.0.0.1:8080/Freeder)
2. Follow the different steps.
3. Once Freeder is installed, enjoy!


## Configure an alias

Command line to start Freeder container is a bit long. You can add an alias in
your ```~/.bashrc```:

```
alias start-freeder='docker run -t -i -v /path/to/Freeder:/var/www/html/Freeder -p 8080:80 freederteam/freeder'
```

Remember to reload ```~/.bashrc``` information with ```source ~/.bashrc```.


### Keep container in background
You may have no need of a shell. You can change ```-t``` argument by ```-d```:

```
alias start-freeder='docker run -d -i -v /path/to/Freeder:/var/www/html/Freeder -p 8080:80 freederteam/freeder'
```
