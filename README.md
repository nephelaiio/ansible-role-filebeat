# nephelaiio.filebeat

[![Build Status](https://github.com/nephelaiio/ansible-role-filebeat/workflows/molecule.yml/badge.svg)](https://github.com/nephelaiio/ansible-role-filebeat/actions/workflows/molecule.yml)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-nephelaiio.filebeat-blue.svg)](https://galaxy.ansible.com/nephelaiio/filebeat/)

An [ansible role](https://galaxy.ansible.com/nephelaiio/filebeat) to install and configure filebeat

## Role Variables

Please refer to the [defaults file](/defaults/main.yml) for an up to date list of input parameters.

## Dependencies

- [nephelaiio.elastic_repo](https://galaxy.ansible.com/nephelaiio/elastic_repo/)

Please review the [dependency configuration](/meta/main.yml) for more details

## Example Playbook

```
- name: Deploy filebeat
  hosts: servers
  vars:
    filebeat_package_state: latest
    filebeat_conf_manage: true
    filebeat_conf:
      fields:
        environment: development
      inputs:
        - type: log
          paths:
            - /var/log/system.log
            - /var/log/wifi.log
        - type: log
          paths:
            - "/var/log/nginx/*.log"
          fields:
            application: nginx
      output:
        elasticsearch:
          enabled: true
          hosts:
            - http://localhost:9200
      setup:
        dashboards:
          enabled: true
          beat: filebeat
          always_kibana: true
        template:
          enabled: true
        kibana:
          host: http://localhost:80
  roles:
     - role: nephelaiio.filebeat
```

## Testing

Please make sure your environment has [docker](https://www.docker.com) installed in order to run role validation tests. Additional python dependencies are listed in the [requirements file](https://github.com/nephelaiio/ansible-role-requirements/blob/master/requirements.txt)

Role is tested against the following distributions (docker images):

- Ubuntu Nobl3
- Ubuntu Jammy
- Ubuntu Focal
- Debian Trixie
- Debian Bookworm
- Rocky Linux 9

You can test the role directly from sources using command `molecule test`

## License

This project is licensed under the terms of the [MIT License](/LICENSE)
