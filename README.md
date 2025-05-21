# Docs

## Monitoring VMware with Grafana

```yaml
version: "3"
services:
  grafana:
    image: grafana/grafana
    container_name: grafana_container
    restart: always
    ports:
      - 3000:3000
    networks:
      - monitoring_network
    volumes:
      - grafana-volume:/var/lib/grafana

  influxdb:
    image: influxdb
    container_name: influxdb_container
    restart: always
    ports:
      - 8086:8086
      - 8089:8089/udp
    networks:
      - monitoring_network
    volumes:
      - influxdb-volume:/var/lib/influxdb

  telegraf:
    image: telegraf
    container_name: telegraf_container
    restart: always
    networks:
      - monitoring_network
    volumes:
      - ./telegraf/telegraf.conf:/etc/telegraf/telegraf.conf:ro

networks:
  monitoring_network:
    external: true

volumes:
  grafana-volume:
    external: true
  influxdb-volume:
    external: true
```



<details>

<summary>Full Storage</summary>

289

Had the exact same problem with a fresh install of Ubuntu Server 18.04.1.

What I had to do was:

# We need to resize the logical volume to use all the existing and free space of the volume group
```bash
lvm
```
```bash
lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
```
```bash
exit
```

# And then, we need to resize the file system to use the new available space in the logical volume
resize2fs /dev/ubuntu-vg/ubuntu-lv
resize2fs 1.44.1 (24-Mar-2018)
Filesystem at /dev/ubuntu-vg/ubuntu-lv is mounted on /; on-line resizing required
old_desc_blocks = 1, new_desc_blocks = 58
The filesystem on /dev/ubuntu-vg/ubuntu-lv is now 120784896 (4k) blocks long.

# Finally, you can check that you now have available space:
$ df -h
Filesystem                         Size  Used Avail Use% Mounted on
udev                               3.9G     0  3.9G   0% /dev
tmpfs                              786M  1.2M  785M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  454G  3.8G  432G   1% /
If you didn't customize the LVM settings, the names for the volume group and logical volume should be the same as mine (ubuntu-vg and ubuntu-lv respectively).

If your partition is completely full, you could get a no space left error when trying to resize the logical volume like:

lvm> lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
  /etc/lvm/archive/.lvm_computer: write error failed: No space left on device
The easiest way to fix this is by removing apt cache (it will get regenerated next time you do apt update), which should give you more than enough space to complete the operation:

$ rm -rf /var/cache/apt/*

</details>

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
