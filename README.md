# Личный OPKG репозиторий для версий OpenWrt 19-21
Позволяет устанавливать такие пакеты: OpenClash, Passwall, ShadowSocksR+ Plus, Wegare STL, Tiny File Manager, Xderm Mini, v2rayA, Modeminfo, dll) dengan mudah.


## Список поддержываемых архитектур:

aarch64_cortex-a53
aarch64_cortex-a72
aarch64_generic
arm_arm1176jzf-s_vfp
arm_cortex-a7_neon-vfpv4
i386_pentium4
mips_24kc
mipsel_24kc
x86_64


## Как добавить данный репозиторый в OpenWrt
Есть 2 способа:
- [Использовать вебинтерфейс LuCI](#menggunakan-luci)
- [Истпользовать Terminal](#menggunakan-terminal)


### Menggunakan LuCI

  
     Добавть  # перед option check_signature чтобы получилось так:
  
      
      ```
      # option check_signature
      ```

     В поле custom feeds добавить:

      ```
      src/gz custom_generic https://raw.githubusercontent.com/Spothz/my-opkg-repo/main/generic
      src/gz custom_arch https://raw.githubusercontent.com/Spothz/my-opkg-repo/main/mipsel_24kc
      ```

      Вместо **mipsel_24kc** вписать архитектуру своего роутера.

      ![](https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/preview/preview1.gif)
 
### Через Terminal
  Скопитуйте и вставте в терминал строки, определение архитектуры произойдёт автоматически:
      
      ```
      sed -i 's/option check_signature/# option check_signature/g' /etc/opkg.conf
      echo "src/gz custom_generic https://raw.githubusercontent.com/Spothz/my-opkg-repo/main/generic" >> /etc/opkg/customfeeds.conf
      echo "src/gz custom_arch https://raw.githubusercontent.com/Spothz/my-opkg-repo/main/$(grep "OPENWRT_ARCH" /etc/os-release | awk -F '"' '{print $2}')" >> /etc/opkg/customfeeds.conf
      ```

      > Для OpenWrt 19.07 нужно установить вручную пакеты: `kcptun-client`, `xray-core` dan `libcap-bin`.
    
      ![](https://raw.githubusercontent.com/lrdrdn/my-opkg-repo/main/preview/preview2.gif)
    

## Cara Install dan Update Paket
Cara instalasi repository ini, dapat menggunakan 2 cara yaitu
- [Menggunakan LuCI](#install-dan-update-paket-menggunakan-luci)
- [Menggunakan Terminal](#install-dan-update-paket-menggunakan-terminal) seperti JuiceSSH/Termius/Termux

### Install dan Update Paket Menggunakan LuCI
  1. Masuk IP LuCI (contoh: 192.168.1.1), Login, Buka **System -> Software -> Configuration**
  2. Tekan tombol **Update Lists**.
  3. Cari nama paket (seperti: `luci-app-passwall`) pada kolom **Filter**.
  4. Tekan tombol **Find Package**.
  5. Scroll sedikit, lihat dibawah ada tab **Installed packages** dan **Available packages** :
      - Installed packages : paket pada daftar tersebut sudah terpasang.
      - Available packages : paket pada dafter tersebut belum terpasang.
  6. Klik **Available packages**, lalu cari nama paket yang di tulis di filter tadi.
  7. Klik tulisan **Install** pada baris yang terdapat pada nama paket tersebut, lalu tunggu hingga instalasi paket selesai.
 
### Install dan Update Paket Menggunakan Terminal
  1. Buka aplikasi terminal yang disuka
  2. Jalankan perintah dibawah ini untuk memperbarui daftar paket yang tersedia di server
      ```
      opkg update
      ```
  
  3. Jalankan perintah `opkg install nama-paket`, ganti `nama-paket` menjadi nama paket yang ada (contoh kali ini akan menggunakan paket `luci-app-passwall`).
      
      ```
      opkg install luci-app-passwall
      ```

## Cara Memeriksa Paket Sudah Terinstal Atau Belum
Cara instalasi repository ini, dapat menggunakan 2 cara yaitu
- [Menggunakan LuCI](#cara-memeriksa-status-paket-dengan-luci)
- [Menggunakan Terminal](#cara-memeriksa-status-paket-dengan-terminal) seperti JuiceSSH/Termius/Termux

### Cara Memeriksa Status Paket dengan LuCI
  1. Masuk IP LuCI (contoh: 192.168.1.1), lalu Login.
      - Jika memasang paket yang terdapat kata `luci-app`, biasanya akan muncul di LuCI System/Services/NAS/VPN/Modem/Network dan lain lain.
      - Jika memasang paket yang terdapat kata `luci-proto`, biasanya akan muncul di **Network -> Pilih salah satu interface -> General Setup -> Protocol**.
      - Jika memasang paket yang terdapat kata `luci-theme`, biasanya akan muncul di **System -> System Properties -> Language and Style -> Design**.
      - Jika memasang paket yang di install tidak terdapat kata luci, maka paket tersebut tidak akan menampilkan apapun di LuCI.

### Cara Memeriksa Status Paket dengan Terminal
  1. Buka terminal
  2. Jalankan perintah `opkg list-installed nama-paket`, ganti `nama-paket` menjadi nama paket yang ada (contoh kali ini akan menggunakan paket `luci-app-passwall`).
      
      ```
      opkg list-installed luci-app-passwall
      ```
      
      Jika di terminal muncul `luci-app-passwall - 4.43-2` maka paket aplikasi sudah terpasang, jika tidak ada maka paket belum terpasang. Angka `4.43-2` pada terminal tadi adalan versi paket aplikasi yang terinstal.
      
      
### Kredit
- [Nugroho](https://radenku.com) sebagai pemilik repo, builder dan yang buat video contoh.
- [Helmi Amirudin](https://helmiau.com/about) sebagai tukang dokumentasi.
