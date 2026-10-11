# 📡 FiChat (Vicinify)

> **Offline-First, Decentralized Peer-to-Peer Mesh Messaging System for Android**

[![Platform](https://img.shields.io/badge/Platform-Android-green.svg)](https://developer.android.com)
[![Kotlin](https://img.shields.io/badge/Kotlin-2.0.21-blue.svg)](https://kotlinlang.org)
[![Compose](https://img.shields.io/badge/UI-Jetpack%20Compose-brightgreen.svg)](https://developer.android.com/jetpack/compose)
[![MinSDK](https://img.shields.io/badge/MinSDK-26%20%28Android%208.0%29-orange.svg)](https://developer.android.com/about/dashboards)
[![TargetSDK](https://img.shields.io/badge/TargetSDK-37-blue.svg)](https://developer.android.com/about/versions/15)
[![License](https://img.shields.io/badge/License-MIT%20%2F%20Proprietary-lightgrey.svg)](#license)

**FiChat** adalah aplikasi komunikasi terdesentralisasi (P2P) berbasis Android yang dirancang untuk memungkinkan pertukaran pesan teks, pesan suara (*voice notes*), transfer berkas, koordinasi lokasi, dan pesan darurat SOS **tanpa memerlukan koneksi internet maupun sinyal menara seluler**.

Aplikasi ini memanfaatkan konektivitas antar-perangkat (*device-to-device*) seperti Bluetooth Low Energy (BLE) dan Wi-Fi Direct untuk membentuk **Jaringan Mesh Lokal (Multi-Hop Mesh Network)**. Ketika penerima berada di luar jangkauan langsung, FiChat akan meneruskan pesan secara otomatis melalui perangkat FiChat terdekat lainnya sebagai perantara (*relay node*).

FiChat sangat ideal untuk situasi tanpa sinyal seluler: **kegiatan luar ruangan (hiking/camping), area terpencil, bencana alam, pemadaman jaringan (network outages), serta kegiatan komunal lokal**.

---

## 🌟 Fitur Utama

### 1. 📵 Komunikasi Off-Grid (Tanpa Internet)
* Kirim dan terima pesan tanpa kuota data, Wi-Fi router, atau menara BTS seluler.
* Menggunakan Bluetooth LE & Wi-Fi Direct secara bersamaan untuk efisiensi dan kecepatan.

### 2. 🔀 Multi-Hop Mesh Routing
* Pesan dapat "melompat" (*hop*) melalui beberapa perangkat FiChat untuk menjangkau tujuan yang jauh.
* Algoritma *smart routing* menghindari pengulangan pesan (*looping prevention*) dan memilih jalur transmisi tercepat.

```text
[ Pengirim A ] ──(BLE/P2P)──> [ Perangkat Relay B ] ──(BLE/P2P)──> [ Penerima C ]
