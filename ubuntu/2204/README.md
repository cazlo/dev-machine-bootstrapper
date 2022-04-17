# ntfs3

put this in `/etc/udisks2/mount_options.conf`:
```shell
[defaults]
ntfs_defaults=uid=$UID,gid=$GID,noatime,prealloc
```

see https://wiki.archlinux.org/title/NTFS#udisks_support