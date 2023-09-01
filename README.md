# Ansible role: rustus

A role that installs a [rustus](https://github.com/s3rius/rustus) server.

## Requirements

No specific requirements, the role is self-contained.

## Role variables

Role variables are documented in the forms of comments on [defaults/main.yml](defaults/main.yml)

## Dependencies

None.

## Example Playbook

```yaml
- name: Install and configure rustus
  hosts: all
  vars:
    rustus_instances:
    # Runs rustus instances as systemd services
      - name: uploads
        # user that rustus will run as
        user: myuser
        # group that rustus will run as
        group: mygroup
        # By default, rustus stores the information about file uploads using the file info
        # storage. The directory where .info files are stored can be controlled using the
        # --info-dir argument, although it defaults to "./data". This means that by default,
        # rustus will refuse to run if it cannot write to its current working directory.
        # Therefore, this role forces you to provide a working directory so that rustus can
        # work even when the --info-dir argument is not provided. This working directory
        # will be automatically created if it does not exist. 
        working_directory: /data/uploads
        # arguments passed to rustus
        args:
          # see https://s3rius.github.io/rustus/configuration/
          - --host "0.0.0.0"
          - --port 1081
          - --data-dir /data/uploads
          - --hooks-http-urls "https://my-app.example.org/api/upload"
          - --hooks-http-proxy-headers "Cookie"
  roles:
    usegalaxy-eu.rustus
```

## License

See [LICENSE.md](LICENSE.md)

## Author Information

This role was created by contributors of the [Galaxy Project](https://galaxyproject.org/). Check the [contributors page](https://github.com/usegalaxy-eu/ansible-rustus/graphs/contributors) for detailed information.

## Acknowledgments

This role stems from [ansible-role-tusd](https://galaxy.ansible.com/galaxyproject/tusd).
