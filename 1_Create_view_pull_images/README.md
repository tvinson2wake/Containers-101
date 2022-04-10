Install Docker on a Linux VM **I used Ubuntu or Centos 7**

*You could install on Windows but it works a bit differently*

This Guide will help with Installation: https://geekflare.com/docker-installation-guide/


# Exercise 1: Creating, pulling and running Docker images

In this exercise, you will create your first Docker image and inspect the history of image to see the layers which create the image. Finally, you will learn how to pull other existing Docker images from DockerHub for usage within your local Docker environment.

## Create a Dockerfile
Create a folder called nginx

Create a file called `Dockerfile` inside of the nginx folder with the following contents:

```
FROM ubuntu
LABEL maintainer="Your Name (your_user_id@waketech.edu)"
RUN apt-get update
RUN apt-get install -y nginx
CMD ["nginx", "-g", "daemon off;"]
EXPOSE 80
```
**Screenshot your Dockerfile**

Our starting point is from an ubuntu image. From there we add several layers to install and configure the latest version of nginx with `RUN`. `CMD` allows us to specify the default command when the container is started. In this case, this will run the nginx executable. Finally, we specify that we want to `EXPOSE` port 80 so that our nginx application can be accessed outside the container. Remember to change the `LABEL` line to use your own name and Email.

## Build your image

To create an image from your Dockerfile first open up the appropriate application. If running Docker-CE for Windows/Mac, ensure that Docker is running in your task bar and open up the `Terminal` application if on Mac or the `Command Prompt` application on Windows. Otherwise, if running Docker Toolbox on Windows, open up the `Docker QuickStart shell`. You will be using this shell environment for the duration of the workshop. To create the image, run:

`docker build -t mynginx:latest .`

The `-t` flag allows us to specify the image name followed by the image tag. By default, the image tag is always 'latest'.
*Note: if you are not in your same directory as your Dockerfile make sure to replace the `.` with the path to the directory containing the Dockerfile.*

## Inspect image history

To see the layers within the image you have just created run the following command:

`docker history mynginx`
**Screenshot the Output**

Notice that the layers which are from the ubuntu image will have a time stamp longer than the layers explicitly defined in your Dockerfile.

## View your local images

To see the images you have installed on your machine run the following command:

`docker images`
**Screenshot the Output**


## Pulling images

You now know how to create a Docker image using a Dockerfile, but with exception of custom built software, you usually want to run images that you don't maintain. Docker Hub is a registry that provides a marketplace for Docker images for all to use. The [official images](https://hub.docker.com/explore/) for products in their Docker-ized format will be built by the maintainers and published here. To pull the official ubuntu image from DockerHub, run the following command:

`docker pull ubuntu`
**Screenshot the Output**


As our custom built image for nginx was running on ubuntu, the docker engine will not actually pull any layers from DockerHub but will use the same layer it pulled when running the `mynginx` image. If you want to be double sure, you can run `docker history ubuntu` and you should see all the same commands and layer sizes as the base layers for `mynginx`.

Congratulations, you now know how to create a Docker image from a Dockerfile, view the history of a Docker image and how to pull images from the Docker registry! Continue on to the [next exercise](../2_Create_view_stop_containers) to learn how to start working with containers.
