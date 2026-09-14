# Networking

## Network Configuration

```text
| Command           | Description                                                |
| ----------------- | ---------------------------------------------------------- |
|   ip addr         | Displays network interfaces and IP addresses.              |
|   ip link         | Displays network interface states.                         |
|   ip route        | Displays the routing table.                                |
|   ip neigh        | Displays the ARP/neighbor table.                           |
|   ip addr add     | Adds an IP address to a network interface.                 |
|   ip link set     | Enables or disables a network interface.                   |
|   hostname -I     | Displays the system's IP addresses.                        |
|   ss -tulnp       | Displays listening TCP/UDP ports and associated processes. |
|   ss -tan         | Displays TCP connections.                                  |
|   ping host       | Tests basic network connectivity.                          |
|   traceroute host | Shows the network path to a destination.                   |
|   tracepath host  | Shows network path and MTU information.                    |

```

## DNS & Network Troubleshooting

```text
| Command                | Description                                                        |
| ---------------------- | ------------------------------------------------------------------ |
|   dig example.com      | Performs detailed DNS queries.                                     |
|   nslookup example.com | Tests DNS resolution.                                              |
|   host example.com     | Displays basic DNS/IP information.                                 |
|   resolvectl status    | Displays system DNS configuration.                                 |
|   curl URL             | Sends HTTP/HTTPS requests to an endpoint.                          |
|   curl -I URL          | Displays only HTTP response headers.                               |
|   curl -v UR`          | Displays detailed HTTP connection information for troubleshooting. |
|   wget URL             | Downloads files from URLs.                                         |
|   nc -zv host port     | Tests whether a specific TCP port is reachable.                    |
|   telnet host port     | Tests a TCP connection manually.                                   |
|   tcpdump              | Captures and analyzes network packets.                             |
|   nmap host            | Discovers open ports and services on a host.                       |

```
