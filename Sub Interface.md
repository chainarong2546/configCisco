# Sub Interface

Sub-interface เป็น interface เสมือน (virtual interface) ที่สร้างขึ้นภายใน physical interface บน router หรือ switch โดยแต่ละ sub-interface สามารถกำหนดค่าต่างๆ เช่น IP address, encapsulation, และ VLAN ID ได้อย่างอิสระ ทำให้หนึ่ง physical interface สามารถจัดการกับการเชื่อมต่อจากหลายๆ VLAN หรือ subnet ได้

## กรารตั้งค่า Sub Interface

### 1. เข้าสู่โหมด Configuration

``` CLI
Router> enable
Router# configure terminal
Router(config)#
```



