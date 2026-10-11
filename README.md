# signal

Ansible role to install [Signal](https://signal.org/) messenger on Debian/Ubuntu systems.

## Requirements

- Debian or Ubuntu host
- `become: true` privileges (sudo)

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `signal_package_name` | `signal-desktop` | Package name to install via apt |
| `signal_gpg_key_url` | `https://updates.signal.org/desktop/apt/keys.asc` | URL to the GPG signing key |
| `signal_gpg_keyring` | `/usr/share/keyrings/signal-desktop-keyring.gpg` | Path for the converted keyring file |
| `signal_sources_url` | `https://updates.signal.org/static/desktop/apt/signal-desktop.sources` | URL to the apt sources file |
| `signal_sources_file` | `/etc/apt/sources.list.d/signal-desktop.sources` | Destination for the apt sources file |

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - role: signal
```

To conditionally install only on private machines:

```yaml
- hosts: all
  become: true
  roles:
    - role: signal
  when: is_private_machine
```

## Manual setup (without Ansible)

```bash
sudo apt install curl gnupg
curl -fL https://updates.signal.org/desktop/apt/keys.asc -o /tmp/signal-keys.asc
sudo gpg --dearmor --yes --output /usr/share/keyrings/signal-desktop-keyring.gpg /tmp/signal-keys.asc
sudo chmod 0644 /usr/share/keyrings/signal-desktop-keyring.gpg
rm /tmp/signal-keys.asc
sudo curl -fL https://updates.signal.org/static/desktop/apt/signal-desktop.sources -o /etc/apt/sources.list.d/signal-desktop.sources
sudo chmod 0644 /etc/apt/sources.list.d/signal-desktop.sources
sudo apt update
sudo apt install signal-desktop
```

## License

MIT

## Author

Varssos