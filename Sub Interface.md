# Sub Interface

Sub-interface เป็น interface เสมือน (virtual interface) ที่สร้างขึ้นภายใน physical interface บน router หรือ switch โดยแต่ละ sub-interface สามารถกำหนดค่าต่างๆ เช่น IP address, encapsulation, และ VLAN ID ได้อย่างอิสระ ทำให้หนึ่ง physical interface สามารถจัดการกับการเชื่อมต่อจากหลายๆ VLAN หรือ subnet ได้

## การตั้งค่า Sub Interface บน Router

### 1. เข้าสู่โหมด Configuration

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. สร้าง Sub-interface บน Interface

``` CLI
Router(config)# interface GigabitEthernet0/0
Router(config-if)# no shutdown
```

### 3. สร้าง Sub-interface สำหรับแต่ละ VLAN

``` CLI
Router(config)# interface GigabitEthernet0/0.10
Router(config-if)# encapsulation dot1Q 10
Router(config-if)# ip address 192.168.10.1 255.255.255.0
Router(config-if)# exit
Router(config)# interface GigabitEthernet0/0.20
Router(config-if)# encapsulation dot1Q 20
Router(config-if)# ip address 192.168.20.1 255.255.255.0
Router(config-if)# exit
```

### 4. ตั้งค่า Interface เชื่อมต่อกับ Switch ให้เป็น Trunk (การตั้งค่านี้ทำบน Switch)

``` CLI
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
```
