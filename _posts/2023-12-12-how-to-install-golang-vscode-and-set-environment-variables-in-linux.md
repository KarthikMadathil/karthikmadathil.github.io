---
layout: post
title:  "How to install Golang, VSCode and set environment variables in Linux"
author: karthik
featured: false
date:   2023-12-12 19:53:52 +0530
categories: [ GO, DevEnvironment, GOlang, Vscode  , Coding]
image: assets/images/golang-installation.png
comments: false
---  
# **Setup the Programming Environment on Linux (Go and VSCode)**

#### **Step 1: Installing Go on Linux (root permissions required)**

Grab the latest version from the official Go downloads page:  [https://golang.org/dl/](https://golang.org/dl/)

On the website, you can find the URL for the latest binary release’s tarball, along with its SHA256 hash.

 

Open a terminal and move to your home directory or a directory with write access:

**_cd ~_**

Download the latest version of Go:

**_curl -O https://golang.org/dl/go1.17.1.linux-amd64.tar.gz_**

Next, extract the downloaded archive. It’s considered best practice to keep it under  _/usr/local_:

**_sudo tar -xzvf go1.13.3.linux-amd64.tar.gz -C /usr/local_**

You will now have a directory called  **_go_**  in the  **/usr/local**  directory. Next, recursively change this directory’s owner and group to root:

**_sudo chown -R root:root /usr/local/go_**

**Congratulations**! You have installed Go on your system.

 

Alternatively, on Ubuntu 16.04+ you can install Go automatically from a repository.

In a terminal run the following commands:

**_sudo apt-get update_**

**_sudo apt-get install golang-go_**

 

If you are using a version of Ubuntu later than 16.04 and want to install the latest Go release you can use the  _longsleep/golang-backports_  PPA.

 

In a terminal run the following commands:

**_sudo add-apt-repository ppa:longsleep/golang-backports_**

**_sudo apt-get update_**

**_sudo apt-get install golang-go_**

 

#### **Step 2 — Creating Your Go Workspace**

The Go workspace will contain three directories at its root:

 

-   **pkg:** The directory contains  **Go package objects**  compiled from Go source code, which are then used, at link time, to create the complete Go executable binary in the bin directory.
   
-   **bin**: The directory that contains executables built and installed by the Go tools.
   
-   **src**: The directory that contains Go source files. You’ll have a subdirectory of src for each Go application.
   

 

The default directory for the Go workspace as of 1.17 is your user’s home directory with a **go**  subdirectory, or **$HOME/go**, where $HOME is a variable that stores your home directory such as /home/john.

 

Run the following command to create the directory structure for your Go workspace:

**_mkdir -p $HOME/go/{bin,src}_**

 

Set  **$PATH**  and  **$GOPATH**  by adding the following lines to **~/.profile**

 

Open  **~/.profile** in your preferred editor  and add:

 

**_export GOPATH=$HOME/go_**

**export PATH=$PATH:$GOPATH/bin:/usr/local/go/bin**

 

To update your shell, run the following command to load the global variables:

**source ~/.profile**

 

Now, check the installed Go version.

In a terminal run:  **_go version_**

 

And you should receive an output similar to this one:  **_go version go1.17.1 linux/amd64_**

 

Now that you have the root of the workspace created and your $GOPATH environment variable set, you can create your future projects with the following directory structure.

 

**mkdir $GOPATH/src/master_go_programming**

 

Each Go program will reside in its own directory in  **$GOPATH/src/master_go_programming**

 

#### **Step 3 — Creating a Simple Program. Test the Installation.**

Create a directory called **hello_world** in  **$GOPATH/src/master_go_programming**

And inside that directory a file called **main.go**

Write your sample program in  **main.go**:

 

**_package main_**

**_import "fmt"_**

**_func main() {_**

**_fmt.Println("Hello Go World!")_**

**_}_**

 

Move to the same directory with  _main.go_  and run: **go run main.go**

You should see an output like this:  **Hello Go World!**

 

**Installing Go on Mobile Devices**

If you want to learn Go on your mobile phone just visit The Go Playground and write your code there:  [https://play.golang.org](https://play.golang.org/)
