# Docker Notes

## Running a docker container

```
docker run hello-word
```
```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
```


```
docker run -it ubuntu bash
```
- `-it`: interactive model
- `ubuntu`: name of docker image
- `bash`: parameter: command to execute in the (`ubuntu`) image

### Run version of an image
```
docker run -it python:3.10
```
- `python`: docker image
- `3.9`: tag: version of docker image

### To install a Python package, enter docker container from `bash`
```
docker run -it --entrypoint=bash python:3.10

pip install pandas
which python
python
```

## Docker build

Create a `Dockerfile` file in the directory to build this file. Then
```
docker build -t test:pandas .
```
- `-t`: tag the image
- `test:pandas`: name of image (`test`) and version of image (`pandas`)
- `.` build the image in the current directory (where the `Dockerfile` exists)

```
[+] Building 20.8s (6/6) FINISHED                                                                                                     
 => [internal] load build definition from Dockerfile                                                                             0.0s
 => => transferring dockerfile: 104B                                                                                             0.0s
 => [internal] load .dockerignore                                                                                                0.0s
 => => transferring context: 2B                                                                                                  0.0s
 => [internal] load metadata for docker.io/library/python:3.10                                                                   0.0s
 => [1/2] FROM docker.io/library/python:3.10                                                                                     0.1s
 => [2/2] RUN pip install pandas                                                                                                19.2s
 => exporting to image                                                                                                           1.3s
 => => exporting layers                                                                                                          1.3s
 => => writing image sha256:8d298d94189705e2bda3bfd7bce41aa62cdb35ac5d9aaf792db2d2573d50ee4f                                     0.0s 
 => => naming to docker.io/library/test:pandas  
 ```
 
 ### Run the built image
 ```
 docker run -it test:pandas
 docker run -it test:pandas 2022-02-12
 docker run -it test:pandas 2022-02-12 123 sdf
 ```
 - `2022-02-12`: argument for python script (`sys.argv[1]`)
 - `2022-02-12 123 sdf`: can specify multiple arguments
 
 
 




