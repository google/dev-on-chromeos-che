# Eclipse Che for remove ChromeOS development

## Prerequsites

Required

* A server that can run docker

Recommended

* A VPN connection to that server - see the opvnvpn image (TODO(Andrew) Add link)
* A private IP address only visible on the server

Seting up the private IP address

* Populate the IP address you want in `99-dev-server-ip.cfg`, replacing 192.168.8.8 with your chosen IP address.
* `cp 99-dev-server-ip.cfg /etc/network/interfaces.d/99-dev-server-ip.cfg`

## Starting

Run

```sh
docker-compose run che start
```

## Docker development in che

If you want to give your che workspaces the ability to run docker commands (say,
for instance that you're developing docker images) then add edit
`chedata/instance/config/che.properties`, by replacing

```
che.docker.privileged=false
```

with

```
che.docker.privileged=true
machine.docker.privilege_mode=true
che.workspace.volume=/var/run/docker.sock:/var/run/docker.sock
```

The run

```sh
docker-compose run che restart
```

## Upgrading to the newest version of Che

Edit docker-compose.yml to pick the version of Che you wish (alternatively you
can just remove the version number and always use the latest).

Then run

```sh
docker pull eclipse/che
docker-compose run che upgrade
```
