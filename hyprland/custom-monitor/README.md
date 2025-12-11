# Setting monitor hyprland

Langkah-langkah Konfigurasi

 -  **Identifikasi nama monitor Anda**:  
    Buka terminal dan jalankan perintah berikut untuk mengetahui nama pengenal (identifier) untuk monitor Anda (misalnya, `eDP-1`, `DP-1`, atau `HDMI-A-1`):
    
    
    ```
    hyprctl monitors
    
    ```
    
    *Gunakan kode dengan hati-hati.*
    

 -   **Edit file konfigurasi Hyprland**:  
    Buka file konfigurasi Anda menggunakan editor teks (misalnya, `nano`):
	    ```
	    
		nano ~/.config/hypr/hyprland.conf
		
		```
	   *Gunakan kode dengan hati-hati.*

 - **Tambahkan file custom baru(opsional)**
   Jika anda tak ingin merubah file konfigurasi default hyprland, anda bisa membuat file custom baru. contoh: *custom_mirror.conf*
   ```
   
   nano ~/.config/hypr/conf/monitors/custom_mirror.conf
   
	```

 - **Tetapkan custom monitors setting jadi default**
 - Setelah membuat atau merubah setingan pada monitor, anda bisa memilih setingan yang sudah anda buat sebagai default

 - **Simpan dan terapkan perubahan**
 Simpan file konfigurasi dan keluar dari editor. Terapkan perubahan pada Hyprland tanpa perlu me-restart sesi Anda dengan menjalankan perintah berikut di terminal:

     hyprctl reload
     
	Atau, restart Hyprland Anda sepenuhnya.

