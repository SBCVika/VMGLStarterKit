# Embedded development Ansible playbook

This playbook configures the local Ubuntu host for embedded development.

## Usage

On a freshly installed Ubuntu system, open a terminal and run:

```sh
sudo apt update
sudo apt install --yes git ansible
git clone https://github.com/dhariach/embedded-dev-bootstrap.git
cd embedded-dev-bootstrap

# Preferred: run Ansible as your regular user and enter your sudo password.
ansible-playbook embedded_development.yml --ask-become-pass

# Fallback: run the playbook with sudo only if Ansible privilege escalation fails.
sudo ansible-playbook embedded_development.yml
```

The user must sign out and back in before the new `dialout` and `plugdev`
membership is available in an existing login session.
