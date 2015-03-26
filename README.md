dockhut ![Dock hut](http://upload.wikimedia.org/wikipedia/commons/thumb/4/4d/EcoTourismDocksChicoasen.jpg/320px-EcoTourismDocksChicoasen.jpg)
=======

Scripts and dockerfiles for Dockerized user "hut" containers with sshd daemon
and automatically setup user account. The normal use case is a single "hut"
container for each "hut" user with an different SSH port for each "hut" user.

This system is very similar to
[dockersh](https://github.com/Yelp/dockersh) but more like the
[Docker SSH Daemon Example](https://docs.docker.com/examples/running_ssh_service/)

Features
--------
* if hut users are using tmux/screen, their terminal session will continue to
  run if they are disconnected
* hut users can not see all the other users or processes running on the host
* hut containers are ephemeral, hut user files and hut SSH keys are stored in
  the host file system, not inside the container image
* no suid is set
* sshd is the only program or script running as root

Downsides
---------
* an sshd daemon process is running per hut user all the time
* each hut users must use a different SSH port exposed on the host

Usage
-----

```
sudo dockhut-useradd bob
sudo dockhut-keygen bob
sudo curl http://example.com/bob/authorized_keys -o ~bob/huthome/.ssh/authorized_keys
sudo dockhut-run bob 606 castedo/dockhut-centos
```

Now `bob` can connect to port 606 on the host and get logged into a "hut"
container for just bob without visibility to the rest of the host system.

