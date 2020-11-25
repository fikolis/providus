# Providus

## Multi-Container Nagios application for Providus

### Installation notes

First we need to build image with following command:

```
docker build --rm -t local/nagios:latest
```
Then run Container

```
docker run --privileged --name nagios -v /sys/fs/cgroup:/sys/fs/cgroup:ro -p 8080:80 -d local/nagios:latest
```

**we should try this with debian buster slim docker image** 
