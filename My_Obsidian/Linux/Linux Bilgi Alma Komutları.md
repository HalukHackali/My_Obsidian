#linux 

### Sürüm Versiyon Kontrolü

```bash
[haluk@lenovo ~]$ grep VERSION /etc/os-release
VERSION="37 (KDE Plasma)"
VERSION_ID=37
VERSION_CODENAME=""
REDHAT_BUGZILLA_PRODUCT_VERSION=37
REDHAT_SUPPORT_PRODUCT_VERSION=37
```

* * *

\[haluk@lenovo ~\]$ cat /etc/os-release

```bash
NAME="Nobara Linux"
VERSION="37 (KDE Plasma)"
ID=nobara
ID_LIKE="rhel centos fedora"
VERSION_ID=37
VERSION_CODENAME=""
PLATFORM_ID="platform:f37"
PRETTY_NAME="Nobara Linux 37 (KDE Plasma)"
ANSI_COLOR="0;38;2;60;110;180"
LOGO=nobara-logo-icon
CPE_NAME="cpe:/o:nobaraproject:nobara:37"
HOME_URL="https://www.nobaraproject.org/"
DOCUMENTATION_URL="https://www.nobaraproject.org/"
SUPPORT_URL="https://www.nobaraproject.org/"
BUG_REPORT_URL=""
REDHAT_BUGZILLA_PRODUCT="Nobara"
REDHAT_BUGZILLA_PRODUCT_VERSION=37
REDHAT_SUPPORT_PRODUCT="Nobara"
REDHAT_SUPPORT_PRODUCT_VERSION=37
PRIVACY_POLICY_URL=""
VARIANT="KDE Plasma"
VARIANT_ID=kde
```

* * *

```bash
[haluk@lenovo ~]$ lsb_release -a

LSB Version:    n/a
Distributor ID: ManjaroLinux
Description:    Manjaro Linux
Release:        21.1.6
Codename:       Pahvo
```

* * *

```bash
[haluk@lenovo ~]$ inxi -Fxz
System:
  Kernel: 6.1.14-201.fsync.fc37.x86_64 arch: x86_64 bits: 64 compiler: gcc
    v: 2.38-25.fc37 Desktop: KDE Plasma v: 5.27.2 Distro: Nobara release 37
    (Thirty Seven) base: RHEL 37
Machine:
  Type: Laptop System: LENOVO product: INVALID v: Ideapad 700-15ISK
    serial: <superuser required>
  Mobo: LENOVO model: Ideapad 700-15ISK v: NO DPK
    serial: <superuser required> UEFI: LENOVO v: E5CN63WW date: 06/14/2018
Battery:
  ID-1: BAT0 charge: 33.1 Wh (100.0%) condition: 33.1/45.0 Wh (73.5%)
    volts: 12.2 min: 11.1 model: SMP L14M3P24 status: full
CPU:
  Info: quad core model: Intel Core i7-6700HQ bits: 64 type: MT MCP
    arch: Skylake-S rev: 3 cache: L1: 256 KiB L2: 1024 KiB L3: 6 MiB
  Speed (MHz): avg: 3243 high: 3293 min/max: 800/3500 cores: 1: 3245 2: 3232
    3: 3275 4: 3293 5: 3206 6: 3265 7: 3228 8: 3200 bogomips: 41599
  Flags: avx avx2 ht lm nx pae sse sse2 sse3 sse4_1 sse4_2 ssse3 vmx
Graphics:
  Device-1: Intel HD Graphics 530 vendor: Lenovo driver: i915 v: kernel
    arch: Gen-9 bus-ID: 00:02.0
  Device-2: NVIDIA GM107M [GeForce GTX 950M] vendor: Lenovo driver: nvidia
    v: 525.85.05 arch: Maxwell bus-ID: 01:00.0
  Device-3: Syntek Lenovo EasyCamera type: USB driver: uvcvideo
    bus-ID: 1-5:3
  Display: wayland server: X.org v: 1.20.14 with: Xwayland v: 22.1.7
    compositor: kwin_wayland driver: X: loaded: modesetting,nvidia
    unloaded: fbdev,nouveau,vesa dri: iris gpu: i915,nvidia
    resolution: 1920x1080
  API: OpenGL v: 4.6 Mesa 23.0.0 renderer: Mesa Intel HD Graphics 530 (SKL
    GT2) direct-render: Yes
Audio:
  Device-1: Intel 100 Series/C230 Series Family HD Audio vendor: Lenovo
    driver: snd_hda_intel v: kernel bus-ID: 00:1f.3
  Sound API: ALSA v: k6.1.14-201.fsync.fc37.x86_64 running: yes
  Sound Server-1: PulseAudio v: 16.1 running: no
  Sound Server-2: PipeWire v: 0.3.66 running: yes
Network:
  Device-1: Intel Dual Band Wireless-AC 3165 Plus Bluetooth driver: iwlwifi
    v: kernel bus-ID: 02:00.0
  IF: wlp2s0 state: up mac: <filter>
  Device-2: Realtek RTL8111/8168/8411 PCI Express Gigabit Ethernet
    vendor: Lenovo driver: r8169 v: kernel port: c000 bus-ID: 03:00.0
  IF: enp3s0 state: up speed: 100 Mbps duplex: full mac: <filter>
Bluetooth:
  Device-1: Intel Bluetooth wireless interface type: USB driver: btusb v: 0.8
    bus-ID: 1-7:4
  Report: rfkill ID: hci0 rfk-id: 4 state: up address: see --recommends
Drives:
  Local Storage: total: 238.47 GiB used: 69.34 GiB (29.1%)
  ID-1: /dev/nvme0n1 vendor: Samsung model: MZVLV256HCHP-000L2
    size: 238.47 GiB temp: 37.9 C
Partition:
  ID-1: / size: 236.88 GiB used: 69.1 GiB (29.2%) fs: btrfs
    dev: /dev/nvme0n1p3
  ID-2: /boot size: 973.4 MiB used: 225.9 MiB (23.2%) fs: ext4
    dev: /dev/nvme0n1p2
  ID-3: /boot/efi size: 598.8 MiB used: 17.3 MiB (2.9%) fs: vfat
    dev: /dev/nvme0n1p1
  ID-4: /home size: 236.88 GiB used: 69.1 GiB (29.2%) fs: btrfs
    dev: /dev/nvme0n1p3
Swap:
  ID-1: swap-1 type: zram size: 8 GiB used: 48.5 MiB (0.6%) dev: /dev/zram0
Sensors:
  System Temperatures: cpu: 45.0 C pch: 57.0 C mobo: N/A
  Fan Speeds (RPM): N/A
Info:
  Processes: 358 Uptime: 5h 28m Memory: 15.42 GiB used: 8.36 GiB (54.2%)
  Init: systemd target: graphical (5) Compilers: gcc: 12.2.1 clang: 15.0.7
  Packages: 32 note: see --rpm Shell: Bash v: 5.2.15 inxi: 3.3.25
```

* * *

## Kernel Listeleme

```
[haluk@lenovo ~]$ rpm -qa kernel
kernel-6.1.11-201.fsync.fc37.x86_64
kernel-6.1.14-201.fsync.fc37.x86_64
```

* * *

## Ortamları ya da Kısımlarını Yazdırır

**\[haluk@lenovo ~\]$** ==printenv==

* * *

**\[haluk@lenovo ~\]$** ==lshw==

```bash
WARNING: you should run this program as super-user.
lenovo                      
    description: Computer
    width: 64 bits
    capabilities: smp vsyscall32
  *-core
       description: Motherboard
       physical id: 0
     *-memory
          description: System memory
          physical id: 0
          size: 16GiB
     *-cpu
          product: Intel(R) Core(TM) i7-6700HQ CPU @ 2.60GHz
          vendor: Intel Corp.
          physical id: 1
          bus info: cpu@0
          size: 3295MHz
          capacity: 3500MHz
          width: 64 bits
          capabilities: fpu fpu_exception wp vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp x86-64 constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp md_clear flush_l1d arch_capabilities cpufreq
     *-pci
          description: Host bridge
          product: Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Host Bridge/DRAM Registers
          vendor: Intel Corporation
          physical id: 100
          bus info: pci@0000:00:00.0
          version: 07
          width: 32 bits
          clock: 33MHz
          configuration: driver=skl_uncore
          resources: irq:0
        *-pci:0
             description: PCI bridge
             product: 6th-10th Gen Core Processor PCIe Controller (x16)
             vendor: Intel Corporation
             physical id: 1
             bus info: pci@0000:00:01.0
             version: 07
             width: 32 bits
             clock: 33MHz
             capabilities: pci normal_decode bus_master cap_list
             configuration: driver=pcieport
             resources: irq:120 ioport:d000(size=4096) memory:d1000000-d1ffffff ioport:a0000000(size=301989888)
           *-display
                description: 3D controller
                product: GM107M [GeForce GTX 950M]
                vendor: NVIDIA Corporation
                physical id: 0
                bus info: pci@0000:01:00.0
                version: a2
                width: 64 bits
                clock: 33MHz
                capabilities: bus_master cap_list rom
                configuration: driver=nvidia latency=0
                resources: irq:139 memory:d1000000-d1ffffff memory:a0000000-afffffff memory:b0000000-b1ffffff ioport:d000(size=128)
        *-display
             description: VGA compatible controller
             product: HD Graphics 530
             vendor: Intel Corporation
             physical id: 2
             bus info: pci@0000:00:02.0
             version: 06
             width: 64 bits
             clock: 33MHz
             capabilities: vga_controller bus_master cap_list rom
             configuration: driver=i915 latency=0
             resources: irq:136 memory:d0000000-d0ffffff memory:c0000000-cfffffff ioport:e000(size=64) memory:c0000-dffff
        *-usb
             description: USB controller
             product: 100 Series/C230 Series Chipset Family USB 3.0 xHCI Controller
             vendor: Intel Corporation
             physical id: 14
             bus info: pci@0000:00:14.0
             version: 31
             width: 64 bits
             clock: 33MHz
             capabilities: xhc_ bus_master cap_list
             configuration: driver=xhci_hcd latency=0
             resources: irq:125 memory:d2300000-d230ffff
        *-generic:0
             description: Signal processing controller
             product: 100 Series/C230 Series Chipset Family Thermal Subsystem
             vendor: Intel Corporation
             physical id: 14.2
             bus info: pci@0000:00:14.2
             version: 31
             width: 64 bits
             clock: 33MHz
             capabilities: cap_list
             configuration: driver=intel_pch_thermal latency=0
             resources: irq:18 memory:d232a000-d232afff
        *-communication UNCLAIMED
             description: Communication controller
             product: 100 Series/C230 Series Chipset Family MEI Controller #1
             vendor: Intel Corporation
             physical id: 16
             bus info: pci@0000:00:16.0
             version: 31
             width: 64 bits
             clock: 33MHz
             capabilities: cap_list
             configuration: latency=0
             resources: memory:d232c000-d232cfff
        *-sata
             description: SATA controller
             product: HM170/QM170 Chipset SATA Controller [AHCI Mode]
             vendor: Intel Corporation
             physical id: 17
             bus info: pci@0000:00:17.0
             version: 31
             width: 32 bits
             clock: 66MHz
             capabilities: sata ahc__1.0 bus_master cap_list
             configuration: driver=ahci latency=0
             resources: irq:124 memory:d2328000-d2329fff memory:d2330000-d23300ff ioport:e080(size=8) ioport:e088(size=4) ioport:e060(size=32) memory:d232e000-d232e7ff
        *-pci:1
             description: PCI bridge
             product: 100 Series/C230 Series Chipset Family PCI Express Root Port #5
             vendor: Intel Corporation
             physical id: 1c
             bus info: pci@0000:00:1c.0
             version: f1
             width: 32 bits
             clock: 33MHz
             capabilities: pci normal_decode bus_master cap_list
             configuration: driver=pcieport
             resources: irq:121 memory:d2200000-d22fffff
           *-network
                description: Wireless interface
                product: Dual Band Wireless-AC 3165 Plus Bluetooth
                vendor: Intel Corporation
                physical id: 0
                bus info: pci@0000:02:00.0
                logical name: wlp2s0
                version: 99
                serial: 68:07:15:51:dc:d1
                width: 64 bits
                clock: 33MHz
                capabilities: bus_master cap_list ethernet physical wireless
                configuration: broadcast=yes driver=iwlwifi driverversion=6.1.14-201.fsync.fc37.x86_64 firmware=29.4063824552.0 7265D-29.ucode ip=192.168.1.107 latency=0 link=yes multicast=yes wireless=IEEE 802.11
                resources: irq:137 memory:d2200000-d2201fff
        *-pci:2
             description: PCI bridge
             product: 100 Series/C230 Series Chipset Family PCI Express Root Port #6
             vendor: Intel Corporation
             physical id: 1c.5
             bus info: pci@0000:00:1c.5
             version: f1
             width: 32 bits
             clock: 33MHz
             capabilities: pci normal_decode bus_master cap_list
             configuration: driver=pcieport
             resources: irq:122 ioport:c000(size=4096) memory:d2100000-d21fffff
           *-network
                description: Ethernet interface
                product: RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller
                vendor: Realtek Semiconductor Co., Ltd.
                physical id: 0
                bus info: pci@0000:03:00.0
                logical name: enp3s0
                version: 15
                serial: 54:ee:75:aa:5e:c1
                size: 100Mbit/s
                capacity: 1Gbit/s
                width: 64 bits
                clock: 33MHz
                capabilities: bus_master cap_list ethernet physical tp mii 10bt 10bt-fd 100bt 100bt-fd 1000bt-fd autonegotiation
                configuration: autonegotiation=on broadcast=yes driver=r8169 driverversion=6.1.14-201.fsync.fc37.x86_64 duplex=full firmware=rtl8168h-2_0.0.2 02/26/15 ip=192.168.1.109 latency=0 link=yes multicast=yes port=twisted pair speed=100Mbit/s
                resources: irq:17 ioport:c000(size=256) memory:d2104000-d2104fff memory:d2100000-d2103fff
        *-pci:3
             description: PCI bridge
             product: 100 Series/C230 Series Chipset Family PCI Express Root Port #9
             vendor: Intel Corporation
             physical id: 1d
             bus info: pci@0000:00:1d.0
             version: f1
             width: 32 bits
             clock: 33MHz
             capabilities: pci normal_decode bus_master cap_list
             configuration: driver=pcieport
             resources: irq:123 ioport:b000(size=4096) memory:d2000000-d20fffff
           *-nvme
                description: NVMe device
                product: SAMSUNG MZVLV256HCHP-000L2
                vendor: Samsung Electronics Co Ltd
                physical id: 0
                bus info: pci@0000:04:00.0
                logical name: /dev/nvme0
                version: 5L0QBXV7
                serial: S27WNX0H812975
                width: 64 bits
                clock: 33MHz
                capabilities: nvme nvm_express bus_master cap_list
                configuration: driver=nvme latency=0 nqn=nqn.2014.08.org.nvmexpress:144d144dS27WNX0H812975      SAMSUNG MZVLV256HCHP-000L2 state=live
                resources: irq:16 memory:d2000000-d2003fff ioport:b000(size=256)
              *-namespace:0
                   description: NVMe disk
                   physical id: 0
                   logical name: hwmon3
              *-namespace:1
                   description: NVMe disk
                   physical id: 2
                   logical name: /dev/ng0n1
              *-namespace:2
                   description: NVMe disk
                   physical id: 1
                   bus info: nvme@0:1
                   logical name: /dev/nvme0n1
                   configuration: wwid=nvme.144d-533237574e583048383132393735-53414d53554e47204d5a564c56323536484348502d3030304c32-00000001
        *-generic:1
             description: Signal processing controller
             product: 100 Series/C230 Series Chipset Family Serial IO UART #0
             vendor: Intel Corporation
             physical id: 1e
             bus info: pci@0000:00:1e.0
             version: 31
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=intel-lpss latency=0
             resources: irq:20 memory:d232d000-d232dfff
        *-isa
             description: ISA bridge
             product: HM170 Chipset LPC/eSPI Controller
             vendor: Intel Corporation
             physical id: 1f
             bus info: pci@0000:00:1f.0
             version: 31
             width: 32 bits
             clock: 33MHz
             capabilities: isa bus_master
             configuration: latency=0
        *-memory UNCLAIMED
             description: Memory controller
             product: 100 Series/C230 Series Chipset Family Power Management Controller
             vendor: Intel Corporation
             physical id: 1f.2
             bus info: pci@0000:00:1f.2
             version: 31
             width: 32 bits
             clock: 33MHz (30.3ns)
             configuration: latency=0
             resources: memory:d2324000-d2327fff
        *-multimedia
             description: Audio device
             product: 100 Series/C230 Series Chipset Family HD Audio Controller
             vendor: Intel Corporation
             physical id: 1f.3
             bus info: pci@0000:00:1f.3
             version: 31
             width: 64 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=snd_hda_intel latency=64
             resources: irq:138 memory:d2320000-d2323fff memory:d2310000-d231ffff
        *-serial
             description: SMBus
             product: 100 Series/C230 Series Chipset Family SMBus
             vendor: Intel Corporation
             physical id: 1f.4
             bus info: pci@0000:00:1f.4
             version: 31
             width: 64 bits
             clock: 33MHz
             configuration: driver=i801_smbus latency=0
             resources: irq:16 memory:d232f000-d232f0ff ioport:efa0(size=32)
     *-pnp00:00
          product: PnP device PNP0c02
          physical id: 2
          capabilities: pnp
          configuration: driver=system
     *-pnp00:01
          product: PnP device PNP0c02
          physical id: 3
          capabilities: pnp
          configuration: driver=system
     *-pnp00:02
          product: PnP device PNP0c02
          physical id: 4
          capabilities: pnp
          configuration: driver=system
     *-pnp00:03
          product: PnP device PNP0c02
          physical id: 5
          capabilities: pnp
          configuration: driver=system
     *-pnp00:04
          product: PnP device PNP0b00
          physical id: 6
          capabilities: pnp
          configuration: driver=rtc_cmos
     *-pnp00:05
          product: PnP device INT3f0d
          vendor: Interphase Corporation
          physical id: 7
          capabilities: pnp
          configuration: driver=system
     *-pnp00:06
          product: PnP device PNP0303
          physical id: 8
          capabilities: pnp
          configuration: driver=i8042 kbd
     *-pnp00:07
          product: PnP device SYN2b61
          vendor: Synaptics Inc
          physical id: 9
          capabilities: pnp
          configuration: driver=i8042 aux
     *-pnp00:08
          product: PnP device PNP0c02
          physical id: a
          capabilities: pnp
          configuration: driver=system
     *-pnp00:09
          product: PnP device PNP0c02
          physical id: b
          capabilities: pnp
          configuration: driver=system
WARNING: output may be incomplete or inaccurate, you should run this program as super-user.
```

* * *

**\[haluk@lenovo ~\]$ ==lsusb==**

```bash
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 8087:0a2a Intel Corp. Bluetooth wireless interface
Bus 001 Device 003: ID 174f:14e6 Syntek Lenovo EasyCamera
Bus 001 Device 002: ID 046d:c534 Logitech, Inc. Unifying Receiver
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

* * *

**\[haluk@lenovo ~\]$ ==wc dosya_adı.py==**

Dosyanızdaki satır, kelime, karakter ve byte sayısını gösteriyor.

Örneğin `wc dosyam.odt` yazdığınızda karşınıza şöyle bir sonuç çıkaracaktır:

`88 454 22378 dosyam.odt`

Bu da dosyamda **88** satır **454** kelime olduğu anlamına geliyor. **22378** ise dosyanın boyutunu byte olarak ifade ediyor.

`-l` argümanıyla sadece satır sayısını,

`-w` argümanıyla sadece kelime sayısını,

`-m` argümanıyla sadece karakter sayısını ve

`-c`argümanıyla sadece byte değerini görebilirsiniz.