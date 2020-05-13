# host-ip-switcher
A lightweight Bash script to automatically modify /etc/hosts based on the local machine's public IP address.
The script checks whether each given (sub)domain name in the config file resolves to the same public IP address as the local machine.
If so, it adds an entry in the local hosts file (`/etc/hosts`) so that all DNS queries for that name are redirected to the IP given in the config file.

This is useful for situations where you want to access a web server hosted on your local network by using the domain name.
DNS would typically resolve the name to the public IP for your network, but accessing the server via that address might not work correctly.
In that case, you can specify an alternate hosts file entry in the config file (`hosts.conf` by default) that the script will apply whenever it is run while your machine is on the same network.

For example, the following config file will map `example.com` to the local IP address `192.168.0.25`:
```
192.168.0.25	example.com
```

We can pair this with a cron job that executes every 5 minutes to ensure the hosts file remains updated when the machine switches networks:
```
*/5 * * * * /path/to/checkip
```
