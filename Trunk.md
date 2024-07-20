# Trunk

## การตั้งค่า Trunk ที่ Switch

### 1. เข้าสู่โหมด Configuration

``` CLI
Switch> enable
Switch# configure terminal
Switch(config)#
```

### 2. กำหนดพอร์ตให้เป็น Trunk

1. เลือกพอร์ตที่ต้องการตั้งค่า Trunk โดยใช้คำสั่ง `interface <interface_id>`
2. กำหนดพอร์ตให้เป็น trunk mode และกำหนด VLAN ที่จะอนุญาตให้ผ่านพอร์ตนี้

``` CLI
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20,30
Switch(config-if)# exit
Switch(config)#
```

### 3. กำหนด Native VLAN (ไม่บังคับ)

โดยปกติแล้ว Native VLAN คือ VLAN 1 แต่สามารถเปลี่ยนได้ตามต้องการ

``` CLI
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# switchport trunk native vlan 99
Switch(config-if)# exit
Switch(config)#
```

### 4. ตรวจสอบการตั้งค่า

ใช้คำสั่ง `show interface trunk` เพื่อดูการตั้งค่าของพอร์ต Trunk

``` CLI
Switch# show interface trunk

Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      99

Port        Vlans allowed on trunk
Fa0/1       10,20,30

Port        Vlans allowed and active in management domain
Fa0/1       10,20,30

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       10,20,30
```

## ตัวอย่างการตั้งค่าทั้งหมด (Trunk ที่ Switch)

``` CLI
Switch> enable
Switch# configure terminal
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20,30
Switch(config-if)# switchport trunk native vlan 99
Switch(config-if)# exit
Switch(config)# end
Switch# show interface trunk
```

## คุณสมบัติและการใช้งานของ Native VLAN

Native VLAN เป็น VLAN ที่ใช้ในการส่งข้อมูลที่ไม่ได้ถูก tag (untagged traffic) บนพอร์ต trunk ในกรณีที่อุปกรณ์ฝั่งหนึ่งส่งข้อมูลโดยไม่ใส่ tag ของ VLAN ข้อมูลนั้นจะถูกจัดให้เป็นส่วนหนึ่งของ Native VLAN บนพอร์ต trunk นั้นๆ

1. Default Setting: โดยค่าเริ่มต้น Native VLAN จะถูกตั้งเป็น VLAN 1 บน Cisco Switch แต่สามารถเปลี่ยนแปลงได้
2. Untagged Traffic: ข้อมูลที่ถูกส่งผ่าน trunk port โดยไม่มี tag จะถูกจัดอยู่ใน Native VLAN
3. Compatibility: ช่วยให้สามารถใช้งานร่วมกับอุปกรณ์ที่ไม่ได้สนับสนุน VLAN tagging ได้
