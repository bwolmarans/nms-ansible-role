# Ansible Playbook for NGINX Instance Manager and NGINX Agent Install

This is an example playbook that uses roles defined in this project for installing NGINX Management Suite (NMS) and NGINX+, and NGINX Agent. It also will install an NMS license, and will install API Connectivity Manager (ACM).

## Prerequisites

- Below are the required dependencies required by this role.
```shell
ansible-galaxy install nginxinc.nginx
ansible-galaxy collection install community.general
```

There are 4 roles defined in this project (located in `roles` directory):

1. install-nms <- this installs just NMS itself, on the NMS host
2. install-nginx-and-agent <- this installs Nginx (could be + or OSS, you can specify this in variables) and the Nginx agent.
3. install-nms-license <- this only installs the nms license, you need to get this from your myF5 trial
4. install-acm <- this only installs the ACM module


## Usage

1. Copy NGINX+ certs to this projects root. Or update the `nginx_license` certificate and keys paths located in `var/nginx-controller.yml` and `var/nginx-data.yml`
2. To modify NGINX Plus install/upgrade on the NMS Host, take a look at `var/nginx-controller.yml` to see variables.
3. To modify NGINX Plus install on the Data Plane Hosts, take a look at `var/nginx-data.yml` to see variables.
4. Anything related to NIM / NGINX Agent, look at variables in `var/nms.yml`. This is work in progress.
5. Update `inventory` file with your NMS Host and Data Plane Hosts. The expectation is at least one of each.
6. Then run `ansible-playbook -i inventory nms-and-agent-install-example.yml`, this does not do the license or ACM, you will do that next
7. `ansible-playbook -i inventory install-just-license.yml`
8. `ansible-playbook -i inventory install-just-acm.yml`
 
