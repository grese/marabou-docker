# Marabou Docker Image ![Build & Push Docker Image](https://github.com/grese/marabou-docker/workflows/Build%20&%20Push%20Docker%20Image/badge.svg)

The [marabou docker image](https://hub.docker.com/r/grese/marabou) is an ubuntu-based docker image with the [Marabou Neural Network Verification Framework](https://github.com/NeuralNetworkVerification/Marabou.git) pre-installed. It also contains a few convenience features and dependencies useful for neural network verification.

## Features

* Runs Ubuntu 18.04 (bionic)
* Based on [jupyter/tensorflow-notebook](https://hub.docker.com/r/jupyter/tensorflow-notebook)
* [Jupyter Lab](https://jupyter.org), Python3, Numpy, Tensorflow, Pandas, and other useful pip packages
* Marabou & Marabou Python APIs installed
* Standord's [NNet format tools](https://github.com/sisl/NNet) installed
* ZShell is default shell
* A few other helpers and convenience features.

## Usage

### Prerequisites

You'll need [docker](https://www.docker.com/products/docker-desktop) installed, so just install that first if you don't have it.

### Get the image

**%** `docker pull grese/marabou`

### Ways to Run Image

The image supports all of the normal docker command line options. Below are a few examples of ways to run the image. Choose the best one for your use-case. For detailed instructions on options and environment variables for the docker image, visit [Jupyter Docker Stacks](https://jupyter-docker-stacks.readthedocs.io/en/latest/).

#### Run the JupyterLab browser app

**%** `docker run -p 9999:9999 grese/marabou`

Once it is running, visit https://localhost:9999?token=TOKEN in your browser (TOKEN will be printed in the console when server starts)

#### Run with a shared folder from your local machine (-v option)

**%** `docker run -p 9999:9999 -v "$PWD":/home/marabou/work grese/marabou`

#### Run container command line

**%** `docker run -p 9999:9999 -it grese/marabou /bin/zsh`

#### Run as daemon

**%** `docker run -d -p 9999:9999 grese/marabou`

#### Run as daemon with mounted volume

**%** `docker run -d -p 9999:9999 -v "$PWD:/home/grese/marabou" grese/marabou`

### Managing, killing, and removing containers

Kill a running container

**%** `docker kill $(docker ps -q --filter ancestor=grese/marabou)`

Remove a container from disk

**%** `docker rm $(docker ps -aq --filter ancestor=grese/marabou)`

### Environment Variables

Environment variables are available to help you do things like specify the SSL cert, password, and token. A few of the relevant environment variables are listed below. Visit [Jupyter Docker Stacks Notebook Options](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/common.html#notebook-options) for additional environment variables and options.

* `SERVER_TOKEN` - specifies the URL token
* `SERVER_CERTFILE` - specifies path to the SSL cert
* `SERVER_KEYFILE` - specifies path to file containing web app's password

The example below shows how these command line options can be passed to the image.

`docker run -d -p 9999:9999 -e SERVER_TOKEN=/path/to/token -e SERVER_CERTFILE=/path/to/cert -e SERVER_KEYFILE=/path/to/keyfile grese/marabou`

### Using Marabou

Marabou has been pre-installed in `~/.bin/marabou` along with all of the source code. Below are a couple of examples of how Marabou can be used within the container.

#### Run Marabou Binary

A ZSH command has been added for Marabou, so you can just run `marabou` from the command line. See examples below.

**%** `marabou --help`

**%** `marabou --input=NNET_FILE --property=PROPERTY_FILE`

### Using Marabou's Python APIs

You can just directly import and use the Marabou Python APIs as you would any other Python module. Below is a quick example using Python's interactive shell.

**%** `python`

```python
> from maraboupy import Marabou
> nnet = Marabou.read_nnet('path/to/nnet_file')
```
