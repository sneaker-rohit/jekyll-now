In this post, I will define the configurations to be made for running the docker daemon on the network port so that it can be accessed by the remote docker client. 

Installing docker on our machine installs 2 components. Docker Client and the Docker Daemon. This is a Client/Server model with `dockerd` acting as the server and 'docker' acting as the client. Docker daemon by default listens to the unix socket created at `/var/lib/docker.sock'. However, it is also possible to run `dockerd` on a network port and make it accessible by a remote machine. 

First, let us see that dockerd is running on a unix socket. To view this, let's first run the docker service.

`service docker start`

Now, let's try and search for "docker.sock".

`lsof | grep "docker.sock"`

You can see that the docker deamon being running under `/var/lib/docker.sock`.

Moreover, to confirm that it's not running on a network port. We can use,

`netstat -tlp | grep "docker"`

There should be no results here. 

Now, let's try and run docker deamon on port 2375. Please note that 2375 is used for unencrypted communications. Ideally, you should be running on 2376 with TLS encryption turned on. For this post, I will cover only the unencrypted way to communicate. 

`dockerd --host 192.1168.0.80:2375`

To verify, you can check `netstat -tlp | grep "docker"` and that should give you the information about docker running on port 2375 in a listen state. 

From the remote machine, ensure first that you have connectivity to the system running the docker daemon. A simple way to check would be to ping the system. ping `192.168.0.80` should give you some replies unless ICMP has been blocked. 

At your remote machine terminal, set an env variable DOCKER_HOST with a value set to `tcp://192.168.0.80:2375`

`export DOCKER_HOST=tcp://192.168.0.80:2375`

Now run,

`docker version`

Look through the details and you should observe that the details being listed are that of the docker daemon running on a different machine.

It is quite possible that you get errors during the process. Please check if your firewall is blocking any traffic.    






