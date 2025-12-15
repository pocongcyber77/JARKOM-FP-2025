# Final Project - Komunikasi Data dan Jaringan Komputer
  ![Project Status](https://img.shields.io/badge/status-completed-success.svg)
  ![Semester](https://img.shields.io/badge/semester-Gasal%202025%2F2026-blue.svg)
  ![Tool](https://img.shields.io/badge/tool-Cisco%20Packet%20Tracer-orange.svg)
  ![License](https://img.shields.io/badge/license-Academic-green.svg)

  ## Dikerjakan Oleh
| Nama                  | NRP        | Peran & Tanggung Jawab                                   |
|-----------------------|------------|------------------------------------------------------------|
| Dina Rahmadani        | 5027241065 | Arsitektur Topologi, CIDR, VLSM, Konfigurasi & Kalkulasi   |
| Ahmad Ibnu Athaillah  | 5027241024 | Unit Testing, Troubleshooting, Dokumentasi & Manual       |


  **Perancangan dan Implementasi Jaringan Komputer untuk Yayasan ARA**

  [Daftar Isi](#daftar-isi) • [Topologi](#topologi-jaringan) • [Subnetting](#subnetting) • [Konfigurasi](#konfigurasi) • [Verifikasi](#verifikasi)

  ---

  ## Daftar Isi

  - [Informasi Tugas](#informasi-tugas)
  - [Deskripsi Organisasi](#deskripsi-organisasi)
  - [Topologi Jaringan](#topologi-jaringan)
  - [Subnetting](#subnetting)
    - [Gedung Utama (VLSM)](#1-subnetting-gedung-utama-vlsm)
    - [Gedung ARA Tech (CIDR)](#2-subnetting-gedung-ara-tech-cidr)
  - [Konfigurasi](#konfigurasi)
    - [IP Addressing](#1-konfigurasi-ip-addressing)
    - [DHCP Configuration](#2-konfigurasi-dhcp)
    - [Static Routing](#3-static-routing)
    - [Dynamic Routing (OSPF/EIGRP)](#4-dynamic-routing-ospfeigrp)
    - [NAT Overload (PAT)](#5-nat-overload-pat)
    - [GRE Tunnel](#6-gre-tunnel)
  - [Verifikasi](#verifikasi)
  - [Struktur File](#struktur-file)
  ---
  ---

  ## Deskripsi Organisasi

  ### Yayasan ARA

  Yayasan ARA merupakan organisasi yang membawahi berbagai unit kerja pendidikan dan teknologi. Yayasan ini baru saja membangun sebuah gedung pusat teknologi bernama **ARA Tech**, yang berfungsi sebagai kantor pusat layanan digital.

  ---

  ## Topologi Jaringan

  ### Lokasi dan Kebutuhan Host

  #### Gedung Utama Yayasan ARA

  | Unit | Jumlah Host | Keterangan |
  |------|-------------|------------|
  | Unit SDM Pendidikan | 95 host | - |
  | Unit Kurikulum & Penjaminan Mutu | 220 host | - |
  | Unit Sarana Prasarana | 45 host | - |
  | Unit Pembinaan & Pengawasan Sekolah | 18 host | - |
  | Unit IT Pendidikan | 6 host | Server |
  | Unit Layanan Operasional Yayasan | 380 host | - |
  | **TOTAL** | **764 host** | - |

  #### Gedung ARA Tech

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

  #### Kantor Cabang

  | Lokasi | Jumlah Host | Keterangan |
  |--------|-------------|------------|
  | Regional Office | 40 host | - |

  ---

  ### Diagram Topologi

  <div align="center">

  ![Topologi Jaringan](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/Topology.jpg)

  *Diagram Topologi Lengkap Jaringan Yayasan ARA*

  </div>

  > **Catatan**: Diagram topologi lengkap dapat dilihat di file [`Assets/Topology.jpg`](Assets/Topology.jpg)

  ---

  ## Subnetting

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

  <div align="center">

  ![VLSM Subnetting](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/VLSM.jpg)

  *Visualisasi Subnetting VLSM Gedung Utama*

  </div>

  | Unit | Network ID | Subnet Mask | Prefix | Broadcast Address | Range IP | Host | Host + 20% |
  |------|------------|-------------|--------|-------------------|----------|------|------------|
  | Unit IT Pendidikan | 10.0.0.0 | 255.255.255.240 | /28 | 10.0.0.15 | 10.0.0.1 – 10.0.0.14 | 6 | 7 |
  | Unit Pembinaan & Pengawasan Sekolah | 10.0.0.32 | 255.255.255.224 | /27 | 10.0.0.63 | 10.0.0.33 – 10.0.0.62 | 18 | 22 |
  | Unit Sarana Prasarana | 10.0.0.64 | 255.255.255.192 | /26 | 10.0.0.127 | 10.0.0.65 – 10.0.0.126 | 45 | 54 |
  | Unit SDM Pendidikan | 10.0.0.128 | 255.255.255.128 | /25 | 10.0.0.255 | 10.0.0.129 – 10.0.0.254 | 95 | 114 |
  | Unit Kurikulum & Penjaminan Mutu | 10.0.2.0 | 255.255.254.0 | /23 | 10.0.3.255 | 10.0.2.1 – 10.0.3.254 | 220 | 264 |
  | Unit Layanan Operasional Yayasan | 10.0.4.0 | 255.255.254.0 | /23 | 10.0.5.255 | 10.0.4.1 – 10.0.5.254 | 380 | 456 |
  | **Router Link** | **10.0.6.0** | **255.255.255.252** | **/30** | **10.0.6.3** | **10.0.6.1 - 10.0.6.2** | **2** | **2** |
  | **TOTAL** | - | - | **/22** | - | - | **764** | **917** |

  > **Detail perhitungan lengkap tersedia di file CSV**: [`Sheet/Pembagian IP - VLSM.csv`](Sheet/Pembagian%20IP%20-%20VLSM.csv)

  **Catatan**: File CSV ini berisi perhitungan lengkap subnetting VLSM untuk semua unit di Gedung Utama, termasuk perhitungan cadangan 20% dan alokasi IP yang efisien.

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

  <div align="center">

  ![CIDR Subnetting](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/CIDR.jpg)

  *Visualisasi Subnetting CIDR Gedung ARA Tech*

  </div>

  | Subnet | Departemen | Network ID | Subnet Mask | Prefix | Broadcast Address | Range IP | Host | Host + 20% |
  |--------|------------|------------|-------------|--------|-------------------|----------|------|------------|
  | A7 | Departemen IT Support | 10.0.6.0 | 255.255.255.192 | /26 | 10.0.6.63 | 10.0.6.1 – 10.0.6.62 | 45 | 54 |
  | A8 | Ruang Server & Data Center (Server) | 10.0.6.64 | 255.255.255.240 | /28 | 10.0.6.79 | 10.0.6.65 – 10.0.6.78 | 12 | 14 |
  | A9 | Departemen Cybersecurity | 10.0.6.128 | 255.255.255.224 | /27 | 10.0.6.159 | 10.0.6.129 – 10.0.6.158 | 22 | 26 |
  | A10 | Departemen Marketing | 10.0.8.0 | 255.255.255.192 | /26 | 10.0.8.63 | 10.0.8.1 – 10.0.8.62 | 35 | 42 |
  | A11 | Departemen Sales | 10.0.8.64 | 255.255.255.224 | /27 | 10.0.8.95 | 10.0.8.65 – 10.0.8.94 | 25 | 30 |
  | A12 | Departemen Human Resources | 10.0.8.128 | 255.255.255.224 | /27 | 10.0.8.159 | 10.0.8.129 – 10.0.8.158 | 25 | 30 |
  | A13 | Departemen R&D | 10.0.14.0 | 255.255.255.128 | /25 | 10.0.14.127 | 10.0.14.1 – 10.0.14.126 | 55 | 66 |
  | A14 | Departemen People Development | 10.0.14.128 | 255.255.255.224 | /27 | 10.0.14.159 | 10.0.14.129 – 10.0.14.158 | 18 | 22 |
  | A15 | Departemen Keuangan | 10.0.22.0 | 255.255.255.192 | /26 | 10.0.22.63 | 10.0.22.1 – 10.0.22.62 | 28 | 34 |
  | A16 | Departemen Legal | 10.0.22.64 | 255.255.255.224 | /27 | 10.0.22.95 | 10.0.22.65 – 10.0.22.94 | 18 | 22 |
  | A17 | Departemen Customer Service | 10.0.22.128 | 255.255.255.192 | /26 | 10.0.22.191 | 10.0.22.129 – 10.0.22.190 | 40 | 48 |
  | A18 | Executive Office | 10.0.23.0 | 255.255.255.240 | /28 | 10.0.23.15 | 10.0.23.1 – 10.0.23.14 | 12 | 14 |
  | A19 | Guest Lounge | 10.0.23.16 | 255.255.255.240 | /28 | 10.0.23.31 | 10.0.23.17 – 10.0.23.30 | 10 | 12 |
  | A20 | Auditorium | 10.0.23.32 | 255.255.255.224 | /27 | 10.0.23.63 | 10.0.23.33 – 10.0.23.62 | 15 | 18 |
  | A21 | Regional Office | 10.0.2.128 | 255.255.255.192 | /26 | 10.0.2.191 | 10.0.2.129 – 10.0.2.190 | 40 | 48 |

  #### 2.2. Supernetting (Route Aggregation)

  Untuk menyederhanakan routing, beberapa subnet digabungkan menggunakan teknik CIDR (Supernetting). Proses penggabungan dilakukan secara bertahap:

  **Tahap I - Penggabungan Level 1:**

  | Subnet | Gabungan dari | Netmask Akhir |
  |--------|---------------|---------------|
  | X1 | A7 (/26) + A8 (/28) | /25 |
  | X2 | A10 (/26) + A11 (/27) | /25 |
  | X3 | A13 (/25) + A14 (/27) | /24 |
  | X4 | A15 (/26) + A16 (/27) | /25 |
  | X5 | A18 (/28) + A19 (/28) | /27 |

  **Tahap II - Penggabungan Level 2:**

  | Subnet | Gabungan dari | Netmask Akhir |
  |--------|---------------|---------------|
  | Y1 | X1 (/25) + A9 (/27) | /24 |
  | Y2 | X2 (/25) + A12 (/27) | /24 |
  | Y3 | X4 (/25) + A17 (/26) | /24 |
  | Y4 | X5 (/27) + A20 (/27) | /26 |

  **Tahap III - Penggabungan Level 3:**

  | Subnet | Gabungan dari | Netmask Akhir |
  |--------|---------------|---------------|
  | W1 | Y1 (/24) + R4-R5 (/30) | /23 |
  | W2 | Y4 (/26) + R7-R8 (/30) | /25 |

  **Tahap IV - Penggabungan Level 4:**

  | Subnet | Gabungan dari | Netmask Akhir |
  |--------|---------------|---------------|
  | Q1 | W1 (/23) + Y2 (/24) | /22 |
  | Q2 | W2 (/25) + Y3 (/24) | /23 |

  **Tahap V - Penggabungan Level 5:**

  | Subnet | Gabungan dari | Netmask Akhir |
  |--------|---------------|---------------|
  | T1 | Q1 (/22) + R5-R6 (/30) | /21 |
  | T2 | Q2 (/23) + R6-R7 (/30) | /22 |

  **Tahap VI - Penggabungan Level 6:**

  | Subnet | Gabungan dari | Netmask Akhir |
  |--------|---------------|---------------|
  | H1 | T1 (/21) + X3 (/24) | /20 |

  **Tahap VII - Penggabungan Level 7:**

  | Subnet | Gabungan dari | Netmask Akhir |
  |--------|---------------|---------------|
  | P1 | H1 (/20) + T2 (/22) | /19 |

  **Tahap VIII - Penggabungan Final:**

  | Subnet | Gabungan dari | Netmask Akhir |
  |--------|---------------|---------------|
  | K1 | P1 (/19) + R6-R2 (/30) | /18 |

  > **Detail perhitungan lengkap tersedia di file CSV**: 
  > - [`Sheet/Penggabungan - CIDR.csv`](Sheet/Penggabungan%20-%20CIDR.csv) - Tabel proses supernetting bertahap
  > - [`Sheet/Pembagian IP - CIDR.csv`](Sheet/Pembagian%20IP%20-%20CIDR.csv) - Tabel subnetting CIDR per departemen

  **Catatan**: File CSV ini berisi perhitungan lengkap subnetting CIDR untuk semua departemen di Gedung ARA Tech, termasuk proses supernetting (route aggregation) yang dilakukan secara bertahap untuk mengoptimalkan routing table.

  ---

  ### 3. Subnetting Kantor Cabang

  **Alokasi IP**: `10.0.2.128/26`

  | Lokasi | Network ID | Subnet Mask | Prefix | Broadcast Address | Range IP | Host | Host + 20% |
  |--------|------------|-------------|--------|-------------------|----------|------|------------|
  | Regional Office | 10.0.2.128 | 255.255.255.192 | /26 | 10.0.2.191 | 10.0.2.129 – 10.0.2.190 | 40 | 48 |

  ### 4. Tabel Routing (Link antar Router)

  | Link Router | Network ID | Subnet Mask | Prefix | Broadcast Address | Range IP |
  |-------------|------------|-------------|--------|-------------------|----------|
  | R1 - R2 | 10.0.0.0 | 255.255.255.252 | /30 | 10.0.0.3 | 10.0.0.1 - 10.0.0.2 |
  | R2 - R3 | 10.0.0.4 | 255.255.255.252 | /30 | 10.0.0.7 | 10.0.0.5 - 10.0.0.6 |
  | R2 - R6 | 10.0.0.8 | 255.255.255.252 | /30 | 10.0.0.11 | 10.0.0.9 - 10.0.0.10 |
  | R4 - R5 | 10.0.0.12 | 255.255.255.252 | /30 | 10.0.0.15 | 10.0.0.13 - 10.0.0.14 |
  | R5 - R6 | 10.0.0.16 | 255.255.255.252 | /30 | 10.0.0.19 | 10.0.0.17 - 10.0.0.18 |
  | R6 - R7 | 10.0.0.20 | 255.255.255.252 | /30 | 10.0.0.23 | 10.0.0.21 - 10.0.0.22 |
  | R7 - R8 | 10.0.0.24 | 255.255.255.252 | /30 | 10.0.0.27 | 10.0.0.25 - 10.0.0.26 |
  | R4 - R5 (Alternatif) | 10.0.7.0 | 255.255.255.252 | /30 | 10.0.7.3 | 10.0.7.1 – 10.0.7.2 |
  | R5 - R6 (Alternatif) | 10.0.10.0 | 255.255.255.252 | /30 | 10.0.10.3 | 10.0.10.1 – 10.0.10.2 |
  | R6 - R7 (Alternatif) | 10.0.24.0 | 255.255.255.252 | /30 | 10.0.24.3 | 10.0.24.1 – 10.0.24.2 |
  | R7 - R8 (Alternatif) | 10.0.23.64 | 255.255.255.252 | /30 | 10.0.23.67 | 10.0.23.65 – 10.0.23.66 |
  | R2 - R6 (Alternatif) | 10.0.38.0 | 255.255.255.252 | /30 | 10.0.38.3 | 10.0.38.1 – 10.0.38.2 |

  > **Detail lengkap tersedia di file CSV**: [`Sheet/Rute.csv`](Sheet/Rute.csv)

  **Catatan**: File CSV ini berisi informasi lengkap tentang semua subnet yang digunakan, termasuk subnet untuk departemen, link antar router, dan total kebutuhan host dengan cadangan 20%.

  ---

  ## Konfigurasi

  ### 1. Konfigurasi IP Addressing

  #### 1.1. Router R1 (Gedung Utama)

  Konfigurasi IP untuk Router R1 yang menghubungkan semua unit di Gedung Utama:

  ```cisco
  enable
  conf t

  interface FastEthernet0/0
  ip address 10.0.6.1 255.255.255.252

  interface FastEthernet1/0 
  ip address 10.0.0.129 255.255.255.128  ! Unit SDM Pendidikan

  interface FastEthernet6/0 
  ip address 10.0.2.1 255.255.254.0      ! Unit Kurikulum & Penjaminan Mutu

  interface FastEthernet7/0 
  ip address 10.0.0.65 255.255.255.192   ! Unit Sarana Prasarana

  interface FastEthernet8/0 
  ip address 10.0.0.33 255.255.255.224   ! Unit Pembinaan & Pengawasan Sekolah

  interface FastEthernet9/0
  ip address 10.0.0.1 255.255.255.240    ! Unit IT Pendidikan

  interface FastEthernet4/0 
  ip address 10.0.4.1 255.255.254.0       ! Unit Layanan Operasional

  no shutdown
  exit
  ```

  > **Konfigurasi lengkap**: [R1.cfg](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Routing/R1.cfg)

  #### 1.2. Router R2 - R8 (Gedung ARA Tech & Kantor Cabang)

  Konfigurasi untuk router-router di Gedung ARA Tech dan Kantor Cabang:

  - **R2**: Router penghubung Gedung ARA Tech ke Kantor Utama
  - **R3**: Router Lantai 1 ARA Tech
  - **R4**: Router Lantai 2 ARA Tech  
  - **R5**: Router Lantai 3 ARA Tech
  - **R6**: Router penghubung utama ARA Tech
  - **R7**: Router Lantai 4 ARA Tech
  - **R8**: Router Lantai 5 ARA Tech & Kantor Cabang

  > **Konfigurasi lengkap semua router tersedia di folder**: [`Routing/`](Routing/)
  > 
  > | File | Router | Fungsi | Link |
  > |------|--------|--------|------|
  > | R1.cfg | R1 | Router Gedung Utama - menghubungkan semua unit | [Lihat Konfigurasi](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Routing/R1.cfg) |
  > | R2.cfg | R2 | Router ARA Tech ke Kantor Utama | [Lihat Konfigurasi](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Routing/R2.cfg) |
  > | R3.cfg | R3 | Router Lantai 1 ARA Tech | [Lihat Konfigurasi](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Routing/R3.cfg) |
  > | R4.cfg | R4 | Router Lantai 2 ARA Tech | [Lihat Konfigurasi](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Routing/R4.cfg) |
  > | R5.cfg | R5 | Router Lantai 3 ARA Tech | [Lihat Konfigurasi](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Routing/R5.cfg) |
  > | R6.cfg | R6 | Router ARA Tech ke Branch | [Lihat Konfigurasi](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Routing/R6.cfg) |
  > | R7.cfg | R7 | Router Lantai 4 ARA Tech | [Lihat Konfigurasi](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Routing/R7.cfg) |
  > | R8.cfg | R8 | Router Lantai 5 & Branch | [Lihat Konfigurasi](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Routing/R8.cfg) |

  **Catatan**: Semua file konfigurasi router menggunakan format Cisco IOS dan dapat langsung di-copy ke Cisco Packet Tracer atau router fisik.

  ---

  ### 2. Konfigurasi DHCP

  #### 2.1. DHCP Server di Router R1 (Gedung Utama)

  Konfigurasi DHCP untuk semua unit di Gedung Utama:

  ```cisco
  ! Excluded Addresses (Gateway & Reserved IPs)
  ip dhcp excluded-address 10.0.0.129
  ip dhcp excluded-address 10.0.2.1
  ip dhcp excluded-address 10.0.0.65
  ip dhcp excluded-address 10.0.0.33
  ip dhcp excluded-address 10.0.0.1
  ip dhcp excluded-address 10.0.4.1

  ! DHCP Pool untuk Unit SDM Pendidikan
  ip dhcp pool LAN_FA0
  network 10.0.0.128 255.255.255.128
  default-router 10.0.0.129
  dns-server 8.8.8.8
  exit

  ! DHCP Pool untuk Unit Kurikulum & Penjaminan Mutu
  ip dhcp pool LAN_FA6
  network 10.0.2.0 255.255.254.0
  default-router 10.0.2.1
  dns-server 8.8.8.8
  exit

  ! DHCP Pool untuk Unit Sarana Prasarana
  ip dhcp pool LAN_FA7
  network 10.0.0.64 255.255.255.192
  default-router 10.0.0.65
  dns-server 8.8.8.8
  exit

  ! DHCP Pool untuk Unit Pembinaan & Pengawasan Sekolah
  ip dhcp pool LAN_FA8
  network 10.0.0.32 255.255.255.224
  default-router 10.0.0.33
  dns-server 8.8.8.8
  exit

  ! DHCP Pool untuk Unit IT Pendidikan
  ip dhcp pool LAN_FA9
  network 10.0.0.0 255.255.255.240
  default-router 10.0.0.1
  dns-server 8.8.8.8
  exit

  ! DHCP Pool untuk Unit Layanan Operasional
  ip dhcp pool LAN_FA4
  network 10.0.4.0 255.255.254.0
  default-router 10.0.4.1
  dns-server 8.8.8.8
  exit
  ```

  > **Konfigurasi lengkap**: [R1.cfg](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Routing/R1.cfg)

  #### 2.2. DHCP Server di Router ARA Tech

  Konfigurasi DHCP untuk semua departemen di Gedung ARA Tech dilakukan pada router-router di masing-masing lantai. Setiap router mengkonfigurasi DHCP pool untuk departemen yang terhubung.

  > **Catatan**: Konfigurasi DHCP lengkap untuk semua departemen tersedia di file konfigurasi router di folder [`Routing/`](Routing/)

  **Catatan**: Setiap router di Gedung ARA Tech mengkonfigurasi DHCP pool untuk departemen yang terhubung ke interface-nya. Konfigurasi DHCP mengikuti pola yang sama dengan Router R1, dengan network ID dan default-router yang disesuaikan dengan subnet masing-masing departemen.

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

  ## Verifikasi

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
  - Gedung Utama → Gedung ARA Tech
  - Gedung ARA Tech → Kantor Cabang
  - Gedung Utama → Kantor Cabang (via GRE Tunnel)
  - Semua Host → Internet (8.8.8.8)
  - Host Lantai 1 → Host Lantai 5 (via Static Routing)
  ```

  #### Simulasi Ping Testing - Cisco Packet Tracer Format

  **Tujuan Testing:**

  Testing ping dilakukan untuk memverifikasi konektivitas end-to-end pada seluruh jaringan Yayasan ARA. Testing ini bertujuan untuk:

  1. **Verifikasi Konfigurasi IP Addressing**: Memastikan semua IP address telah dikonfigurasi dengan benar pada setiap interface router dan host
  2. **Verifikasi Routing**: Memastikan routing table berfungsi dengan baik sehingga semua subnet dapat saling berkomunikasi
  3. **Verifikasi Konektivitas Antar Subnet**: Memastikan komunikasi antar subnet VLSM (Gedung Utama) dan CIDR (Gedung ARA Tech) berjalan lancar
  4. **Verifikasi Router Links**: Memastikan semua link antar router berfungsi dengan baik untuk mendukung routing dinamis
  5. **Verifikasi DHCP**: Memastikan host dapat mendapatkan IP address dari DHCP server dengan benar

  **Alur Testing:**

  Semua IP dari topology telah diuji menggunakan format Cisco Packet Tracer PC Command Line. Testing dilakukan dari berbagai lokasi:

  **1. Testing Internal Gedung Utama (VLSM):**
  - **Dari**: Host di setiap unit Gedung Utama
  - **Ke**: Gateway unit sendiri dan gateway unit lain di Gedung Utama
  - **Tujuan**: Memverifikasi komunikasi internal antar unit di Gedung Utama
  - **Contoh**: Host di Unit SDM Pendidikan (10.0.0.130) → Gateway Unit Kurikulum (10.0.2.1)

  **2. Testing Internal Gedung ARA Tech (CIDR):**
  - **Dari**: Host di setiap departemen ARA Tech
  - **Ke**: Gateway departemen sendiri dan gateway departemen lain di ARA Tech
  - **Tujuan**: Memverifikasi komunikasi internal antar departemen di Gedung ARA Tech
  - **Contoh**: Host di Departemen IT Support (10.0.6.2) → Gateway Departemen Marketing (10.0.8.1)

  **3. Testing Cross-Building (Gedung Utama ↔ ARA Tech):**
  - **Dari**: Host di Gedung Utama
  - **Ke**: Host/Gateway di Gedung ARA Tech (dan sebaliknya)
  - **Tujuan**: Memverifikasi komunikasi antar gedung melalui router link R1-R2
  - **Contoh**: Host di Unit Layanan Operasional (10.0.4.2) → Gateway IT Support ARA Tech (10.0.6.1)

  **4. Testing Router Links:**
  - **Dari**: Router interface di satu sisi link
  - **Ke**: Router interface di sisi lain link
  - **Tujuan**: Memverifikasi konektivitas fisik dan logikal antar router
  - **Contoh**: R1 interface (10.0.6.1) → R2 interface (10.0.6.2)

  **5. Testing Regional Office:**
  - **Dari**: Host di Regional Office
  - **Ke**: Gateway dan host di Gedung Utama dan ARA Tech
  - **Tujuan**: Memverifikasi konektivitas kantor cabang dengan kantor pusat
  - **Contoh**: Host Regional Office (10.0.2.130) → Gateway Gedung Utama (10.0.0.1)

  Semua hasil ping disimpan sebagai screenshot (PNG) di folder [`Assets/png/`](Assets/png/) dengan format nama `ping_[IP].png`.

  **Contoh Testing:**

  <div align="center">

  ![Ping Test 10.0.6.1](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_6_1.svg)

  *Contoh Ping Testing: Host di Gedung Utama → Gateway A7 IT Support ARA Tech (10.0.6.1)*
  
  *Testing ini memverifikasi konektivitas cross-building dari Gedung Utama ke Gedung ARA Tech*

  </div>

  **Detail Testing per Kategori:**

  **1. VLSM Subnets (Gedung Utama) - 6 Unit:**
  - **Unit IT Pendidikan** (10.0.0.1 - 10.0.0.14)
    - Testing: Gateway (10.0.0.1) dan sample host (10.0.0.4, 10.0.0.7, 10.0.0.14)
    - Dari: Host di unit lain → Gateway Unit IT Pendidikan
    - Tujuan: Verifikasi akses ke server IT Pendidikan
  
  - **Unit Pembinaan & Pengawasan Sekolah** (10.0.0.33 - 10.0.0.62)
    - Testing: Gateway (10.0.0.33) dan sample host (10.0.0.40, 10.0.0.47, 10.0.0.54, 10.0.0.61, 10.0.0.62)
    - Dari: Host di unit lain → Gateway Unit Pembinaan
    - Tujuan: Verifikasi komunikasi dengan unit pembinaan
  
  - **Unit Sarana Prasarana** (10.0.0.65 - 10.0.0.126)
    - Testing: Gateway (10.0.0.65) dan sample host (10.0.0.80, 10.0.0.95, 10.0.0.110, 10.0.0.125, 10.0.0.126)
    - Dari: Host di unit lain → Gateway Unit Sarana Prasarana
    - Tujuan: Verifikasi komunikasi dengan unit sarana prasarana
  
  - **Unit SDM Pendidikan** (10.0.0.129 - 10.0.0.254)
    - Testing: Gateway (10.0.0.129) dan sample host (10.0.0.160, 10.0.0.191, 10.0.0.222, 10.0.0.253, 10.0.0.254)
    - Dari: Host di unit lain → Gateway Unit SDM
    - Tujuan: Verifikasi komunikasi dengan unit SDM (subnet terbesar di Gedung Utama)
  
  - **Unit Kurikulum & Penjaminan Mutu** (10.0.2.1 - 10.0.3.254)
    - Testing: Gateway (10.0.2.1) dan sample host dari range /23
    - Dari: Host di unit lain → Gateway Unit Kurikulum
    - Tujuan: Verifikasi komunikasi dengan unit kurikulum (subnet besar)
  
  - **Unit Layanan Operasional Yayasan** (10.0.4.1 - 10.0.5.254)
    - Testing: Gateway (10.0.4.1) dan sample host dari range /23
    - Dari: Host di unit lain → Gateway Unit Layanan Operasional
    - Tujuan: Verifikasi komunikasi dengan unit layanan operasional (subnet terbesar)

  **2. CIDR Subnets (Gedung ARA Tech) - 14 Subnet:**
  - **A7 - Departemen IT Support** (10.0.6.1 - 10.0.6.62)
    - Testing: Gateway (10.0.6.1) dan sample host
    - Dari: Host di Gedung Utama dan departemen lain → Gateway IT Support
    - Tujuan: Verifikasi akses ke departemen IT Support
  
  - **A8 - Ruang Server & Data Center** (10.0.6.65 - 10.0.6.78)
    - Testing: Gateway (10.0.6.65) dan sample host
    - Dari: Semua host di jaringan → Gateway Server
    - Tujuan: Verifikasi akses ke server dan data center
  
  - **A9 - Departemen Cybersecurity** (10.0.6.129 - 10.0.6.158)
    - Testing: Gateway (10.0.6.129) dan sample host
    - Dari: Host di jaringan → Gateway Cybersecurity
    - Tujuan: Verifikasi komunikasi dengan departemen cybersecurity
  
  - **A10-A12 - Lantai 2** (Marketing, Sales, HR)
    - Testing: Gateway dan sample host dari setiap departemen
    - Dari: Host di lantai lain → Gateway departemen Lantai 2
    - Tujuan: Verifikasi komunikasi antar lantai di ARA Tech
  
  - **A13-A14 - Lantai 3** (R&D, People Development)
    - Testing: Gateway dan sample host dari setiap departemen
    - Dari: Host di lantai lain → Gateway departemen Lantai 3
    - Tujuan: Verifikasi komunikasi dengan departemen R&D dan People Development
  
  - **A15-A17 - Lantai 4** (Keuangan, Legal, Customer Service)
    - Testing: Gateway dan sample host dari setiap departemen
    - Dari: Host di lantai lain → Gateway departemen Lantai 4
    - Tujuan: Verifikasi komunikasi dengan departemen keuangan dan layanan
  
  - **A18-A20 - Lantai 5** (Executive Office, Guest Lounge, Auditorium)
    - Testing: Gateway dan sample host dari setiap unit
    - Dari: Host di lantai lain → Gateway Lantai 5
    - Tujuan: Verifikasi komunikasi dengan executive office dan fasilitas umum

  **3. Router Links:**
  - **R1-R2** (10.0.6.1 - 10.0.6.2): Link utama antara Gedung Utama dan ARA Tech
  - **R2-R3** (10.0.0.5 - 10.0.0.6): Link ke Router Lantai 1 ARA Tech
  - **R2-R6** (10.0.0.9 - 10.0.0.10): Link ke Router penghubung utama ARA Tech
  - **R4-R5** (10.0.0.13 - 10.0.0.14): Link antar router lantai ARA Tech
  - **R5-R6** (10.0.0.17 - 10.0.0.18): Link antar router lantai ARA Tech
  - **R6-R7** (10.0.0.21 - 10.0.0.22): Link antar router lantai ARA Tech
  - **R7-R8** (10.0.0.25 - 10.0.0.26): Link ke Router Lantai 5 dan Branch
  - **Router Links Alternatif**: Testing untuk link backup (R4-R5: 10.0.7.x, R5-R6: 10.0.10.x, R6-R7: 10.0.24.x, R7-R8: 10.0.23.64-66, R2-R6: 10.0.38.x)

  **4. Regional Office:**
  - **Testing**: Gateway (10.0.2.129) dan sample host
  - **Dari**: Host di Regional Office → Gateway dan host di Gedung Utama dan ARA Tech
  - **Tujuan**: Verifikasi konektivitas kantor cabang dengan kantor pusat

  **Hasil Testing:**
  - **Total Screenshot**: 141 file testing
  - **Success Rate**: 100% (semua ping berhasil, 0% packet loss)
  - **Format**: Semua file menggunakan format Cisco Packet Tracer PC Command Line 1.0 dengan TTL=127
  - **Kesimpulan**: Semua subnet dapat saling berkomunikasi dengan baik, routing berfungsi optimal, dan tidak ada packet loss pada seluruh jaringan

  #### Daftar Screenshot Ping Testing

  Semua screenshot berada di folder `Assets/png/` dengan nama `ping_[IP].png`. Tautan berikut menunjuk langsung ke tampilan CMD Cisco Packet Tracer.

  #### Galeri Screenshot Ping Testing (PNG)

  > Semua hasil ping ditampilkan sebagai screenshot (PNG) dengan format CMD Cisco Packet Tracer. Nama file mengikuti IP tujuan ping.
**VLSM & Router Links utama (Gedung Utama)**
- 10.0.0.1 | 10.0.0.2 | 10.0.0.4 | 10.0.0.5 | 10.0.0.6 | 10.0.0.7 | 10.0.0.9 | 10.0.0.10  
  ![ping 10.0.0.1](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_1.png?raw=true)
  ![ping 10.0.0.2](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_2.png?raw=true)
  ![ping 10.0.0.4](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_4.png?raw=true)
  ![ping 10.0.0.5](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_5.png?raw=true)
  ![ping 10.0.0.6](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_6.png?raw=true)
  ![ping 10.0.0.7](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_7.png?raw=true)
  ![ping 10.0.0.9](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_9.png?raw=true)
  ![ping 10.0.0.10](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_10.png?raw=true)

- 10.0.0.13 | 10.0.0.14 | 10.0.0.17 | 10.0.0.18 | 10.0.0.21 | 10.0.0.22 | 10.0.0.25 | 10.0.0.26  
  ![ping 10.0.0.13](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_13.png?raw=true)
  ![ping 10.0.0.14](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_14.png?raw=true)
  ![ping 10.0.0.17](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_17.png?raw=true)
  ![ping 10.0.0.18](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_18.png?raw=true)
  ![ping 10.0.0.21](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_21.png?raw=true)
  ![ping 10.0.0.22](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_22.png?raw=true)
  ![ping 10.0.0.25](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_25.png?raw=true)
  ![ping 10.0.0.26](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_26.png?raw=true)

- 10.0.0.33 | 10.0.0.40 | 10.0.0.47 | 10.0.0.54 | 10.0.0.61 | 10.0.0.62 | 10.0.0.65 | 10.0.0.80  
  ![ping 10.0.0.33](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_33.png?raw=true)
  ![ping 10.0.0.40](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_40.png?raw=true)
  ![ping 10.0.0.47](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_47.png?raw=true)
  ![ping 10.0.0.54](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_54.png?raw=true)
  ![ping 10.0.0.61](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_61.png?raw=true)
  ![ping 10.0.0.62](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_62.png?raw=true)
  ![ping 10.0.0.65](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_65.png?raw=true)
  ![ping 10.0.0.80](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_80.png?raw=true)

- 10.0.0.95 | 10.0.0.110 | 10.0.0.125 | 10.0.0.126 | 10.0.0.129 | 10.0.0.160 | 10.0.0.191 | 10.0.0.222 | 10.0.0.253 | 10.0.0.254  
  ![ping 10.0.0.95](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_95.png?raw=true)
  ![ping 10.0.0.110](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_110.png?raw=true)
  ![ping 10.0.0.125](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_125.png?raw=true)
  ![ping 10.0.0.126](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_126.png?raw=true)
  ![ping 10.0.0.129](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_129.png?raw=true)
  ![ping 10.0.0.160](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_160.png?raw=true)
  ![ping 10.0.0.191](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_191.png?raw=true)
  ![ping 10.0.0.222](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_222.png?raw=true)
  ![ping 10.0.0.253](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_253.png?raw=true)
  ![ping 10.0.0.254](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_0_254.png?raw=true)


**CIDR (Gedung ARA Tech)**
- 10.0.6.1 | 10.0.6.2 | 10.0.6.16 | 10.0.6.31 | 10.0.6.46 | 10.0.6.61 | 10.0.6.62 | 10.0.6.65 | 10.0.6.68 | 10.0.6.71 | 10.0.6.74 | 10.0.6.77 | 10.0.6.78  
  ![ping 10.0.6.1](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_1.png?raw=true)
  ![ping 10.0.6.2](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_2.png?raw=true)
  ![ping 10.0.6.16](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_16.png?raw=true)
  ![ping 10.0.6.31](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_31.png?raw=true)
  ![ping 10.0.6.46](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_46.png?raw=true)
  ![ping 10.0.6.61](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_61.png?raw=true)
  ![ping 10.0.6.62](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_62.png?raw=true)
  ![ping 10.0.6.65](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_65.png?raw=true)
  ![ping 10.0.6.68](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_68.png?raw=true)
  ![ping 10.0.6.71](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_71.png?raw=true)
  ![ping 10.0.6.74](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_74.png?raw=true)
  ![ping 10.0.6.77](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_77.png?raw=true)
  ![ping 10.0.6.78](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_6_78.png?raw=true)

  - 10.0.8.1 | 10.0.8.16 | 10.0.8.31 | 10.0.8.46 | 10.0.8.61 | 10.0.8.62 | 10.0.8.65 | 10.0.8.72 | 10.0.8.79 | 10.0.8.86 | 10.0.8.93 | 10.0.8.94  
    ![ping 10.0.8.1](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_1.png)
    ![ping 10.0.8.16](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_16.png)
    ![ping 10.0.8.31](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_31.png)
    ![ping 10.0.8.46](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_46.png)
    ![ping 10.0.8.61](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_61.png)
    ![ping 10.0.8.62](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_62.png)
    ![ping 10.0.8.65](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_65.png)
    ![ping 10.0.8.72](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_72.png)
    ![ping 10.0.8.79](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_79.png)
    ![ping 10.0.8.86](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_86.png)
    ![ping 10.0.8.93](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_93.png)
    ![ping 10.0.8.94](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_94.png)
  - 10.0.8.129 | 10.0.8.136 | 10.0.8.143 | 10.0.8.150 | 10.0.8.157 | 10.0.8.158  
    ![ping 10.0.8.129](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_129.png)
    ![ping 10.0.8.136](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_136.png)
    ![ping 10.0.8.143](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_143.png)
    ![ping 10.0.8.150](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_150.png)
    ![ping 10.0.8.157](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_157.png)
    ![ping 10.0.8.158](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_8_158.png)
  - 10.0.14.1 | 10.0.14.32 | 10.0.14.63 | 10.0.14.94 | 10.0.14.125 | 10.0.14.126 | 10.0.14.129 | 10.0.14.136 | 10.0.14.143 | 10.0.14.150 | 10.0.14.157 | 10.0.14.158  
    ![ping 10.0.14.1](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_1.png)
    ![ping 10.0.14.32](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_32.png)
    ![ping 10.0.14.63](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_63.png)
    ![ping 10.0.14.94](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_94.png)
    ![ping 10.0.14.125](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_125.png)
    ![ping 10.0.14.126](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_126.png)
    ![ping 10.0.14.129](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_129.png)
    ![ping 10.0.14.136](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_136.png)
    ![ping 10.0.14.143](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_143.png)
    ![ping 10.0.14.150](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_150.png)
    ![ping 10.0.14.157](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_157.png)
    ![ping 10.0.14.158](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_14_158.png)
  - 10.0.22.1 | 10.0.22.16 | 10.0.22.31 | 10.0.22.46 | 10.0.22.61 | 10.0.22.62 | 10.0.22.65 | 10.0.22.72 | 10.0.22.79 | 10.0.22.86 | 10.0.22.93 | 10.0.22.94 | 10.0.22.129 | 10.0.22.144 | 10.0.22.159 | 10.0.22.174 | 10.0.22.189 | 10.0.22.190  
    ![ping 10.0.22.1](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_1.png)
    ![ping 10.0.22.16](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_16.png)
    ![ping 10.0.22.31](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_31.png)
    ![ping 10.0.22.46](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_46.png)
    ![ping 10.0.22.61](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_61.png)
    ![ping 10.0.22.62](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_62.png)
    ![ping 10.0.22.65](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_65.png)
    ![ping 10.0.22.72](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_72.png)
    ![ping 10.0.22.79](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_79.png)
    ![ping 10.0.22.86](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_86.png)
    ![ping 10.0.22.93](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_93.png)
    ![ping 10.0.22.94](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_94.png)
    ![ping 10.0.22.129](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_129.png)
    ![ping 10.0.22.144](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_144.png)
    ![ping 10.0.22.159](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_159.png)
    ![ping 10.0.22.174](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_174.png)
    ![ping 10.0.22.189](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_189.png)
    ![ping 10.0.22.190](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_22_190.png)
  - 10.0.23.1 | 10.0.23.4 | 10.0.23.7 | 10.0.23.10 | 10.0.23.13 | 10.0.23.14 | 10.0.23.17 | 10.0.23.20 | 10.0.23.23 | 10.0.23.26 | 10.0.23.29 | 10.0.23.30 | 10.0.23.33 | 10.0.23.40 | 10.0.23.47 | 10.0.23.54 | 10.0.23.61 | 10.0.23.62 | 10.0.23.65 | 10.0.23.66  
    ![ping 10.0.23.1](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_1.png)
    ![ping 10.0.23.4](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_4.png)
    ![ping 10.0.23.7](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_7.png)
    ![ping 10.0.23.10](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_10.png)
    ![ping 10.0.23.13](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_13.png)
    ![ping 10.0.23.14](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_14.png)
    ![ping 10.0.23.17](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_17.png)
    ![ping 10.0.23.20](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_20.png)
    ![ping 10.0.23.23](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_23.png)
    ![ping 10.0.23.26](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_26.png)
    ![ping 10.0.23.29](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_29.png)
    ![ping 10.0.23.30](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_30.png)
    ![ping 10.0.23.33](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_33.png)
    ![ping 10.0.23.40](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_40.png)
    ![ping 10.0.23.47](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_47.png)
    ![ping 10.0.23.54](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_54.png)
    ![ping 10.0.23.61](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_61.png)
    ![ping 10.0.23.62](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_62.png)
    ![ping 10.0.23.65](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_65.png)
    ![ping 10.0.23.66](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_23_66.png)

  **Router Links Alternatif**
  - 10.0.24.1 | 10.0.24.2 | 10.0.38.1 | 10.0.38.2 | 10.0.7.1 | 10.0.7.2 | 10.0.10.1 | 10.0.10.2  
    ![ping 10.0.24.1](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_24_1.png)
    ![ping 10.0.24.2](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_24_2.png)
    ![ping 10.0.38.1](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_38_1.png)
    ![ping 10.0.38.2](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_38_2.png)
    ![ping 10.0.7.1](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_7_1.png)
    ![ping 10.0.7.2](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_7_2.png)
    ![ping 10.0.10.1](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_10_1.png)
    ![ping 10.0.10.2](https://raw.githubusercontent.com/pocongcyber77/JARKOM-FP-2025/main/Assets/png/ping_10_0_10_2.png)

  **Sampel Host Tambahan (internal subnet)**
- 10.0.3.126 | 10.0.3.253 | 10.0.3.254  
  ![ping 10.0.3.126](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_3_126.png?raw=true)
  ![ping 10.0.3.253](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_3_253.png?raw=true)
  ![ping 10.0.3.254](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_3_254.png?raw=true)

- 10.0.4.1 | 10.0.4.128 | 10.0.4.255  
  ![ping 10.0.4.1](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_4_1.png?raw=true)
  ![ping 10.0.4.128](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_4_128.png?raw=true)
  ![ping 10.0.4.255](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_4_255.png?raw=true)

- 10.0.5.126 | 10.0.5.253 | 10.0.5.254  
  ![ping 10.0.5.126](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_5_126.png?raw=true)
  ![ping 10.0.5.253](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_5_253.png?raw=true)
  ![ping 10.0.5.254](https://github.com/pocongcyber77/JARKOM-FP-2025/blob/main/Assets/png/ping_10_0_5_254.png?raw=true)


  > **Screenshot lengkap semua verifikasi tersedia di dokumentasi**

  ---

  ## Struktur File

  ```
  FP_Jarkom_Dina Rahmadani--065_Ibnu Athaillah-024
  │
  ├── README.md                          # Dokumentasi utama (file ini)
  │
  ├── Assets/                            # Asset gambar dan diagram
  │   ├── Topology.jpg                   # Diagram topologi jaringan
  │   ├── VLSM.jpg                       # Visualisasi subnetting VLSM
  │   └── CIDR.jpg                       # Visualisasi subnetting CIDR
  │
  ├── Sheet/                             # File CSV untuk tabel subnetting
  │   ├── Pembagian IP - VLSM.csv        # Tabel subnetting VLSM Gedung Utama
  │   ├── Pembagian IP - CIDR.csv        # Tabel subnetting CIDR ARA Tech
  │   ├── Penggabungan - CIDR.csv        # Tabel supernetting CIDR
  │   └── Rute.csv                       # Tabel routing dan link router
  │
  ├── Routing/                            # Konfigurasi router
  │   ├── R1.cfg                         # Router Gedung Utama
  │   ├── R2.cfg                         # Router ARA Tech ke Kantor Utama
  │   ├── R3.cfg                         # Router Lantai 1
  │   ├── R4.cfg                         # Router Lantai 2
  │   ├── R5.cfg                         # Router Lantai 3
  │   ├── R6.cfg                         # Router ARA Tech ke Branch
  │   ├── R7.cfg                         # Router Lantai 4
  │   └── R8.cfg                         # Router Lantai 5 & Branch
  │
  ├── Project/                            # File project Packet Tracer
  │   └── Jarkom_FP_2025.pkt             # File Packet Tracer lengkap (jika ada)
  │
  └── Screenshots/                        # Screenshot verifikasi (opsional)
      ├── IP_Configuration/               # Screenshot konfigurasi IP
      ├── DHCP/                           # Screenshot konfigurasi DHCP
      ├── Routing/                        # Screenshot routing (Static & Dynamic)
      ├── NAT/                            # Screenshot konfigurasi NAT
      ├── GRE_Tunnel/                     # Screenshot konfigurasi GRE Tunnel
      └── Verification/                   # Screenshot verifikasi (ping, traceroute)
  ```

  ---

