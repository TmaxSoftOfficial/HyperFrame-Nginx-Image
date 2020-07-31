# HyperFrameOE-Nginx

This Nginx docker file is for HyperFrame Open Edition.

### Prerequisites

Docker 19.03.12 (Workspace version, recommended)

### Set up Info

1) OS : CentOS 7
2) Nginx : Nginx 1.17.X

### Directory Structure

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

### Installation Steps:

#### 1. Download Dockerfile.

#### 2. To change the configuration, modify the file under the conf directory.

#### 3. Place the Dockerfile and start.sh files and the conf, license, and ssl directories in the same path.

#### 4. Build a Docker Image.

```bash
$ docker build -t <create image_name>:<image_version> .
```

#### 5. Generate a Container from the Image.

```bash
$ docker run -p 8080:80 -p 443:443 <image_name>:<image_version>
```

### License

Projects are licensed under the BSD license.

### Version History

[HyperFrame OE, Nginx 1.17.9](https://github.com/TmaxSoftOfficial/HyperFrameOE-Nginx/blob/master/nginx_1.17/Dockerfile "dockerfile link") (latest)
