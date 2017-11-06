# docker-systemd
This role creates systemd unit files for Docker containers.

## Requirements
The target host needs to be running systemd and needs to have Docker installed.

## Role Variables

### Required Variables
* `name` *string* - the name for the container. This is used in a number of
  places, including the container name, the service file name, and the
  description.
* `ìmage` *string* - the image to run.

### Optional Variables
* `description` *string* - the unit description; some tools display this as a
  friendly name for the unit.
* `pull_image` *boolean* - if true, pull the image before starting the
  service. Defaults to true.
* `recreate_container` *boolean* - if true, the container is deleted when the
  service is stopped and recreated when it is restarted. Defaults to true.
* `cmd` *string* - the command to pass to `docker run`. Defaults to an empty
  string, meaning the default command specified in the image is used.
* `service_name` *string* - the full name of the service file, including the
  extension.
* `ports` *list of strings* - a list of Docker port specifications.
* `volumes` *list of strings* - a list of Docker volume specifications.
* `extra_options` *list of strings* - a list of additional command-line options
  that are passed as-is to `docker run`.
* `env` *list of strings* - a list of `name=value` strings specifying additional
  environment variables to set for the container.
* `link` *list of strings* - a list of container names to link using the
  `--link` flag to `docker run`.
* `autostart` *boolean* - if true, the created service is enabled and started.

## Example
This playbook snippet creates a service file to run Portainer:

    - role: docker-systemd
      name: portainer
      description: Portainer - Docker management UI
      image: portainer/portainer:latest
      ports:
        - 9000:9000
      volumes:
        - portainer-data:/data
        - /var/run/docker.sock:/var/run/docker.sock

## License
This software is licensed under the 2-clause BSD license. See the accompanying
`LICENSE.md` file.
Copyright (c) 2017, Felix Krull. All rights reserved.
