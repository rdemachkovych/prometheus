<p><img src="https://cdn.worldvectorlogo.com/logos/prometheus.svg" alt="prometheus logo" title="prometheus" align="right" height="60" /></p>

Ansible Role: prometheus
========================

[![Build Status](https://ci.devops.sosoftware.pl/buildStatus/icon?job=SoInteractive/prometheus/master)](https://ci.devops.sosoftware.pl/blue/organizations/jenkins/SoInteractive%2Fprometheus/activity) [![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT) [![Ansible Role](https://img.shields.io/ansible/role/18272.svg)](https://galaxy.ansible.com/SoInteractive/prometheus/) [![Twitter URL](https://img.shields.io/twitter/follow/sointeractive.svg?style=social&label=Follow%20%40SoInteractive)](https://twitter.com/sointeractive)

Deploy Prometheus monitoring system

More info
---------

An Ansible role that installs Prometheus Monitoring server.

Requirements
------------

None

Role Variables
--------------

Have a look at the [defaults/main.yml](defaults/main.yml) for variables that can be overridden.

Example usage
-------------

```yaml
---
- hosts: all
  gather_facts: yes

- hosts: all
  become: yes
  become_user: root
  roles:
  - role:
      - SoInteractive.prometheus
  vars:
    prometheus_external_labels:
      monitoring: a
    prometheus_tgroup:
      - port: 9100
        labels:
          env: {{ system_domain }}
          job: node
        targets_group: all 
```

Defining alerting rules files
-----------------------------

Put the rules files to rules folder

Alerting rules are defined in the following syntax:
```yaml
ALERT <alert name>
  IF <expression>
  [ FOR <duration> ]
  [ LABELS <label set> ]
  [ ANNOTATIONS <label set> ]
```
Example Alertmanager rules files:
```yaml
# Alert for any instance that is unreachable for >5 minutes.
ALERT InstanceDown
  IF up == 0
  FOR 5m
  LABELS { severity = "page" }
  ANNOTATIONS {
    summary = "Instance {{ $labels.instance }} down",
    description = "{{ $labels.instance }} of job {{ $labels.job }} has been down for more than 5 minutes.",
  }
```
