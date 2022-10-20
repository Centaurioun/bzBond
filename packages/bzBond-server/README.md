# fmbond-server

# Introduction

fmbond-server is a microservice that runs on your FileMaker server and allows you to run JavaScript code. It is intended to be accessed through the FMBond relay script in the mode `PERFORM_JAVASCRIPT` only when the script is running on the server.

# Installation

These installations assume a default installation of FileMaker Server on the specified platform

## Ubuntu Linux Installation

### Add files

1. Unzip the application files to `/usr/bin/fmbond-server`
1. Ensure `root` is the owner and group for the directory and its contents
1. Ensure the permissions are rwxr-xr-x for the directory and its contents (755)

### Setup management with systemd<sup>1</sup>

1. Create the following file in `/lib/systemd/system/fmbond-server.service`
```
[Unit]
Description=fmbond-server – JavaScript microservice for FileMaker Server
Documentation=https://github.com/beezwax/fmbond-server
After=network.target

[Service]
Type=simple
User=fmserver
ExecStart="/opt/FileMaker/FileMaker Server/node/bin/node" /usr/bin/fmbond-server/server.js
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
2. Run the command `sudo systemctl daemon-reload` to refresh systemd
3. Launch fmbond-server with the command `sudo systemctl start fmbond-server`
4. Test the fmbond-server is running with the command `curl http://localhost:8999` this should output `{"message":"Route GET:/ not found","error":"Not Found","statusCode":404}`
5. Check the status of fmbond-server with the command `sudo systemctl status fmbond-server`
6. Ensure fmbond-server starts with the system with the command `sudo systemctl enable fmbond-server`


1: [https://nodesource.com/blog/running-your-node-js-app-with-systemd-part-1/](https://nodesource.com/blog/running-your-node-js-app-with-systemd-part-1/)

## macOs Installation

## Windows Server Installation