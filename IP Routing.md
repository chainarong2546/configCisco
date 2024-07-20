# IP Routing

การตั้งค่า IP Routing มีสองวิธีหลัก ๆ คือ

- Static Routing และการใช้
- Dynamic Routing Protocols
  - OSPF (Open Shortest Path First)
  - EIGRP (Enhanced Interior Gateway Routing Protocol)
  - BGP ** ไม่มีตัวอย่าง

## การตั้งค่า Static Route

Static Routing เป็นการกำหนดเส้นทางโดยตรงจาก router หนึ่งไปยัง router อื่นโดยการตั้งค่า manual

### 1. เข้าสู่โหมด Configuration

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. กำหนดเส้นทาง Route

``` CLI
Router(config)# ip route <DESTINATION_NETWORK> <SUBNET_MASK> <NEXT_HOP_IP>
Router(config)# end
```

แทนที่ `<DESTINATION_NETWORK>` ด้วยเครือข่ายปลายทาง, `<SUBNET_MASK>` ด้วย subnet mask ของเครือข่ายปลายทาง และ `<NEXT_HOP_IP>` ด้วย IP Address ของ router ถัดไป

ตัวอย่าง:

``` CLI
Router(config)# ip route 192.168.2.0 255.255.255.0 10.1.1.2
```

## การตั้งค่า Dynamic Routing Protocols (OSPF)

### 1. เข้าสู่โหมด Configuration_

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. เปิดใช้งาน OSPF และกำหนด process ID

``` CLI
Router(config)# router ospf 1
Router(config-router)# network <NETWORK> <WILDCARD_MASK> area <AREA_ID>
Router(config-router)# end
```

แทนที่ `<NETWORK>` ด้วยเครือข่ายที่ต้องการประกาศ, `<WILDCARD_MASK>` ด้วย wildcard mask ของเครือข่าย และ `<AREA_ID>` ด้วย area ID ของ OSPF

ตัวอย่าง:

``` CLI
Router(config)# router ospf 1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# end
```

## การตั้งค่า Dynamic Routing Protocols (EIGRP)

### 1. เข้าสู่โหมด Configuration__

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. เปิดใช้งาน EIGRP และกำหนด autonomous system number

``` CLI
Router(config)# router eigrp 100
Router(config-router)# network <NETWORK> <WILDCARD_MASK>
Router(config-router)# end
```

แทนที่ `<NETWORK>` ด้วยเครือข่ายที่ต้องการประกาศ, `<WILDCARD_MASK>` ด้วย wildcard mask ของเครือข่าย

ตัวอย่าง:

``` CLI
Router(config)# router eigrp 100
Router(config-router)# network 192.168.1.0 0.0.0.255
Router(config-router)# end
```

## การตรวจสอบการตั้งค่า Routing

1. ดูตาราง Routing

   ``` CLI
   Router# show ip route
   ```

2. ดูสถานะ OSPF

   ``` CLI
   Router# show ip ospf neighbor
   ```

3. ดูสถานะ EIGRP

   ``` CLI
   Router# show ip eigrp neighbors
   ```

## ตัวอย่างการตั้งค่าทั้งหมด

### Static Routing

``` CLI
Router> enable
Router# configure terminal
Router(config)# ip route 192.168.2.0 255.255.255.0 10.1.1.2
Router(config)# end
Router# show ip route
```

### OSPF

``` CLI
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# end
Router# show ip ospf neighbor
```

### EIGRP

``` CLI
Router> enable
Router# configure terminal
Router(config)# router eigrp 100
Router(config-router)# network 192.168.1.0 0.0.0.255
Router(config-router)# end
Router# show ip eigrp neighbors
```
