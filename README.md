#  Репозиторий для версий OpenWrt 19-21
Позволяет устанавливать такие пакеты: OpenClash, Passwall, ShadowSocksR+ Plus, Wegare STL, Tiny File Manager, Xderm Mini, v2rayA, Modeminfo.


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
      Через веб интерфейс LuCI 
      Через Terminal

### Через LuCI
     Добавть  # перед option check_signature чтобы получилось так:
  
      # option check_signature

     В поле custom-feeds добавить:

      src/gz custom_generic https://raw.githubusercontent.com/Spothz/my-opkg-repo/main/generic
      src/gz custom_arch https://raw.githubusercontent.com/Spothz/my-opkg-repo/main/mipsel_24kc
    
      Вместо **mipsel_24kc** вписать архитектуру своего роутера.
 
### Через Terminal
  Скопитуйте и вставте в терминал строки, определение архитектуры произойдёт автоматически:
      
      sed -i 's/option check_signature/# option check_signature/g' /etc/opkg.conf
      echo "src/gz custom_generic https://raw.githubusercontent.com/Spothz/my-opkg-repo/main/generic" >> /etc/opkg/customfeeds.conf
      echo "src/gz custom_arch https://raw.githubusercontent.com/Spothz/my-opkg-repo/main/$(grep "OPENWRT_ARCH" /etc/os-release | awk -F '"' '{print $2}')" >> /etc/opkg/customfeeds.conf
      
 
### Установка passwall через Terminal
  
      opkg update
      opkg install luci-app-passwall

 ### Для OpenWrt 19.07 нужно установить вручную пакеты:
      opkg install kcptun-client xray-core libcap-bin
      
### Все необходимые для работы пакеты:

      ipset 
      ipt2socks 
      iptables iptables-legacy 
      iptables-mod-iprange
      iptables-mod-socket iptables-mod-tproxy 
      kmod-ipt-nat 
      coreutils 
      coreutils-base64 
      coreutils-nohup 
      curl
      dns2socks 
      ip-full 
      libuci-lua 
      luci-compat
      luci-lib-jsonc 
      microsocks 
      resolveip 
      tcping 
      unzip
      v2ray-extra
      v2ray-geoip
      v2ray-geosite
      v2ray-ctl 
      xray-geodata
