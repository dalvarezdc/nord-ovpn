# nord-ovpn

A simple Bash script to help connect to NordVPN using OpenVPN manual configurations.

## Prerequisites

- OpenVPN installed
- NordVPN account with username and password
- Sudo access (required for running OpenVPN)

## Installation

1. **Download NordVPN OpenVPN configuration files:**
   ```bash
   wget https://downloads.nordcdn.com/configs/archives/servers/ovpn.zip
   unzip ovpn.zip
   sudo mv ovpn_tcp /etc/openvpn/
   ```

2. **Create authentication file:**
   ```bash
   sudo tee /etc/openvpn/nord.auth > /dev/null <<EOF
   your_username
   your_password
   EOF
   sudo chmod 600 /etc/openvpn/nord.auth
   ```

3. **Install the script:**
   ```bash
   sudo cp nord-ovpn /usr/local/bin/
   sudo chmod +x /usr/local/bin/nord-ovpn
   ```

## Usage

Run commands with `sudo` as OpenVPN requires root privileges.

- **Help:** `sudo nord-ovpn --help`
- **List available countries:** `sudo nord-ovpn list`
- **List servers in a country:** `sudo nord-ovpn list <country_code>` (e.g., `sudo nord-ovpn list ch`)
- **Connect to a country:** `sudo nord-ovpn connect <country_code>` (e.g., `sudo nord-ovpn connect ch`)
- **Connect to a random server in a country:** `sudo nord-ovpn connect <country_code> --random` (e.g., `sudo nord-ovpn connect us --random`)
- **Connect using a specific .ovpn file:** `sudo nord-ovpn connect-file <path_to_ovpn>` (e.g., `sudo nord-ovpn connect-file /etc/openvpn/ovpn_tcp/ch217.nordvpn.com.tcp.ovpn`)

## Notes

- Country codes are two-letter ISO country codes (e.g., `ch` for Switzerland, `us` for United States).
- The script uses TCP configurations located in `/etc/openvpn/ovpn_tcp`.
- Authentication credentials are read from `/etc/openvpn/nord.auth` (two lines: username on first, password on second).
- The script will pick the first available server unless `--random` is specified.

## License

This script is provided as-is. Please refer to NordVPN's terms of service for usage of their configurations.
