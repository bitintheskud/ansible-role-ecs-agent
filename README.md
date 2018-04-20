# Centos ECS Agent Ansible Role

This role allow configuration of ECS container agent on vanilla CentOS 7 hosts. 

## Requirements

* Ansible 2.2+
* Tested on CentOS 7.4.1708

## Role Variables

For more information see : 

http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-agent-config.html  

* `ecs_agent_loglevel`: `ECS_LOGLEVEL` (Default: info)
* `ecs_agent_cluster_name`: `ECS_CLUSTER` (Default: default)
* `ecs_agent_enable_iam_role`: `ECS_ENABLE_TASK_IAM_ROLE` (Default: true)
* `ecs_agent_enable_task_iam_role_network_host`: `ECS_ENABLE_TASK_IAM_ROLE_NETWORK_HOST` (Default: true)
* `ecs_agent_reserved_ports`: `ECS_RESERVED_PORTS` (Default: "[22, 2375, 2376, 51678]")
* `ecs_agent_container_stop_timeout`: `ECS_CONTAINER_STOP_TIMEOUT` (Default: 30s)
* `ecs_agent_auth_type`: `ECS_ENGINE_AUTH_TYPE` (Default: "")
* `ecs_agent_auth_data`: `ECS_ENGINE_AUTH_DATA` (Default: "")
* `ecs_agent_data_dir`: `ECS_DATADIR` (Default: "/data")
* `ecs_agent_log_file`: `ECS_LOGFILE` (Default: "/log/ecs_agent.log")

## Dependencies

Docker need to be installed and running. 

See :
 
* https://github.com/bitintheskud/ansible-role-docker-ce-centos.git

## Example Playbook

```yaml

---
- name: AWS ECS Agent Playbook
  hosts: all
  become: yes
  vars:
    - ecs_agent_cluster_name: MyClusterName
  roles:
    - ansible-role-ecs-agent
```

## License

Licensed under the MIT License. See the LICENSE file for details.
