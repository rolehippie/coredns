# coredns

[![Source Code](https://img.shields.io/badge/github-source%20code-blue?logo=github&logoColor=white)](https://github.com/rolehippie/coredns) [![Testing Build](https://github.com/rolehippie/coredns/workflows/testing/badge.svg)](https://github.com/rolehippie/coredns/actions?query=workflow%3Atesting) [![Readme Build](https://github.com/rolehippie/coredns/workflows/readme/badge.svg)](https://github.com/rolehippie/coredns/actions?query=workflow%3Areadme) [![Galaxy Build](https://github.com/rolehippie/coredns/workflows/galaxy/badge.svg)](https://github.com/rolehippie/coredns/actions?query=workflow%3Agalaxy) [![License: Apache-2.0](https://img.shields.io/github/license/rolehippie/coredns)](https://github.com/rolehippie/coredns/blob/master/LICENSE)

Ansible role to install and configure CoreDNS server.

## Sponsor

[![Proact Deutschland GmbH](https://proact.eu/wp-content/uploads/2020/03/proact-logo.png)](https://proact.eu)

Building and improving this Ansible role have been sponsored by my employer **Proact Deutschland GmbH**.

## Table of content

- [Default Variables](#default-variables)
  - [coredns_default_zones](#coredns_default_zones)
  - [coredns_download](#coredns_download)
  - [coredns_extra_zones](#coredns_extra_zones)
  - [coredns_general_config](#coredns_general_config)
  - [coredns_general_enabled](#coredns_general_enabled)
  - [coredns_general_name](#coredns_general_name)
  - [coredns_general_plugins](#coredns_general_plugins)
  - [coredns_listen_port](#coredns_listen_port)
  - [coredns_version](#coredns_version)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Default Variables

### coredns_default_zones

List of default zone file definitions

#### Default value

```YAML
coredns_default_zones: []
```

#### Example usage

```YAML
coredns_default_zones:
  - name: example.org
    plugins:
      - name: prometheus
      - name: log
      - name: errors
      - name: chaos
        args: CoreDNS-001 info@coredns.io
      - name: dnssec
        config: |
          key file Kexample.org.+013+45330
    content: |
      $ORIGIN example.org.
      @	3600 IN	SOA sns.dns.icann.org. noc.dns.icann.org. (
              2017042745 ; serial
              7200       ; refresh (2 hours)
              3600       ; retry (1 hour)
              1209600    ; expire (2 weeks)
              3600       ; minimum (1 hour)
              )

        3600 IN NS a.iana-servers.net.
        3600 IN NS b.iana-servers.net.

      www     IN A     127.0.0.1
              IN AAAA  ::1
  - name: example.de
    url: http://example.com/example-zone
  - name: example.eu
    src: path/to/template.j2
  - name: example.org
    state: absent
```

### coredns_download

URL to the archive of the release to install

#### Default value

```YAML
coredns_download: https://github.com/coredns/coredns/releases/download/v{{ coredns_version
  }}/coredns_{{ coredns_version }}_linux_amd64.tgz
```

### coredns_extra_zones

List of extra zone file definitions

#### Default value

```YAML
coredns_extra_zones: []
```

#### Example usage

```YAML
coredns_extra_zones:
  - name: example.org
    plugins:
      - name: prometheus
      - name: log
      - name: errors
      - name: chaos
        args: CoreDNS-001 info@coredns.io
      - name: dnssec
        config: |
          key file Kexample.org.+013+45330
    content: |
      $ORIGIN example.org.
      @	3600 IN	SOA sns.dns.icann.org. noc.dns.icann.org. (
              2017042745 ; serial
              7200       ; refresh (2 hours)
              3600       ; retry (1 hour)
              1209600    ; expire (2 weeks)
              3600       ; minimum (1 hour)
              )

        3600 IN NS a.iana-servers.net.
        3600 IN NS b.iana-servers.net.

      www     IN A     127.0.0.1
              IN AAAA  ::1
  - name: example.de
    url: http://example.com/example-zone
  - name: example.eu
    src: path/to/template.j2
  - name: example.org
    state: absent
```

### coredns_general_config

Optional raw config to overwrite the Corefile

#### Default value

```YAML
coredns_general_config:
```

### coredns_general_enabled

Enable the default zone part of core config

#### Default value

```YAML
coredns_general_enabled: true
```

### coredns_general_name

Zone for the general standard configuration

#### Default value

```YAML
coredns_general_name: .
```

### coredns_general_plugins

List of plugins for standard configuration

#### Default value

```YAML
coredns_general_plugins:
  - name: errors
  - name: log
  - name: prometheus
  - name: hosts
  - name: forward
    args: . 8.8.8.8 1.1.1.1
  - name: cache
    args: 30
  - name: loop
  - name: loadbalance
```

#### Example usage

```YAML
coredns_general_plugins:
  - name: errors
  - name: log
  - name: prometheus
  - name: chaos
    args: CoreDNS-001 info@coredns.io
  - name: cache
    args: 30
  - name: loop
  - name: loadbalance
```

### coredns_listen_port

Override the port binding for CoreDNS

#### Default value

```YAML
coredns_listen_port:
```

### coredns_version

Version of the release to install

#### Default value

```YAML
coredns_version: 1.9.0
```

## Discovered Tags

**_coredns_**


## Dependencies

- None

## License

Apache-2.0

## Author

[Thomas Boerger](https://github.com/tboerger)
