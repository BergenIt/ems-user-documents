# Создание бекапов и восстановление EMS

Для создания бекапа из файловой системы ОС необходимо создать бекап директоктории `/opt/config` и бекап вольюмов докера на всех нодах.

На ноде мастер это вольюмы:

* `ems_kv`
* `ems_opensearch`
* `ems_psql`

На ноде транспорт это вольюмы:

* `ems_minio`
* `ems_leaf-nats`

Ниже представлен пример процессов создания и восстановления системы из бекапов с помощью утилиты `tar` и `docker exec`.

Также вольюмы могут быть сохранены и восстановлены с помощью `fs` ОС и утилиты `tar`, без использования `docker exec`.

Для этого используя команду `docker volume inspect VOLUME_NAME`, где `VOLUME_NAME` - имя вольюма, найдите директорию в которую монтируется вольюм и сделайте бекап из нее.

Рекомендуется создавать бекапы на остановленной системе, восстанавливать бекапы необходимо на остановленной системе, с чистыми вольюмами.

## backup

Команды для создания бекапов на master-node, с помощью утилиты `tar` и `docker exec`:

```bash
tar -zcvf $(pwd)/ems-backup/ems-config.tar.gz /opt/ems
docker run --rm \
    -v ems_kv:/backup-volume \
    -v "$(pwd)/ems-backup":/backup alpine tar \
    -zcvf /backup/ems_kv.tar.gz /backup-volume
docker run --rm \
    -v ems_psql:/backup-volume \
    -v "$(pwd)/ems-backup":/backup alpine tar \
    -zcvf /backup/ems_psql.tar.gz /backup-volume
docker run --rm \
    -v ems_opensearch:/backup-volume \
    -v "$(pwd)/ems-backup":/backup alpine tar \
    -zcvf /backup/ems_opensearch.tar.gz /backup-volume
```

Команды для создания бекапов на transport-node, с помощью утилиты `tar` и `docker exec`:

```bash
tar -zcvf $(pwd)/ems-backup/ems-config.tar.gz /opt/ems
docker run --rm \
    -v ems_minio:/backup-volume \
    -v "$(pwd)/ems-backup":/backup alpine tar \
    -zcvf /backup/ems_minio.tar.gz /backup-volume
docker run --rm \
    -v ems_leaf-nats:/backup-volume \
    -v "$(pwd)/ems-backup":/backup alpine tar \
    -zcvf /backup/ems_leaf-nats.tar.gz /backup-volume
```

Команды для создания бекапов на tool-node, с помощью утилиты `tar` и `docker exec`:

```bash
tar -zcvf $(pwd)/ems-backup/ems-config.tar.gz /opt/ems
```

## restore

Команды для восстановления системы из бекапов на transport-node, с помощью утилиты `tar` и `docker exec`:

```bash
mkdir -p /opt/ems
tar zxvf $(pwd)/ems-backup/ems-config.tar.gz --directory /opt/ems
docker run --rm \
    -v ems_leaf-nats:/restored-data \
    -v "$(pwd)/ems-backup/ems_leaf-nats.tar.gz:/backup.tar.gz" alpine \
    sh -c "tar zxvf /backup.tar.gz && mv -rf backup-volume/* /restored-data/"
docker run --rm \
    -v ems_minio:/restored-data \
    -v "$(pwd)/ems-backup/ems_minio.tar.gz:/backup.tar.gz" alpine \
    sh -c "tar zxvf /backup.tar.gz && mv -rf backup-volume/* /restored-data/"
```

Команды для восстановления системы из бекапов на master-node, с помощью утилиты `tar` и `docker exec`:

```bash
mkdir -p /opt/ems
tar zxvf $(pwd)/ems-backup/ems-config.tar.gz --directory /opt/ems
docker run --rm \
    -v ems_kv:/restored-data \
    -v "$(pwd)/ems-backup/ems_kv.tar.gz:/backup.tar.gz" alpine \
    sh -c "tar zxvf /backup.tar.gz && mv -rf backup-volume/* /restored-data/"
docker run --rm \
    -v ems_psql:/restored-data \
    -v "$(pwd)/ems-backup/ems_psql.tar.gz:/backup.tar.gz" alpine \
    sh -c "tar zxvf /backup.tar.gz && mv -rf backup-volume/* /restored-data/"
docker run --rm \
    -v ems_opensearch:/restored-data \
    -v "$(pwd)/ems-backup/ems_opensearch.tar.gz:/backup.tar.gz" alpine \
    sh -c "tar zxvf /backup.tar.gz && mv -f backup-volume/* /restored-data/"
```

Команды для восстановления системы из бекапов на tool-node, с помощью утилиты `tar` и `docker exec`:

```bash
mkdir -p /opt/ems
tar zxvf $(pwd)/ems-backup/ems-config.tar.gz --directory /opt/ems
```
