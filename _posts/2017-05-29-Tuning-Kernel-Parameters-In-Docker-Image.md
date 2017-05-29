
In this post, I will walkthrough the basic steps needed in order to tune the kernel parameters 
in the docker image of your desired distro.

Pull the docker image from the dockerhub.

`docker pull ubuntu`

Execute the command 

`docker run -it --rm --privileged ubuntu` 

-it options tells it run in interactive mode; --rm tells that the container must be destroyed when we exit 
the system; --privileged needs to be set as we are trying to make changes to the proc and sys directories 
for which the docker does not allow any changes when in normal mode. Therefore, we need privileged mode.

Once you are into the system, you can now install any packages you want. Make all the desired configurations.
As an example, let's enable IP forwaring on this image. Execute 

`sysctl -w net.ipv4.ip_forward=1`

Keep this terminal open.

Open another terminal. Now, let's try to make a new image which will have these settings.

`docker commit <containerid> <imagename>:<imagetag>`

`docker commit fe1799e6987e tuning:latest`

You can now view the images by typing

`docker images -a`

If you want to push the image to the dockerhub then, login and create a tag and push.

`docker login` 

`docker tag tuning:latest rohittahiliani/practice` 

`docker push rohittahiliani/practice`
