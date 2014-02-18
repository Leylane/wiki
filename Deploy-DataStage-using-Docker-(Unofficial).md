### Introduction

In its present state, DataStage isn't well-suited for installations on systems being shared by other services (especially other Django web applications). Reasons for this include a number of assumptions DataStage makes regarding your Python environment.

In an attempt to work around this without resorting to running an entire virtual machine dedicated to DataStage, a Dockerfile has been written to facilitate an automated installation inside a [Docker](https://www.docker.io/) container. In testing, this appears to work on an Amazon EC2 Micro instance running Ubuntu 12.04 with Docker 0.8 installed.

### Caveats

The author of this document and the linked Dockerfile is not associated with the DataStage project and makes no guarantees regarding its performance.
This Dockerfile will build a Docker image wherein DataStage, Apache, PostgreSQL, and SSHD are all installed and running together, with no robust process management taking place.
A better container design might be to have separate containers for each of these services.
This image may not be suitable for production use.

### Download the Dockerfile

* [View on Gist](https://gist.github.com/BHSPitMonkey/9081509)
* [Download (raw) from Gist](https://gist.github.com/BHSPitMonkey/9081509/raw)

### Instructions

Some basic instructions are provided in the comments in the header of the Dockerfile itself.
To start, create a new directory on your server and save/copy the Dockerfile there.
Be sure to `cd` into this directory before moving on.

#### To install using the DataStage apt repository:

If the DataStage apt repository (http://apt-repo.bodleian.ox.ac.uk/datastage) is available and you wish to use it, you will need to edit the Dockerfile and make the changes indicated in the header.

#### To install using local deb packages:

If the DataStage apt repository is unavailable or you wish not to use it, you must create a directory alongside your Dockerfile named `debs/` and place the .deb packages within. At the very least, you must supply the following packages (since none of these are available through Ubuntu's repositories):

* dataflow-datastage
* python-django-longliving  
* python-libmount
* python-django-conneg
* python-django-pam
* python-sword-client

#### Build the image

    sudo docker build -t datastage .

Once this command completes, you will have a Docker image called "datastage" ready to use and create containers with.

#### Create and run a container

    sudo docker run -d -p HOST_WEB_PORT:80 -p HOST_SSH_PORT:22 -v HOST_DIRECTORY:/srv/datastage:rw -name ds datastage

In the command above, you will need to replace the following placeholders:

* `HOST_WEB_PORT`: The port on your host machine which will forward to the DataStage web application (port 80 on the container). Example: `8080`
* `HOST_SSH_PORT`: The port on your host machine which will forward to the container's SSH service (port 22). Example: `2222`
* `HOST_DIRECTORY`: The path on your host machine which should be mounted in the container at `/srv/datastage`, which is where DataStage stores all of your data. Example: `/srv/datastage`

#### Log in using SSH to set up users

    ssh -p HOST_SSH_PORT root@localhost # Replace HOST_SSH_PORT with what you chose before

Using the default password of "badpassword", this will log you into your container as root.
You should use the following command to change the root password to something better:

    passwd

And then use the following command to open the DataStage configuration tool:

    datastage-config

Follow the [usual DataStage configuration steps](https://github.com/dataflow/DataStage/wiki/_pages) to set up user accounts, give them passwords, and so on. Note that this Dockerfile does not install samba by default, so you should skip the `smbpasswd` steps.

#### Try out the web interface

Keeping in mind the web port you chose earlier, visit the following address in your web browser:

    http://HOSTNAME:HOST_WEB_PORT

Just replace `HOSTNAME` with the IP address or DNS name of your server. Use `localhost` if you're accessing the web page from the same machine you installed the Docker container onto.