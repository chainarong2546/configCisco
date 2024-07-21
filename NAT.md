# NAT / PAT

มีสองประเภทหลักของ NAT ที่ใช้กันทั่วไปคือ Static NAT และ Dynamic NAT (PAT - Port Address Translation)

## การตั้งค่า Static NAT

Static NAT ใช้ในการแปลที่อยู่ IP ภายในเครือข่ายไปยังที่อยู่ IP ภายนอกแบบคงที่ (one-to-one mapping)

### 1. เข้าสู่โหมด Configuration

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. กำหนดการแปล IP

``` CLI
Router(config)# ip nat inside source static 192.168.1.10 203.0.113.5
```

### 3. กำหนด Interfaces

``` CLI
Router(config)# interface FastEthernet 0/0
Router(config-if)# ip nat inside
Router(config-if)# exit
Router(config)# interface FastEthernet 0/1
Router(config-if)# ip nat outside
Router(config-if)# exit
Router(config)#
```

## การตั้งค่า Dynamic NAT (PAT)

Dynamic NAT ใช้ในการแปลหลายๆ ที่อยู่ IP ภายในไปยังที่อยู่ IP ภายนอกแบบไดนามิก โดยใช้ Pool ของ IP ที่กำหนด

### 1. เข้าสู่โหมด Configuration_

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. กำหนด Pool ของ IP ภายนอก (ทำหรือไม่ทำก็ได้)

``` CLI
Router(config)# ip nat pool MY_POOL 203.0.113.10 203.0.113.20 netmask 255.255.255.0
```

### 3. กำหนด Access List เพื่ออนุญาตให้ IP ภายในเข้าถึง Pool

``` CLI
Router(config)# access-list 1 permit 192.168.1.0 0.0.0.255
```

### 4. กำหนดการแปล IP แบบ Dynamic NAT

``` CLI
Router(config)# ip nat inside source list 1 pool MY_POOL overload
```

หรือ

``` CLI
Router(config)# ip nat inside source list 1 interface <INTERFACE NAME> overload
```

### 5. กำหนด Interfaces

``` CLI
Router(config)# interface FastEthernet 0/0
Router(config-if)# ip nat inside
Router(config-if)# exit
Router(config)# interface FastEthernet 0/1
Router(config-if)# ip nat outside
Router(config-if)# exit
Router(config)#
```

## การตรวจสอบการตั้งค่า NAT

1. ดูการแมป NAT

   ``` CLI
   Router# show ip nat translations
   ```

2. ดูสถิติการใช้งาน NAT

   ``` CLI
   Router# show ip nat statistics
   ```

## ตัวอย่างการตั้งค่าทั้งหมด (Dynamic NAT)

``` CLI
Router> enable
Router# configure terminal
Router(config)# ip nat pool MY_POOL 203.0.113.10 203.0.113.20 netmask 255.255.255.0
Router(config)# access-list 1 permit 192.168.1.0 0.0.0.255
Router(config)# ip nat inside source list 1 pool MY_POOL overload
Router(config)# interface FastEthernet 0/0
Router(config-if)# ip nat inside
Router(config-if)# exit
Router(config)# interface FastEthernet 0/1
Router(config-if)# ip nat outside
Router(config-if)# exit
Router(config)#
Router# show ip nat translations
Router# show ip nat statistics
```
