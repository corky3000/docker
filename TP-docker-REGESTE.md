# TP/TD Docker et sécurité Docker
## Mathis REGESTE

### 1- Objectifs du TP

### 2- Pré-requis, recommandations et notation du TP

```sh
docker run -d -p 8000:8080 --restart="always" <youruser>/dillinger:${package.json.version}
```


#### 2.1- Installation de Docker et obtenir de l’aide.
##### 2.1.1 Rappel : Installation de Docker sous Linux.
Je le fais sous vbox
##### 2.1.2  Aide sur Docker.

```sh
man docker-run
man docker-create
```
### 3- Docker sous Linux.
#### 3.1  Installation de Docker sous Linux
1-
````sh
command docker version
Client: Docker Engine - Community
 Version:           19.03.5
 API version:       1.40
 Go version:        go1.12.12
 Git commit:        633a0ea838
 Built:             Wed Nov 13 07:29:52 2019
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.5
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.12.12
  Git commit:       633a0ea838
  Built:            Wed Nov 13 07:28:22 2019
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.2.10
  GitCommit:        b34a5c8af56e510852c35414db4c1f4fa6172339
 runc:
  Version:          1.0.0-rc8+dev
  GitCommit:        3e425f80a8c931f88e6d94a8c831b9d5aa481657
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
````
2-a
````sh

docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:4fe721ccc2e8dc7362278a29dc660d833570ec2682f4e4194f4ee23e415e1064
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
````
En gros le client docker contact le deamon docker qui va chercher l'image hello world depuis un repos Docker.
Le deamon à créé un container depuis cette image qui va exécuter la réponse de la commande `docker run hello-world` .

b) `https://hub.docker.com/_/hello-world`

c)

3-
````sh
docker search busybox
NAME                      DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
busybox                   Busybox base image.                             1742                [OK]
progrium/busybox                                                          71                                      [OK]
radial/busyboxplus        Full-chain, Internet enabled, busybox made f…   25                                      [OK]
arm32v7/busybox           Busybox base image.                             8
armhf/busybox             Busybox base image.                             6
yauritux/busybox-curl     Busybox with CURL                               5
odise/busybox-curl                                                        4                                       [OK]
arm64v8/busybox           Busybox base image.                             3
s390x/busybox             Busybox base image.                             2
aarch64/busybox           Busybox base image.                             2
p7ppc64/busybox           Busybox base image for ppc64.                   2
arm32v6/busybox           Busybox base image.                             2
prom/busybox              Prometheus Busybox Docker base images           2                                       [OK]
i386/busybox              Busybox base image.                             2
joeshaw/busybox-nonroot   Busybox container with non-root user nobody     2
ppc64le/busybox           Busybox base image.                             1
spotify/busybox           Spotify fork of https://hub.docker.com/_/bus…   1
arm32v5/busybox           Busybox base image.                             0
vukomir/busybox           busybox and curl                                0
concourse/busyboxplus                                                     0
sou856099/busybox                                                         0
emccorp/busybox           Busybox                                         0
trollin/busybox                                                           0
ggtools/busybox-ubuntu    Busybox ubuntu version with extra goodies       0                                       [OK]
amd64/busybox             Busybox base image.                             0

docker pull busybox
Using default tag: latest
latest: Pulling from library/busybox
322973677ef5: Pull complete
Digest: sha256:1828edd60c5efd34b2bf5dd3282ec0cc04d47b2ff9caa0b6d4f07a21d1c08084
Status: Downloaded newer image for busybox:latest
docker.io/library/busybox:latest
````

4- Création premier container
````sh
docker run -d debian
8ce4722688ee0f2a51e3a6da9e019c72e56db1982cf32cf32f87e6dec8f68a3c

````

5-

````sh
docker run -d debian
b1a12f1e4daf390dae812e763f2d98bf734d0706ec48caf8acd189c53e0328d4

docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS               NAMES



command docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
b1a12f1e4daf        debian              "bash"              3 seconds ago       Exited (0) 1 second ago                         inspiring_robinson
317f5ef2356d        hello-world         "/hello"            26 minutes ago      Exited (0) 26 minutes ago                       mystifying_boyd

````
Vu qu'on a fait un `docker run`: le container est créé et started.


6-
````sh
docker run -d debian bash -c "trap : TERM INT ; sleep infinity & wait"
f605eb34bd8f97e8f57f5f7fd0d545c81328d4f701b8b1d6d01be15bb844e73d
````


7-

````sh
docker stop f605eb34bd8f
f605eb34bd8f

docker start f605eb34bd8f
f605eb34bd8f

````

8-
````sh
docker rm f605eb34bd8f

Error response from daemon: You cannot remove a running container f605eb34bd8f97e8f57f5f7fd0d545c81328d4f701b8b1d6d01be15bb844e73d. Stop the container before attempting removal or force remove
````

9-
````sh
docker run -itd debian
````

10-
````sh
docker run -itd --name=debianOne debian
```

11-
````sh
docker attach fromage
root@d941fb6e63a2:/# exit
exit
````

12-

````sh
docker exec fromage3 bash
````

13-

````sh
docker container ls -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                        PORTS               NAMES
ebd1a6ff50af        debian              "bash"                   6 minutes ago       Up 4 minutes                                      fromage3
b456dd85e5d4        debian              "bash"                   7 minutes ago       Exited (0) 7 minutes ago                          fromage2
d941fb6e63a2        debian              "bash"                   14 minutes ago      Exited (130) 12 minutes ago                       fromage
ae129d767174        debian              "bash"                   15 minutes ago      Up 15 minutes                                     intelligent_volhard
848734421b24        debian              "-it"                    15 minutes ago      Created                                           trusting_wescoff
146c8a6997cc        debian              "bash"                   15 minutes ago      Up 15 minutes                                     nervous_blackwell
f605eb34bd8f        debian              "bash -c 'trap : TER…"   20 minutes ago      Up 17 minutes                                     clever_williams
e4ee3301b660        debian              "trap : TERM INT ; s…"   21 minutes ago      Created                                           objective_lamarr
7c72754838fc        debian              "bach -c 'trap : TER…"   21 minutes ago      Created                                           blissful_benz
b1a12f1e4daf        debian              "bash"                   24 minutes ago      Exited (0) 24 minutes ago                         inspiring_robinson
317f5ef2356d        hello-world         "/hello"                 51 minutes ago      Exited (0) 51 minutes ago                         mystifying_boyd

````

14-

````sh
docker rm fromage2
fromage2

supprimer l'images :
command docker rmi <image_id>

````

15- Delete tous les containers.

````sh
command docker rm $(docker ps -a -q)
````
Delete toutes les images.
````sh
command docker rmi $(docker images -q)
````

16- Il supprime par defaut tous les containers non used.
````sh
docker system prune -a
````
### 4  Création d’images Docker
````sh
git clone https://registry.iutbeziers.fr:5443/pouchou/tpdocker.git
````
#### 4.1  Build d’une image Docker Debian

1-

```sh
vim /tpdocker/Dockerfile/

#comment ligne 12 et 13
#RUN echo "deb http://debian.iutbeziers.fr/debian/ stretch main contrib non-free"  > /etc/apt/sources.list
#RUN echo "deb http://security.debian.org/ stretch/updates main" >> /etc/apt/sources.list


docker build -f Dockerfile -t debian:mr .

```
```sh
#Le from montre la nature du dockerfile: debian en stretch.
FROM debian:stretch
MAINTAINER jean-marc Pouchoulon


#Le ENV concerne le langage ici français.

ENV LC_ALL=fr_FR.UTF-8
ENV LANG=fr_FR.UTF-8
ENV LANGUAGE=fr_FR:fr
ENV LC_TIME=fr_FR.UTF-8
ENV LC_COLLATE=fr_FR.UTF-8


#le run permet de run des commandes

RUN echo "Europe/Paris" > /etc/timezone && \
    dpkg-reconfigure -f noninteractive tzdata && \
    sed -i -e 's/# fr_FR.UTF-8 UTF-8/fr_FR.UTF-8 UTF-8/' /etc/locale.gen && \
    echo 'LANG="fr_FR.UTF-8"'>/etc/default/locale && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=fr_FR.UTF-8

# Adding git user
RUN mkdir -p /home/git/.ssh

```
3-
AuFS (Advanced multi layered Unification FileSystem or AnotherUnionFS) est un service du système de fichiers de Linux dérivé
 de Unionfs, qui permet de fusionner plusieurs points de montage appelés « branches » : c'est un union mount.
Ca diminue la taille de l'espace.

4-
Je modifie le dockerfile en y mettant ces deux ligne et en changant le FROM:
```sh
FROM debianmr:pingfour
.
.
.
#ping
ENTRYPOINT ["/bin/ping", "-c", "4"]
CMD ["127.0.0.1"]
````
Puis je build une image grâce à ça

`docker build -f Dockerfile -t debianmr:pingfour .`

```sh
docker attach 0f9f144b6654dbb56a8c9e4a0a05dd3e9bb52d7c85ffe83f9ec75835c2200ce6
PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.017 ms
64 bytes from 127.0.0.1: icmp_seq=2 ttl=64 time=0.061 ms
64 bytes from 127.0.0.1: icmp_seq=3 ttl=64 time=0.056 ms
64 bytes from 127.0.0.1: icmp_seq=4 ttl=64 time=0.061 ms

--- 127.0.0.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3048ms
rtt min/avg/max/mdev = 0.017/0.048/0.061/0.020 ms
```
5-
 Automatically remove the container when it exits
 Pour pas qu'il y est un probleme de nommage.

```sh
docker run --rm -it debianmr:pingfour
PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.020 ms
64 bytes from 127.0.0.1: icmp_seq=2 ttl=64 time=0.060 ms
64 bytes from 127.0.0.1: icmp_seq=3 ttl=64 time=0.038 ms
64 bytes from 127.0.0.1: icmp_seq=4 ttl=64 time=0.048 ms

--- 127.0.0.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3062ms
rtt min/avg/max/mdev = 0.020/0.041/0.060/0.016 ms
```

6- Il suffit de rebuild une image et run un container utilisant cette image.

7-  On change comme ceci:
```sh
#ping
ENTRYPOINT ["/bin/ping6", "-c", "4"]
CMD ["::1"]
```

8-
```sh
docker commit 0f9f144b6654
sha256:2133d4b00a83ba0a1f99aa652a4118bd8e91aa7febd4a1f0b6b350b43da8f41b

```
9- c'est bon
https://registry.iutbeziers.fr:3000/users/edit

10-

```sh
docker commit 7da991feb8a7

docker tag debianmr:pingfour registry.iutbeziers.fr:3000/namespaces/94

docker push registry.iutbeziers.fr:3000/namespaces/94
The push refers to repository [registry.iutbeziers.fr:3000/namespaces/94]
efaf44a6b95e: Preparing
ee8cfe95e417: Preparing
2059e756da36: Preparing
872bc0df517a: Preparing
64b4f5228e3c: Preparing
9f0e1cd0ed8b: Preparing
50a7df1bdee9: Preparing
6138bcd8775a: Preparing
3b1d7b769276: Preparing
1c72d5c1b0e1: Preparing
6a1bbc157d5f: Preparing
bf2b653ec2ef: Preparing
bb43fa90e36b: Preparing
e4b20fcc48f4: Preparing

Mais ça ne fonctionne pas.

```

11-
```sh
git pull registry.iutbeziers.fr:3000/namespaces/94/containersupermegastylé

```
### 4.2  Création d’un Dockerfile afin de générer une image debian ssh


### 5-  Installation d’un "insecure registry" sur votre poste de travail


### 6- Réseaux Docker
En suivant https://docs.docker.com/registry/insecureinstallez un registry sur votre VM ettestez-le.
