# Ansible role for configuring dnsmasq and stubby

This is a Ansible role that configures [dnsmasq](https://dnsmasq.org/) as a
caching DNS server, forwarding the traffic to [stubby](https://github.com/getdnsapi/stubby)
which is acting as a DNS Privacy stub resolver.

Primary usage is on a [Raspberry Pi](https://www.raspberrypi.com/), or similar,
running as a local DNS on a small network.

> **Note**
>
> Do not use this role without first testing in a non-operational environment.

> **Note**
>
> There is a [SLSA](https://slsa.dev/) artifact present under the
> [slsa action workflow](https://github.com/konstruktoid/ansible-role-dns/actions/workflows/slsa.yml)
> for verification.

## Task list overview

- Create custom facts directory
- Add systemd version fact
- Update facts
- Run apt update
- Install packages
- Get installed dnsmasq version
- Configure systemd-resolved
- Add /etc/hosts script
- Stat resolv.conf
- Fix systemd resolv link
- Install stubby configuration
- Configure dnsmasq
- Flush all handlers
- Verify DNS servers
- Generate a new /etc/hosts

## Defaults

```yaml
---
dnsmasq_cache_size: 4096
dnsmasq_listen_address: "127.0.0.1,{{ ansible_default_ipv4.address | default(ansible_all_ipv4_addresses[0]) }}"
stubby_idle_timeout: 1000
stubby_port: 5353
stubby_round_robin_upstreams: 1
...
```

If `dnsmasq_listen_address: ""`, then the `listen-address` option will be
omitted.

## Contributing

Do you want to contribute? Great! Contributions are always welcome,
no matter how large or small. If you found something odd, feel free to submit a
issue, improve the code by creating a pull request, or by
[sponsoring this project](https://github.com/sponsors/konstruktoid).

## License

Apache License Version 2.0

## Author Information

[https://github.com/konstruktoid](https://github.com/konstruktoid "github.com/konstruktoid")
