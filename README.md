ansible-role-claude
=========

Installs [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) for a specific user on Ubuntu VMs.

- Claude Code is installed to the user's default prefix (`~/.local/bin/claude`) — **never as root**
- Node.js and npm are installed system-wide via apt as prerequisites
- The role verifies that the target user and projects directory exist before proceeding

Requirements
------------

- Ubuntu 22.04 / 24.04 (Noble)
- `become: true` — required to install system packages (nodejs, npm) and create directories

Role Variables
--------------

| Variable | Required | Default | Description |
|---|---|---|---|
| `claude_user` | yes | `""` | System user for whom Claude Code is installed. Must exist. Claude is never installed as root. |
| `claude_projects_dir` | yes | `""` | Directory where the user's projects will live. Must exist unless `claude_create_projects_dir: true`. |
| `claude_create_projects_dir` | no | `false` | Create `claude_projects_dir` if it does not exist. |
| `claude_version` | no | `"latest"` | npm package version (e.g. `"1.0.3"`). |

The Claude Code binary is installed at `~{{ claude_user }}/.local/bin/claude`.  
Add `~/.local/bin` to the user's `PATH` to use it directly.

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: vms
  become: true
  roles:
    - role: afreisinger.claude
      vars:
        claude_user: "devops"
        claude_projects_dir: "/home/devops/projects"
        claude_create_projects_dir: true
```

License
-------

MIT

Author Information
------------------

© Adrián Freisinger 2026
