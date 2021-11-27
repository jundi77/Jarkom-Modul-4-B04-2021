# Jarkom-Modul-4-B04-2021

Naufal Fajar Imani 05111940000007

Jundullah H. R. 05111940000144

Yeremia D Limantara 05111940000232

----

`Note: VLSM=GNS3 CIDR=GNS3`
![CPT Preview](https://user-images.githubusercontent.com/40772378/143675024-7f705bb3-722e-43ee-bd1b-9eb9ec7bdcd9.png)
![GNS3 Preview](https://user-images.githubusercontent.com/40772378/143675087-fd0b21a3-adb2-484b-bb65-c32da99704de.png)
 
Diinginkan struktur node-node pada gambar di atas, di mana tiap-tiap node memiliki IP dari subnet-subnet tertentu, dan dapat berkomunikasi dengan subnet lain dengan perantara router. Kami memilih bahwa untuk GNS3 akan digunakan ip dengan subnet hasil dari pembagian VLSM, dan untuk CPT (Cisco Packet Tracer) akan digunakan ip dengan subnet hasil dari pembagian CIDR.
 
## Tabel Bantu Subnet Mask

Berikut adalah tabel bantu subnet mask yang berguna saat ingin mengetahui subnet mask dari length ip tertentu (/0-/32).

|Subnet Mask    |Length|
|---------------|------|
|0.0.0.0        |/0    |
|128.0.0.0      |/1    |
|192.0.0.0      |/2    |
|224.0.0.0      |/3    |
|240.0.0.0      |/4    |
|248.0.0.0      |/5    |
|252.0.0.0      |/6    |
|254.0.0.0      |/7    |
|255.0.0.0      |/8    |
|255.128.0.0    |/9    |
|255.192.0.0    |/10   |
|255.224.0.0    |/11   |
|255.240.0.0    |/12   |
|255.248.0.0    |/13   |
|255.252.0.0    |/14   |
|255.254.0.0    |/15   |
|255.255.0.0    |/16   |
|255.255.128.0  |/17   |
|255.255.192.0  |/18   |
|255.255.224.0  |/19   |
|255.255.240.0  |/20   |
|255.255.248.0  |/21   |
|255.255.252.0  |/22   |
|255.255.254.0  |/23   |
|255.255.255.0  |/24   |
|255.255.255.128|/25   |
|255.255.255.192|/26   |
|255.255.255.224|/27   |
|255.255.255.240|/28   |
|255.255.255.248|/29   |
|255.255.255.252|/30   |
|255.255.255.254|/31   |
|255.255.255.255|/32   |

## VLSM

Pada VLSM, diperlukan rancangan subnet-subnet yang nanti akan ditentukan IP-nya. Kami menggunakan pengelompokan seperti berikut:

![Shift_VLSM_pembagian](https://user-images.githubusercontent.com/40772378/143675327-15322a84-751b-48fe-88ce-c933ca4d9121.png)

Dari pengelompokkan tersebut, dapat diketahui banyak host yang akan ada di tiap-tiap subnet, sehingga selanjutnya dapat dilakukan penentuan netmask subnet:

| Subnet | Jumlah IP | Netmask | Subnet Mask     |
| ------ | --------- | ------- | --------------- |
| A1     | 101       | 25      | 255.255.255.128 |
| A2     | 701       | 22      | 255.255.252.0   |
| A3     | 2         | 30      | 255.255.255.252 |
| A4     | 2021      | 21      | 255.255.248.0   |
| A5     | 2         | 30      | 255.255.255.252 |
| A6     | 521       | 22      | 255.255.252.0   |
| A7     | 252       | 24      | 255.255.255.0   |
| A8     | 1001      | 22      | 255.255.252.0   |
| A9     | 2         | 30      | 255.255.255.252 |
| A10    | 2         | 30      | 255.255.255.252 |
| A11    | 721       | 22      | 255.255.252.0   |
| A12    | 502       | 23      | 255.255.254.0   |
| A13    | 13        | 28      | 255.255.252.240 |
| Total  | 5841      | 19      | 255.255.224.0   |

Setelah netmask tiap subnet didapat, kemudian dilanjutkan dengan membuat pohon pembagian IP, kami memilih untuk dimulai dari `10.9.0.0` hingga seterusnya:

![Shift_VLSM_tree](https://user-images.githubusercontent.com/40772378/143675330-17139dcc-4a59-4d5e-80a0-f6232a0b0ba8.png)

Dari pohon pembagian IP tersebut, didapat NID (Network ID) untuk tiap-tiap subnet:

|Subnet|NID           |
|------|------------  |
|A1    |10.9.27.0     |
|A2    |10.9.16.0     |
|A3    |10.9.27.144   |
|A4    |10.9.0.0      |
|A5    |10.9.27.148   |
|A6    |10.9.20.0     |
|A7    |10.9.26.0     |
|A8    |10.9.8.0      |
|A9    |10.9.27.152   |
|A10   |10.9.27.156   |
|A11   |10.9.12.0     |
|A12   |10.9.24.0     |
|A13   |10.9.27.128   |

## CIDR

Pada CIDR, diperlukan rancangan subnet-subnet yang nanti akan ditentukan IP-nya beserta netmask-nya. Kami menggunakan hasil dari pengelompokan VLSM, sehingga rancangan subnetnya menjadi seperti berikut:

![CIDR Helper](https://user-images.githubusercontent.com/40772378/143675331-42918a9a-8b0e-4415-9370-c496e53c997c.png)

Dari pengelompokkan tersebut, dilakukan penggabungan tiap-tiap subnet per 2 subnet menjadi 1 subnet, dilakukan terus-menerus hingga seluruh subnet tergabung:

![Shift_CIDR_pembagian](https://user-images.githubusercontent.com/40772378/143675343-cf7ebdbd-d693-41c4-a0bb-c07e3008a8f8.png)

Setelah subnet digabung, maka telah diketahui rancangan pohon IP yang akan dibuat berdasarkan hasil gabungan subnet. Maka untuk pohon pembagian IP menjadi seperti berikut:

![Shift_CIDR_tree](https://user-images.githubusercontent.com/40772378/143675333-1e5bd747-6631-4622-aed4-08a15453119a.png)

Dari pohon pembagian IP tersebut, didapat NID untuk tiap-tiap subnet:

|Subnet|NID         |
|------|------------|
|A1    |10.9.0.0    |
|A2    |10.9.24.0   |
|A3    |10.9.28.0   |
|A4    |10.9.16.0   |
|A5    |10.9.100.0  |
|A6    |10.9.80.0   |
|A7    |10.9.76.0   |
|A8    |10.9.96.0   |
|A9    |10.9.84.0   |
|A10   |10.9.68.0   |
|A11   |10.9.72.0   |
|A12   |10.9.64.0   |
|A13   |10.9.66.0   |

----
## Aset gambar untuk membantu lapres
![Foosha CPT Interface](https://user-images.githubusercontent.com/40772378/143675154-37b202c8-f1b9-45c3-8a53-f14c9167f82d.png)
![Router CPT Interface](https://user-images.githubusercontent.com/40772378/143675172-a4609a93-e0be-4c30-b1e2-f93e66becebc.png)
![Router Interface Config](https://user-images.githubusercontent.com/40772378/143675225-6fdd4f49-2adb-4198-93bb-bc1abcc891ba.png)
![Client Interface Config](https://user-images.githubusercontent.com/40772378/143675240-5062553e-3cdf-4c1a-adbc-c0e1c3415cd4.png)
![Router Routing Table](https://user-images.githubusercontent.com/40772378/143675268-37308b09-b751-423f-b1ce-ff84bd3842f4.png)
![Network config GNS3](https://user-images.githubusercontent.com/40772378/143675359-53467843-0261-4680-bd3c-e1be40545534.png)
![Contoh Syntax Routing Table di Foosha](https://user-images.githubusercontent.com/40772378/143675407-2f4bd58d-7edc-4e0b-b17a-ed2ab7f4eaa8.png)
