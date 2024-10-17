# Praktikum RTOS - SEMESTER 5 (3 Teknik Komputer A)
 
- **Diva Sakananda (3222600013)**
- **Billy Lukito Danuharja (3222600027)**

# Task 3 - Priority Task RTOS

## Deskripsi Projek
Dalam scheduling preemptive dengan prioritas, tugas dengan prioritas lebih tinggi akan mengambil alih tugas dengan prioritas lebih rendah yang sedang berjalan. Ketika tugas dengan prioritas lebih tinggi siap dijalankan, scheduler akan menangguhkan tugas dengan prioritas lebih rendah dan menjalankan tugas prioritas lebih tinggi. Dalam sesi praktik ini, kita mengontrol 4 LED yang terhubung ke pin STM32 A3, A4, A5, dan A6, dengan resistor yang terhubung ke ground.

1. Pengaturan Prioritas
FlashRedLedTask, yang bertanggung jawab untuk menyalakan LED selama 0,5 detik menggunakan fungsi FlashRedLed(), diberi prioritas lebih tinggi dibandingkan dengan FlashGreenLedTask, yang menyalakan LED selama 4 detik menggunakan fungsi FlashGreenLed(). Karena scheduling preemptive, kapan pun tugas prioritas lebih tinggi siap dijalankan, tugas prioritas lebih rendah yang sedang berjalan akan ditangguhkan sampai tugas prioritas lebih tinggi selesai atau tertunda.
Sebagai contoh, dalam proyek ini terdapat tugas-tugas berikut:

- FlashRedLedTask (prioritas di atas normal)
- FlashGreenLedTask (prioritas normal)

Dalam situasi di mana kedua tugas siap dijalankan, RTOS akan menjalankan FlashRedLedTask terlebih dahulu. Jika FlashGreenLedTask sedang berjalan, tugas tersebut hanya akan melanjutkan eksekusinya setelah FlashRedLedTask selesai atau tertunda (misalnya, menggunakan osDelay). Diagram waktu yang diharapkan akan menunjukkan bahwa LED merah berkedip lebih sering atau memiliki prioritas lebih tinggi dibandingkan LED hijau ketika keduanya siap dijalankan.


2. Scheduling Preemptive
Scheduling preemptive memungkinkan tugas dengan prioritas lebih tinggi untuk menginterupsi tugas dengan prioritas lebih rendah kapan pun tugas dengan prioritas lebih tinggi siap dijalankan, memastikan bahwa tugas-tugas kritis ditangani dengan cepat. Dalam sistem waktu nyata seperti ini, tugas-tugas yang terkait dengan operasi real-time, seperti kedipan LED yang lebih cepat, harus diberi prioritas lebih tinggi.

- Ketika FlashRedLedTask siap, ia akan menginterupsi FlashGreenLedTask yang sedang berjalan.
- FlashGreenLedTask hanya akan melanjutkan setelah FlashRedLedTask selesai atau ditangguhkan.

## Hasil Ketika Diunggah ke Board STM32

Tugas dengan prioritas lebih tinggi (misalnya, FlashRedLedTask) akan mendapatkan waktu CPU lebih sering dibandingkan dengan tugas dengan prioritas lebih rendah.
Jika tugas dengan prioritas lebih rendah (misalnya, FlashGreenLedTask) sedang berjalan, tugas tersebut akan terinterupsi saat tugas dengan prioritas lebih tinggi siap dijalankan.
Pergantian tugas akan ditangani secara otomatis oleh scheduler RTOS tanpa intervensi langsung dari program utama.
Perilaku yang dapat diamati termasuk satu LED (kemungkinan LED merah) berkedip lebih sering atau secara terus-menerus, sementara LED lainnya (hijau) tampak tertunda atau tidak berkedip, menandakan bahwa tugas yang bertanggung jawab untuk menyalakannya telah ditangguhkan oleh tugas dengan prioritas lebih tinggi.


## Foto Hardware
![foto hardware task 3](https://github.com/user-attachments/assets/c8a2dd88-2ce8-482a-b1ff-c46423380af9)

## Short Video Hardware
https://github.com/user-attachments/assets/8b8af570-5e38-4beb-88b5-a83d66bfc9ba
