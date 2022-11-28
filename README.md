TeamCity on Kubernetes Ansible Role
===============================
This role will deploy this TeamCity helm chart (https://github.com/codaglobal/teamcity_helm) onto a k8s cluster (tested only in microk8s, due to specific storage class)

Requirements
------------
A functioning nicrok8s installation. You can use the following role to boot up such a cluster:
https://github.com/capitanh/microk8s_ansible_role

Role Variables
--------------
Tne variables required by this role are:
```yaml
teamcity_app_name:      teamcity    # Helm chart release name
teamcity_namespace:     teamcity    # K8S namespace
teamcity_port:          8111        # Server port
teamcity_service_port:  30002       # Service port to access from outside

# Storage
storage:
  data:                             # TeamCity Data storage
    size: 500Mi
    path: /opt/teamcity/datadir
  config:                           # TeamCity Config storage
    size: 5Mi
    path: /opt/teamcity/config
  logs:                             # TeamCity Logs storage
    size: 500Mi
    path: /opt/teamcity/logs

```

Dependencies
------------
* pip

Example Playbook
----------------
Register the role in requirements.yml:
```yaml
    - src: capitanh.teamcity_ansible_role
      name: teamcity
```
Include it in your playbooks:
```yaml
    - hosts: servers
      roles:
      - teamcity
```

License
-------
BSD
