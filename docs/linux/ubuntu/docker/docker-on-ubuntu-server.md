# Docker on Ubuntu Server

### Installtion

Start with a fresh Ubuntu Server install with nothing extra installed on it

Then you are going to want to create a new user. Replace ** with the user
```bash
sudo adduser rcuttriss
```

Then give the user admin permissions. Replace the ** with the user
```bash
sudo usermod -a -G sudo rcuttriss
```

Now switch to the user. Replace the ** with the user
```bash
su -l rcuttriss
```


Next start to install Docker

1. Run this command in your ubuntu server terminal

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

2. Run this command in you terminal as well

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

3. Run these commands to check the version of Docker that was installed.
```bash
docker compose version
```
```bash
docker --version
```
```bash
docker version
```

