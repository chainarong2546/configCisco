# VLAN

## การตั้งค่า VLAN ที่ Switch

### 1. เข้าสู่โหมด Configuration

``` CLI
Switch> enable
Switch# configure terminal
Switch(config)#
```

### 2. สร้าง VLAN

ใช้คำสั่ง `vlan <VLAN_ID>` เพื่อสร้าง VLAN

``` CLI
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit
Switch(config)#
```

### 3. กำหนดพอร์ตให้กับ VLAN

1. เลือกพอร์ตที่ต้องการกำหนดให้กับ VLAN โดยใช้คำสั่ง `interface <interface_id>`
2. กำหนดพอร์ตให้เป็น access mode และ ตั้งให้กับ VLAN ที่ต้องการ

``` CLI
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
Switch(config)#
```

### 4. ตรวจสอบการตั้งค่า

ใช้คำสั่ง `show vlan brief` เพื่อดูการตั้งค่า VLAN ที่สร้างขึ้น

``` CLI
Switch# show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/2, Fa0/3, Fa0/4, Fa0/5
10   Sales                            active    Fa0/1
```

## ตัวอย่างการตั้งค่าทั้งหมด (VLAN ที่ Switch)

``` CLI
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
Switch(config)# end
Switch# show vlan brief
```
