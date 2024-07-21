# BasicConfig

## ตั้งค่า Hostname และ Password

``` CLI
Router> enable
Router# configure terminal
Router(config)# hostname [ชื่ออุปกรณ์]
Router(config)# enable secret [password]
Router(config)# line console 0
Router(config-line)# password [password]
Router(config-line)# login
Router(config)# exit
Router(config)# line vty 0 4
Router(config-line)# password [password]
Router(config-line)# login
Router(config-line)# exit
```

## ตั้งค่า logging synchronous

``` CLI
Router(config)# line console 0
Router(config)# logging synchronous
```

## ตั้งค่า IP Address ให้กับ แต่ละ Interface

``` CLI
Router(config)# interface [ชื่ออินเตอร์เฟส]
Router(config-if)# ip address [IP Address] [Subnet Mask]
Router(config-if)# no shutdown
Router(config-if)# duplex full
Router(config-if)# speed 1000
Router(config-if)# exit
```
