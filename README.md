# Assignment 9 – DHCP and DHCP Relay

Juniper SRX configurations for Assignment 9. The configurations use the topology and DHCP ranges from the HLD.

## Configuration files

| File | Purpose |
|---|---|
| `R1_part1_local-dhcp_and_nat.conf` | R1 provides local DHCP for the `192.168.10.0/24` and `192.168.11.0/24` networks. |
| `R2_part1_local-dhcp_and_nat.conf` | R2 provides local DHCP for the `192.168.12.0/24` and `192.168.13.0/24` networks and performs source NAT toward the LabLan. |
| `R1_part2_dhcp-server-centralized.conf` | R1 provides centralized DHCP for all four client networks. |
| `R2_part2_dhcp-relay.conf` | R2 relays DHCP requests from the two local client networks to R1. |

## DHCP ranges

| Network | Subnet | DHCP range | Gateway |
|---|---|---|---|
| Net3 | `192.168.10.0/24` | `192.168.10.15–20` | `192.168.10.1` |
| Net4 | `192.168.11.0/24` | `192.168.11.22–32` | `192.168.11.1` |
| Net1 | `192.168.12.0/24` | `192.168.12.33–44` | `192.168.12.1` |
| Net2 | `192.168.13.0/24` | `192.168.13.55–66` | `192.168.13.1` |

R2 connects to the LabLan using `10.56.16.85/22` with default gateway `10.56.16.1`. The `.85` address is within the HLD reserved range `10.56.16.80–99`.

## Loading a configuration

On the relevant SRX:

```text
configure
load override terminal
```

Paste one configuration file, press `Ctrl+D`, then run:

```text
commit check
commit
```

Part 1 is for local DHCP. Part 2 is for centralized DHCP with R2 acting as the relay.
