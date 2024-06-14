# thystips.php_fpm_exporter

[![Maintainer](https://img.shields.io/badge/maintained%20by-thystips-e00000?style=flat-square)](https://github.com/thystips)
[![License](https://img.shields.io/github/license/thystips/ansible-php_fpm_exporter?style=flat-square)](https://github.com/thystips/ansible-php_fpm_exporter/blob/main/LICENSE)
[![Release](https://img.shields.io/github/v/release/thystips/ansible-php_fpm_exporter?style=flat-square)](https://github.com/thystips/ansible-php_fpm_exporter/releases)
[![Status](https://img.shields.io/github/workflow/status/thystips/ansible-php_fpm_exporter/Ansible%20Molecule?style=flat-square&label=tests)](https://github.com/thystips/ansible-php_fpm_exporter/actions?query=workflow%3A%22Ansible+Molecule%22)
[![Ansible Galaxy](https://img.shields.io/badge/ansible-galaxy-black.svg?style=flat-square&logo=ansible)](https://galaxy.ansible.com/thystips/php_fpm_exporter)[![Ansible version](https://img.shields.io/badge/ansible-%3E%3D2.10-black.svg?style=flat-square&logo=ansible)](https://github.com/ansible/ansible)

⭐ Star us on GitHub — it motivates us a lot!

Install php-fpm prometheus exporter

**Platforms Supported**:

| Platform | Versions |
|----------|----------|
| EL | all |
| Amazon | all |
| Debian | all |
| Ubuntu | all |

## ⚠️ Requirements

Ansible >= 2.1.

### Ansible role dependencies

None.

## ⚡ Installation

### Install with Ansible Galaxy

```shell
ansible-galaxy install thystips.php_fpm_exporter
```

### Install with git

If you do not want a global installation, clone it into your `roles_path`.

```bash
git clone https://github.com/thystips/ansible-php_fpm_exporter  thystips.php_fpm_exporter
```

But I often add it as a submodule in a given `playbook_dir` repository.

```bash
git submodule add https://github.com/thystips/ansible-php_fpm_exporter roles/thystips.php_fpm_exporter
```

As the role is not managed by Ansible Galaxy, you do not have to specify the
github user account.

### ✏️ Example Playbook

Basic usage is:

```yaml
- hosts: all
  roles:
    - role: thystips.php_fpm_exporter
      vars:
        php_fpm_additional_args: []
        php_fpm_exporter_after_services: network-online.target
        php_fpm_exporter_default_template: default/php-fpm_exporter.j2
        php_fpm_exporter_download_url: https://github.com/{{ php_fpm_exporter_github_repo}}/releases/download/v{{ php_fpm_exporter_version }} /php-fpm_exporter_{{ php_fpm_exporter_version}}_linux_{{ __architecture }}
        php_fpm_exporter_force_reinstall: false
        php_fpm_exporter_install_dir: /usr/local/bin
        php_fpm_exporter_service_template: systemd/php-fpm_exporter.service.j2
        php_fpm_exporter_start_service_at_role_end: true
        php_fpm_exporter_system_group: {{ php_fpm_exporter_system_user }}
        php_fpm_exporter_system_user: php-fpm-exporter
        php_fpm_exporter_test_service: true
        php_fpm_exporter_version: latest
        php_fpm_fix_process_count: false
        php_fpm_log_level: warn
        php_fpm_scrape_uri: unix:///run/php-fpm.sock;/status
        php_fpm_web_listen_address: 127.0.0.1:9253
        php_fpm_web_telemetry_path: /metrics
```

## ⚙️ Role Variables

Variables are divided in three types.

The **default vars** section shows you which variables you may
override in your ansible inventory. As a matter of fact, all variables should
be defined there for explicitness, ease of documentation as well as overall
role manageability.

The **context variables** are shown in section below hint you
on how runtime context may affects role execution.

### Default variables
Role default variables from `defaults/main.yml`.

| Variable Name | Value |
|---------------|-------|
| php_fpm_exporter_force_reinstall | False |
| php_fpm_exporter_start_service_at_role_end | True |
| php_fpm_exporter_test_service | True |
| php_fpm_exporter_version | latest |
| php_fpm_exporter_install_dir | /usr/local/bin |
| php_fpm_exporter_system_user | php-fpm-exporter |
| php_fpm_exporter_system_group | {{ php_fpm_exporter_system_user }} |
| php_fpm_log_level | warn |
| php_fpm_web_listen_address | 127.0.0.1:9253 |
| php_fpm_web_telemetry_path | /metrics |
| php_fpm_scrape_uri | unix:///run/php-fpm.sock;/status |
| php_fpm_fix_process_count | False |
| php_fpm_additional_args | []<br> |
| php_fpm_exporter_after_services | network-online.target |
| php_fpm_exporter_download_url | https://github.com/{{ php_fpm_exporter_github_repo }}/releases/download/v{{ php_fpm_exporter_version }} /php-fpm_exporter_{{ php_fpm_exporter_version }}_linux_{{ __architecture }}<br> |
| php_fpm_exporter_default_template | default/php-fpm_exporter.j2 |
| php_fpm_exporter_service_template | systemd/php-fpm_exporter.service.j2 |

### Context variables

Those variables from `vars/*.{yml,json}` are loaded dynamically during task
runtime using the `include_vars` module.

Variables loaded from `vars/main.yml`.

| Variable Name | Value |
|---------------|-------|
| php_fpm_exporter_github_repo | hipages/php-fpm_exporter |
| php_fpm_exporter_binary | php-fpm_exporter |
| go_arch_map | aarch64: arm64<br>x86_64: amd64<br> |
| __architecture | {{ go_arch_map[ansible_architecture]  \| default('amd64') }} |
| systemd_lib_directory | /etc/systemd/system |
| systemd_default_directory | /etc/default |

## Author Information

ThysTips
