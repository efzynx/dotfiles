

# Mengaktifkan/Menonaktifkan Touchpad di Arch Linux (Hyprland)

Panduan ini menjelaskan cara membuat skrip _toggle_ sederhana dan mengikatnya ke pintasan keyboard atau tombol fungsi khusus di lingkungan Hyprland Wayland di Arch Linux.

Prasyarat

-   Arch Linux
-   Hyprland Wayland Compositor
-   `libnotify` (Opsional, untuk notifikasi desktop):
    
    
    ```
    sudo pacman -S libnotify
    
    ```
    
    Gunakan kode dengan hati-hati.
    

-   `wev` (Opsional, untuk mengidentifikasi nama kunci keyboard):
    
    
    ```
    sudo pacman -S wev
    
    ```
    
    Gunakan kode dengan hati-hati.
    

Langkah 1: Identifikasi Nama Perangkat Touchpad Anda

Anda perlu mengetahui nama persis touchpad Anda untuk memberitahu Hyprland perangkat mana yang harus dinonaktifkan.

Buka terminal dan jalankan:

    hyprctl devices

Gunakan kode dengan hati-hati.

Cari bagian `mice:` atau `touchpad:` dan catat nama lengkap perangkat Anda. Contoh:  `elan1300:00-04f3:3087-touchpad`.

Langkah 2: Buat Skrip Toggle

Buat direktori untuk skrip Hyprland Anda jika belum ada, lalu buat skrip baru:

    mkdir -p ~/.config/hypr/scripts
    nano ~/.config/hypr/scripts/toggle_touchpad.sh

*Gunakan kode dengan hati-hati.*

Salin dan tempel kode berikut ke dalam file, **memastikan `DEVICE_NAME` cocok dengan nama yang Anda identifikasi di Langkah 1**:

    #!/bin/bash
    
    # Ganti dengan nama perangkat Anda yang sebenarnya dari 'hyprctl devices'
    DEVICE_NAME="elan1300:00-04f3:3087-touchpad"
    STATE_FILE="/tmp/touchpad_state"
    
    if [ -f "$STATE_FILE" ]; then
        # Jika file status ada, touchpad dinonaktifkan. Aktifkan.
        hyprctl keyword "device[$DEVICE_NAME]:enabled" true
        rm "$STATE_FILE"
        notify-send "Touchpad Enabled"
    else
        # Jika file status tidak ada, touchpad diaktifkan. Nonaktifkan.
        hyprctl keyword "device[$DEVICE_NAME]:enabled" false
        touch "$STATE_FILE"
        notify-send "Touchpad Disabled"
    fi
*Gunakan kode dengan hati-hati.*

Simpan dan keluar dari editor (`Ctrl+O`, `Enter`, `Ctrl+X` di nano).

Langkah 3: Jadikan Skrip Dapat Dieksekusi

Anda harus memberikan izin eksekusi pada skrip agar dapat dijalankan:

    chmod +x ~/.config/hypr/scripts/toggle_touchpad.sh

*Gunakan kode dengan hati-hati.*

Anda dapat menguji skrip sekarang dengan menjalankannya dari terminal:

    ~/.config/hypr/scripts/toggle_touchpad.sh

*Gunakan kode dengan hati-hati.*

Langkah 4: Identifikasi Nama Kunci Keyboard yang Benar (Opsional/Penting untuk Tombol Fungsi)

Untuk keyboard laptop (terutama ASUS), tombol fungsi khusus mungkin memerlukan nama kunci spesifik yang berbeda dari `F6`.

Gunakan `wev` untuk menemukan nama kunci yang tepat:

    sudo pacman -S wev
    wev

Gunakan kode dengan hati-hati.

Tekan tombol fungsi touchpad fisik Anda (misalnya `Fn + F6`). Catat `sym:` yang muncul di output (`F6` atau `XF86TouchpadToggle` adalah yang paling umum).

Langkah 5: Tautkan Skrip ke Pintasan Keyboard

Edit file konfigurasi Hyprland utama Anda (biasanya `~/.config/hypr/hyprland.conf` atau `~/.config/hypr/conf/custom.conf`):

    nano ~/.config/hypr/conf/custom.conf

*Gunakan kode dengan hati-hati*.

Tambahkan baris `bind` menggunakan nama kunci yang Anda temukan di Langkah 4.

**Opsi A: Menggunakan `SUPER` + `F6`:**

conf

    # Bind Super + F6 to toggle the touchpad
    bind = SUPER + F6, exec, ~/.config/hypr/scripts/toggle_touchpad.sh

*Gunakan kode dengan hati-hati.*

**Opsi B: Menggunakan Tombol Fungsi Tunggal (direkomendasikan jika `wev` mengembalikan nama khusus):**

conf

    # Bind the specific function key (e.g., F6 or XF86TouchpadToggle) to the script
    bind =, F6, exec, ~/.config/hypr/scripts/toggle_touchpad.sh

*Gunakan kode dengan hati-hati.*

_Catatan: Parameter pertama setelah `bind =` adalah modifier key (seperti SUPER, ALT, CTRL, SHIFT). Jika Anda ingin tombol bekerja sendirian, biarkan kosong seperti `bind =, F6, ...`._

Langkah 6: Muat Ulang Hyprland

Simpan file konfigurasi Anda dan muat ulang Hyprland untuk menerapkan perubahan:

    hyprctl reload

*Gunakan kode dengan hati-hati.*

Sekarang Anda dapat menggunakan pintasan keyboard Anda untuk mengaktifkan dan menonaktifkan touchpad!
