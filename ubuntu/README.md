# Ubuntu Dev Env Setup

## Common apps
```shell script

sudo apt install -y ansible

sudo apt install -y \
 gnome-shell-extensions gnome-tweaks \
 htop vim \
 curl wget jq \
 awscli

sudo apt-get install -y jq gettext bash-completion curl wget docker docker-compose
```

## Podman
docker is doing a bunch of cash grabs lately

seems prudent to look at alternatives

podman aims to be an api compatible drop in for docker(compose), with ability to run most stuff rootless

https://github.com/containers/podman/blob/main/docs/tutorials/rootless_tutorial.md

setup on 22.04 is pretty easy and not too for simple examples attempted:
```shell
sudo apt remove -y docker
sudo apt install -y podman podman-toolbox podman-docker docker-compose
```
for backwards compatibility search for unqualified images somewhere (legacy behavior was default to search in docker.io)

see https://src.fedoraproject.org/rpms/containers-common/raw/main/f/registries.conf

https://www.redhat.com/sysadmin/manage-container-registries
```shell
sudo tee -a /etc/containers/registries.conf > /dev/null <<EOT
unqualified-search-registries = ["registry.fedoraproject.org", "registry.access.redhat.com", "docker.io", "quay.io"]

# use local registry without tls to make dev easier
[[registry]]
location="localhost:5000"
insecure=true
EOT
```

podman-compose is a thing https://github.com/containers/podman-compose

but docker-compose works with podman as a "drop in" with little effort

enabling docker-compose with root done with:
```shell
sudo systemctl enable podman.socket
sudo systemctl start podman.socket
sudo systemctl status podman.socket

# validate it works, should return "OK"
sudo curl -H "Content-Type: application/json" --unix-socket /var/run/docker.sock http://localhost/_ping
```
this will use a socket at `/run/podman/podman.sock` which gets symlinked to the typical `/var/run/docker.sock` place 

rootless docker-compose:
```shell
systemctl --user enable podman.socket
systemctl --user start podman.socket
systemctl --user status podman.socket
export DOCKER_HOST=unix:///run/user/$UID/podman/podman.sock
echo "export DOCKER_HOST=unix:///run/user/$UID/podman/podman.sock" >> $HOME/.zprofile
```
only problem seen so far with the rootless docker-compose sometimes does not work correctly when run in the "blocking mode" (docker-compose up)

interestingly enough everything is working ok when running as daemon
```shell
docker-compose up -d; docker-compose logs -f
```

not a big deal for my scripts because this is usually how I do things in makefiles.
but it will probably break random CI stuff in the wild that is expecting exit status 0 from the docker-compose cmd
