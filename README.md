# Docs

```yml
# Radarr
services:
  radarr:
    container_name: radarr
    image: ghcr.io/hotio/radarr
    ports:
      - "7878:7878"
    environment:
      - PUID=1000
      - PGID=1000
      - UMASK=002
      - TZ=Etc/UTC
    volumes:
      - /<host_folder_config>:/config
      - /<host_folder_data>:/data

# Sonarr
services:
  sonarr:
    container_name: sonarr
    image: ghcr.io/hotio/sonarr
    ports:
      - "8989:8989"
    environment:
      - PUID=1000
      - PGID=1000
      - UMASK=002
      - TZ=Etc/UTC
    volumes:
      - /<host_folder_config>:/config
      - /<host_folder_data>:/data

# Prowlarr
services:
  prowlarr:
    container_name: prowlarr
    image: ghcr.io/hotio/prowlarr
    ports:
      - "9696:9696"
    environment:
      - PUID=1000
      - PGID=1000
      - UMASK=002
      - TZ=Etc/UTC
    volumes:
      - /<host_folder_config>:/config

# Transmission
---
services:
  transmission:
    image: lscr.io/linuxserver/transmission:latest
    container_name: transmission
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - TRANSMISSION_WEB_HOME= #optional
      - USER= #optional
      - PASS= #optional
      - WHITELIST= #optional
      - PEERPORT= #optional
      - HOST_WHITELIST= #optional
    volumes:
      - /path/to/transmission/data:/config
      - /path/to/downloads:/downloads
      - /path/to/watch/folder:/watch
    ports:
      - 9091:9091
      - 51413:51413
      - 51413:51413/udp
    restart: unless-stopped
```


Token for n8n
```
21GRvokHPo7X6j4VB7rM1oYMk0vdgVQGwKu2RTyBMLeFXLvW2F5f0EjtbQXQ4GZM
```

## Mounting a SMB share in linux

First run this command to install and update all packages
```bash
sudo apt update && sudo apt upgrade
```

Then run this command to install the packages needed to install the smb share packages
```bash
sudo apt install cifs-utils psmisc
```

Then run this command to mount the chares
```bash
mount -t cifs -o username=user_name //server_name/share_name /mnt/
```

```bash
     __
    |@@@g_
    |@@ <@@g_              ~~,
    |@@   @@@@a_           @@|
    |@@   @@@@@@@_         @@|
    |@@   @@@@@@@@@@@@@@@@@@@|
    |@@   @@@@@@@@"        @@|
    |@@   @@@@@P           @@|
    |@@ _~@@P              @@|
    |@@@@P
```

<details>

<summary>Markdown Testing</summary>
Testing a table

| First Header | Second Header |
| ------------ | ------------- |
| Content Cell | Content Cell  |
| Content Cell | Content Cell  |


Here is a simple flow chart:

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

<details>

<summary>Alerts</summary>

### Alerts

> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.

</details>

<details>

<summary>Task lists</summary>

### Task Lists

- [x] #739
- [ ] https://github.com/octo-org/octo-repo/issues/740
- [ ] Add delight to the experience when all tasks are complete :tada:

</detials>


```bash

        .;;,.
        .ccccc:,.
         :cccclll:.      ..,,
          :ccccclll.   ;ooodc
           'ccll:;ll .oooodc
             .;cll.;;looo:.
                 .. ','.
                .',,,,,,'.
              .',,,,,,,,,,.
            .',,,,,,,,,,,,....
          ....''',,,,,,,'.......
        .........  ....  .........
        ..........      ..........
        ..........      ..........
        .........  ....  .........
          ........,,,,,,,'......
            ....',,,,,,,,,,,,.
               .',,,,,,,,,'.
                .',,,,,,'.
                  ..'''.
```
