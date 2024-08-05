## Addressing Table

| Device | Interface | IP Address      | Subnet Mask       |
|--------|------------|-----------------|-------------------|
| Web Server | Fa0/0     | 209.165.200.224 | 255.255.255.252   |
| ISP        | Fa0/0     | 209.165.201.1   | 255.255.255.252   |
| HQ         | Fa0/1/0   | 10.0.0.1        | 255.255.255.252   |
| HQ         | Fa0/1/1   | 10.0.0.5        | 255.255.255.252   |
| HQ         | Fa0/0/0   | 10.0.0.9        | 255.255.255.252   |
| HQ         | Fa0/0/1   | 10.0.0.13       | 255.255.255.252   |
| HQ         | Fa0/0     | 192.168.0.129   | 255.255.255.128   |
| B1         | Fa0/0/0   | 10.0.0.2        | 255.255.255.252   |
| B1         | Fa0/0/1   | 192.168.1.1     | 255.255.255.0     |
| B2         | Fa0/0/0   | 10.0.0.6        | 255.255.255.252   |
| B2         | Fa0/0/1   | 172.16.0.1      | 255.255.0.0       |
| B3         | Fa0/0/0   | 10.0.0.10       | 255.255.255.252   |
| B3         | Fa0/1/0   | 172.20.0.1      | 255.255.0.0       |

## คำสั่ง Config OSPF

### HQ Configuration

```plaintext
HQ(config)# router ospf 1
HQ(config-router)# network 10.0.0.0 0.0.0.255 area 0
HQ(config-router)# network 192.168.0.128 0.0.0.127 area 0
HQ(config-router)# exit
HQ(config)# interface fa0/1/0
HQ(config-if)# ip address 10.0.0.1 255.255.255.252
HQ(config-if)# no shutdown
HQ(config-if)# exit
HQ(config)# interface fa0/1/1
HQ(config-if)# ip address 10.0.0.5 255.255.255.252
HQ(config-if)# no shutdown
HQ(config-if)# exit
HQ(config)# interface fa0/0/0
HQ(config-if)# ip address 10.0.0.9 255.255.255.252
HQ(config-if)# no shutdown
HQ(config-if)# exit
HQ(config)# interface fa0/0/1
HQ(config-if)# ip address 10.0.0.13 255.255.255.252
HQ(config-if)# no shutdown
HQ(config-if)# exit
HQ(config)# interface fa0/0
HQ(config-if)# ip address 192.168.0.129 255.255.255.128
HQ(config-if)# no shutdown
HQ(config-if)# exit
```

### B1 Configuration

```plaintext
B1(config)# router ospf 1
B1(config-router)# network 10.0.0.0 0.0.0.255 area 0
B1(config-router)# network 192.168.1.0 0.0.0.255 area 0
B1(config-router)# exit
B1(config)# interface fa0/0/0
B1(config-if)# ip address 10.0.0.2 255.255.255.252
B1(config-if)# no shutdown
B1(config-if)# exit
B1(config)# interface fa0/0/1
B1(config-if)# ip address 192.168.1.1 255.255.255.0
B1(config-if)# no shutdown
B1(config-if)# exit
```

### B2 Configuration

```plaintext
B2(config)# router ospf 1
B2(config-router)# network 10.0.0.0 0.0.0.255 area 0
B2(config-router)# network 172.16.0.0 0.0.255.255 area 0
B2(config-router)# exit
B2(config)# interface fa0/0/0
B2(config-if)# ip address 10.0.0.6 255.255.255.252
B2(config-if)# no shutdown
B2(config-if)# exit
B2(config)# interface fa0/0/1
B2(config-if)# ip address 172.16.0.1 255.255.0.0
B2(config-if)# no shutdown
B2(config-if)# exit
```

### B3 Configuration

```plaintext
B3(config)# router ospf 1
B3(config-router)# network 10.0.0.0 0.0.0.255 area 0
B3(config-router)# network 172.20.0.0 0.0.255.255 area 0
B3(config-router)# exit
B3(config)# interface fa0/0/0
B3(config-if)# ip address 10.0.0.10 255.255.255.252
B3(config-if)# no shutdown
B3(config-if)# exit
B3(config)# interface fa0/1/0
B3(config-if)# ip address 172.20.0.1 255.255.0.0
B3(config-if)# no shutdown
B3(config-if)# exit
```
