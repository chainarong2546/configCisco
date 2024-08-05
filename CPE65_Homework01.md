### Addressing Table

| Device      | Interface | IP Address       | Subnet Mask      |
|-------------|-----------|------------------|------------------|
| R1 (HQ)     | S0/0      | 10.0.0.1         | 255.255.255.252  |
|             | S0/1      | 10.0.0.5         | 255.255.255.252  |
|             | S0/2      | 10.0.0.9         | 255.255.255.252  |
|             | S0/3      | 10.0.0.13        | 255.255.255.252  |
|             | S1/0      | 209.165.201.2    | 255.255.255.252  |
| B1          | Fa0/0     | 192.168.1.1      | 255.255.255.0    |
|             | Fa0/1     | 192.168.1.2      | 255.255.255.0    |
|             | Fa1/0     | 192.168.1.3      | 255.255.255.0    |
|             | Fa1/1     | 192.168.1.4      | 255.255.255.0    |
|             | S0/0      | 10.0.0.2         | 255.255.255.252  |
| B2          | Fa0/0     | 172.16.0.1       | 255.255.0.0      |
|             | Fa0/1     | 172.16.0.2       | 255.255.0.0      |
|             | Fa1/0     | 172.16.0.3       | 255.255.0.0      |
|             | Fa1/1     | 172.16.0.4       | 255.255.0.0      |
|             | S0/0      | 10.0.0.6         | 255.255.255.252  |
| B3          | Fa0/0     | 172.20.0.1       | 255.255.0.0      |
|             | Fa0/1     | 172.20.0.2       | 255.255.0.0      |
|             | Fa1/0     | 172.20.0.3       | 255.255.0.0      |
|             | Fa1/1     | 172.20.0.4       | 255.255.0.0      |
|             | S0/0      | 10.0.0.10        | 255.255.255.252  |
| B4          | Fa0/0     | Not specified    | Not specified    |
|             | Fa0/1     | Not specified    | Not specified    |
|             | Fa1/0     | Not specified    | Not specified    |
|             | Fa1/1     | Not specified    | Not specified    |
|             | S0/0      | Not specified    | Not specified    |
| ISP         | S0/0      | 209.165.201.1    | 255.255.255.252  |
|             | Fa0/0     | 209.165.200.225  | 255.255.255.252  |
| Web Server  | NIC       | 209.165.200.226  | 255.255.255.252  |

This table is based on the network diagram provided. Adjust any unspecified IP addresses and subnet masks based on your network requirements.



ในการตั้งค่า OSPF (Open Shortest Path First) บนอุปกรณ์ Cisco Router คุณสามารถใช้คำสั่งต่อไปนี้สำหรับการตั้งค่าเบื้องต้น:

### ตัวอย่างการตั้งค่า OSPF บน Router R1
```plaintext
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# network 10.0.0.0 0.0.0.3 area 0
Router(config-router)# network 10.0.0.4 0.0.0.3 area 0
Router(config-router)# network 10.0.0.8 0.0.0.3 area 0
Router(config-router)# network 10.0.0.12 0.0.0.3 area 0
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# exit
Router(config)# end
Router# write memory
```

### ตัวอย่างการตั้งค่า OSPF บน Router B1
```plaintext
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# network 10.0.0.0 0.0.0.3 area 0
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# exit
Router(config)# end
Router# write memory
```

### ตัวอย่างการตั้งค่า OSPF บน Router B2
```plaintext
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# network 10.0.0.4 0.0.0.3 area 0
Router(config-router)# network 172.16.0.0 0.0.255.255 area 0
Router(config-router)# exit
Router(config)# end
Router# write memory
```

### ตัวอย่างการตั้งค่า OSPF บน Router B3
```plaintext
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# network 10.0.0.8 0.0.0.3 area 0
Router(config-router)# network 172.20.0.0 0.0.255.255 area 0
Router(config-router)# exit
Router(config)# end
Router# write memory
```

### ตัวอย่างการตั้งค่า OSPF บน Router B4
```plaintext
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# exit
Router(config)# end
Router# write memory
```

### ตัวอย่างการตั้งค่า OSPF บน Router ISP
```plaintext
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# network 209.165.201.0 0.0.0.3 area 0
Router(config-router)# network 209.165.200.224 0.0.0.3 area 0
Router(config-router)# exit
Router(config)# end
Router# write memory
```

ในตัวอย่างข้างต้น เราได้กำหนด `network` commands สำหรับ interface ที่ต้องการใช้ OSPF และระบุ area เป็น `0` ซึ่งเป็น backbone area ของ OSPF คุณสามารถปรับเปลี่ยน area และ IP address ตามที่คุณต้องการได้

### สรุปการตั้งค่า OSPF
1. เข้าโหมดการตั้งค่าของ Router ด้วย `enable` และ `configure terminal`
2. เข้าโหมดการตั้งค่า OSPF ด้วย `router ospf <process-id>`
3. ใช้คำสั่ง `network` เพื่อระบุ network ที่ต้องการให้ OSPF ทำงาน
4. ออกจากโหมดการตั้งค่าและบันทึกการตั้งค่าด้วย `end` และ `write memory`

ปรับค่าตามโครงสร้างเครือข่ายและความต้องการเฉพาะของคุณ
