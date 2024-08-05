### Addressing Table
The addressing table based on the provided diagram and IP ranges can be set up as follows:

| Device      | Interface | IP Address       | Subnet Mask     |
|-------------|-----------|------------------|-----------------|
| Web Server  | Fa0/0     | 209.165.200.224  | 255.255.255.248 |
| ISP         | Fa0/0     | 209.165.200.225  | 255.255.255.248 |
| ISP         | Fa0/1     | 209.165.201.1    | 255.255.255.252 |
| HQ          | Fa0/0     | 192.168.0.129    | 255.255.255.128 |
| HQ          | Fa0/1     | 192.168.0.130    | 255.255.255.128 |
| HQ          | S0/0/0    | 10.0.0.1         | 255.255.255.252 |
| HQ          | S0/0/1    | 10.0.0.5         | 255.255.255.252 |
| HQ          | S0/1/0    | 10.0.0.9         | 255.255.255.252 |
| HQ          | S0/1/1    | 10.0.0.13        | 255.255.255.252 |
| B1          | Fa0/0     | 192.168.1.1      | 255.255.255.0   |
| B1          | Fa0/1     | 192.168.1.2      | 255.255.255.0   |
| B1          | Fa1/0     | 192.168.1.3      | 255.255.255.0   |
| B1          | Fa1/1     | 192.168.1.4      | 255.255.255.0   |
| B1          | S0/0/0    | 10.0.0.2         | 255.255.255.252 |
| B1          | S0/0/1    | 10.0.0.17        | 255.255.255.252 |
| B2          | Fa0/0     | 172.16.0.1       | 255.255.0.0     |
| B2          | Fa0/1     | 172.16.0.2       | 255.255.0.0     |
| B2          | Fa1/0     | 172.16.0.3       | 255.255.0.0     |
| B2          | Fa1/1     | 172.16.0.4       | 255.255.0.0     |
| B2          | S0/0/0    | 10.0.0.6         | 255.255.255.252 |
| B2          | S0/0/1    | 10.0.0.18        | 255.255.255.252 |
| B2          | S0/1/0    | 10.0.0.10        | 255.255.255.252 |
| B3          | Fa0/0     | 172.20.0.1       | 255.255.0.0     |
| B3          | Fa0/1     | 172.20.0.2       | 255.255.0.0     |
| B3          | Fa1/0     | 172.20.0.3       | 255.255.0.0     |
| B3          | Fa1/1     | 172.20.0.4       | 255.255.0.0     |
| B3          | S0/0/0    | 10.0.0.14        | 255.255.255.252 |
| B3          | S0/0/1    | 10.0.0.11        | 255.255.255.252 |

### Configuration Commands
#### Configuring Web Server
```bash
interface FastEthernet0/0
 ip address 209.165.200.224 255.255.255.248
 no shutdown
```

#### Configuring ISP Router
```bash
interface FastEthernet0/0
 ip address 209.165.200.225 255.255.255.248
 no shutdown

interface FastEthernet0/1
 ip address 209.165.201.1 255.255.255.252
 no shutdown
```

#### Configuring HQ Router
```bash
interface FastEthernet0/0
 ip address 192.168.0.129 255.255.255.128
 no shutdown

interface FastEthernet0/1
 ip address 192.168.0.130 255.255.255.128
 no shutdown

interface Serial0/0/0
 ip address 10.0.0.1 255.255.255.252
 clock rate 64000
 no shutdown

interface Serial0/0/1
 ip address 10.0.0.5 255.255.255.252
 clock rate 64000
 no shutdown

interface Serial0/1/0
 ip address 10.0.0.9 255.255.255.252
 clock rate 64000
 no shutdown

interface Serial0/1/1
 ip address 10.0.0.13 255.255.255.252
 clock rate 64000
 no shutdown
```

#### Configuring B1 Router
```bash
interface FastEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown

interface FastEthernet0/1
 ip address 192.168.1.2 255.255.255.0
 no shutdown

interface FastEthernet1/0
 ip address 192.168.1.3 255.255.255.0
 no shutdown

interface FastEthernet1/1
 ip address 192.168.1.4 255.255.255.0
 no shutdown

interface Serial0/0/0
 ip address 10.0.0.2 255.255.255.252
 clock rate 64000
 no shutdown

interface Serial0/0/1
 ip address 10.0.0.17 255.255.255.252
 clock rate 64000
 no shutdown
```

#### Configuring B2 Router
```bash
interface FastEthernet0/0
 ip address 172.16.0.1 255.255.0.0
 no shutdown

interface FastEthernet0/1
 ip address 172.16.0.2 255.255.0.0
 no shutdown

interface FastEthernet1/0
 ip address 172.16.0.3 255.255.0.0
 no shutdown

interface FastEthernet1/1
 ip address 172.16.0.4 255.255.0.0
 no shutdown

interface Serial0/0/0
 ip address 10.0.0.6 255.255.255.252
 clock rate 64000
 no shutdown

interface Serial0/0/1
 ip address 10.0.0.18 255.255.255.252
 clock rate 64000
 no shutdown

interface Serial0/1/0
 ip address 10.0.0.10 255.255.255.252
 clock rate 64000
 no shutdown
```

#### Configuring B3 Router
```bash
interface FastEthernet0/0
 ip address 172.20.0.1 255.255.0.0
 no shutdown

interface FastEthernet0/1
 ip address 172.20.0.2 255.255.0.0
 no shutdown

interface FastEthernet1/0
 ip address 172.20.0.3 255.255.0.0
 no shutdown

interface FastEthernet1/1
 ip address 172.20.0.4 255.255.0.0
 no shutdown

interface Serial0/0/0
 ip address 10.0.0.14 255.255.255.252
 clock rate 64000
 no shutdown

interface Serial0/0/1
 ip address 10.0.0.11 255.255.255.252
 clock rate 64000
 no shutdown
```

### OSPF Configuration
```bash
router ospf 1
 network 192.168.0.128 0.0.0.127 area 0
 network 192.168.1.0 0.0.0.255 area 0
 network 172.16.0.0 0.0.255.255 area 0
 network 172.20.0.0 0.0.255.255 area 0
 network 10.0.0.0 0.0.0.255 area 0
```

### DNS Configuration
```bash
ip dns server
ip domain-lookup
ip name-server 8.8.8.8
```

###

 Web Server Configuration
```bash
ip http server
```

### Testing Commands
```bash
# On any PC
ipconfig

# From any device
ping 209.165.200.224  # Pinging the web server
```

These configurations should be applied to each respective device and interface as per the table provided. Ensure that the OSPF configuration is consistent across all routers to enable proper routing of the network.
