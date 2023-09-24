# fail2ban-remote-iptables
A collection of configuration file for [fail2ban](https://www.fail2ban.org) to manage remote iptables via local fail2ban.

It is primarily intended for selfhosted services that needs remote, extenal access points, like reverse proxies. In this case you can choose to have local applications' logs replicated on the remote reverse proxy (bad: your logs are leaving your premises, plus you're consuming bandwidth both at your premises and in the cloud) or setup a local control point.

You're supposed to have SSH key exchange in place and sudo properly configured for your local user (usually root, as fail2ban runs with administrative privileges) to an unprivileged user in the remote system. Such user must also be able to run ```iptables``` command without password, so that you can manage the firewall.

Following scenarios are covered:
* docker - suitable for blocking docker containers on your local systems (works at OS level, on FORWARD chain)
* remote - suitable for driving your remote system (works at OS level, on INPUT chain)
* docker remote - suitable for driving your remote systems' docker containers (works at OS level, but on the FORWARD chain)

Please note that docker actions will block the IP from all docker containers, as they work outside the container itself. For more granular actions you must either target the port or work with fail2ban inside containers.
