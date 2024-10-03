# TrueCommand

Installation
Installing/Starting the image
To fetch/use these images, run the following:
```bash
docker pull ixsystems/truecommand
docker run --detach -v "[hostdirectory]:/data" -p [portnumber]:80 -p [sslportnumber]:443 ixsystems/truecommand
```
Where the “[hostdirectory]” should point to some persistent directory on the host to use as the long-lived data directory for the container.
Checking the status of the running containers
This will also return which port numbers on the local host get redirected to the TrueCommand container
```bash
docker ps
```

Stopping the container
```bash
docker stop [container ID]
```
Other resources

TrueCommand on Docker Hub


The username and password for the VM images are both “truecommand”

```
https://hooks.slack.com/services/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
```