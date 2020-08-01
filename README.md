# network-scanner
 Simple network scanner built with Scapy for Python

## Usage
Perform either an ARP scan or TCP scan.
- An ARP scan will send ARP requests to all devices on the local network, and collect the ARP replies to discover IP address to MAC address mappings.
- A TCP scan will send TCP SYN packets to all specified ports, and collect the SYN+ACK replies to discover which ports are open.

If you are on a UNIX-based system, please run the script as root (use sudo).
```
usage: scanner.py [-h] {ARP,TCP} ...

positional arguments:
  {ARP,TCP}   Command to perform.
    ARP       Perform a network scan using ARP requests.
    TCP       Perform a TCP scan using SYN packets.

optional arguments:
  -h, --help  show this help message and exit
```
### ARP Scan
Either an IP address or IP address range can be used. For example, ```python3 scanner.py ARP 192.168.2.1/24``` scans all IP addresses in the 192.168.2.0/24 subnet.
```
usage: scanner.py ARP [-h] IP

positional arguments:
  IP          An IP address (e.g. 192.168.1.1) or address range (e.g.
              192.168.1.1/24) to scan.

optional arguments:
  -h, --help  show this help message and exit
```

### TCP Scan
Either specific ports or a range of ports can be used. For example, ```python3 scanner.py TCP 192.168.2.1 --range 0 1000``` scans all ports from 0 to 1000.
```
usage: scanner.py TCP [-h] [--range] IP ports [ports ...]

positional arguments:
  IP          An IP address or hostname to target.
  ports       Ports to scan, delimited by spaces. When --range is specified,
              scan a range of ports. Otherwise, scan individual ports.

optional arguments:
  -h, --help  show this help message and exit
  --range     Specify a range of ports. When this option is specified, <ports>
              should be given as <low_port> <high_port>.
```

### Common Errors
If you receive ```AttributeError: 'L2bpfSocket' object has no attribute 'ins'```, you likely need to run the script as root (use sudo).
See https://stackoverflow.com/questions/55881295/l3packetsocket-object-has-no-attribute-ins-when-using-send-command
