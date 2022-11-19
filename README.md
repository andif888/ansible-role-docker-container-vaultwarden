# ansible-role-docker-container-vaultwarden

Role to run Vaultwarden in a docker container

## Table of content

- [Default Variables](#default-variables)
  - [docker_container_vaultwarden_env](#docker_container_vaultwarden_env)
  - [docker_container_vaultwarden_image](#docker_container_vaultwarden_image)
  - [docker_container_vaultwarden_labels](#docker_container_vaultwarden_labels)
  - [docker_container_vaultwarden_name](#docker_container_vaultwarden_name)
  - [docker_container_vaultwarden_networks](#docker_container_vaultwarden_networks)
  - [docker_container_vaultwarden_ports](#docker_container_vaultwarden_ports)
  - [docker_container_vaultwarden_restic_enable](#docker_container_vaultwarden_restic_enable)
  - [docker_container_vaultwarden_restic_retention](#docker_container_vaultwarden_restic_retention)
  - [docker_container_vaultwarden_restic_s3_bucket_name](#docker_container_vaultwarden_restic_s3_bucket_name)
  - [docker_container_vaultwarden_restic_s3_endpoint](#docker_container_vaultwarden_restic_s3_endpoint)
  - [docker_container_vaultwarden_restic_s3_repo](#docker_container_vaultwarden_restic_s3_repo)
  - [docker_container_vaultwarden_restic_s3_repo_access_key](#docker_container_vaultwarden_restic_s3_repo_access_key)
  - [docker_container_vaultwarden_restic_s3_repo_password](#docker_container_vaultwarden_restic_s3_repo_password)
  - [docker_container_vaultwarden_restic_s3_repo_secret_key](#docker_container_vaultwarden_restic_s3_repo_secret_key)
  - [docker_container_vaultwarden_restic_tag](#docker_container_vaultwarden_restic_tag)
  - [docker_container_vaultwarden_volume_dir](#docker_container_vaultwarden_volume_dir)
  - [docker_container_vaultwarden_volumes](#docker_container_vaultwarden_volumes)
  - [docker_image_vaultwarden_name](#docker_image_vaultwarden_name)
  - [docker_image_vaultwarden_pull](#docker_image_vaultwarden_pull)
  - [docker_network_vaultwarden_name](#docker_network_vaultwarden_name)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Default Variables

### docker_container_vaultwarden_env

Dictionery of key,value pairs for docker environment variables to configure vaultwarden.

#### Default value

```YAML
docker_container_vaultwarden_env:
  WEBSOCKET_ENABLED: 'true'
```

### docker_container_vaultwarden_image

Repository path and tag used to create the container. If an image is not found or pull is true, the image will be pulled from the registry. If no tag is included, latest will be used.

#### Default value

```YAML
docker_container_vaultwarden_image: '{{ docker_image_vaultwarden_name }}'
```

### docker_container_vaultwarden_labels

Dictionary of key value pairs for container labels.

Example:

```yaml

docker_container_vaultwarden_labels:

traefik.enable: "true"

```

#### Default value

```YAML
docker_container_vaultwarden_labels: {}
```

### docker_container_vaultwarden_name

Name for the container

#### Default value

```YAML
docker_container_vaultwarden_name: vaultwarden
```

### docker_container_vaultwarden_networks

List of networks the container belongs to.

#### Default value

```YAML
docker_container_vaultwarden_networks:
  - name: '{{ docker_network_vaultwarden_name }}'
```

### docker_container_vaultwarden_ports

List of ports to publish from the container to the host.

#### Default value

```YAML
docker_container_vaultwarden_ports:
  - 3012:3012
  - 80:80
```

### docker_container_vaultwarden_restic_enable

Enable restic backup for the container's mounted volumes.

#### Default value

```YAML
docker_container_vaultwarden_restic_enable: false
```

### docker_container_vaultwarden_restic_retention

Retention settions for `restic forget` after the `restic backup`.

#### Default value

```YAML
docker_container_vaultwarden_restic_retention:
  keep_last: 1
  keep_daily: 7
  keep_weekly: 4
```

### docker_container_vaultwarden_restic_s3_bucket_name

Minio S3 bucket name for restic backup storage.

#### Default value

```YAML
docker_container_vaultwarden_restic_s3_bucket_name: restic-{{ docker_container_vaultwarden_name
  }}
```

### docker_container_vaultwarden_restic_s3_endpoint

Minio S3 endpoint for restic backup storage.

Example:

```yaml

docker_container__base__restic_s3_endpoint: "https://minio.{{ dns_domain }}"

docker_container_vaultwarden_restic_s3_endpoint: "{{ docker_container__base__restic_s3_endpoint }}"

```

#### Default value

```YAML
docker_container_vaultwarden_restic_s3_endpoint: '{{ docker_container__base__restic_s3_endpoint
  }}'
```

### docker_container_vaultwarden_restic_s3_repo

Minio S3 repo URL for restic backup storage.

#### Default value

```YAML
docker_container_vaultwarden_restic_s3_repo: s3:{{ docker_container_vaultwarden_restic_s3_endpoint
  }}/{{ docker_container_vaultwarden_restic_s3_bucket_name }}
```

### docker_container_vaultwarden_restic_s3_repo_access_key

Minio S3 repo access key for restic backup storage.

#### Default value

```YAML
docker_container_vaultwarden_restic_s3_repo_access_key: '{{ docker_container__base__restic_s3_repo_access_key
  }}'
```

### docker_container_vaultwarden_restic_s3_repo_password

Minio S3 repo password for restic backup storage.

#### Default value

```YAML
docker_container_vaultwarden_restic_s3_repo_password: '{{ docker_container__base__restic_s3_repo_password
  }}'
```

### docker_container_vaultwarden_restic_s3_repo_secret_key

Minio S3 repo secret key for restic backup storage.

#### Default value

```YAML
docker_container_vaultwarden_restic_s3_repo_secret_key: '{{ docker_container__base__restic_s3_repo_secret_key
  }}'
```

### docker_container_vaultwarden_restic_tag

Tag for the `restic backup` command

#### Default value

```YAML
docker_container_vaultwarden_restic_tag: '{{ docker_container_vaultwarden_name }}'
```

### docker_container_vaultwarden_volume_dir

Volume mount host directory, where Treafik config files are stored.

#### Default value

```YAML
docker_container_vaultwarden_volume_dir: '{{ docker_container__base__volume_dir }}/{{
  docker_container_vaultwarden_name }}'
```

### docker_container_vaultwarden_volumes

List of volumes to mount within the container.

#### Default value

```YAML
docker_container_vaultwarden_volumes:
  - '{{ docker_container_vaultwarden_volume_dir }}/data:/data'
```

### docker_image_vaultwarden_name

Repository path and tag for the container image.

#### Default value

```YAML
docker_image_vaultwarden_name: vaultwarden/server:latest
```

### docker_image_vaultwarden_pull

Indicate to always pull the docker image.

#### Default value

```YAML
docker_image_vaultwarden_pull: no
```

### docker_network_vaultwarden_name

Name of the docker network created for vaultwarden.

#### Default value

```YAML
docker_network_vaultwarden_name: '{{ docker_container_vaultwarden_name }}_backend'
```

## Discovered Tags

**_docker-container-backup-all_**\
&emsp;Backup all containers' volume mounts.

**_docker-container-backup-init-all_**\
&emsp;Run init backup task for all container.

**_docker-container-backup-init-vaultwarden_**\
&emsp;Run init backup task for vaultwarden if restic is enabled.

**_docker-container-backup-list-all_**\
&emsp;List all containers' backups.

**_docker-container-backup-list-vaultwarden_**\
&emsp;List vaultwarden backups.

**_docker-container-backup-vaultwarden_**\
&emsp;Backup vaultwarden volume mounts.

**_docker-container-prereq-all_**\
&emsp;Ensure all pre-requisites are installed

**_docker-container-prereq-vaultwarden_**\
&emsp;Ensure all pre-requisites for vaultwarden are installed

**_docker-container-purge-all_**\
&emsp;Remove all containers and delete volume mounts.

**_docker-container-purge-vaultwarden_**\
&emsp;Remove vaultwarden and delete volume mounts.

**_docker-container-remove-all_**\
&emsp;Remove all containers.

**_docker-container-remove-vaultwarden_**\
&emsp;Remove vaultwarden.

**_docker-container-restore-all_**\
&emsp;Run restic restore for all restic enabled containers.

**_docker-container-restore-vaultwarden_**\
&emsp;Run restic restore for vaultwarden if restic is enabled.

**_docker-container-setup-all_**\
&emsp;Run setup task for all containers.

**_docker-container-setup-vaultwarden_**\
&emsp;Run setup task for vaultwarden.

**_never_**


## Dependencies

None.

## License

license (GPL-2.0-or-later, MIT, etc)

## Author

andif888
