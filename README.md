# Unraid Docker templates

## GitLab-CE

This template is built from the GitLab-CE Omnibus package, and should work out of the box.

### Pre-configuring the container

To setup the GitLab-CE docker container with an external URL, some extra setup is required. This section documents the additional `docker run` parameters that are needed.

First, the external URL should be set using unRAID's `Extra Parameters` field like so:

```
--hostname <my.domain.com>
```

Here's an example for configuring GitLab to use an external URL using a reverse proxy using the `GITLAB_OMNIBUS_CONFIG` environment variable field:

```
external_url '<http://my.domain.com/>'; letsencrypt['enable'] = false; nginx['listen_port'] = 80; nginx['listen_https'] = false;
```

More information about pre-configuring the GitLab Docker container can be found [here](https://docs.gitlab.com/omnibus/docker/#use-tagged-versions-of-gitlab)

## Nginx Proxy Manager

This template is based directly on the upstream [Nginx Proxy Manager](https://hub.docker.com/r/jc21/nginx-proxy-manager). Unlike some of the other templates available on unRAID, this one does not include the database. It is recommended to use MariaDB separately. By not bundling the DB, this template can pull directly from the Nginx Proxy Manager image , without needing an intermediate image for the database. This means when the Nginx Proxy Manager image is updated, those upstream updates will be detected by unRAID and will not rely on the intermediate image being updated each time.
