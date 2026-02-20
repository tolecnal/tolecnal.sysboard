# tolecnal.sysboard

A homebrew, minimalist alternative to tools like `fastfetch` or `neofetch`, specifically designed for server diagnostics upon SSH login. It provides a high-density, "pimped up" TUI dashboard for Debian and Ubuntu systems.

## 🚀 Features

- **Resource Monitoring:** Real-time CPU (1.0s sampling), RAM, and Disk progress bars.
- **System Health:** Failed `systemd` units, `journalctl` boot errors, and `dmesg` critical/OOM events.
- **Host Intelligence:** Automatically identifies hypervisor/hardware (e.g., KVM/QEMU, Dell, HP).
- **Container Awareness:** Native Docker status via socket (no `sudo` required if in `docker` group).
- **Security Audit:** Tracks failed SSH login attempts and pending security updates.
- **Smart Hook:** Runs only on **interactive login shells**. Stays silent during `su`, `sudo`, or non-interactive automation (SCP/SFTP).
- **Cross-Shell:** Full support for **Bash** and **Zsh**.

## 🛠 Role Variables (defaults/main.yml)

| Variable                                | Default | Description                                      |
| --------------------------------------- | ------- | ------------------------------------------------ |
| `system_dashboard_width`                | `90`    | Fixed terminal width for the dashboard.          |
| `system_dashboard_disable_default_motd` | `true`  | Silences standard SSH/Static MOTD.               |
| `system_dashboard_purge_motd_scripts`   | `true`  | Removes default Ubuntu/Debian help/news scripts. |

## 📦 Usage

Add the role to your playbook:

```yaml
- name: Setup tolecnal.sysboard
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: tolecnal.sysboard
```

## 🖥 Manual Trigger

The dashboard triggers automatically on login. You can also run it manually at any time:

```bash
/usr/local/bin/system_stats.py
```

## ⚠️ Requirements

- Python
  - python3-psutil, python3-rich (installed by the role).
- Permissions
  - For full data, ensure your user is in the adm group (for logs) and docker group (for container stats).
