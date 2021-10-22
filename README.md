# docker_setup

0. install
```
sudo apt updated
sudo api install docker docker-compose
```

1. Create a file to /etc/systemd/system/docker_limit.slice
```
[Unit]
Description=Slice that limits docker resources
Before=slices.target

[Slice]
CPUAccounting=true
CPUQuota=700%
#Memory Management
MemoryAccounting=true
MemoryLimit=25G
```
2. systemctl start docker_limit.slice

3. Edit /etc/docker/daemon.json

{
  
  "cgroup-parent": "/docker_limit.slice",
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "50m",
    "max-file": "3"
  }
}

4. Restart Docker daemon: systemctl restart docker
