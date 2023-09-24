# fail2ban-remote-iptables
A collection of configuration file for [fail2ban](https://www.fail2ban.org) to manage remote iptables via local fail2ban.

It is primarily intended for selfhosted services that needs remote, extenal access points, like reverse proxies. In this case you can choose to have local applications' logs replicated on the remote reverse proxy (bad: your logs are leaving your premises, plus you're consuming bandwidth both at your premises and in the cloud) or setup a local control point.

You're supposed to have SSH key exchange in place and sudo properly configured for your local user (usually root, as fail2ban runs with administrative privileges) to an unprivileged user in the remote system. Such user must also be able to run ```iptables``` command without password, so that you can manage the firewall.

Following scenarios are covered:
* remote - suitable for driving your remote system (works at OS level, on INPUT chain)
* docker remote - suitable for driving your remote systems' docker containers (works at OS level, but on the FORWARD chain)
