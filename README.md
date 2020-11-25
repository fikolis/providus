# Providus

Multi-Container app for Providus

First build image with

`docker build --rm -t local/nagios:latest`

Then run Container

`docker run --privileged --name nagios -v /sys/fs/cgroup:/sys/fs/cgroup:ro -p 8080:80 -d local/nagios:latest`