[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: http://deluge-torrent.org/
[hub]: https://hub.docker.com/r/lsioarmhf/deluge-aarch64/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/deluge-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/deluge-aarch64.svg)](https://microbadger.com/images/lsioarmhf/deluge-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/deluge-aarch64.svg)](http://microbadger.com/images/lsioarmhf/deluge-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/deluge-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/deluge-aarch64.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-arm64/lsioarm64-deluge)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-arm64/job/lsioarm64-deluge/)

[deluge](http://deluge-torrent.org/) Deluge is a lightweight, Free Software, cross-platform BitTorrent client.

* Full Encryption
* WebUI
* Plugin System
* Much more...

[![deluge](https://avatars2.githubusercontent.com/u/6733935?v=3&s=200)][appurl]

## Usage

```
docker create \
  --name deluge \
  --net=host \
  -e PUID=<UID> -e PGID=<GID> \
  -e TZ=<timezone> \
  -e UMASK_SET=<022> \
  -v </path/to/your/downloads>:/downloads \
  -v </path/to/deluge/config>:/config \
  lsioarmhf/deluge-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `--net=host` - Shares host networking with container, **required**.
* `-v /config` - deluge configs
* `-v /downloads` - torrent download directory
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e UMASK_SET` for umask setting of deluge, *optional* , default if left unset is 022. 
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it deluge /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application 
`IMPORTANT... THIS IS THE ARM64 VERSION`

The admin interface is available at http://<ip>:8112 with a default user/password of admin/deluge.

To change the password (recommended) log in to the web interface and go to Preferences->Interface->Password.

Change the downloads location in the webui in Preferences->Downloads and use /downloads for completed downloads.

## Info

* Monitor the logs of the container in realtime `docker logs -f deluge`.

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' deluge`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/deluge-aarch64`

## Versions

+ **27.05.17:** Rebase to alpine 3.6. 
+ **29.04.17:** Initial Release. 
