In this post, I will walk through the basic commands which are often used while dealing with containers. We will look into starting, stopping, restarting and removing containers. We will also have a look at the processes running inside a container and how we can get the low level information about containers. Finally, we will look at removing containers.

**Start, Stop and Restart Containers**

Let's assume that you have already instantiated an container. If not, you can do so by 

`docker run -it ubuntu /bin/bash`

You will be taken into the shell mode in the container. Let's just exit for now and return back to our prompt.

Now, let's have a look at the running docker processes. We should be able to see our container which exited a few seconds ago.

`docker ps -a`

If you just want to know the status for the last container that executed, you can look by 

`docker ps -l`

Now, make a note of the container id as we need it to perform most of the tasks. Let's first try to start a container. 

`docker start 3bda38531a06`

3bda38531a06 is the container id for me. You must replace this with yours. Now, if we check the status again, we will see that it's running. But how do we attach to the terminal?

`docker attach 3bda38531a06`

This will take us to the prompt. Now, let's exit from here by typing `exit`.

Great. Now, let'c check the `docker ps -l` and we should see the status being changed to exited. Hang on, what if we needed just to exit the prompt but actually wanted the container to keep running? Let's accomplish this with the help of `docker exec`. However, let's start the container first.

`docker start 3bda38531a06`

and now

`docker exec -it 3bda38531a06 /bin/bash`

We will be taken to the prompt for the container. However, now when we exit from here, it does not exit/kill the container. We can execute `docker ps -l` and see that the container is still up. Now, a simple way to attach to it would be to use the `docker attach` as we looked before.

`docker attach 3bda38531a06`

That's it. Now, let's try some more commands. These are fairly simple and need no explanation. Let's try to stop and restart.

`docker stop 3bda38531a06`

`docker restart 3bda38531a06`


**Looking Inside Containers**

What if we wanted to have a look into the running processes inside a container?

`docker top 3bda38531a06`

What if we wanted to have a look into the low level info such as host configurations, network configurations and much more?

`docker inspect 3bda38531a06`

What if we wanted to look into the recent activity in the container?

`docker logs 3bda38531a06`

**Removing Containers**

We have looked into most of the basic commands that we would make use of while working with containers. Therefore, let's try and remove these containers now. 

`docker rm 3bda38531a06`

If the container is running; it will throw an error. However, we can remove it forcefully by using the -f switch. 

`docker rm -f 3bda38531a06`

That's all for this post. I hope this has been useful. :)


