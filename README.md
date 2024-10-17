# Praktikum RTOS - SEMESTER 5 (3 Teknik Komputer A)
 
- **Diva Sakananda (3222600013)**
- **Billy Lukito Danuharja (3222600027)**

# Task 3 - Preemptive Scheduling

## Deskripsi Projek
# Preemptive Scheduling dengan RTOS pada STM32

Proyek ini mendemonstrasikan konsep preemptive scheduling menggunakan RTOS (Real-Time Operating System) pada mikrokontroler STM32. Kami mengontrol empat LED yang terhubung ke pin PA8, PA9, PA10, dan PA11 pada STM32, dengan detail berikut:

- **PA8**: LED Hijau
- **PA9**: LED Biru (Indikator untuk tugas LED Hijau)
- **PA10**: LED Merah
- **PA11**: LED Oranye (Indikator untuk tugas LED Merah)

RTOS digunakan untuk membuat dua task dengan prioritas berbeda:

- `LedRedTask`: Bertanggung jawab untuk mengedipkan LED merah dan oranye dengan prioritas High.
- `LedGreenTask`: Bertanggung jawab untuk mengedipkan LED hijau dan biru dengan prioritas Normal.

## Gambaran Proyek

Proyek ini mengimplementasikan mekanisme preemptive scheduling di mana task-task diberi prioritas yang berbeda. Preemptive scheduling memungkinkan task dengan prioritas lebih tinggi untuk menginterupsi dan mengambil alih CPU dari task prioritas lebih rendah ketika task prioritas tinggi siap dijalankan.

### Deskripsi Task

1. **LedRedTask (Prioritas Tinggi)**
   - **Pin yang digunakan**: PA10 (LED Merah) dan PA11 (LED Oranye - indikator)
   - **Eksekusi**: Mengedipkan LED merah selama 0,5 detik (frekuensi 20 Hz) dan kemudian berhenti selama 1,5 detik. LED oranye (indikator) dinyalakan saat LED merah berkedip dan dimatikan setelahnya.
   - **Prioritas**: Tinggi

2. **LedGreenTask (Prioritas Normal)**
   - **Pin yang digunakan**: PA8 (LED Hijau) dan PA9 (LED Biru - indikator)
   - **Eksekusi**: Mengedipkan LED hijau selama 4 detik (frekuensi 20 Hz) dan kemudian berhenti selama 6 detik. LED biru (indikator) dinyalakan saat LED hijau berkedip dan dimatikan setelahnya.
   - **Prioritas**: Normal

### Preemptive Scheduling

RTOS menggunakan strategi preemptive scheduling untuk menangani eksekusi task. Preemptive scheduling memastikan CPU selalu diberikan kepada task dengan prioritas tertinggi yang siap untuk berjalan. Jika task dengan prioritas lebih tinggi menjadi siap sementara task prioritas lebih rendah sedang berjalan, RTOS akan menangguhkan task prioritas lebih rendah dan memberikan kontrol kepada task prioritas lebih tinggi.

### Contoh pada proyek ini:
- **LedRedTask** diberi prioritas lebih tinggi dibandingkan dengan **LedGreenTask**.
- Ketika kedua task siap, scheduler RTOS akan mengeksekusi **LedRedTask** terlebih dahulu. **LedGreenTask** akan diinterupsi (preempted) dan hanya akan dilanjutkan setelah **LedRedTask** selesai dieksekusi atau masuk ke dalam status delay.
  
### Perilaku Waktu:
- **LedRedTask** (dengan prioritas lebih tinggi) mengedipkan LED merah lebih sering, mengambil alih dari **LedGreenTask**. Hal ini terlihat ketika LED hijau tampak tertunda atau ditangguhkan ketika task LED merah sedang berjalan.

### Detail Scheduling Task

- **LedRedTask** menggunakan fungsi `osDelay(1500)` untuk menunda eksekusi selama 1,5 detik setelah menyelesaikan pengedipan LED selama 0,5 detik.
- **LedGreenTask** menggunakan fungsi `osDelay(6000)` untuk menunda eksekusi selama 6 detik setelah menyelesaikan pengedipan LED selama 4 detik.

Dalam lingkungan preemptive scheduling, ketika **LedRedTask** siap untuk dijalankan, task tersebut akan menginterupsi **LedGreenTask** dan mengambil alih CPU. Setelah **LedRedTask** menyelesaikan eksekusinya atau masuk ke status penundaan, **LedGreenTask** dapat dilanjutkan.
Karena LedRedTask memiliki prioritas lebih tinggi, ketika LedGreenTask dan LedRedTask keduanya siap, LedRedTask akan menginterupsi LedGreenTask dan mengambil alih CPU. LedGreenTask hanya akan berjalan kembali setelah LedRedTask selesai atau masuk ke status penundaan.

### Pengamatan
LedRedTask akan mengedipkan LED merah lebih sering karena memiliki prioritas lebih tinggi.
LedGreenTask hanya akan berjalan ketika LedRedTask tidak aktif, menyebabkan pengedipan LED hijau tampak tertunda ketika task LED merah sedang berjalan.
LED indikator (biru dan oranye) menunjukkan saat masing-masing task sedang aktif berjalan.


## Foto Hardware
![foto hardware task 3](https://github.com/user-attachments/assets/c8a2dd88-2ce8-482a-b1ff-c46423380af9)

## Short Video Hardware
https://github.com/user-attachments/assets/8b8af570-5e38-4beb-88b5-a83d66bfc9ba
