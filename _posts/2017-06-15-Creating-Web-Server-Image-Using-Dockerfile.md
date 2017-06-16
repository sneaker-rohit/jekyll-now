In this post, I will walk through the basics of building an image from a Dockerfile. In order to do so, we will understand some of the Dockerfile instructions. Furthermore, we will have a look at the image layers and their relation to the Dockerfile. 

Dockerfile is a way of providing instructions that must be followed while creating a new image. We can build the images from a Dockerfile by using the `docker build` command. 

Some of the Dockerfile instructions that we will be using in this example are:

`FROM` -> mention the base image and tag using which the new image should be created.

`RUN` -> gets executed at build time. For example, installing some additional packages on the base image.

`EXPOSE` -> specify the port that you want to expose to the outside world. All the containers that are spinned up using this image will have this port exposed.

`CMD` -> gets executed at the run time. Therefore, once the container is up CMD instruction gets executed. Only one CMD instruction is permitted per container.

Let's create a simple Dockerfile in our directory. In this Dockerfile, we will create an image for an apache web server using the base image as ubuntu. Moreover, let's try to install some more packages such as ping and nano for our demonstration purposes. Please make sure that the case is right. It should be Dockerfile and not dockerfile or DockerFile.

`nano Dockerfile` 

and paste the below contents in the file and save the file.

`# Launching a web server using a Dockerfile`

`FROM  ubuntu:latest`

`RUN apt-get update && apt-get install -y iputils-ping \
				   && apt-get install -y apache2 apache2-utils nano \
				   && apt-get clean` 

`EXPOSE 80`

`CMD ["apache2ctl","-D","FOREGROUND"]`

Now, let's build the image using the below command. webserver is the name of the image and version1 is the tag we have specified.

`docker build -t "webserver:version1"`

Once the build process is completed, let's run our container using the new image we just created.

`docker run -d -p 80:80 webserver:version1 .`

The `.` at the end indicates that the Dockerfile is present in this directory. 

80:80 indicates that the port 80 on the Docker Host is mapped on to the port 80 of the Container.

Now, let's see if our container is running.

`docker ps -l`

Great! Now, we need to know the IP address of the container and one of the ways to get that is by using the `docker inspect`.

`docker inspect containerid`

Now, that we have the IP address for the container, let's go to the browser and hit 172.17.0.2:80. Replace this IP with the IP address of your container.

You should see a apache web server page being served :)

Now, one important note is that every time when a `RUN` instruction is used in the Dockerfile, a new layer of image is created. Creating too many layers is not a good idea and therefore you can see that we have clubbed the installation of ping, nano and apache webserver in one `RUN` instruction.

That's all for this post. This is just to get you familar with the Dockerfile basics and instructions. I hope it has been helpful. If you would like to suggest any modifications to the post, please feel free to get in touch. I will be happy to make the revisions and improve the quality further. 

Thank you for reading :)