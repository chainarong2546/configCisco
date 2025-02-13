# โจทย์สำหรับฝึกแบ่ง IP Address

## โจทย์ที่ 1

คุณได้รับ IP Address ชุดหนึ่งคือ `10.0.0.0/16` และคุณต้องการแบ่งเครือข่ายนี้ออกเป็นเครือข่ายย่อยที่มีจำนวนโฮสต์ต่างกันดังนี้:

1. เครือข่ายที่ 1: มีจำนวนโฮสต์ 500 เครื่อง
2. เครือข่ายที่ 2: มีจำนวนโฮสต์ 200 เครื่อง
3. เครือข่ายที่ 3: มีจำนวนโฮสต์ 50 เครื่อง
4. เครือข่ายที่ 4: มีจำนวนโฮสต์ 30 เครื่อง

<details>
  <summary>เฉลย</summary>

  ### เฉลย

  **เครือข่ายที่ 1: มีจำนวนโฮสต์ 500 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 512 IP addresses
  - Subnet Mask: /23 (เพราะ 2^(32-23) = 512)
  - Network Address: `10.0.0.0/23`
  - IP Range: `10.0.0.1 - 10.0.1.254`
  - Broadcast Address: `10.0.1.255`

  **เครือข่ายที่ 2: มีจำนวนโฮสต์ 200 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 256 IP addresses
  - Subnet Mask: /24 (เพราะ 2^(32-24) = 256)
  - Network Address: `10.0.2.0/24`
  - IP Range: `10.0.2.1 - 10.0.2.254`
  - Broadcast Address: `10.0.2.255`

  **เครือข่ายที่ 3: มีจำนวนโฮสต์ 50 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 64 IP addresses
  - Subnet Mask: /26 (เพราะ 2^(32-26) = 64)
  - Network Address: `10.0.3.0/26`
  - IP Range: `10.0.3.1 - 10.0.3.62`
  - Broadcast Address: `10.0.3.63`

  **เครือข่ายที่ 4: มีจำนวนโฮสต์ 30 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 32 IP addresses
  - Subnet Mask: /27 (เพราะ 2^(32-27) = 32)
  - Network Address: `10.0.3.64/27`
  - IP Range: `10.0.3.65 - 10.0.3.94`
  - Broadcast Address: `10.0.3.95`

</details>


## โจทย์ที่ 2

คุณได้รับ IP Address ชุดหนึ่งคือ `172.16.0.0/12` และคุณต้องการแบ่งเครือข่ายนี้ออกเป็นเครือข่ายย่อยที่มีจำนวนโฮสต์ต่างกันดังนี้:

1. เครือข่ายที่ 1: มีจำนวนโฮสต์ 1000 เครื่อง
2. เครือข่ายที่ 2: มีจำนวนโฮสต์ 600 เครื่อง
3. เครือข่ายที่ 3: มีจำนวนโฮสต์ 200 เครื่อง
4. เครือข่ายที่ 4: มีจำนวนโฮสต์ 100 เครื่อง

<details>
  <summary>เฉลย</summary>

  ### เฉลย

  **เครือข่ายที่ 1: มีจำนวนโฮสต์ 1000 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 1024 IP addresses (2^10 = 1024)
  - Subnet Mask: /22 (เพราะ 32 - 10 = 22)
  - Network Address: `172.16.0.0/22`
  - IP Range: `172.16.0.1 - 172.16.3.254`
  - Broadcast Address: `172.16.3.255`

  **เครือข่ายที่ 2: มีจำนวนโฮสต์ 600 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 1024 IP addresses (2^10 = 1024)
  - Subnet Mask: /22 (เพราะ 32 - 10 = 22)
  - Network Address: `172.16.4.0/22`
  - IP Range: `172.16.4.1 - 172.16.7.254`
  - Broadcast Address: `172.16.7.255`

  **เครือข่ายที่ 3: มีจำนวนโฮสต์ 200 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 256 IP addresses (2^8 = 256)
  - Subnet Mask: /24 (เพราะ 32 - 8 = 24)
  - Network Address: `172.16.8.0/24`
  - IP Range: `172.16.8.1 - 172.16.8.254`
  - Broadcast Address: `172.16.8.255`

  **เครือข่ายที่ 4: มีจำนวนโฮสต์ 100 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 128 IP addresses (2^7 = 128)
  - Subnet Mask: /25 (เพราะ 32 - 7 = 25)
  - Network Address: `172.16.9.0/25`
  - IP Range: `172.16.9.1 - 172.16.9.126`
  - Broadcast Address: `172.16.9.127`

</details>


## โจทย์ที่ 3

คุณได้รับ IP Address ชุดหนึ่งคือ `192.168.10.0/24` และคุณต้องการแบ่งเครือข่ายนี้ออกเป็นเครือข่ายย่อยที่มีจำนวนโฮสต์ต่างกันดังนี้:

1. เครือข่ายที่ 1: มีจำนวนโฮสต์ 60 เครื่อง
2. เครือข่ายที่ 2: มีจำนวนโฮสต์ 30 เครื่อง
3. เครือข่ายที่ 3: มีจำนวนโฮสต์ 14 เครื่อง
4. เครือข่ายที่ 4: มีจำนวนโฮสต์ 6 เครื่อง

<details>
  <summary>เฉลย</summary>

  ### เฉลย

  **เครือข่ายที่ 1: มีจำนวนโฮสต์ 60 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 64 IP addresses (2^6 = 64)
  - Subnet Mask: /26 (เพราะ 32 - 6 = 26)
  - Network Address: `192.168.10.0/26`
  - IP Range: `192.168.10.1 - 192.168.10.62`
  - Broadcast Address: `192.168.10.63`

  **เครือข่ายที่ 2: มีจำนวนโฮสต์ 30 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 32 IP addresses (2^5 = 32)
  - Subnet Mask: /27 (เพราะ 32 - 5 = 27)
  - Network Address: `192.168.10.64/27`
  - IP Range: `192.168.10.65 - 192.168.10.94`
  - Broadcast Address: `192.168.10.95`

  **เครือข่ายที่ 3: มีจำนวนโฮสต์ 14 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 16 IP addresses (2^4 = 16)
  - Subnet Mask: /28 (เพราะ 32 - 4 = 28)
  - Network Address: `192.168.10.96/28`
  - IP Range: `192.168.10.97 - 192.168.10.110`
  - Broadcast Address: `192.168.10.111`

  **เครือข่ายที่ 4: มีจำนวนโฮสต์ 6 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 8 IP addresses (2^3 = 8)
  - Subnet Mask: /29 (เพราะ 32 - 3 = 29)
  - Network Address: `192.168.10.112/29`
  - IP Range: `192.168.10.113 - 192.168.10.118`
  - Broadcast Address: `192.168.10.119`

</details>


## โจทย์ที่ 4

คุณได้รับ IP Address ชุดหนึ่งคือ `192.168.100.0/22` และคุณต้องการแบ่งเครือข่ายนี้ออกเป็นเครือข่ายย่อยที่มีจำนวนโฮสต์ต่างกันดังนี้:

1. เครือข่ายที่ 1: มีจำนวนโฮสต์ 200 เครื่อง
2. เครือข่ายที่ 2: มีจำนวนโฮสต์ 100 เครื่อง
3. เครือข่ายที่ 3: มีจำนวนโฮสต์ 50 เครื่อง
4. เครือข่ายที่ 4: มีจำนวนโฮสต์ 20 เครื่อง

<details>
  <summary>เฉลย</summary>

  ### เฉลย

  **เครือข่ายที่ 1: มีจำนวนโฮสต์ 200 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 256 IP addresses (2^8 = 256)
  - Subnet Mask: /24 (เพราะ 32 - 8 = 24)
  - Network Address: `192.168.100.0/24`
  - IP Range: `192.168.100.1 - 192.168.100.254`
  - Broadcast Address: `192.168.100.255`

  **เครือข่ายที่ 2: มีจำนวนโฮสต์ 100 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 128 IP addresses (2^7 = 128)
  - Subnet Mask: /25 (เพราะ 32 - 7 = 25)
  - Network Address: `192.168.101.0/25`
  - IP Range: `192.168.101.1 - 192.168.101.126`
  - Broadcast Address: `192.168.101.127`

  **เครือข่ายที่ 3: มีจำนวนโฮสต์ 50 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 64 IP addresses (2^6 = 64)
  - Subnet Mask: /26 (เพราะ 32 - 6 = 26)
  - Network Address: `192.168.101.128/26`
  - IP Range: `192.168.101.129 - 192.168.101.190`
  - Broadcast Address: `192.168.101.191`

  **เครือข่ายที่ 4: มีจำนวนโฮสต์ 20 เครื่อง**
  - ต้องใช้ subnet ที่มีอย่างน้อย 32 IP addresses (2^5 = 32)
  - Subnet Mask: /27 (เพราะ 32 - 5 = 27)
  - Network Address: `192.168.101.192/27`
  - IP Range: `192.168.101.193 - 192.168.101.222`
  - Broadcast Address: `192.168.101.223`

</details>


สำหรับแต่ละโจทย์ คุณต้องคำนวณ Subnet Mask, Network Address, Broadcast Address, และ Usable IP Range ของแต่ละเครือข่ายย่อย ตามที่ได้แสดงในตัวอย่างข้างต้น
