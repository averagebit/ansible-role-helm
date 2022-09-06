# Helm (Ansible Role)

[![CI](https://github.com/averagebit/ansible-role-helm/workflows/CI/badge.svg?branch=main&event=push)](https://github.com/averagebit/ansible-role-helm/actions?query=workflow%3ACI)

## Description

Ansible role to install [Helm](https://helm.sh/).

## Requirements

The role was developed and tested with the following Ansible versions.

| Name                                                   | Version     |
| ------------------------------------------------------ | ----------- |
| [ansible](https://pypi.org/project/ansible-base/)      | `>= 2.9.13` |
| [ansible-base](https://pypi.org/project/ansible-base/) | `>= 2.10.1` |
| [ansible-core](https://pypi.org/project/ansible-core/) | `>= 2.11.2` |

## Platforms

The role was tested on the following distributions and releases.

| Name   | Version |
| ------ | ------- |
| Ubuntu | `jammy` |
| Ubuntu | `focal` |

## Installation

`ansible-galaxy install averagebit.helm` will install the latest
stable release.

`ansible-galaxy install -r requirements.yml` will install the role
from a requirements file.

```yaml
# requirements.yml
---
roles:
  - name: averagebit.helm
    version: 1.0.0
```

## Variables

- `helm_os`
  - Default: `"linux"`
  - Description: The OS target for the binary.
- `helm_version`
  - Default: `"latest"`
  - Description: The version of the binary can be a specific version such as: `"3.9.0"`.
- `helm_owner`
  - Default: `"root"`
  - Description: The owner of the installed binary.
- `helm_group`
  - Default: `"root"`
  - Description: The group of the installed binary.
- `helm_mode`
  - Default: `"0755"`
  - Description: The permissions of the installed binary.
- `helm_bin_dir_mode`
  - Default: `"0755"`
  - Description: The permissions of the binary directory.
- `helm_bin_dir`
  - Default: `"/usr/local/share/helm"`
  - Description: The directory to install the binary in.
- `helm_bin_path`
  - Default: `"{{ helm_bin_dir }}/helm"`
  - Description: The full path to the binary.
- `helm_link_path`
  - Default: `"/usr/local/bin/helm"`
  - Description: The symlink path created to the binary.
- `helm_download_dir`
  - Default: `"/tmp"`
  - Description: The directory the file will be downloaded in.
- `helm_download_path`
  - Default: `"{{ helm_download_dir }}/helm.tar.gz"`
  - Description: The full path to the downloaded file.
- `helm_repo_url`
  - Default: `"https://get.helm.sh"`
  - Description: The URL to the repository.
- `helm_file_url`
  - Default: `"{{ helm_repo_url }}/helm-v{{ helm_version }}-{{ helm_os }}-{{ helm_architecture }}.tar.gz"`
  - Description: The URL to the file.
- `helm_version_url`
  - Default: `"https://api.github.com/repos/helm/helm/releases/latest"`
  - Description: The URL to fetch the latest version from.
- `helm_checksum_url`
  - Default: `"{{ helm_file_url }}.sha256sum"`
  - Description: The URL to the checksum of the file.
- `helm_architecture`
  - Default: `"{{ helm_architecture_map[ansible_architecture] }}"`
  - Description: The architecture target for the binary.
- `helm_architecture_map`
  - Default: `{"aarch": "arm64", "aarch64": "arm64", "amd64": "amd64", "arm64": "arm64", "armhf": "armhf", "armv7l": "armhf", "ppc64le": "ppc64le", "s390x": "s390x", "x86_64": "amd64"}`
  - Description: The architecture map used to set the correct name
    according to the repository binary naming.

## Usage

```yaml
# playbook.yml
- hosts: servers
  roles:
    - role: averagebit.helm
      become: true # required unless specified at the playbooks top level
      tags: helm # (optional) convenience tag
  vars:
    - helm_version: latest # or a specific version such as: 3.9.0
```

## Legal

Copyright 2022 averagebit <[averagebit@pm.me](mailto:averagebit@pm.me)>

Licensed under the Apache License, Version 2.0 (the "License"); you may
not use this file except in compliance with the License. You may obtain
a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
