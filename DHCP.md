# DHCP

Dynamic Host Configuration Protocol (DHCP) ใช้ในการจัดการและแจกจ่ายที่อยู่ IP และข้อมูลการตั้งค่าเครือข่ายอื่นๆ ให้กับอุปกรณ์ในเครือข่ายโดยอัตโนมัติ

## การตั้งค่า DHCP Server

### 1. เข้าสู่โหมด Configuration

เพื่อเริ่มต้นการตั้งค่า DHCP คุณต้องเข้าสู่โหมด configuration ของ router

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. กำหนด DHCP Pool

สร้าง DHCP Pool ที่จะใช้ในการแจกจ่ายที่อยู่ IP ให้กับอุปกรณ์ในเครือข่าย

``` CLI
Router(config)# ip dhcp pool MY_POOL
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
Router(config)#
```

### 3. กำหนด IP Address ของ Interface

กำหนด IP Address สำหรับ interface ที่จะเชื่อมต่อกับเครือข่ายที่ใช้ DHCP

``` CLI
Router(config)# interface FastEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)#
```

### 4. ตรวจสอบการตั้งค่า DHCP

ดูรายการที่อยู่ IP ที่ถูกแจกจ่าย

``` CLI
Router# show ip dhcp binding
```

ดูรายละเอียดของ DHCP Pool

``` CLI
Router# show ip dhcp pool
```

# การตั้งค่า DHCP Relay (IP Helper)

หากมี DHCP Server อยู่ในเครือข่ายอื่นและต้องการให้ router ของคุณทำหน้าที่เป็น relay สำหรับ DHCP Requests

### 1. เข้าสู่โหมด Configuration

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. กำหนด IP Helper Address บน Interface

กำหนด IP Helper Address บน interface ที่ต้องการให้ relay DHCP Requests ไปยัง DHCP Server

``` CLI
Router(config)# interface FastEthernet 0/1
Router(config-if)# ip address 10.0.0.1 255.255.255.0
Router(config-if)# ip helper-address 192.168.1.10
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)#
```

โดย IP Helper Address คือที่อยู่ IP ของ DHCP Server ที่ต้องการ relay ไป

### 3. ตรวจสอบการตั้งค่า DHCP Relay

ตรวจสอบสถานะของ Interface

``` CLI
Router# show ip interface brief
```

ตรวจสอบการตั้งค่า IP Helper Address

``` CLI
Router# show running-config | include ip helper-address
```

## ตัวอย่างการตั้งค่าทั้งหมด (DHCP Server)

``` CLI
Router> enable
Router# configure terminal
Router(config)# ip dhcp pool MY_POOL
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
Router(config)# interface FastEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# exit
Router# show ip dhcp binding
Router# show ip dhcp pool
```
