# HyperFrameOE-Nginx-Image

This Nginx docker file is for HyperFrame Open Edition.

## Prerequisites

Docker 19.03.12 (Workspace version, recommended)

## Requirements

#### 1) OS : CentOS 7
#### 2) Nginx : Nginx 1.17.x

## Directory Structure

```bash
${pwd}
|- nginx_1.17
|   |- Dockerfile_list               # Dockerfile list directory
|   |   |-<dockerfile_version> ...       # Dockerfile version
|   |   |   |- Dockerfile
|   |- conf                          # Configuration directory
|   |   |- nginx.conf                    # Main configuration file
|   |- license                       # license directory
|   |   |- LICENSE                       # Nginx license
|   |- ssl                           # ssl directory
|   |   |- server.crt                    # Self-signed sample certificate
|   |   |- server.key                    # Private sample key for SSL certificate
|   |   |- ssl_passwd                    # Script for setting passwords for sample SSL keys
|   |- CHANGES
|   |- [latest]Dockerfile
|   |- start.sh
-- README.md
```

## Installation Steps:

### You can choose one of the following two installation methods.

### Method 1. Using Dockerfile and binary downloaded from GitHub

#### 1. Go to the following site: https://github.com/TmaxSoftOfficial/HyperFrameOE-Nginx-Image.

#### 2. Download the Dockerfile and binary.

#### 3. To change the configuration, modify files under the conf directory.

#### 4. Place the Dockerfile and start.sh files and the conf, license, and ssl directories in the same path.

#### 5. Build a Docker Image.
```bash
$ docker build -t <create image_name>:<image_version> .
```

#### 6. Generate a Container from the Image.
```bash
$ docker run -d -p 8080:80 -p 443:443 <image_name>:<image_version>
```

### Method 2. Using Image of Docker Hub

#### 1. Search for the Image.
- It can be searched from Docker Hub (https://hub.docker.com/repository/docker/tmaxsoftofficial/hyperframeoe-nginx) or with the following docker search command.
```bash 
$ docker search hyperframeoe-nginx
```

#### 2. Pull the Image.
```bash
$ docker pull tmaxsoftofficial/hyperframeoe-nginx:latest
```

#### 3. Build a Docker Image.
```bash
$ docker build -t tmaxsoftofficial/hyperframeoe-nginx:latest .
```

#### 4. Generate a Container from the Image.
```bash
$ docker run -d -p 8080:80 -p 443:443 tmaxsoftofficial/hyperframeoe-nginx:latest
```

## License

Projects are licensed under the BSD license. See the [License](https://github.com/TmaxSoftOfficial/HyperFrameOE-Nginx/blob/master/nginx_1.17/license/LICENSE) file.

## Version History

[HyperFrame OE, Nginx 1.17.9](https://github.com/TmaxSoftOfficial/HyperFrameOE-Nginx/blob/master/nginx_1.17/Dockerfile "dockerfile link") (latest)

## HyperFrameOE Service Level
[HyperFrameOE Service Level](https://github.com/TmaxSoftOfficial/HyperFrameOE-About/blob/master/ServiceLevel.md)
