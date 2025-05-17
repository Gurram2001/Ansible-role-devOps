

### 📄 `roles/devops_tools/README.md`


# Ansible Role: DevOps Tools Setup

This Ansible role installs and configures essential tools required for a DevOps environment. It includes the installation of Docker, Docker Compose, Git, and other helpful command-line utilities. Optional tools like `kubectl`, `helm`, and `terraform` can also be installed based on variables.

---

## 📦 Features

- Installs Docker and enables the Docker service
- Installs Docker Compose (v2)
- Adds specified users to the Docker group
- Installs commonly used CLI tools: `git`, `curl`, `jq`, `unzip`, `python3-pip`
- Optional installation of:
  - `kubectl` (Kubernetes CLI)
  - `helm` (Helm CLI)
  - `terraform` (HashiCorp IaC tool)

---

## 📁 Role Structure

```text
devops_tools/
├── defaults/
│   └── main.yml
├── handlers/
│   └── main.yml
├── tasks/
│   └── main.yml
├── vars/
│   └── main.yml
└── README.md
````

---

## 🚀 Requirements

* Ubuntu/Debian-based Linux systems
* `sudo` privileges on target hosts

---

## 🔧 Role Variables

You can override these variables in your playbook or inventory.

| Variable            | Default      | Description                            |
| ------------------- | ------------ | -------------------------------------- |
| `docker_users`      | `['ubuntu']` | List of users to add to `docker` group |
| `install_kubectl`   | `false`      | Set to `true` to install `kubectl`     |
| `install_terraform` | `false`      | Set to `true` to install Terraform     |
| `install_helm`      | `false`      | Set to `true` to install Helm          |

---

## 📝 Example Usage

### Inventory

**`inventory.ini`**

```ini
[dev]
your-ec2-ip-or-hostname ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### Playbook

**`site.yml`**

```yaml
- name: Setup DevOps Tools
  hosts: dev
  become: true
  roles:
    - role: devops_tools
      vars:
        docker_users:
          - ubuntu
          - ansible
        install_kubectl: true
        install_terraform: true
        install_helm: false
```

---

## ▶️ Run It

```bash
ansible-playbook -i inventory.ini site.yml
```

---

## 📌 Notes

* The role is optimized for Ubuntu/Debian-based hosts. You may need to adapt it for RHEL/CentOS.
* Docker Compose is installed manually as a binary (v2 format).
* Tools are installed directly from official sources (e.g., GitHub, HashiCorp).

---

## ✅ Best Practices

* Use `group_vars` or `host_vars` to manage environment-specific configs.
* Parameterize versions of tools if you want tighter control over reproducibility.
* Run `ansible-lint` on this role if you’re enforcing YAML or Ansible coding standards.

---

## 📃 License

MIT License

---

## 🙋‍♂️ Author

Gurram Mani Karthik

Inspired by real-world DevOps onboarding needs.


```
