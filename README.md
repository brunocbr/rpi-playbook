# Raspberry Pi Fleet Setup Playbook

This Ansible playbook automates the configuration and management of a fleet of Raspberry Pi devices. It includes network configuration, tool installations, custom setups for text processing, Emacs environment, and more.

## Features

- **Network Setup**: Configure Wi-Fi, access points, USB gadget mode, and more.
- **Tool Installations**: Install tools like Seafile, Tailscale, Babashka, and sync notifications.
- **Emacs Environment**: Build and install Emacs from source, along with Spacemacs and tmux service integration.
- **Text Processing**: Set up tools like Pandoc, TexLive, and Zettel Composer.
- **Diogenes & TLG**: Set up Diogenes with Thesaurus Linguae Graecae (TLG) data for ancient Greek texts.
- **Custom Git Repositories**: Manage personal Git repositories with credentials.

## Setup Instructions

1. **Clone the repository** to your Ansible control node.
2. **Create a `credentials.yml`** file with sensitive information like Git credentials.
3. **Run the playbook** on your Raspberry Pi devices using:
   ```bash
   ansible-playbook -i hosts playbook.yml
   ```
4. You can target specific features by using `--tags` with the appropriate tag(s).

## Requirements

- Ansible installed on the control node.
- SSH access to the Raspberry Pi devices (e.g., `orion`, `castor`).
- Devices running a Debian-based OS (e.g., Raspberry Pi OS).

## Roles and Tags

The playbook consists of the following roles and corresponding tags:

### Raspberry Pi Setup
- **`zero-2w-setup`**: Configures the Raspberry Pi Zero 2 W (`tags: zero2`).

### Network & Basic Tools
- **`apt-update`**: Performs an APT update on the system (`tags: foundational, apt-update`).
- **`tailscale`**: Sets up the Tailscale VPN (`tags: foundational, tailscale`).
- **`seafile-client`**: Installs and configures Seafile client (`tags: foundational, seafile`).
- **`sync-notify`**: Sets up sync notification scripts (`tags: foundational, sync-notify`).
- **`shell`**: Configures shell environment (e.g., tmux, mosh) (`tags: foundational, shell`).
- **`babashka`**: Installs Babashka scripting tool (`tags: foundational, babashka`).
- **`wifi-networks`**: Configures known Wi-Fi networks (`tags: network, wifi-networks`).
- **`wifi-access-point`**: Sets up a Wi-Fi access point (`tags: network, wifi-access-point`).
- **`usb-gadget`**: Configures the Raspberry Pi as a USB Ethernet gadget (`tags: network, usb-gadget`).

### Emacs Environment
- **`emacs-build`**: Builds and installs Emacs (`tags: emacs, emacs-build`, configurable `emacs_version`).
- **`spacemacs`**: Sets up Spacemacs environment (`tags: emacs, spacemacs`).
- **`tmux-service`**: Configures tmux as a service (`tags: emacs, tmux-service`).

### Diogenes & TLG
- **`tlg-data`**: Sets up Thesaurus Linguae Graecae (TLG) data (`tags: tlg, tlg-data`).
- **`diogenes`**: Installs Diogenes for reading TLG data (`tags: tlg, diogenes`, configurable `diogenes_server_interface`).

### Text Processing
- **`texlive`**: Installs TexLive for LaTeX processing (`tags: text, texlive`).
- **`pandoc`**: Installs Pandoc (`tags: text, pandoc`, configurable `pandoc_version`).
- **`zettel-composer`**: Sets up [Zettel Composer](https://github.com/brunocbr/zettel-composer) for combining notes (`tags: text, zettel-composer`).
- **`premarkable`**: Preview Markdown files on your browser using [premarkable](https://github.com/brunocbr/premarkable) (`tags: text, premarkable`).

### Git Repositories
- **`git-with-creds`**: Clones and manages private Git repositories (`tags: git-pvt-repo`, supports repositories like `bibs`, `profile-src`, `profile`).
- **`profile-links`**: Configures profile links for the system (`tags: git-pvt-repo, profile-links, profile`).

### Power Management
- **`poweroff`**: Sets up routines for powering off the system (`tags: poweroff`).

## Example Commands

Run the full playbook:
```bash
ansible-playbook playbook.yml
```

Run only Wi-Fi network configuration:
```bash
ansible-playbook playbook.yml --tags wifi-networks
```

To run the Ansible playbook for a particular host, you can use the `--limit` option when executing the `ansible-playbook` command. Here's the basic syntax:

For example, if you want to run the playbook for the host `orion`, you would run:

```bash
ansible-playbook playbook.yml --limit orion
```

This will limit the playbook execution to only the `orion` host defined in your inventory file.

## License

MIT License

## Author

Prof. Bruno Loureiro Conte
