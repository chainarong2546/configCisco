# ACL

การตั้งค่า Access Control List (ACL) บน Router หรือ Switch ช่วยให้สามารถควบคุมการเข้าถึงและการส่งผ่านข้อมูลในเครือข่ายได้อย่างมีประสิทธิภาพ

## การตั้งค่า ACL ที่ Router

### 1. เข้าสู่โหมด Configuration

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. สร้าง Standard ACL

1. สร้าง ACL หมายเลข 1 และอนุญาตการเข้าถึงจากเครือข่าย 192.168.1.0/24
2. ปฏิเสธการเข้าถึงจากเครือข่ายอื่น ๆ

``` CLI
Router(config)# access-list 1 permit 192.168.1.0 0.0.0.255
Router(config)# access-list 1 deny any
```

### 3. สร้าง Extended ACL

1. สร้าง ACL หมายเลข 100 และอนุญาตการเข้าถึง HTTP จากเครือข่าย 192.168.1.0/24 ไปยังเครือข่าย 203.0.113.0/24
2. ปฏิเสธการเข้าถึงจากเครือข่ายอื่น ๆ

 ``` CLI
 Router(config)# access-list 100 permit tcp 192.168.1.0 0.0.0.255 203.0.113.0 0.0.0.255 eq 80
 Router(config)# access-list 100 deny ip any any
 ```

### 4. ใช้ ACL บน Interface

1. เลือก Interface ที่ต้องการใช้งาน ACL
2. ใช้คำสั่ง `ip access-group` เพื่อผูก ACL กับ Interface นั้น

 ``` CLI
 Router(config)# interface FastEthernet 0/0
 Router(config-if)# ip access-group 1 in
 Router(config-if)# exit
 ```

 ``` CLI
 Router(config)# interface FastEthernet 0/0
 Router(config-if)# ip access-group 100 in
 Router(config-if)# exit
 ```

## การตรวจสอบการตั้งค่า ACL

1. ดูการตั้งค่า ACL ที่สร้างขึ้น โดยใช้คำสั่ง `show access-lists`

    ``` CLI
    Router# show access-lists
    ```

2. ดูการตั้งค่า ACL บน Interface โดยใช้คำสั่ง `show ip interface`

    ``` CLI
    Router# show ip interface FastEthernet 0/0
    ```

## ตัวอย่างการตั้งค่าทั้งหมด (Extended ACL)

``` CLI
Router> enable
Router# configure terminal
Router(config)# access-list 100 permit tcp 192.168.1.0 0.0.0.255 203.0.113.0 0.0.0.255 eq 80
Router(config)# access-list 100 deny ip any any
Router(config)# interface FastEthernet 0/0
Router(config-if)# ip access-group 100 in
Router(config-if)# exit
Router(config)#
Router# show access-lists
Router# show ip interface FastEthernet 0/0
```
