[ HOME ](README.md)
# Read 31 - Django REST Framework & Docker

## A Beginner's Guide to Docker
> An analogy we can use here is that of homes and apartments. Virtual Machines are like homes: stand-alone buildings with their own infrastructure including plumbing and heating, as well as a kitchen, bathrooms, bedrooms, and so on. Docker containers are like apartments: they share common infrastructure like plumbing and heating, but come in various sizes that match the exact needs of an owner.


- Docker which is a way to isolate and run entire applications.
- With Docker it doesn’t matter if you are using a Mac, Windows, or Linux computer anymore. 
- The entire development environment is isolated: programming language, software packages, databases, and more.
- **_With Docker we now longer have to mess around with virtual environments._**
- Docker is really just Linux containers which are a type of virtualization.
- Virtual machines are complete copies of a computer system from the operating system on up.
- What’s the downside to a virtual machine? Size and speed. 
- Linux containers, also known as “containerization”.
- Fundamentally, is what Docker is. A way to implement Linux containers!

### Containers vs Virtual Environments

- Containers are a lightweight alternative to Virtual Machines
- Containers are a running instance of an image.

Virtual environments are used to isolate Python software packages locally. We can create an isolated box for individual projects so one can use Python 2.7 and Django 1.5 while another can use Python 3.5 and Django 2.1 on **_the same computer. _**

**_But…virtual environments can only isolate Python packages._**

### Images and Containers
- An image is a snapshot in time of what a project **_contains_**. 
- A container is a _**running instance of the image**_.

### Images
- Every image is made up of one or more image layers. This is called _**image layering.**_ 
- Image layering exists for two main reasons:
  - First, each image layer is immutable–unchanged–like a git commit. This helps ensure consistency when two developers build the same image. 
  - The second reason is performance.

- To create a image we use `Dockerfile`.
```
$ touch Dockerfile
```
- The first instruction must be the FROM command which lets us import a base image to use for our image. Then in that file, add:

```
# Dockerfile
FROM python:3.7-alpine
```

#### Build the image
```
$ docker image build .
```

### Containers
- Dockerfile is a list of image instructions.
- docker-compose.yml file that is a list of container instructions.


# Sources

[Begginers Guide to Docker](https://wsvincent.com/beginners-guide-to-docker/)

[Dive into Docker](https://diveintodocker.com/ref-dfp)

#  Library Website and API

> The most important takeaway is that Django creates websites containing webpages, while Django REST Framework creates web APIs which are a collection of URL endpoints containing available HTTP verbs that return JSON.


- Django REST Framework works alongside the Django web framework to create web APIs.


[Tutorial](https://djangoforapis.com/library-website-and-api/)
