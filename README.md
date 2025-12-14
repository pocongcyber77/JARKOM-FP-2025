# 📡 Final Project - Komunikasi Data dan Jaringan Komputer

<div align="center">

![Project Status](https://img.shields.io/badge/status-completed-success.svg)
![Semester](https://img.shields.io/badge/semester-Gasal%202025%2F2026-blue.svg)
![Tool](https://img.shields.io/badge/tool-Cisco%20Packet%20Tracer-orange.svg)
![License](https://img.shields.io/badge/license-Academic-green.svg)

**Perancangan dan Implementasi Jaringan Komputer untuk Yayasan ARA**

[📋 Daftar Isi](#-daftar-isi) • [🏗️ Topologi](#️-topologi-jaringan) • [📊 Subnetting](#-subnetting) • [⚙️ Konfigurasi](#️-konfigurasi) • [✅ Verifikasi](#-verifikasi)

</div>

---

## 📋 Daftar Isi

- [📖 Informasi Tugas](#-informasi-tugas)
- [🏢 Deskripsi Organisasi](#-deskripsi-organisasi)
- [🏗️ Topologi Jaringan](#️-topologi-jaringan)
- [📊 Subnetting](#-subnetting)
  - [Gedung Utama (VLSM)](#1-subnetting-gedung-utama-vlsm)
  - [Gedung ARA Tech (CIDR)](#2-subnetting-gedung-ara-tech-cidr)
- [⚙️ Konfigurasi](#️-konfigurasi)
  - [IP Addressing](#1-konfigurasi-ip-addressing)
  - [DHCP Configuration](#2-konfigurasi-dhcp)
  - [Static Routing](#3-static-routing)
  - [Dynamic Routing (OSPF/EIGRP)](#4-dynamic-routing-ospfeigrp)
  - [NAT Overload (PAT)](#5-nat-overload-pat)
  - [GRE Tunnel](#6-gre-tunnel)
- [✅ Verifikasi](#-verifikasi)
- [📁 Struktur File](#-struktur-file)
- [👥 Tim](#-tim)

---

## 📖 Informasi Tugas

| Detail | Keterangan |
|--------|------------|
| **Mata Kuliah** | Komunikasi Data dan Jaringan Komputer |
| **Semester** | Gasal 2025/2026 |
| **Jenis** | Final Project (Kelompok) |
| **Deadline** | Minggu, 14 Desember 2025, 23.59 |
| **Tool** | Cisco Packet Tracer |
| **Format Pengumpulan** | File .ZIP berisi: .pkt, .png, .xlsx, .pdf/.md |

---

## 🏢 Deskripsi Organisasi

### Yayasan ARA

Yayasan ARA merupakan organisasi yang membawahi berbagai unit kerja pendidikan dan teknologi. Yayasan ini baru saja membangun sebuah gedung pusat teknologi bernama **ARA Tech**, yang berfungsi sebagai kantor pusat layanan digital.

---

## 🏗️ Topologi Jaringan

### 📍 Lokasi dan Kebutuhan Host

#### 🏛️ Gedung Utama Yayasan ARA

| Unit | Jumlah Host | Keterangan |
|------|-------------|------------|
| Unit SDM Pendidikan | 95 host | - |
| Unit Kurikulum & Penjaminan Mutu | 220 host | - |
| Unit Sarana Prasarana | 45 host | - |
| Unit Pembinaan & Pengawasan Sekolah | 18 host | - |
| Unit IT Pendidikan | 6 host | Server |
| Unit Layanan Operasional Yayasan | 380 host | - |
| **TOTAL** | **764 host** | - |

#### 🏢 Gedung ARA Tech

##### Lantai 1
| Departemen | Jumlah Host | Keterangan |
|------------|-------------|------------|
| Departemen IT Support | 45 host | - |
| Ruang Server & Data Center | 12 host | 12 Server |
| Departemen Cybersecurity | 22 host | 2 Server |

##### Lantai 2
| Departemen | Jumlah Host | Keterangan |
|------------|-------------|------------|
| Departemen Marketing | 35 host | - |
| Departemen Sales | 25 host | - |
| Departemen Human Resources | 25 host | - |

##### Lantai 3
| Departemen | Jumlah Host | Keterangan |
|------------|-------------|------------|
| Departemen R&D | 55 host | 5 Server |
| Departemen People Development | 18 host | - |

##### Lantai 4
| Departemen | Jumlah Host | Keterangan |
|------------|-------------|------------|
| Departemen Keuangan | 28 host | - |
| Departemen Legal | 18 host | - |
| Departemen Customer Service | 40 host | - |

##### Lantai 5
| Departemen | Jumlah Host | Keterangan |
|------------|-------------|------------|
| Executive Office | 12 host | - |
| Guest Lounge | 10 host | - |
| Auditorium | 15 host | - |

**TOTAL Gedung ARA Tech: 360 host**

#### 🏪 Kantor Cabang

| Lokasi | Jumlah Host | Keterangan |
|--------|-------------|------------|
| Regional Office | 40 host | - |

---

### 🗺️ Diagram Topologi

```
                    ┌─────────────────────────────────┐
                    │      INTERNET (8.8.8.8)         │
                    └──────────────┬──────────────────┘
                                   │
                          ┌────────▼────────┐
                          │  Router Utama   │
                          │   (NAT/PAT)    │
                          └────────┬────────┘
                                   │
                    ┌──────────────┴──────────────┐
                    │                             │
         ┌──────────▼──────────┐    ┌────────────▼──────────┐
         │   Gedung Utama      │    │   Gedung ARA Tech     │
         │   Yayasan ARA       │    │   (5 Lantai)          │
         │                     │    │                       │
         │  ┌────────────────┐ │    │  ┌─────────────────┐ │
         │  │ Router Utama   │ │    │  │ Router Lantai 1 │ │
         │  │ Gedung Utama   │ │    │  │ Router Lantai 2 │ │
         │  └────────────────┘ │    │  │ Router Lantai 3 │ │
         │                     │    │  │ Router Lantai 4 │ │
         │  Unit 1: 95 host    │    │  │ Router Lantai 5 │ │
         │  Unit 2: 220 host   │    │  └─────────────────┘ │
         │  Unit 3: 45 host    │    │                       │
         │  Unit 4: 18 host    │    │  Lantai 1: 79 host   │
         │  Unit 5: 6 host     │    │  Lantai 2: 85 host   │
         │  Unit 6: 380 host   │    │  Lantai 3: 73 host   │
         └─────────────────────┘    │  Lantai 4: 86 host   │
                                    │  Lantai 5: 37 host   │
                                    └──────────────────────┘
                                             │
                                    ┌────────▼────────┐
                                    │  Router Cabang  │
                                    │  (GRE Tunnel)   │
                                    └────────┬────────┘
                                             │
                                    ┌────────▼────────┐
                                    │  Kantor Cabang  │
                                    │  40 host        │
                                    └─────────────────┘
```

> **Catatan**: Diagram topologi lengkap dapat dilihat di file `topology.png`

---

## 📊 Subnetting

### 1. Subnetting Gedung Utama (VLSM)

**Alokasi IP**: `10.0.0.0/8` (disediakan untuk Gedung Utama)

#### Perhitungan Kebutuhan Host (dengan cadangan 20%)

| Unit | Host Dibutuhkan | Cadangan 20% | Total Host | Subnet Mask | Prefix |
|------|-----------------|--------------|------------|-------------|--------|
| Unit Layanan Operasional | 380 | 76 | 456 | /23 | 255.255.254.0 |
| Unit Kurikulum & Penjaminan Mutu | 220 | 44 | 264 | /24 | 255.255.255.0 |
| Unit SDM Pendidikan | 95 | 19 | 114 | /25 | 255.255.255.128 |
| Unit Sarana Prasarana | 45 | 9 | 54 | /26 | 255.255.255.192 |
| Unit Pembinaan & Pengawasan Sekolah | 18 | 4 | 22 | /27 | 255.255.255.224 |
| Unit IT Pendidikan | 6 | 2 | 8 | /29 | 255.255.255.248 |

#### Tabel Subnetting VLSM Gedung Utama

| Unit | Network ID | Subnet Mask | Prefix | Broadcast Address | Range IP | Jumlah Host | Cadangan |
|------|------------|-------------|--------|-------------------|----------|-------------|----------|
| Unit Layanan Operasional | 10.0.0.0 | 255.255.254.0 | /23 | 10.0.1.255 | 10.0.0.1 - 10.0.1.254 | 380 | 20% |
| Unit Kurikulum & Penjaminan Mutu | 10.0.2.0 | 255.255.255.0 | /24 | 10.0.2.255 | 10.0.2.1 - 10.0.2.254 | 220 | 20% |
| Unit SDM Pendidikan | 10.0.3.0 | 255.255.255.128 | /25 | 10.0.3.127 | 10.0.3.1 - 10.0.3.126 | 95 | 20% |
| Unit Sarana Prasarana | 10.0.3.128 | 255.255.255.192 | /26 | 10.0.3.191 | 10.0.3.129 - 10.0.3.190 | 45 | 20% |
| Unit Pembinaan & Pengawasan Sekolah | 10.0.3.192 | 255.255.255.224 | /27 | 10.0.3.223 | 10.0.3.193 - 10.0.3.222 | 18 | 20% |
| Unit IT Pendidikan | 10.0.3.224 | 255.255.255.248 | /29 | 10.0.3.231 | 10.0.3.225 - 10.0.3.230 | 6 | 20% |

> **Detail perhitungan lengkap tersedia di file Excel**: `subnetting-gedung-utama.xlsx`

---

### 2. Subnetting Gedung ARA Tech (CIDR)

**Alokasi IP**: `172.16.0.0/12` (disediakan untuk Gedung ARA Tech)

#### 2.1. Subnetting Per Departemen

##### Perhitungan Kebutuhan Host (dengan cadangan 20%)

| Departemen | Lantai | Host Dibutuhkan | Cadangan 20% | Total Host | Subnet Mask | Prefix |
|------------|--------|-----------------|--------------|------------|-------------|--------|
| Ruang Server & Data Center | 1 | 12 | 3 | 15 | /28 | 255.255.255.240 |
| Departemen IT Support | 1 | 45 | 9 | 54 | /26 | 255.255.255.192 |
| Departemen Cybersecurity | 1 | 22 | 5 | 27 | /27 | 255.255.255.224 |
| Departemen Marketing | 2 | 35 | 7 | 42 | /26 | 255.255.255.192 |
| Departemen Sales | 2 | 25 | 5 | 30 | /27 | 255.255.255.224 |
| Departemen Human Resources | 2 | 25 | 5 | 30 | /27 | 255.255.255.224 |
| Departemen R&D | 3 | 55 | 11 | 66 | /26 | 255.255.255.192 |
| Departemen People Development | 3 | 18 | 4 | 22 | /27 | 255.255.255.224 |
| Departemen Keuangan | 4 | 28 | 6 | 34 | /26 | 255.255.255.192 |
| Departemen Legal | 4 | 18 | 4 | 22 | /27 | 255.255.255.224 |
| Departemen Customer Service | 4 | 40 | 8 | 48 | /26 | 255.255.255.192 |
| Executive Office | 5 | 12 | 3 | 15 | /28 | 255.255.255.240 |
| Guest Lounge | 5 | 10 | 2 | 12 | /28 | 255.255.255.240 |
| Auditorium | 5 | 15 | 3 | 18 | /27 | 255.255.255.224 |

#### Tabel Subnetting CIDR Per Departemen

| Departemen | Lantai | Network ID | Subnet Mask | Prefix | Broadcast Address | Range IP | Jumlah Host | Cadangan |
|------------|--------|------------|-------------|--------|-------------------|----------|-------------|----------|
| Ruang Server & Data Center | 1 | 172.16.0.0 | 255.255.255.240 | /28 | 172.16.0.15 | 172.16.0.1 - 172.16.0.14 | 12 | 20% |
| Departemen IT Support | 1 | 172.16.0.16 | 255.255.255.192 | /26 | 172.16.0.63 | 172.16.0.17 - 172.16.0.62 | 45 | 20% |
| Departemen Cybersecurity | 1 | 172.16.0.64 | 255.255.255.224 | /27 | 172.16.0.95 | 172.16.0.65 - 172.16.0.94 | 22 | 20% |
| Departemen Marketing | 2 | 172.16.0.96 | 255.255.255.192 | /26 | 172.16.0.159 | 172.16.0.97 - 172.16.0.158 | 35 | 20% |
| Departemen Sales | 2 | 172.16.0.160 | 255.255.255.224 | /27 | 172.16.0.191 | 172.16.0.161 - 172.16.0.190 | 25 | 20% |
| Departemen Human Resources | 2 | 172.16.0.192 | 255.255.255.224 | /27 | 172.16.0.223 | 172.16.0.193 - 172.16.0.222 | 25 | 20% |
| Departemen R&D | 3 | 172.16.0.224 | 255.255.255.192 | /26 | 172.16.0.255 | 172.16.0.225 - 172.16.0.254 | 55 | 20% |
| Departemen People Development | 3 | 172.16.1.0 | 255.255.255.224 | /27 | 172.16.1.31 | 172.16.1.1 - 172.16.1.30 | 18 | 20% |
| Departemen Keuangan | 4 | 172.16.1.32 | 255.255.255.192 | /26 | 172.16.1.63 | 172.16.1.33 - 172.16.1.62 | 28 | 20% |
| Departemen Legal | 4 | 172.16.1.64 | 255.255.255.224 | /27 | 172.16.1.95 | 172.16.1.65 - 172.16.1.94 | 18 | 20% |
| Departemen Customer Service | 4 | 172.16.1.96 | 255.255.255.192 | /26 | 172.16.1.159 | 172.16.1.97 - 172.16.1.158 | 40 | 20% |
| Executive Office | 5 | 172.16.1.160 | 255.255.255.240 | /28 | 172.16.1.175 | 172.16.1.161 - 172.16.1.174 | 12 | 20% |
| Guest Lounge | 5 | 172.16.1.176 | 255.255.255.240 | /28 | 172.16.1.191 | 172.16.1.177 - 172.16.1.190 | 10 | 20% |
| Auditorium | 5 | 172.16.1.192 | 255.255.255.224 | /27 | 172.16.1.223 | 172.16.1.193 - 172.16.1.222 | 15 | 20% |

#### 2.2. Supernetting (Route Aggregation)

Untuk menyederhanakan routing, beberapa subnet digabungkan menggunakan teknik CIDR (Supernetting):

| CIDR Block | Prefix Baru | Range IP | Subnet yang Digabungkan | Alasan Penggabungan |
|------------|-------------|----------|-------------------------|---------------------|
| 172.16.0.0/25 | /25 | 172.16.0.0 - 172.16.0.127 | Ruang Server & Data Center (/28), IT Support (/26), Cybersecurity (/27) | Semua departemen di Lantai 1, menghemat routing table |
| 172.16.0.128/25 | /25 | 172.16.0.128 - 172.16.0.255 | Marketing (/26), Sales (/27), HR (/27) | Semua departemen di Lantai 2, routing lebih efisien |
| 172.16.1.0/25 | /25 | 172.16.1.0 - 172.16.1.127 | R&D (/26), People Development (/27) | Semua departemen di Lantai 3, mengurangi jumlah route |
| 172.16.1.128/25 | /25 | 172.16.1.128 - 172.16.1.255 | Keuangan (/26), Legal (/27), Customer Service (/26) | Semua departemen di Lantai 4, optimasi routing table |
| 172.16.2.0/26 | /26 | 172.16.2.0 - 172.16.2.63 | Executive Office (/28), Guest Lounge (/28), Auditorium (/27) | Semua departemen di Lantai 5, supernetting untuk efisiensi |

> **Detail perhitungan lengkap tersedia di file Excel**: `subnetting-ara-tech.xlsx`

---

### 3. Subnetting Kantor Cabang

**Alokasi IP**: `192.168.1.0/24`

| Lokasi | Network ID | Subnet Mask | Prefix | Broadcast Address | Range IP | Jumlah Host | Cadangan |
|--------|------------|-------------|--------|-------------------|----------|-------------|----------|
| Regional Office | 192.168.1.0 | 255.255.255.192 | /26 | 192.168.1.63 | 192.168.1.1 - 192.168.1.62 | 40 | 20% |

---

## ⚙️ Konfigurasi

### 1. Konfigurasi IP Addressing

#### 1.1. Gedung Utama

```cisco
! Router Utama Gedung Utama
interface GigabitEthernet0/0
 ip address 10.0.0.1 255.255.254.0  ! Unit Layanan Operasional
!
interface GigabitEthernet0/1
 ip address 10.0.2.1 255.255.255.0   ! Unit Kurikulum & Penjaminan Mutu
!
interface GigabitEthernet0/2
 ip address 10.0.3.1 255.255.255.128 ! Unit SDM Pendidikan
!
interface GigabitEthernet0/3
 ip address 10.0.3.129 255.255.255.192 ! Unit Sarana Prasarana
!
interface Serial0/0/0
 ip address 10.100.0.1 255.255.255.252 ! Link ke Router Utama (Internet)
!
interface Serial0/0/1
 ip address 10.200.0.1 255.255.255.252 ! Link ke Gedung ARA Tech (OSPF/EIGRP)
```

#### 1.2. Gedung ARA Tech

```cisco
! Router Lantai 1
interface GigabitEthernet0/0
 ip address 172.16.0.1 255.255.255.240 ! Ruang Server & Data Center
!
interface GigabitEthernet0/1
 ip address 172.16.0.17 255.255.255.192 ! IT Support
!
interface GigabitEthernet0/2
 ip address 172.16.0.65 255.255.255.224 ! Cybersecurity
!
interface Serial0/0/0
 ip address 10.200.0.2 255.255.255.252 ! Link ke Gedung Utama
!
interface Serial0/0/1
 ip address 10.201.0.1 255.255.255.252 ! Link ke Router Lantai 2 (Static)
```

> **Catatan**: Konfigurasi lengkap untuk semua router tersedia di file Packet Tracer

---

### 2. Konfigurasi DHCP

#### 2.1. DHCP Server di Gedung Utama

```cisco
! Router Utama Gedung Utama - DHCP Configuration
ip dhcp pool UNIT_LAYANAN_OPERASIONAL
 network 10.0.0.0 255.255.254.0
 default-router 10.0.0.1
 dns-server 8.8.8.8 8.8.4.4
!
ip dhcp pool UNIT_KURIKULUM
 network 10.0.2.0 255.255.255.0
 default-router 10.0.2.1
 dns-server 8.8.8.8 8.8.4.4
!
ip dhcp pool UNIT_SDM
 network 10.0.3.0 255.255.255.128
 default-router 10.0.3.1
 dns-server 8.8.8.8 8.8.4.4
!
ip dhcp excluded-address 10.0.0.1 10.0.0.10
ip dhcp excluded-address 10.0.2.1 10.0.2.10
ip dhcp excluded-address 10.0.3.1 10.0.3.10
```

#### 2.2. DHCP Server di Gedung ARA Tech

```cisco
! Router Lantai 1 - DHCP Configuration
ip dhcp pool LANTAI1_SERVER
 network 172.16.0.0 255.255.255.240
 default-router 172.16.0.1
 dns-server 8.8.8.8 8.8.4.4
!
ip dhcp pool LANTAI1_IT_SUPPORT
 network 172.16.0.16 255.255.255.192
 default-router 172.16.0.17
 dns-server 8.8.8.8 8.8.4.4
!
ip dhcp pool LANTAI1_CYBERSECURITY
 network 172.16.0.64 255.255.255.224
 default-router 172.16.0.65
 dns-server 8.8.8.8 8.8.4.4
```

> **Catatan**: Konfigurasi DHCP lengkap untuk semua departemen tersedia di dokumentasi

---

### 3. Static Routing

**Digunakan untuk routing internal antar lantai di Gedung ARA Tech**

#### Router Lantai 1

```cisco
! Static Routes ke Lantai Lain
ip route 172.16.0.128 255.255.255.128 10.201.0.2  ! Lantai 2
ip route 172.16.1.0 255.255.255.128 10.201.0.2    ! Lantai 3
ip route 172.16.1.128 255.255.255.128 10.202.0.2  ! Lantai 4
ip route 172.16.2.0 255.255.255.192 10.202.0.2   ! Lantai 5
```

#### Router Lantai 2

```cisco
! Static Routes
ip route 172.16.0.0 255.255.255.128 10.201.0.1    ! Lantai 1
ip route 172.16.1.0 255.255.255.128 10.203.0.2    ! Lantai 3
ip route 172.16.1.128 255.255.255.128 10.203.0.2  ! Lantai 4
ip route 172.16.2.0 255.255.255.192 10.203.0.2   ! Lantai 5
```

> **Catatan**: Konfigurasi static routing lengkap untuk semua router lantai tersedia di file Packet Tracer

---

### 4. Dynamic Routing (OSPF/EIGRP)

**Digunakan untuk:**
- Koneksi antar Gedung Utama dan Gedung ARA Tech
- Koneksi Gedung ARA Tech dan Kantor Cabang

#### 4.1. OSPF Configuration

##### Router Utama Gedung Utama

```cisco
router ospf 1
 router-id 1.1.1.1
 network 10.0.0.0 0.0.1.255 area 0
 network 10.0.2.0 0.0.0.255 area 0
 network 10.0.3.0 0.0.0.127 area 0
 network 10.200.0.0 0.0.0.3 area 0
```

##### Router Gedung ARA Tech (Lantai 1)

```cisco
router ospf 1
 router-id 2.2.2.2
 network 172.16.0.0 0.0.255.255 area 0
 network 10.200.0.0 0.0.0.3 area 0
 network 10.204.0.0 0.0.0.3 area 0  ! Link ke Kantor Cabang
```

#### 4.2. EIGRP Configuration (Alternatif)

##### Router Utama Gedung Utama

```cisco
router eigrp 100
 network 10.0.0.0
 network 10.200.0.0
 no auto-summary
```

##### Router Gedung ARA Tech

```cisco
router eigrp 100
 network 172.16.0.0
 network 10.200.0.0
 network 10.204.0.0
 no auto-summary
```

> **Catatan**: Pilih salah satu protokol (OSPF atau EIGRP). Konfigurasi lengkap tersedia di file Packet Tracer

---

### 5. NAT Overload (PAT)

**Konfigurasi NAT untuk akses internet**

#### Router Utama (Internet Gateway)

```cisco
! Access List untuk NAT
access-list 1 permit 10.0.0.0 0.0.255.255
access-list 1 permit 172.16.0.0 0.0.255.255
access-list 1 permit 192.168.1.0 0.0.0.255

! NAT Overload (PAT) Configuration
interface Serial0/0/0
 ip address 203.0.113.1 255.255.255.252
 ip nat outside
!
interface GigabitEthernet0/0
 ip nat inside
!
ip nat inside source list 1 interface Serial0/0/0 overload
```

**Verifikasi NAT:**

```cisco
show ip nat translations
show ip nat statistics
```

> **Screenshot verifikasi NAT tersedia di dokumentasi**

---

### 6. GRE Tunnel

**Konfigurasi GRE Tunnel antara Gedung Utama dan Kantor Cabang**

#### Router Utama Gedung Utama

```cisco
! GRE Tunnel Configuration
interface Tunnel0
 ip address 10.250.0.1 255.255.255.252
 tunnel source Serial0/0/0
 tunnel destination 203.0.113.2
 tunnel mode gre ip
!
! Routing melalui GRE Tunnel
router ospf 1
 network 10.250.0.0 0.0.0.3 area 0
```

#### Router Kantor Cabang

```cisco
! GRE Tunnel Configuration
interface Tunnel0
 ip address 10.250.0.2 255.255.255.252
 tunnel source Serial0/0/1
 tunnel destination 203.0.113.1
 tunnel mode gre ip
!
! Routing melalui GRE Tunnel
router ospf 1
 network 10.250.0.0 0.0.0.3 area 0
 network 192.168.1.0 0.0.0.63 area 0
```

**Verifikasi GRE Tunnel:**

```cisco
show interface tunnel0
ping 10.250.0.2  ! Dari Router Gedung Utama
ping 10.250.0.1  ! Dari Router Kantor Cabang
```

> **Screenshot verifikasi GRE Tunnel tersedia di dokumentasi**

---

## ✅ Verifikasi

### 1. Verifikasi Konfigurasi IP

```cisco
show ip interface brief
show ip route
```

### 2. Verifikasi DHCP

```cisco
show ip dhcp binding
show ip dhcp pool
```

### 3. Verifikasi Static Routing

```cisco
show ip route
ping [destination_ip]
traceroute [destination_ip]
```

### 4. Verifikasi Dynamic Routing (OSPF)

```cisco
show ip ospf neighbor
show ip ospf database
show ip route ospf
```

### 5. Verifikasi Dynamic Routing (EIGRP)

```cisco
show ip eigrp neighbors
show ip eigrp topology
show ip route eigrp
```

### 6. Verifikasi NAT

```cisco
show ip nat translations
show ip nat statistics
ping 8.8.8.8  ! Dari host di jaringan lokal
```

### 7. Verifikasi GRE Tunnel

```cisco
show interface tunnel0
ping [ip_destination_via_tunnel]
traceroute [ip_destination_via_tunnel]
```

### 8. Verifikasi Konektivitas End-to-End

**Test Ping dari berbagai lokasi:**

```
✅ Gedung Utama → Gedung ARA Tech
✅ Gedung ARA Tech → Kantor Cabang
✅ Gedung Utama → Kantor Cabang (via GRE Tunnel)
✅ Semua Host → Internet (8.8.8.8)
✅ Host Lantai 1 → Host Lantai 5 (via Static Routing)
```

> **Screenshot lengkap semua verifikasi tersedia di dokumentasi**

---

## 📁 Struktur File

```
FP_Jarkom_Kelompok_XXX_YYY_ZZZ/
│
├── 📄 README.md                          # Dokumentasi utama (file ini)
├── 📄 Dokumentasi_Konfigurasi.pdf        # Dokumentasi lengkap dengan screenshot
│
├── 📂 Packet_Tracer/
│   └── 📄 Jarkom_FP_2025.pkt             # File Packet Tracer lengkap
│
├── 📂 Diagram/
│   └── 📄 topology.png                   # Diagram topologi jaringan
│
├── 📂 Subnetting/
│   ├── 📄 subnetting-gedung-utama.xlsx   # Tabel subnetting VLSM
│   └── 📄 subnetting-ara-tech.xlsx       # Tabel subnetting CIDR
│
└── 📂 Screenshots/
    ├── 📂 IP_Configuration/              # Screenshot konfigurasi IP
    ├── 📂 DHCP/                          # Screenshot konfigurasi DHCP
    ├── 📂 Routing/                       # Screenshot routing (Static & Dynamic)
    ├── 📂 NAT/                           # Screenshot konfigurasi NAT
    ├── 📂 GRE_Tunnel/                    # Screenshot konfigurasi GRE Tunnel
    └── 📂 Verification/                  # Screenshot verifikasi (ping, traceroute)
```

---

## 📝 Catatan Penting

### ⚠️ Persyaratan Tugas

- ✅ Menggunakan Cisco Packet Tracer untuk semua konfigurasi
- ✅ Tidak terlalu bergantung pada GenAI / Subnet Calculator
- ✅ Menggunakan alamat IP private (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16)
- ✅ Cadangan subnet ~20% untuk skalabilitas
- ✅ Semua subnet dapat saling berkomunikasi
- ✅ Tidak hanya mengandalkan default route global

### 📋 Checklist Pengumpulan

- [ ] File Packet Tracer (.pkt) lengkap dan berfungsi
- [ ] Diagram topologi (.png) jelas dan rapi
- [ ] Tabel subnet Excel (.xlsx) lengkap dan akurat
- [ ] Dokumentasi konfigurasi (.pdf atau .md) dengan screenshot
- [ ] Verifikasi konektivitas (ping/traceroute) berhasil
- [ ] Semua file dikompres dalam .ZIP
- [ ] Format nama file sesuai: `FP_Jarkom_kelompok_XXX_YYY_ZZZ.ZIP`

---

## 👥 Tim

| Nama | NRP | Kontribusi |
|------|-----|------------|
| [Nama Anggota 1] | [NRP 1] | [Deskripsi kontribusi] |
| [Nama Anggota 2] | [NRP 2] | [Deskripsi kontribusi] |
| [Nama Anggota 3] | [NRP 3] | [Deskripsi kontribusi] |

---

## 📚 Referensi

- [Cisco Packet Tracer Documentation](https://www.netacad.com/courses/packet-tracer)
- [VLSM Subnetting Guide](https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html)
- [CIDR and Route Aggregation](https://www.cisco.com/c/en/us/support/docs/ip/enhanced-interior-gateway-routing-protocol-eigrp/8606-subnet.html)
- [OSPF Configuration Guide](https://www.cisco.com/c/en/us/td/docs/ios/iproute_ospf/configuration/12-4t/iro-12-4t-book.html)
- [NAT Overload (PAT) Configuration](https://www.cisco.com/c/en/us/support/docs/ip/network-address-translation-nat/13772-12.html)
- [GRE Tunnel Configuration](https://www.cisco.com/c/en/us/support/docs/security-vpn/ipsec-negotiation-ike-protocols/14106-dynamic-gre.html)

---

## 🎓 Informasi Akademik

| Detail | Keterangan |
|--------|------------|
| **Mata Kuliah** | Komunikasi Data dan Jaringan Komputer |
| **Semester** | Gasal 2025/2026 |
| **Dosen** | [Nama Dosen] |
| **Institusi** | [Nama Universitas] |
| **Deadline** | Minggu, 14 Desember 2025, 23.59 |

---

<div align="center">

### 📞 Kontak

Jika ada pertanyaan atau butuh bantuan, silakan hubungi:

**Email**: [email@example.com]  
**GitHub**: [@username](https://github.com/username)

---

**⭐ Jika dokumentasi ini membantu, berikan star! ⭐**

Dibuat dengan ❤️ oleh Tim Kelompok Jarkom FP 2025

**Semoga mendapatkan nilai yang memuaskan! 🎉**

</div>
