# Dockerized nexus3 repository

## Usage
  - Configure variable in .env. See .env.example for template.

  - Run with docker-compose
    ```
    $ docker-compose up -d
    ```
## Configuration
### Configure repositories
  - Docker
    https://blog.sonatype.com/using-nexus-3-as-your-repository-part-3-docker-images
    https://guides.sonatype.com/repo3/technical-guides/secure-docker-registries/
  - Npm
    https://blog.sonatype.com/using-nexus-3-as-your-repository-part-2-npm-packages or https://help.sonatype.com/repomanager3/formats/npm-registry
###  Backups
https://help.sonatype.com/repomanager3/backup-and-restore

### Manual static asset upload
```
for i in *.tar.gz; do echo $i; curl -L -v --user USER:${USER_PWD} --upload-file $i https://nexus3.linkurious.net/repository/static-assets/com/linkurious/documentation/ogma/$i; done;
```

## Scaleway block storage
### Increase block storage size
https://www.scaleway.com/en/docs/storage/block/how-to/increase-block-volume/

For backups:
```
umount /backup
e2fsck -f /dev/sdb
resize2fs /dev/sdb
e2fsck  /dev/sdb
mount -a
```

confirm with `df- h`

For main data folder:
```
docker stop nexus3
umount /data
e2fsck -f /dev/sda
resize2fs /dev/sda
e2fsck  /dev/sda
mount -a
```
confirm with `df- h` and `docker restart nexus3`
