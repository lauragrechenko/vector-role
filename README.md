Role Name
=========

Installs Vector (observability/log pipeline) from a tar archive, deploys a config, and runs it as a systemd service.

Requirements
------------

Ansible ≥ 2.12

OS: EL 8/9

Provide a Vector config template (vector.toml), or set vector_template_local_path.

Ensure the host can reach your sinks/outputs (network, firewall).

Role Variables
--------------

### Version & download URL
```
vector_version: "0.36.0"
vector_url: "https://packages.timber.io/vector/{{ vector_version }}/vector-{{ vector_version }}-x86_64-unknown-linux-gnu.tar.gz"
```

### Where to place the downloaded tarball on the target
```
vector_archive_path: "/tmp/vector.tar.gz"
```

### Install prefix and paths
```
vector_install_dir: "/opt/vector"
vector_bin_dir: "{{ vector_install_dir }}/bin"
vector_config_dir: "/etc/vector"
vector_data_dir: "/var/lib/vector"
```

### Name of the directory created by the tarball
```
vector_extracted_dirname: "vector-x86_64-unknown-linux-gnu"
```

### Full path to the extracted binary (derived from the dirname above)
```
vector_bin_src: "{{ vector_install_dir }}/{{ vector_extracted_dirname }}/bin/vector"
```

### Template to use for config (relative to role or absolute path)
```
vector_config_template: "vector.toml.j2"
```

### Systemd service name
```
vector_service_name: "vector"
```

Dependencies
------------

None.

Example Playbook
----------------

```
- hosts: vector
  become: true
  roles:
    - role: vector
      vars:
        vector_url: "https://packages.timber.io/vector/0.39.0/vector-x86_64-unknown-linux-gnu.tar.gz"
        vector_archive_path: "/tmp/vector-0.39.0.tar.gz"
        vector_install_dir: "/opt/vector"
        vector_config_dir: "/etc/vector"
        vector_data_dir: "/var/lib/vector"
        vector_template_local_path: "templates/vector.toml.j2"
```

License
-------

MIT

Author Information
------------------

Laura
