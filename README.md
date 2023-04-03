ansible-role-dns

Ansible role to manage dns


## Requirements

    None


## Dependencies

    None


## Role Variables

### General

**dns_server_enable**

    Toggle whether or not to install and configure the DNS server
    (default: false) CIS

**dns_server_chroot_dir**

    Path to the bind9 chroot directory
    (default: /var/named/chroot)

### Server Role

**dns_server_role**

    Specify whether the server is a 'master' or 'slave'
    (default: master)

**dns_server_slaves**

    Hash of DNS slave servers
    Format:
        [dns-server-slave-name]:
            address: [address]
            algorithm: [algorithem]
            secret: [secret]
        (default: <undefined>)

**dns_server_masters**

    Master server to which the slaves servers should synchronize
    (default: <undefined>)

### Forwarding

**dns_server_forwarders**

    Array of DNS resolvers to which non-authoritative requests should be forwarded.
    (default: <empty-array>)

**dns_server_forwarded_zones**

    Hash of zones to be forwarded to specific resolvers
    [zone]:
        forwarders:
            - [forwarder1]
            - [forwarder2]
            - etc
    (default: <undefined>)

### Zones

**dns_server_zones**

    Hash of zones to be configured
    Format:
        [zone]:
            allow_transfer:
                [host]:
                    address:   [ip]
                    algorithm: [algorithm]
                    secret:    [secret]
            allow_update:
                [host]:
                    address:   [ip]
                    algorithm: [algorithm]
                    secret:    [secret]
            zone_files:
                [zone_file_name]:
                    ttl:       [ttl]
                    refresh:   [refresh]
                    retry:     [retry]
                    expire:    [expire]
                    cache_ttl: [cache_ttl]
                    resource_records:
                        - [record1]
                        - [record2]
                        - etc
    (default: <undefined>)

### Default access control

**dns_server_blackhole**

    Array of items, in __address_match_list__ format, to add to the blackhole configuration
    (default: <empty_array>)

**dns_server_allow_query**

    Array of clients that are permitted to query this resolver
    (default: <empty_array>)

**dns_server_allow_query_cache**

    Array of clients that are permitted to query this resolver's cache
    (default: <empty_array>)


**dns_server_allow_recursion**

    Array of clients that are permitted to submit
    recursive queries.
    (default: <empty_array>)


**dns_server_allow_transfers**

    Array of clients that are permitted to perform zone transfers
    (default: [ 'none' ])

### Performance tunings

**dns_server_dnssec_validation**

    Perform DNSSEC validation
    (default: false)

**dns_server_clients_per_query**

    Starting limit for the number of clients that can be
    simultaneously querying for the same resource.
    (default: 10)

**dns_server_max_clients_per_query**

    Maximum limit for the number of clients that can be
    simultaneously querying for the same resource.
    (default: 100)

**dns_server_recursive_clients**

    Maximum number of recursive clients to permit
    (default: 1000)

**dns_server_responses_per_second**

    Limit response to rapid queries for DDOS mitigation
    (default: 5)

### Zone file SOA defaults

**dns_server_soa_hostmaster_email**

    The value to be used as the hostmaster email in the SOA record
    (default: hostmaster.{{ ansible_domain }})

**dns_server_soa_primary_name_server**

    The value to be used as the primary name server in the SOA record
    (default: {{ ansible_fqdn }})

**dns_server_refresh**

    How often a secondary will poll the primary server to
    see if the serial number for the zone has increased
    (default: 604800)

**dns_server_retry**

    If a secondary was unable to contact the primary at the
    last refresh, wait the retry value before trying again.
    (default: 86400)

**dns_server_expire**

    How long a secondary will still treat its copy of the zone
    data as valid if it can't contact the primary.
    (default: 2419200)

**dns_server_cache_ttl**

    Time to live for the purpose of negative caching
    (default: 604800)

**dns_server_serial**

    Serial number for the zone.
    Note: This CM automates serial nunber management therefore
          setting this value is most likely unnecessary.
    (default: 0)

**dns_server_ttl**

    Default time to live for the zone records
    (default: 604800)

## Example playbook

    ```yaml
    ---
    - hosts: all

      roles:
          - foolean/dns
    ```


## Supported operating systems

    * Debian (11)
    * Raspbian (11)
    * RedHat (8)
    * Rocky (8)


## Compliance

    * CIS Debian Linux 11 Benchmark v1.0.0
    * CIS RedHat Enterprise Linux 8 Benchmark v2.0.0
    * CIS Rocky Linux 8 Benchmark v1.0.0

    * CIS ISC BIND DNS Server 9.11 Benchmark v1.0.0

## License

    BSD-3-Clause
