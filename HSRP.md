# HSRP

การตั้งค่า Hot Standby Router Protocol (HSRP) ช่วยเพิ่มความมั่นคงของการเชื่อมต่อเครือข่าย โดยการให้ routers หลายตัวทำงานร่วมกันเพื่อให้ความพร้อมใช้งานสูงสุด (high availability) หาก router ตัวหนึ่งล้มเหลว router อีกตัวจะเข้ามาทำงานแทน

## การตั้งค่า HSRP ที่ Router

### 1. เข้าสู่โหมด Configuration

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. กำหนดค่าพื้นฐาน HSRP บน Router ทั้งสองตัว

#### Router 1 (Primary)

1. เลือก Interface ที่ต้องการตั้งค่า HSRP
2. กำหนด IP Address ให้กับ Interface
3. เปิดใช้งาน HSRP และกำหนดหมายเลขกลุ่ม HSRP (เช่น 1)
4. กำหนด IP Address เสมือน (Virtual IP) ที่ Router ทั้งสองจะใช้ร่วมกัน
5. กำหนด Priority สูงกว่าอีกตัวเพื่อให้เป็น Primary

``` CLI
Router1(config)# interface GigabitEthernet 0/0
Router1(config-if)# ip address 192.168.1.2 255.255.255.0
Router1(config-if)# standby 1 ip 192.168.1.1
Router1(config-if)# standby 1 priority 110
Router1(config-if)# standby 1 preempt
Router1(config-if)# exit
```

#### Router 2 (Secondary)

1. เลือก Interface ที่ต้องการตั้งค่า HSRP
2. กำหนด IP Address ให้กับ Interface
3. เปิดใช้งาน HSRP และกำหนดหมายเลขกลุ่ม HSRP (เช่น 1)
4. กำหนด IP Address เสมือน (Virtual IP) ที่ Router ทั้งสองจะใช้ร่วมกัน
5. กำหนด Priority ต่ำกว่า Primary

 ``` CLI
 Router2(config)# interface GigabitEthernet 0/0
 Router2(config-if)# ip address 192.168.1.3 255.255.255.0
 Router2(config-if)# standby 1 ip 192.168.1.1
 Router2(config-if)# standby 1 priority 100
 Router2(config-if)# standby 1 preempt
 Router2(config-if)# exit
 ```

## การตรวจสอบการตั้งค่า HSRP

``` CLI
Router1# show standby brief
```

``` CLI
Router2# show standby brief
```

## ตัวอย่างการตั้งค่าทั้งหมด

1. Router 1 (Primary)

    ``` CLI
    Router1> enable
    Router1# configure terminal
    Router1(config)# interface GigabitEthernet 0/0
    Router1(config-if)# ip address 192.168.1.2 255.255.255.0
    Router1(config-if)# standby 1 ip 192.168.1.1
    Router1(config-if)# standby 1 priority 110
    Router1(config-if)# standby 1 preempt
    Router1(config-if)# exit
    ```

2. Router 2 (Secondary)

    ``` CLI
    Router2> enable
    Router2# configure terminal
    Router2(config)# interface GigabitEthernet 0/0
    Router2(config-if)# ip address 192.168.1.3 255.255.255.0
    Router2(config-if)# standby 1 ip 192.168.1.1
    Router2(config-if)# standby 1 priority 100
    Router2(config-if)# standby 1 preempt
    Router2(config-if)# exit
    ```
