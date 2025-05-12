---
title: Docker Example Code / Project Starters
parent: Docker
nav_order: 52
layout: default
---

# What now?

_Ok? so what now? How Do I practice this? How do I use this?_... you may be wondering. 

Here are some short sample projects you can go through to get an idea of how to use docker and what it can do, because the best way to learn anything, is by doing it! (If you want to, you can skip to the end where there is a link with 10 project ideas)

**Note**: It is strongly recommended that you manage docker as a non-root user when working with docker as it makes life mush easier.
```bash 
sudo usermod -aG docker $USER
```

--- 

## Example 1 - Nginx webserver
This example will cover pullng the nginx image and what you can expect and how you can use it. Nginx (pronounced engine-x) is a high performance web server known for its speed, stability and low resource usage. It helps deliver web pages to users. When you type a website address in your browser, Nginx is often the software that takes that request and finds the right content to send back, like HTML files, images, or videos.

1. **Create a new directory for the project and pull the nginx image**
    ```bash
    # create the project file
    mkdir project_name

    sudo docker pull nginx
    ```
2. **Run the image**
    ```bash
    sudo docker run -p 80:80 nginx
    ```
    **_Explanation_**:
    - `-p` specifies a specific port for the hosting of the nginx server on your machine. 
3. **Open a browser**
    Type _localhost_ into the search bar 
    - **Note**: if you do not specify the port, you will recieve an "unable to connect" or a similar error
    You should see something like:
        ```bash
        Welcome to nginx!
        If you see this page, the nginx web server is successfully installed and working. 
        Further configuration is required.
        ...

        ```
        This is the default nginx page. 
        Also, keep in mind that if you want to choose a specific port, you can do so with 

        ```bash
        # where XXXX is your  port of choice
        sudo docker run -p XXXX:80 nginx

        # for example port 5000 would look like
        sudo docker run -p XXXX:80 nginx
        ```
        And when you search local host in the browser you would just append the port number to the end of your local host search. You would type it like so...
        _localhost:5000_...
        
4. **Add some html elements**
    create dockerfile: (you can do this through an editor like nano, vim or you can use an IDE like VScode)
    ```bash
    # for simplicity we will make the dockerfile in VScode
    # navigate to the project directory (project_name) and type...
    code . 
    ...
    ```
    VScode should open. And click File > New file and call it "_Dockerfile_"
    - Now create a folder in the project and call it static (Dockerfile should be outside of this file)
    - Inside of the static folder, Create another file called _index.html_ and write some html in it...
        ```bash 
        <!DOCTYPE html>
        <html>
        <head>
            <title>My Nginx Page</title>
        </head>
        <body>
            <h1>Hello, Missing SENG!</h1>
            <p>This is a custom page served by Nginx.</p>
            <p>Put your html here!</p>

        </body>
        </html>
        ```

5. **Building the dockerfile**
    You can copy this into the dockerfile

    ```bash
    FROM nginx:1.27.0

    COPY static /usr/share/nginx/html
    ```
    **Explanation**: 
    - `FROM` specifies the base image that you are using. 
    - `COPY` Copies all the files from the local static/ directory on your machine into the /usr/share/nginx/html directory inside the container. This is where Nginx looks for the files it serves, like index.html, images, or stylesheets. In other words, it tells Nginx what to display when you visit your site.

6. **Build the docker image**
    Remember, to run our container, we first need to build an _image_. 
    
    ```bash 
    # here is the base template to create your image
    # you can make image_name any name you would like
    sudo docker build -t image_name .
    ...
    # for demonstration we will make the image_name, firstsite 
    sudo docker build -t firstsite . 
    ```
7. **Run the image in a container**

    ```bash
    docker run -p 80:80 firstsite:latest
    ```
    Now when we check our local host our html me wrote should be served. 

---

## Example 2  - Golang

Golang or simply GO, is a simple and efficient compiled programing language (meaning it compiles down to machine language, and generally out performs interpreted languages). GO is well known for its fast compile times and support for creating concurrent applications. GO is a very popular for efficient server side applications and was the tool used to create docker. GO is usually used for web backends, cloud computing tools, microservices, and networking applications. 
As a beginner, you may encounter some troubles when trying to work with go (especially on windows). 

This Example will allow you to program and write go applications without the need to actually install GO. The idea here is to use a base Golang image to create a container which you can then use without needing to install go to your machine.

1. **Create a Dockerfile and image**
    Create a new project folder and navigate to it. Then create the Dockerfile ( you can use vim, nvim, nano or vscode to do so)
    ```bash
    FROM golang:latest

    WORKDIR /app

    RUN apt update && apt install -y nano

    CMD ["bash"]
    ```
    *_Explanation_: we are building off of the base golang image. We are setting our working directory in the container to the /app directory and we are updating the apt package manager so that we can install nano ( so that we can have a text editor when we open the image in a container)

    Then we can build our new image as custom-go-image

    ```bash
    docker build -t custom-go-image .
    ```
2. **Create a volume and container**
    
    In order for us to be able to keep our data when we exit our container we will need a volume

    ```bash
    docker volume create go-example-project
    ```

    After this, we can run the following to create a container of our new custom image and run it with our new volume

    ```bash
    docker run -it -v go-example-project:/app custom-go-image:latest bash

    ```

    _Explanation_: 
    - `it` creates allows us to interact with the container through the terminal. (Almost as if it was another directory)
    - `v` indicates your container is interacting with a volume, in our case it is the _go-example-project_. (If you do not specify this, you will not save your data)
    - `:/app` specifies the directory in the container that will load to and pull from the volume, in this case the _/app_ directory.
    - `custom-go-image:latest` is just the image you are containerizing with the `run` command.
    - `bash` overrides whatever **CMD** or **ENTRYPOINT** is set in the image and launches a Bash shell instead.

    **Note**: Your terminal should now display the Container ID with root infront of it (You should be in the app directory)
    ```bash 
    root@<containerID>:/app#
    ```
3. **Create a go file**
    Now we can create our go file. Name it how you please, however for demonstration it will be named main.go
    ```bash
    # create the main.go file in nano
    nano main.go

    # nano menu will open and write the following program
    ... 
    package main

    import "fmt"

    func main(){
        fmt.Println("Hello from inside the GO container!")
    }
    ```
    (Press ctrl+O, then ctrl+X to save and exit) 
4. **Running or program**
    There are two ways to run our program: we can simply use
    ```bash 
    go run main.go
    ```
    which will just run our code once. Or you can compile the file into a binary file like so 
    ```bash 
    # create the binaries
    go build main.go
    
    # run the binary file
    ./main.go
    
    ...

    # Expected output:
    Hello from inside the GO container!
    ```

**Note**:If at any point you want to exit any container, you can do so by entering `exit` command into the terminal. 

---

### Congratulations on creating your first Docker programs!
For more project ideas take a look at these [10 Docker Project Ideas](https://www.datacamp.com/blog/docker-projects) to build your GitHub portfolio ... (see github section)