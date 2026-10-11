# FiChat

> **Offline-First, Decentralized Peer-to-Peer Mesh Messaging System for Android**

[![Platform](https://img.shields.io/badge/Platform-Android-green.svg)](https://developer.android.com)
[![Kotlin](https://img.shields.io/badge/Kotlin-2.0.21-blue.svg)](https://kotlinlang.org)
[![Compose](https://img.shields.io/badge/UI-Jetpack%20Compose-brightgreen.svg)](https://developer.android.com/jetpack/compose)
[![MinSDK](https://img.shields.io/badge/MinSDK-26%20%28Android%208.0%29-orange.svg)](https://developer.android.com/about/dashboards)
[![TargetSDK](https://img.shields.io/badge/TargetSDK-37-blue.svg)](https://developer.android.com/about/versions/15)
[![License](https://img.shields.io/badge/License-MIT%20%2F%20Proprietary-lightgrey.svg)](#license)

**FiChat** adalah aplikasi komunikasi terdeentralisasi (P2P) berbasis Android yang dirancang untuk memungkinkan pertukaran pesan teks, pesan suara (*voice notes*), transfer berkas, koordinasi lokasi, dan pesan darurat SOS **tanpa memerlukan koneksi internet maupun sinyal menara seluler**.

Aplikasi ini memanfaatkan konektivitas antar-perangkat (*device-to-device*) seperti Bluetooth Low Energy (BLE) dan Wi-Fi Direct untuk membentuk **Jaringan Mesh Lokal (Multi-Hop Mesh Network)**. Ketika penerima berada di luar jangkauan langsung, FiChat akan meneruskan pesan secara otomatis melalui perangkat FiChat terdekat lainnya sebagai perantara (*relay node*).

FiChat sangat ideal untuk situasi tanpa sinyal seluler: **kegiatan luar ruangan (hiking/camping), area terpencil, bencana alam, pemadaman jaringan (network outages), serta kegiatan komunal lokal**.

---

## Fitur Utama

### 1. Komunikasi Off-Grid (Tanpa Internet)
* Kirim dan terima pesan tanpa kuota data, Wi-Fi router, atau menara BTS seluler.
* Menggunakan Bluetooth LE & Wi-Fi Direct secara bersamaan untuk efisiensi dan kecepatan.

### 2. Multi-Hop Mesh Routing
* Pesan dapat "melompat" (*hop*) melalui beberapa perangkat FiChat untuk menjangkau tujuan yang jauh.
* Algoritma *smart routing* menghindari pengulangan pesan (*looping prevention*) dan memilih jalur transmisi tercepat.

```text
[ Pengirim A ] ──(BLE/P2P)──> [ Perangkat Relay B ] ──(BLE/P2P)──> [ Penerima C ]
```

### 3. Keamanan & Enkripsi End-to-End (E2EE)
* Enkripsi tingkat aplikasi (*application-level encryption*) dengan AES-256 dan Android KeyStore.
* Perangkat perantara (*relay nodes*) hanya meneruskan paket data terenkripsi tanpa bisa membaca isi pesan.
* Proteksi aplikasi tambahan dengan **Biometric Authentication** (Kunci Sidik Jari/Wajah).

### 4. Radar Perangkat & Peer Discovery
* Visualisasi perangkat FiChat di sekitar pengguna secara *real-time*.
* Penandaan indikator kualitas sinyal (RSSI) dan status perangkat aktif.

### 5. Pesan Kaya Fitur (Rich Messaging)
* **Pesan Teks & Emotikon**
* **Voice Notes / Pesan Suara** (perekaman dan pemutaran audio luring)
* **Transfer Gambar & Berkas**
* **Self-Destruct Messages** (pesan hapus otomatis setelah waktu yang ditentukan)
* **Pesan Darurat SOS** dengan prioritas tinggi di dalam jaringan mesh.

### 6. Peta Offline (Offline Map Caching)
* Integrasi **osmdroid** untuk menampilkan peta dan koordinat GPS tanpa jaringan internet.
* Fitur *tile caching* untuk menyimpan peta area sekitar sebelum bepergian.

### 7. Global Bridge
* Apabila salah satu perangkat terhubung ke internet, FiChat dapat menjembatani pesan jaringan mesh lokal ke server awan (*Cloud*) untuk meneruskannya ke pengguna FiChat di tempat lain.

### 8. Sensor Lingkungan & Outdoor Dashboard
* Kompas digital, altimeter, dan pemantau kondisi jaringan mesh sekitar untuk kebutuhan luar ruangan.

---

## Arsitektur Aplikasi

FiChat dibangun menggunakan standar **Clean Architecture + MVVM (Model-View-ViewModel)** dengan komponen Jetpack modern:

```text
┌───────────────────────────────────────────────────────────┐
│                       UI Layer                            │
│           Jetpack Compose + Material 3                    │
└─────────────────────────────┬─────────────────────────────┘
                              │
┌─────────────────────────────▼─────────────────────────────┐
│                    ViewModel Layer                        │
│             StateFlow + Coroutine Scopes                  │
└─────────────────────────────┬─────────────────────────────┘
                              │
┌─────────────────────────────▼─────────────────────────────┐
│                    Domain Layer                           │
│        Repositories, Models, Mesh Messaging Rules         │
└─────────────────────────────┬─────────────────────────────┘
                              │
┌─────────────────────────────▼─────────────────────────────┐
│                     Data Layer                            │
│ ┌──────────────────────┐ ┌──────────────────────────────┐ │
│ │   Room Database      │ │     BluetoothMeshManager     │ │
│ │  (Messages, Users)   │ │    (BLE Advert/Scanner)     │ │
│ └──────────────────────┘ └──────────────────────────────┘ │
│ ┌──────────────────────┐ ┌──────────────────────────────┐ │
│ │ EncryptedPrefs / Crypto│ │ MeshService (Foreground Service)│ │
│ └──────────────────────┘ └──────────────────────────────┘ │
└───────────────────────────────────────────────────────────┘
```

---

## Teknologi & Dependencies

| Kategori | Teknologi / Library |
| :--- | :--- |
| **Bahasa Utama** | [Kotlin](https://kotlinlang.org/) (JVM 11, Desugaring Enabled) |
| **UI Framework** | [Jetpack Compose](https://developer.android.com/jetpack/compose) + Material 3 |
| **Arsitektur** | MVVM, Clean Architecture, Kotlin Coroutines & Flow |
| **Database Lokal** | [Room Database](https://developer.android.com/training/data-storage/room) (KSP) |
| **Konektivitas P2P** | Bluetooth LE (GATT Client & Server), Android Nearby Services |
| **Peta & Lokasi** | [osmdroid](https://github.com/osmdroid/osmdroid), Play Services Location |
| **Enkripsi & Keamanan** | AndroidX Security Crypto, Biometric Prompt |
| **Background Tasks** | AndroidX WorkManager, Foreground Services (`MeshService`) |
| **Kompresi Image/QR** | ZXing (QR Code Scanner & Generator), Coil Compose |

---

## Panduan Memulai (Getting Started)

### Prasyarat
1. **Android Studio:** Ladybug (2024.2.1) atau versi lebih baru.
2. **JDK:** Java 17 atau Java 21.
3. **Target Android:** Android 8.0 (API level 26) hingga Android 15 (API level 35/37).
4. **Perangkat Pengujian:** Minimal **2 Perangkat Android Fisik** (sangat direkomendasikan karena emulator Android tidak mendukung penuh BLE Advertising & Wi-Fi Direct P2P).

### Langkah Instalasi

1. **Clone Repository**
   ```bash
   git clone https://github.com/restualfauzi/FiChat.git
   cd FiChat
   ```

2. **Buka Proyek di Android Studio**
   * Jalankan Android Studio, pilih `Open` dan arahkan ke folder `FiChat`.
   * Tunggu hingga proses **Gradle Sync** selesai.

3. **Jalankan Aplikasi**
   * Hubungkan perangkat Android via USB Debugging atau Wi-Fi Debugging.
   * Tekan tombol **Run (Shift + F10)**.

---

## Cara Pengujian Jaringan Mesh

Untuk menguji fitur multi-hop messaging:

1. Siapkan **3 Perangkat Android** (Perangkat A, Perangkat B, dan Perangkat C).
2. Posisikan perangkat secara berderet:
   * **Perangkat A** berada dekat dengan **Perangkat B**.
   * **Perangkat C** berada jauh dari **Perangkat A**, tetapi berada dalam jangkauan **Perangkat B**.
3. Buka aplikasi **FiChat** di ketiga perangkat dan pastikan izin Bluetooth & Lokasi disetujui.
4. Kirim pesan dari **Perangkat A** ke **Perangkat C**.
5. Pesan akan diteruskan melalui **Perangkat B** (*relay node*) secara otomatis dan tiba di **Perangkat C**.

---

## Struktur Proyek

```text
FiChat/
├── app/
│   ├── src/main/
│   │   ├── java/com/visentastudio/fichat/
│   │   │   ├── data/
│   │   │   │   ├── bluetooth/      # BLE GATT, Scanner, Advertiser, Mesh Router
│   │   │   │   ├── local/          # Room DB, DAOs, Entities, Encrypted Preferences
│   │   │   │   ├── media/          # VoiceNote Recorder & Player
│   │   │   │   ├── repository/     # MeshRepository implementation
│   │   │   │   └── security/       # AES Encryption & Biometric Helper
│   │   │   ├── domain/             # Models, Interfaces, UseCases
│   │   │   ├── service/            # MeshService (Foreground Service)
│   │   │   ├── ui/                 # Compose UI Screens, ViewModels, Themes
│   │   │   └── receiver/           # BootReceiver untuk auto-start mesh service
│   │   ├── res/                    # Drawables, Avatars, Icons, Layouts
│   │   └── AndroidManifest.xml
│   ├── build.gradle.kts
│   └── proguard-rules.pro
├── build.gradle.kts
├── settings.gradle.kts
└── README.md
```

---

## Keamanan & Privasi

* **Tidak Ada Pelacakan Terpusat:** Data pesan disimpan secara lokal di perangkat Anda (*Room DB*).
* **Anonymized Peer IDs:** Identifikasi perangkat menggunakan ID acak terenkripsi.
* **Izin Akses Terbatas:** Lokasi hanya digunakan untuk keperluan pemindaian Bluetooth LE & Wi-Fi Direct sesuai ketentuan sistem operasi Android.

---

## Kontribusi

Kontribusi selalu terbuka! Jika Anda ingin melaporkan bug atau menambahkan fitur baru:

1. Fork repository ini.
2. Buat branch fitur baru (`git checkout -b feature/FiturBaru`).
3. Commit perubahan Anda (`git commit -m 'feat: Menambahkan fitur baru'`).
4. Push ke branch (`git push origin feature/FiturBaru`).
5. Buat **Pull Request**.

---

## Lisensi

Hak Cipta © 2026 **Circle Mesh Limited / Restu Alfauzi**.

---

<p align="center">
  <b>FiChat</b> • <i>Communication Anywhere, Beyond Cellular Limits.</i><br>
  Bluetooth Mesh • End-to-End Encrypted • Offline Maps • Global Bridge
</p>
