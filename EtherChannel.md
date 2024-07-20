# EtherChannel

การตั้งค่า EtherChannel ช่วยเพิ่มแบนด์วิธและความมั่นคงให้กับการเชื่อมต่อเครือข่าย โดยการรวมพอร์ตหลายๆ พอร์ตเข้าด้วยกันเป็นหนึ่งพอร์ตลอจิคัล

## การตั้งค่า EtherChannel บน Switch

### 1. เข้าสู่โหมด Configuration

``` CLI
Switch> enable
Switch# configure terminal
Switch(config)#
```

### 2. เลือกพอร์ตและสร้าง EtherChannel

1. เลือกพอร์ตที่ต้องการรวมเข้าด้วยกัน
2. สร้าง EtherChannel ด้วยคำสั่ง `channel-group` และกำหนดหมายเลข

``` CLI
Switch(config)# interface range FastEthernet 0/1 - 2
Switch(config-if-range)# channel-group 1 mode active
Switch(config-if-range)# exit
```

ในตัวอย่างนี้ พอร์ต FastEthernet 0/1 และ FastEthernet 0/2 จะถูกรวมเข้าด้วยกันเป็น EtherChannel หมายเลข 1 โดยใช้โหมด active (LACP - Link Aggregation Control Protocol)

** ดูรายการโหมดต่างๆที่หัวข้อ _**โหมดของ EtherChannel**_

### 3. กำหนดค่าพอร์ต Channel

1. กำหนดค่าพอร์ต Channel เพื่อให้ใช้งานกับ EtherChannel ที่สร้างขึ้น
2. ตั้งค่าเพิ่มเติมเช่นพอร์ต Trunk หรือ Access ตามต้องการ

``` CLI
Switch(config)# interface Port-channel 1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan all
Switch(config-if)# exit
```

## ตรวจสอบการตั้งค่า

1. ดูสถานะ EtherChannel

    ``` CLI
    Switch# show etherchannel summary
    ```

2. ดูรายละเอียด EtherChannel

    ``` CLI
    Switch# show etherchannel 1 detail
    ```

## ตัวอย่างการตั้งค่าทั้งหมด

``` CLI
Switch> enable
Switch# configure terminal
Switch(config)# interface range FastEthernet 0/1 - 2
Switch(config-if-range)# channel-group 1 mode active
Switch(config-if-range)# exit
Switch(config)# interface Port-channel 1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan all
Switch(config-if)# exit
Switch(config)#
Switch# show etherchannel summary
Switch# show etherchannel 1 detail
```

## โหมดของ EtherChannel

1. **LACP (Link Aggregation Control Protocol):**
   - `active`: พอร์ตจะส่งและตอบสนองต่อ LACP packets
   - `passive`: พอร์ตจะตอบสนองต่อ LACP packets เท่านั้น

2. **PAgP (Port Aggregation Protocol):**
   - `auto`: พอร์ตจะตอบสนองต่อ PAgP packets เท่านั้น
   - `desirable`: พอร์ตจะส่งและตอบสนองต่อ PAgP packets

3. **Static (ไม่ใช้โปรโตคอล):**
   - `on`: พอร์ตจะรวมเข้าด้วยกันโดยไม่ใช้โปรโตคอลใดๆ
