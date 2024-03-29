# system logs
System logs are managed by `journalctl`. Services are identified by the name of their unit file, usually with the suffix `.service`. 
- To filter for logs generated by a specific service, use `-u` flag, e.g. `journalctl -u NetworkManager.service`
- `-f` will tail the log in real-time

# networking
- `NetworkManager` handles network interfaces on modern Debian
- `nmcli` is terminal utility for interacting with `NetworkManager`, good docs [here](https://developer-old.gnome.org/NetworkManager/unstable/nmcli.html)
- `nmcli device status` is a quick way to list all the network interfaces `NetworkManager` knows about
- `nmcli device modify <device id> <updates>` updates settings for the given device
- `nmcli connection` is useful for setting up new connections.