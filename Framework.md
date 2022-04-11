# Framework Fedora Setup

## General setup resources
https://github.com/lightrush/framework-laptop-formula

https://community.frame.work/c/framework-laptop/linux/91

https://community.frame.work/t/ubuntu-20-04-4-lts-on-the-framework-laptop/5702

https://community.frame.work/t/ubuntu-22-04-on-the-framework-laptop/14238/10

https://community.frame.work/t/ubuntu-21-10-on-the-framework-laptop/7941

https://luisartola.com/solving-the-framework-laptop-battery-drain/



## Fingerprint reset when switching between OS

https://community.frame.work/t/fingerprint-scanner-compatibility-with-linux-ubuntu-fedora-etc/1501/88  

https://gitlab.freedesktop.org/libfprint/libfprint/-/issues/415#note_1063158  

```shell
 sudo apt install gir1.2-fprint-2.0 
 ./unenroll-fingerprints.sh
```
update pam auth to enable fingerprint for sudo
```shell
sudo pam-auth-update
```

https://community.frame.work/t/fedora-linux-35-fedora-35-on-the-framework-laptop/6613

## Power optimizations

### base
```shell
sudo apt install powertop 
```

### gpu accelerated video
```shell
sudo apt install intel-gpu-tools intel-media-va-driver

rm -f ~/.config/chrome-flags.conf
cat <<EOT >> ~/.config/chrome-flags.conf
--enable-features=VaapiVideoDecoder
--use-gl=egl
--ignore-gpu-blocklist
--enable-gpu-rasterization
--enable-zero-copy
--disable-gpu-driver-bug-workarounds
--ozone-platform=wayland
--force-device-scale-factor=1
EOT

```