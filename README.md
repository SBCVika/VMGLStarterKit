# Embedded development Ansible playbook

This playbook configures the local Ubuntu host for embedded development.

## Student laptop requirements

For the student masterclass, bring a laptop with at least:

- A 64-bit x86-64 processor with hardware virtualization support (Intel VT-x
  or AMD-V); virtualization must be enabled in the BIOS/UEFI settings.
- 16 GB of RAM.
- 100 GB of free SSD storage.
- Ubuntu Linux installed, as the provided setup is for Ubuntu.
- Ethernet connectivity (a built-in Ethernet port or a suitable adapter).
- Two additional free USB ports for connecting development hardware.

## Tools installed by Ansible

The playbook installs the following tools and supporting packages:

### Editing and building software

- **Visual Studio Code** is the code editor used for the development exercises.
- **C/C++ Extension Pack for Visual Studio Code** adds C and C++ language
  support, including code navigation, IntelliSense, and debugging.
- **MCU-Debug for Visual Studio Code** adds embedded microcontroller debugging
  support.
- **Arm GNU Toolchain** provides the `arm-none-eabi` compiler, assembler,
  linker, and related tools for building firmware for Arm microcontrollers.
- **build-essential** provides the standard native build tools, including a C/C++
  compiler and `make`.
- **CMake** configures software builds, and **Ninja** runs those builds.
- **Git** downloads and manages the source code used in the exercises.

### Connecting to and debugging hardware

- **OpenOCD** connects to supported debug probes and lets a debugger program
  and debug a microcontroller.
- **ST-Link tools** provide command-line utilities for working with ST-Link
  debug probes. The playbook also installs device rules to help Ubuntu grant
  access to the probe.
- **Minicom** is a terminal program for communicating with development boards
  over a serial connection.
- **Wireshark** captures and examines network traffic, useful when learning
  about or troubleshooting network communication.
- The playbook adds your account to the `dialout` and `plugdev` groups so it can
  access serial devices and development hardware without running every
  development tool as administrator. Sign out and back in for this change to
  take effect.

### Messaging and supporting packages

- **MQTT Explorer** provides a graphical interface for viewing and testing
  MQTT messaging.
- **ca-certificates** supplies trusted certificates used for secure connections
  when downloading software.
- **python3-debian** provides Debian package metadata support for Ansible's
  package and repository tasks.
- **snapd** enables installation and management of Snap applications, including
  MQTT Explorer.
- **xz-utils** supports handling the compressed Arm GNU Toolchain archive.

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
