# Assignment 9 – DHCP og DHCP-relay

Juniper SRX-konfigurationer til Assignment 9. Konfigurationerne følger topologien og DHCP-ranges fra HLD’en.

## Konfigurationsfiler

| Fil | Formål |
|---|---|
| `R1_part1_local-dhcp_and_nat.conf` | R1 leverer lokal DHCP til netværkene `192.168.10.0/24` og `192.168.11.0/24`. |
| `R2_part1_local-dhcp_and_nat.conf` | R2 leverer lokal DHCP til netværkene `192.168.12.0/24` og `192.168.13.0/24` samt source NAT mod LabLan. |
| `R1_part2_dhcp-server-centralized.conf` | R1 leverer centraliseret DHCP til alle fire klientnetværk. |
| `R2_part2_dhcp-relay.conf` | R2 videresender DHCP-forespørgsler fra sine to klientnetværk til R1. |

## DHCP-ranges

| Netværk | Subnet | DHCP-range | Gateway |
|---|---|---|---|
| Net3 | `192.168.10.0/24` | `192.168.10.15–20` | `192.168.10.1` |
| Net4 | `192.168.11.0/24` | `192.168.11.22–32` | `192.168.11.1` |
| Net1 | `192.168.12.0/24` | `192.168.12.33–44` | `192.168.12.1` |
| Net2 | `192.168.13.0/24` | `192.168.13.55–66` | `192.168.13.1` |

R2 er forbundet til LabLan med `10.56.16.85/22` og bruger `10.56.16.1` som default gateway. Adressen `.85` ligger i HLD’ens reserverede område `10.56.16.80–99`.

## Indlæsning af en konfiguration

På den relevante SRX-router:

```text
configure
load override terminal
```

Indsæt én konfigurationsfil, tryk `Ctrl+D`, og kør derefter:

```text
commit check
commit
```

Part 1 bruges til lokal DHCP. Part 2 bruges til centraliseret DHCP, hvor R2 fungerer som DHCP-relay.
