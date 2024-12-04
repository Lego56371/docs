# Docs

```yml
# sonarr
Sonarr:
    image: ghcr.io/hotio/sonarr
    volumes:
        - /path/to/config/sonarr:/config
        - /host/data:/data
    environment:
        - PUID=111
        - PGID=321
        - UMASK=002

# deluge
Deluge:
    image: binhex/arch-delugevpn
    volumes:
        - /path/to/config/deluge:/config
        - /host/data/torrents:/data/torrents
    environment:
        - PUID=222
        - PGID=321
        - UMASK=002

# SABnzbd
SABnzbd:
    image: ghcr.io/hotio/sabnzbd
    volumes:
        - /path/to/config/sabnzbd:/config
        - /host/data/usenet:/data/usenet
    environment:
        - PUID=333
        - PGID=321
        - UMASK=002

# plex
Plex:
    image: ghcr.io/hotio/plex
    volumes:
        - /path/to/config/plex:/config
        - /host/data/media:/data/media

    environment:
        - PUID=444
        - PGID=321
        - UMASK=002
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
