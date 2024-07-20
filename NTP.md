# NTP

การตั้งค่า Network Time Protocol (NTP) บน Router หรือ Switch ช่วยให้เครือข่ายมีการซิงโครไนซ์เวลาที่ถูกต้องและแม่นยำ ซึ่งเป็นสิ่งสำคัญสำหรับการตรวจสอบและบันทึกเหตุการณ์ต่างๆ ในเครือข่าย

## การตั้งค่า NTP

### 1. เข้าสู่โหมด Configuration

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```

### 2. ตั้งค่า NTP Server

1. กำหนด NTP Server ที่ต้องการใช้งาน (เช่น 192.168.1.100)
2. ตั้งค่าเวลาที่จะถูกซิงโครไนซ์จาก NTP Server

``` CLI
Router(config)# ntp server <NTP_SERVER_IP>
```

### 3. ตั้งค่า NTP Authentication (ไม่บังคับ)

เพื่อเพิ่มความปลอดภัย คุณสามารถตั้งค่า NTP Authentication เพื่อให้แน่ใจว่า Router หรือ Switch จะซิงโครไนซ์เวลาจาก NTP Server ที่ถูกต้องเท่านั้น

1. สร้าง key และกำหนดหมายเลข key (เช่น 1) และรหัสผ่าน
2. กำหนด key เป็น trusted key
3. กำหนดให้ NTP Server ใช้ key นั้น

``` CLI
Router(config)# ntp authentication-key 1 md5 <PASSWORD>
Router(config)# ntp authenticate
Router(config)# ntp trusted-key 1
Router(config)# ntp server <NTP_SERVER_IP> key 1
```

แทนที่ `<PASSWORD>` ด้วยรหัสผ่านที่คุณต้องการและ `<NTP_SERVER_IP>` ด้วย IP Address ของ NTP Server

### 4. ตั้งค่า NTP Client (ไม่บังคับ)

หากต้องการให้ Router หรือ Switch ทำหน้าที่เป็น NTP Server ให้กับอุปกรณ์อื่นในเครือข่าย คุณสามารถตั้งค่า NTP Client บนอุปกรณ์เหล่านั้น

``` CLI
Router(config)# ntp master <STRATUM_LEVEL>
```

แทนที่ `<STRATUM_LEVEL>` ด้วยระดับ stratum ที่คุณต้องการ (ค่าตั้งแต่ 1 ถึง 15 โดยค่าเริ่มต้นคือ 8)

## การตรวจสอบการตั้งค่า NTP

1. ดูสถานะ NTP

    ``` CLI
    Router# show ntp status
    ```

2. ดูรายละเอียด NTP associations

    ``` CLI
    Router# show ntp status
    ```

## ตัวอย่างการตั้งค่าทั้งหมด

``` CLI
Router> enable
Router# configure terminal
Router(config)# ntp server 192.168.1.100
Router(config)# ntp authentication-key 1 md5 MySecurePassword
Router(config)# ntp authenticate
Router(config)# ntp trusted-key 1
Router(config)# ntp server 192.168.1.100 key 1
Router(config)# ntp master 5
Router(config)# end
Router# show ntp status
Router# show ntp associations
```
