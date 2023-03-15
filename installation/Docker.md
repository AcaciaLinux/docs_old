# Getting the container image
## Pulling the container
 We do provide a image on the docker hub. You can download it using the following command. You can skip the step of creating your container.
 ```bash
 docker pull maxkofler/acacialinux
 ```

 If you want to create the image yourself, follow the steps of "Creating a Docker container image"

# Creating a Docker container image

This guide helps you to create a docker image of your AcaciaLinux, this is mainly for development reasons.

## Creating the rootfs

First of all, you will need a rootfs tarball, eg. ```acacialinux.tar.xz``` . You need to create a directory for building your docker image:

```bash
mkdir acaciaImage
```

To which you will copy the rootfs tarball and extract it:

```bash
cp ....../acacialinux.tar.xz acaciaImage/
cd acaciaImage
tar xpfv acacialinux.tar.xz
```

## Creating the Dockerfile

Docker needs a file that describes the image, but ours will be very simple. Create `acaciaImage/Dockerfile` and paste the following contents:

```dockerfile
FROM scratch
ADD . /
```

Note that the `Dockerfile` has to be **IN** the rootfs. This says that we create a image from scratch using the contents of the current directory (the directory of the Dockerfile) as root.

## Creating the image

Once the upper steps are done, you can build the docker image using the following command:

```bash
docker build -t acacialinux/acacialinux acaciaImage
```

# Creating a container

Once we created the image, we can instantiate containers from it using the following command:

```bash
docker create --name myAcaciaLinux -t -i maxkofler/acacialinux:latest bash
```

This will create a container named `myAcaciaLinux` using our generated image and on startup, it will execute the command `bash`.

If you created the container yourself, use `acacialinux/acacialinux` instead of `maxkofler/acacialinux`.

# Starting the container

Before using the container, you will have to start it using the following command:

```bash
docker start myAcaciaLinux
```

# Using the container

If you want to receive a shell from the container just use the following command on your host:

```bash
docker exec -it myAcaciaLinux bash
```

And to apply your bash config once in the container:

```bash
source /etc/profile
```

# Passing through a directory

If you want to pass the container a local directory you can skip the steps of pulling, creating and starting the container and use this step immediately:
```bash
docker run --name=<myName> -it -d -v /absolute/path/to/source/:/path/in/container maxkofler/acacialinux bash
```

# That's it!

You now have a AcaciaLinux container at your disposal, and you can create many more from your image!
