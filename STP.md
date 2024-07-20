# STP

การตั้งค่า Spanning Tree Protocol (STP) สามารถช่วยป้องกันปัญหา loop ในเครือข่าย LAN ได้ STP มักจะเปิดใช้งานโดยค่าเริ่มต้น แต่เราสามารถกำหนดค่าเพิ่มเติมได้ เช่น การกำหนดค่ารูท (Root) Bridge

## การตั้งค่า STP ที่ Switch

### 1. เข้าสู่โหมด Configuration

``` CLI
Switch> enable
Switch# configure terminal
Switch(config)#
```

### 2. กำหนดค่ารูท (Root) Bridge

ให้ Switch หนึ่งในเครือข่ายเป็นรูท Bridge โดยการตั้ง Priority ต่ำสุด (ค่า Priority เริ่มต้นคือ 32768)

``` CLI
Switch(config)# spanning-tree vlan 1 priority 4096
```

### 3. กำหนดค่ารูทสำรอง (Secondary Root)

ให้ Switch อีกตัวหนึ่งเป็นรูทสำรอง (ค่า Priority รองลงมา)

``` CLI
Switch_2(config)# spanning-tree vlan 1 priority 8192
```

## ปรับแต่งการตั้งค่าเพิ่มเติม (ไม่บังคับ)

### 1. เปิดใช้งาน Rapid Spanning Tree Protocol (RSTP)

ใช้คำสั่ง `spanning-tree mode rapid-pvst` เพื่อเปิดใช้งาน RSTP

``` CLI
Switch(config)# spanning-tree mode rapid-pvst
```

### 2. กำหนดค่า PortFast

ใช้คำสั่ง `spanning-tree portfast` บนพอร์ตที่เชื่อมต่อกับอุปกรณ์ที่ไม่ใช่สวิตช์ เช่น PC หรือเซิร์ฟเวอร์ เพื่อเร่งการสร้าง connection

``` CLI
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# spanning-tree portfast
Switch(config-if)# exit
```

### 3. เปิดใช้งาน BPDU Guard

ช่วยป้องกันการเกิด loop โดยการปิดพอร์ตที่ได้รับ BPDU บนพอร์ตที่มีการเปิดใช้งาน PortFast

``` CLI
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# spanning-tree bpduguard enable
Switch(config-if)# exit
```

## ตรวจสอบการตั้งค่า STP

1. ดูสถานะ STP

    ``` CLI
    Switch# show spanning-tree
    ```

2. ดูพอร์ตที่มีการเปิดใช้งาน PortFast:

    ``` CLI
    Switch# show spanning-tree interface FastEthernet 0/1 portfast
    ```

## ตัวอย่างการตั้งค่าทั้งหมด

``` CLI
Switch> enable
Switch# configure terminal
Switch(config)# spanning-tree vlan 1 priority 4096
Switch(config)# spanning-tree vlan 1 priority 8192
Switch(config)# spanning-tree mode rapid-pvst
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# spanning-tree portfast
Switch(config-if)# spanning-tree bpduguard enable
Switch(config-if)# exit
Switch(config)#
Switch# show spanning-tree
Switch# show spanning-tree interface FastEthernet 0/1 portfast
```
