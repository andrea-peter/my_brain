# 01 - Build

[https://www.youtube.com/watch?v=fY7u6PiV8qA\&list=PLRsiDZNEIs\_T-AjQROqpwlzdLoJCkRab7](https://www.youtube.com/watch?v=fY7u6PiV8qA\&list=PLRsiDZNEIs_T-AjQROqpwlzdLoJCkRab7)

#### Clone YOCTO poky release

```
git clone -b scarthgap git://git.yoctoproject.org/poky poky-rpi
```

#### Clone BSP layer `meta-raspberrypi`

```
cd poky-rpi
git clone -b scarthgap https://github.com/agherzan/meta-raspberrypi.git
```

#### Setup environment

```
source oe-init-build-env
```

this should cd into `build/`

#### Add meta-raspberrypi layer

```
bitbake-layers add-layer ../meta-raspberrypi/
```

This should add the layer in `config/bblayers.conf`

#### Adjust `conf/local.conf`, append the following lines:

```
MACHINE = "raspberrypi5"

INIT_MANAGER = "systemd"

LICENSE_FLAGS_ACCEPTED = "synaptics-killswitch"
```

{% hint style="info" %}
On Ubuntu 24.04 you need to adjust an apparmor setting

Edit the file `/etc/sysctl.d/60_apparmor-namespace.conf`, add the following file:

```
kernel.apparmor_restrict_unprivileged_userns=0
```
{% endhint %}

#### Deactivate pyenv

First we need to deactivate pynev, otherwise we have the error:

```
pyenv/libexec/pyenv-exec: Argument list too long
```

so comment out the pyenv initialization in our `.bashrc`

#### Build image (this will take a lot of time the first time)

```
bitbake core-image-base
```

The images are output in

```
build/tmp/deploy/images/raspberyypi5/
```

Our image is&#x20;

```
build/tmp/deploy/images/raspberrypi5/core-image-base-raspberrypi5.rootfs.wic.bz2
```

## Flash image on uSD card

```
bzcat build/tmp/deploy/images/raspberrypi5/core-image-base-raspberrypi5.rootfs.wic.bz2 | sudo dd of=/dev/sdb
```

## Boot with debug probe

```
picocom -b 115200 /dev/ACM0
```

<details>

<summary>Reference boot messages</summary>

```
RPi: BOOTSYS release VERSION:4c845bd3 DATE: 2024/02/16 TIME: 15:28:41
BOOTMODE: 0x06 partition 0 build-ts BUILD_TIMESTAMP=1708097321 serial bd7106ae boardrev c04170 stc 824325
AON_RESET: 00000003 PM_RSTS 00001000
RP1_BOOT chip ID: 0x20001927
PM_RSTS: 0x00001000
part 00000000 reset_info 00000000
PMIC reset-event 00000000 rtc 00000000 alarm 00000000 enabled 0
uSD voltage 3.3V
Initialising SDRAM 'Micron' 16Gb x2 total-size: 32 Gbit 4267
DDR 4267 1 0 32 152
RP1_BOOT chip ID: 0x20001927

RP1_BOOT chip ID: 0x20001927
RP1_BOOT: fw size 25968
PCI2 init
PCI2 reset
PCIe scan 00001de4:00000001
RP1_CHIP_INFO 20001927

RPi: BOOTLOADER release VERSION:4c845bd3 DATE: 2024/02/16 TIME: 15:28:41
BOOTMODE: 0x06 partition 0 build-ts BUILD_TIMESTAMP=1708097321 serial bd7106ae boardrev c04170 stc 3851885
AON_RESET: 00000003 PM_RSTS 00001000
M.2 PCIe HAT not detected.
usb_pd_init status 0
XHCI-STOP
xHC0 ver: 272 HCS: 03000440 140000f1 07ff000a HCC: 0240fe6d
USBSTS 1
xHC0 ver: 272 HCS: 03000440 140000f1 07ff000a HCC: 0240fe6d
xHC0 ports 3 slots 64 intrs 4
XHCI-STOP
xHC1 ver: 272 HCS: 03000440 140000f1 07ff000a HCC: 0240fe6d
USBSTS 1
xHC1 ver: 272 HCS: 03000440 140000f1 07ff000a HCC: 0240fe6d
xHC1 ports 3 slots 64 intrs 4
Boot mode: SD (01) order f4
SD HOST: 200000000 CTL0: 0x00800000 BUS: 400000 Hz actual: 390625 HZ div: 512 (256) status: 0x1fff0000 delay: 276
SD HOST: 200000000 CTL0: 0x00800f00 BUS: 400000 Hz actual: 390625 HZ div: 512 (256) status: 0x1fff0000 delay: 276
OCR c0ff8000 [116]
CID: 004134325344344742305de800e700f3
CSD: 400e00325b5900001d6f7f800a400000
SD: bus-width: 4 spec: 2 SCR: 0x02358003 0x00000000
SD HOST: 200000000 CTL0: 0x00800f04 BUS: 50000000 Hz actual: 50000000 HZ div: 4 (2) status: 0x1fff0000 delay: 2
MBR: 0x00002000,  266240 type: 0x0c
MBR: 0x00044000,  575078 type: 0x83
MBR: 0x00000000,       0 type: 0x00
MBR: 0x00000000,       0 type: 0x00
Trying partition: 0
type: 16 lba: 8192 'mkfs.fat' '  V       ^ ' clusters 33241 (8)
rsc 8 fat-sectors 136 root dir cluster 1 sectors 32 entries 512
FAT16 clusters 33241
[sdcard] autoboot.txt not found
Select partition rsts 0 C(boot_partition) 0 EEPROM config 0 result 0
Trying partition: 0
type: 16 lba: 8192 'mkfs.fat' '  V       ^ ' clusters 33241 (8)
rsc 8 fat-sectors 136 root dir cluster 1 sectors 32 entries 512
FAT16 clusters 33241
Read config.txt bytes     2505 hnd 0x24
[sdcard] pieeprom.upd not found
usb_max_current_enable default 0 max-current 3000
Read bcm2712-rpi-5-b.dtb bytes    81203 hnd 0x2
dt-match: compatible: raspberrypi,5-model-b match: brcm,bcm2712
dt-match: compatible: brcm,bcm2712 match: brcm,bcm2712
Selecting USB low current limit

NOTICE:  BL31: v2.6(release):v2.6-239-g2a9ede0bd
NOTICE:  BL31: Built : 14:26:57, Jun 22 2023
[    0.000000] Booting Linux on physical CPU 0x0000000000 [0x414fd0b1]
[    0.000000] Linux version 6.6.63-v8-16k (oe-user@oe-host) (aarch64-poky-linux-gcc (GCC) 13.3.0, GNU ld (GNU Binutils) 2.42.0.20240723) #1 SMP PREEMPT Fri Dec  6 10:10:05 UTC 2024
[    0.000000] KASLR enabled
[    0.000000] random: crng init done
[    0.000000] Machine model: Raspberry Pi 5 Model B Rev 1.0
[    0.000000] efi: UEFI not found.
[    0.000000] Reserved memory: created CMA memory pool at 0x0000000002000000, size 64 MiB
[    0.000000] OF: reserved mem: initialized node linux,cma, compatible id shared-dma-pool
[    0.000000] OF: reserved mem: 0x0000000002000000..0x0000000005ffffff (65536 KiB) map reusable linux,cma
[    0.000000] OF: reserved mem: 0x0000000000000000..0x000000000007ffff (512 KiB) nomap non-reusable atf@0
[    0.000000] OF: reserved mem: 0x000000003fd16ac0..0x000000003fd16af7 (0 KiB) nomap non-reusable nvram@0
[    0.000000] NUMA: No NUMA configuration found
[    0.000000] NUMA: Faking a node at [mem 0x0000000000000000-0x00000000ffffffff]
[    0.000000] NUMA: NODE_DATA [mem 0xffd892c0-0xffd8bfff]
[    0.000000] Zone ranges:
[    0.000000]   DMA      [mem 0x0000000000000000-0x00000000ffffffff]
[    0.000000]   DMA32    empty
[    0.000000]   Normal   empty
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000000000000-0x000000000007ffff]
[    0.000000]   node   0: [mem 0x0000000000080000-0x000000003fbfffff]
[    0.000000]   node   0: [mem 0x0000000040000000-0x00000000ffffffff]
[    0.000000] Initmem setup node 0 [mem 0x0000000000000000-0x00000000ffffffff]
[    0.000000] On node 0, zone DMA: 256 pages in unavailable ranges
[    0.000000] psci: probing for conduit method from DT.
[    0.000000] psci: PSCIv1.1 detected in firmware.
[    0.000000] psci: Using standard PSCI v0.2 function IDs
[    0.000000] psci: MIGRATE_INFO_TYPE not supported.
[    0.000000] psci: SMC Calling Convention v1.2
[    0.000000] percpu: Embedded 14 pages/cpu s185192 r8192 d35992 u229376
[    0.000000] Detected PIPT I-cache on CPU0
[    0.000000] CPU features: detected: Virtualization Host Extensions
[    0.000000] CPU features: detected: Hardware dirty bit management
[    0.000000] CPU features: detected: Spectre-v4
[    0.000000] CPU features: detected: Spectre-BHB
[    0.000000] CPU features: kernel page table isolation forced ON by KASLR
[    0.000000] CPU features: detected: Kernel page table isolation (KPTI)
[    0.000000] CPU features: detected: SSBS not fully self-synchronizing
[    0.000000] alternatives: applying boot alternatives
[    0.000000] Kernel command line: reboot=w coherent_pool=1M 8250.nr_uarts=1 pci=pcie_bus_safe cgroup_disable=memory numa_policy=interleave  smsc95xx.macaddr=2C:CF:67:5E:38:58 vc_mem.mem_base=0x3fc00000 vc_mem.mem_size=0x40000000  dwc_otg.lpm_enable=0 root=/dev/mmcblk0p2 rootfstype=ext4 rootwait  net.ifnames=0
[    0.000000] cgroup: Disabling memory control group subsystem
[    0.000000] mempolicy: NUMA default policy overridden to 'interleave:0'
[    0.000000] Dentry cache hash table entries: 524288 (order: 8, 4194304 bytes, linear)
[    0.000000] Inode-cache hash table entries: 262144 (order: 7, 2097152 bytes, linear)
[    0.000000] Fallback order for Node 0: 0 
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 260864
[    0.000000] Policy zone: DMA
[    0.000000] mem auto-init: stack:all(zero), heap alloc:off, heap free:off
[    0.000000] Memory: 4069712K/4190208K available (14528K kernel code, 2268K rwdata, 4736K rodata, 5376K init, 1228K bss, 54960K reserved, 65536K cma-reserved)
[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=4, Nodes=1
[    0.000000] ftrace: allocating 46941 entries in 46 pages
[    0.000000] ftrace: allocated 46 pages with 4 groups
[    0.000000] trace event string verifier disabled
[    0.000000] rcu: Preemptible hierarchical RCU implementation.
[    0.000000] rcu: 	RCU event tracing is enabled.
[    0.000000] rcu: 	RCU restricting CPUs from NR_CPUS=256 to nr_cpu_ids=4.
[    0.000000] 	Trampoline variant of Tasks RCU enabled.
[    0.000000] 	Rude variant of Tasks RCU enabled.
[    0.000000] 	Tracing variant of Tasks RCU enabled.
[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 25 jiffies.
[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=4
[    0.000000] NR_IRQS: 64, nr_irqs: 64, preallocated irqs: 0
[    0.000000] Root IRQ handler: gic_handle_irq
[    0.000000] GIC: Using split EOI/Deactivate mode
[    0.000000] rcu: srcu_init: Setting srcu_struct sizes based on contention.
[    0.000000] arch_timer: cp15 timer(s) running at 54.00MHz (phys).
[    0.000000] clocksource: arch_sys_counter: mask: 0xffffffffffffff max_cycles: 0xc743ce346, max_idle_ns: 440795203123 ns
[    0.000000] sched_clock: 56 bits at 54MHz, resolution 18ns, wraps every 4398046511102ns
[    0.000236] Console: colour dummy device 80x25
[    0.000241] printk: console [tty0] enabled
[    0.000517] Calibrating delay loop (skipped), value calculated using timer frequency.. 108.00 BogoMIPS (lpj=216000)
[    0.000529] pid_max: default: 32768 minimum: 301
[    0.000567] LSM: initializing lsm=capability,integrity
[    0.000640] Mount-cache hash table entries: 8192 (order: 2, 65536 bytes, linear)
[    0.000657] Mountpoint-cache hash table entries: 8192 (order: 2, 65536 bytes, linear)
[    0.001417] RCU Tasks: Setting shift to 2 and lim to 1 rcu_task_cb_adjust=1 rcu_task_cpu_ids=4.
[    0.001457] RCU Tasks Rude: Setting shift to 2 and lim to 1 rcu_task_cb_adjust=1 rcu_task_cpu_ids=4.
[    0.001491] RCU Tasks Trace: Setting shift to 2 and lim to 1 rcu_task_cb_adjust=1 rcu_task_cpu_ids=4.
[    0.001572] rcu: Hierarchical SRCU implementation.
[    0.001578] rcu: 	Max phase no-delay instances is 1000.
[    0.002439] EFI services will not be available.
[    0.002531] smp: Bringing up secondary CPUs ...
[    0.002736] Detected PIPT I-cache on CPU1
[    0.002791] CPU1: Booted secondary processor 0x0000000100 [0x414fd0b1]
[    0.003028] Detected PIPT I-cache on CPU2
[    0.003075] CPU2: Booted secondary processor 0x0000000200 [0x414fd0b1]
[    0.003289] Detected PIPT I-cache on CPU3
[    0.003332] CPU3: Booted secondary processor 0x0000000300 [0x414fd0b1]
[    0.003374] smp: Brought up 1 node, 4 CPUs
[    0.003402] SMP: Total of 4 processors activated.
[    0.003408] CPU features: detected: 32-bit EL0 Support
[    0.003414] CPU features: detected: Data cache clean to the PoU not required for I/D coherence
[    0.003420] CPU features: detected: Common not Private translations
[    0.003426] CPU features: detected: CRC32 instructions
[    0.003432] CPU features: detected: RCpc load-acquire (LDAPR)
[    0.003437] CPU features: detected: LSE atomic instructions
[    0.003443] CPU features: detected: Privileged Access Never
[    0.003448] CPU features: detected: RAS Extension Support
[    0.003454] CPU features: detected: Speculative Store Bypassing Safe (SSBS)
[    0.003501] CPU: All CPU(s) started at EL2
[    0.003506] alternatives: applying system-wide alternatives
[    0.005648] devtmpfs: initialized
[    0.009969] Enabled cp15_barrier support
[    0.009983] Enabled setend support
[    0.010108] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7645041785100000 ns
[    0.010121] futex hash table entries: 1024 (order: 2, 65536 bytes, linear)
[    0.010393] pinctrl core: initialized pinctrl subsystem
[    0.010556] DMI not present or invalid.
[    0.010755] NET: Registered PF_NETLINK/PF_ROUTE protocol family
[    0.011449] DMA: preallocated 1024 KiB GFP_KERNEL pool for atomic allocations
[    0.011521] DMA: preallocated 1024 KiB GFP_KERNEL|GFP_DMA pool for atomic allocations
[    0.011597] DMA: preallocated 1024 KiB GFP_KERNEL|GFP_DMA32 pool for atomic allocations
[    0.011623] audit: initializing netlink subsys (disabled)
[    0.011689] audit: type=2000 audit(0.008:1): state=initialized audit_enabled=0 res=1
[    0.011871] thermal_sys: Registered thermal governor 'step_wise'
[    0.011887] cpuidle: using governor menu
[    0.011975] hw-breakpoint: found 6 breakpoint and 4 watchpoint registers.
[    0.012019] ASID allocator initialised with 32768 entries
[    0.012474] Serial: AMBA PL011 UART driver
[    0.013899] bcm2835-mbox 107c013880.mailbox: mailbox enabled
[    0.014436] 107d001000.serial: ttyAMA10 at MMIO 0x107d001000 (irq = 15, base_baud = 0) is a PL011 rev2
[    0.014456] printk: console [ttyAMA10] enabled
[    0.778801] raspberrypi-firmware soc:firmware: Attached to firmware from 2024-02-16T15:28:41, variant start_cd
[    0.792858] raspberrypi-firmware soc:firmware: Firmware hash is 4c845bd300000000000000000000000000000000
[    0.810079] Modules: 2G module region forced by RANDOMIZE_MODULE_REGION_FULL
[    0.817169] Modules: 0 pages in range for non-PLT usage
[    0.817171] Modules: 129292 pages in range for PLT usage
[    0.827111] bcm2835-dma 1000010000.dma: DMA legacy API manager, dmachans=0x1
[    0.840064] iommu: Default domain type: Translated
[    0.844891] iommu: DMA domain TLB invalidation policy: strict mode
[    0.851563] SCSI subsystem initialized
[    0.855389] usbcore: registered new interface driver usbfs
[    0.860914] usbcore: registered new interface driver hub
[    0.866258] usbcore: registered new device driver usb
[    0.871474] pps_core: LinuxPPS API ver. 1 registered
[    0.876459] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    0.885638] PTP clock support registered
[    0.889638] Advanced Linux Sound Architecture Driver Initialized.
[    0.896062] vgaarb: loaded
[    0.898901] clocksource: Switched to clocksource arch_sys_counter
[    1.269585] VFS: Disk quotas dquot_6.6.0
[    1.273567] VFS: Dquot-cache hash table entries: 2048 (order 0, 16384 bytes)
[    1.280694] FS-Cache: Loaded
[    1.283635] CacheFiles: Loaded
[    1.288962] NET: Registered PF_INET protocol family
[    1.293984] IP idents hash table entries: 65536 (order: 5, 524288 bytes, linear)
[    1.303272] tcp_listen_portaddr_hash hash table entries: 2048 (order: 1, 32768 bytes, linear)
[    1.311868] Table-perturb hash table entries: 65536 (order: 4, 262144 bytes, linear)
[    1.319650] TCP established hash table entries: 32768 (order: 4, 262144 bytes, linear)
[    1.327802] TCP bind hash table entries: 32768 (order: 6, 1048576 bytes, linear)
[    1.336036] TCP: Hash tables configured (established 32768 bind 32768)
[    1.342723] MPTCP token hash table entries: 4096 (order: 2, 98304 bytes, linear)
[    1.350205] UDP hash table entries: 2048 (order: 2, 65536 bytes, linear)
[    1.357009] UDP-Lite hash table entries: 2048 (order: 2, 65536 bytes, linear)
[    1.364301] NET: Registered PF_UNIX/PF_LOCAL protocol family
[    1.370132] RPC: Registered named UNIX socket transport module.
[    1.376085] RPC: Registered udp transport module.
[    1.380809] RPC: Registered tcp transport module.
[    1.385530] RPC: Registered tcp-with-tls transport module.
[    1.391043] RPC: Registered tcp NFSv4.1 backchannel transport module.
[    1.397518] PCI: CLS 0 bytes, default 64
[    1.401700] kvm [1]: IPA Size Limit: 40 bits
[    1.406008] kvm [1]: GICV region size/alignment is unsafe, using trapping (reduced performance)
[    1.414774] kvm [1]: vgic interrupt IRQ9
[    1.418728] kvm [1]: VHE mode initialized successfully
[    1.424415] Initialise system trusted keyrings
[    1.428936] workingset: timestamp_bits=42 max_order=18 bucket_order=0
[    1.435430] zbud: loaded
[    1.438158] NFS: Registering the id_resolver key type
[    1.443240] Key type id_resolver registered
[    1.447439] Key type id_legacy registered
[    1.451468] nfs4filelayout_init: NFSv4 File Layout Driver Registering...
[    1.458199] nfs4flexfilelayout_init: NFSv4 Flexfile Layout Driver Registering...
[    1.465673] F2FS not supported on PAGE_SIZE(16384) != 4096
[    1.471250] Key type asymmetric registered
[    1.475364] Asymmetric key parser 'x509' registered
[    1.480276] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 246)
[    1.487745] io scheduler mq-deadline registered
[    1.492296] io scheduler kyber registered
[    1.496330] io scheduler bfq registered
[    1.500466] irq_brcmstb_l2: registered L2 intc (/soc/interrupt-controller@7c502000, parent irq: 26)
[    1.509647] irq_brcmstb_l2: registered L2 intc (/soc/intc@7d503000, parent irq: 27)
[    1.517408] irq_brcmstb_l2: registered L2 intc (/soc/intc@7d508380, parent irq: 28)
[    1.525167] irq_brcmstb_l2: registered L2 intc (/soc/intc@7d508400, parent irq: 29)
[    1.532929] irq_brcmstb_l2: registered L2 intc (/soc/interrupt-controller@7d510600, parent irq: 30)
[    1.542086] irq_brcmstb_l2: registered L2 intc (/soc/intc@7d517b00, parent irq: 31)
[    1.581698] Serial: 8250/16550 driver, 1 ports, IRQ sharing enabled
[    1.588580] 107d50c000.serial: ttyS0 at MMIO 0x107d50c000 (irq = 33, base_baud = 6000000) is a Broadcom BCM7271 UART
[    1.599230] serial serial0: tty port ttyS0 registered
[    1.604754] iproc-rng200 107d208000.rng: hwrng registered
[    1.610261] vc-mem: phys_addr:0x00000000 mem_base=0x3fc00000 mem_size:0x40000000(1024 MiB)
[    1.618889] bcm2712-iommu-cache 1000005b00.iommuc: bcm2712_iommu_cache_probe
[    1.629538] brd: module loaded
[    1.634502] loop: module loaded
[    1.637821] bcm2835-power bcm2835-power: Broadcom BCM2835 power domains driver
[    1.645266] Loading iSCSI transport class v2.0-870.
[    1.651449] usbcore: registered new device driver r8152-cfgselector
[    1.657755] usbcore: registered new interface driver r8152
[    1.663271] usbcore: registered new interface driver lan78xx
[    1.668966] usbcore: registered new interface driver smsc95xx
[    1.674820] dwc_otg: version 3.00a 10-AUG-2012 (platform bus)
[    1.680804] usbcore: registered new interface driver uas
[    1.686152] usbcore: registered new interface driver usb-storage
[    1.692315] mousedev: PS/2 mouse device common for all mice
[    1.705344] rpi-rtc soc:rpi_rtc: registered as rtc0
[    1.711638] rpi-rtc soc:rpi_rtc: setting system clock to 1970-01-01T00:00:09 UTC (9)
[    1.719928] bcm2835-wdt bcm2835-wdt: Poweroff handler already present!
[    1.726493] bcm2835-wdt bcm2835-wdt: Broadcom BCM2835 watchdog timer
[    1.735182] sdhci: Secure Digital Host Controller Interface driver
[    1.741420] sdhci: Copyright(c) Pierre Ossman
[    1.745873] sdhci-pltfm: SDHCI platform and OF driver helper
[    1.751846] ledtrig-cpu: registered to indicate activity on CPUs
[    1.757954] SMCCC: SOC_ID: ARCH_SOC_ID not implemented, skipping ....
[    1.764440] hid: raw HID events driver (C) Jiri Kosina
[    1.769630] usbcore: registered new interface driver usbhid
[    1.775235] usbhid: USB HID core driver
[    1.779551] hw perfevents: enabled with armv8_cortex_a76 PMU driver, 7 counters available
[    1.788442] NET: Registered PF_PACKET protocol family
[    1.793553] Key type dns_resolver registered
[    1.806090] registered taskstats version 1
[    1.810292] Loading compiled-in X.509 certificates
[    1.818866] Key type .fscrypt registered
[    1.822817] Key type fscrypt-provisioning registered
[    1.828693] brcm-pcie 1000120000.pcie: host bridge /axi/pcie@120000 ranges:
[    1.836009] brcm-pcie 1000120000.pcie:   No bus range found for /axi/pcie@120000, using [bus 00-ff]
[    1.845117] brcm-pcie 1000120000.pcie:      MEM 0x1f00000000..0x1ffffffffb -> 0x0000000000
[    1.853427] brcm-pcie 1000120000.pcie:      MEM 0x1c00000000..0x1effffffff -> 0x0400000000
[    1.861751] brcm-pcie 1000120000.pcie:   IB MEM 0x1f00000000..0x1f003fffff -> 0x0000000000
[    1.870063] brcm-pcie 1000120000.pcie:   IB MEM 0x0000000000..0x0fffffffff -> 0x1000000000
[    1.879556] brcm-pcie 1000120000.pcie: Forcing gen 2
[    1.884731] brcm-pcie 1000120000.pcie: PCI host bridge to bus 0000:00
[    1.891235] pci_bus 0000:00: root bus resource [bus 00-ff]
[    1.896763] pci_bus 0000:00: root bus resource [mem 0x1f00000000-0x1ffffffffb] (bus address [0x00000000-0xfffffffb])
[    1.907349] pci_bus 0000:00: root bus resource [mem 0x1c00000000-0x1effffffff pref] (bus address [0x400000000-0x6ffffffff])
[    1.918564] pci 0000:00:00.0: [14e4:2712] type 01 class 0x060400
[    1.924642] pci 0000:00:00.0: PME# supported from D0 D3hot
[    1.931549] pci 0000:00:00.0: bridge configuration invalid ([bus 00-00]), reconfiguring
[    2.046915] brcm-pcie 1000120000.pcie: link up, 5.0 GT/s PCIe x4 (!SSC)
[    2.053582] pci 0000:01:00.0: [1de4:0001] type 00 class 0x020000
[    2.059636] pci 0000:01:00.0: reg 0x10: [mem 0xffffc000-0xffffffff]
[    2.065938] pci 0000:01:00.0: reg 0x14: [mem 0xffc00000-0xffffffff]
[    2.072243] pci 0000:01:00.0: reg 0x18: [mem 0xffff0000-0xffffffff]
[    2.078612] pci 0000:01:00.0: supports D1
[    2.082641] pci 0000:01:00.0: PME# supported from D0 D1 D3hot D3cold
[    2.098934] pci_bus 0000:01: busn_res: [bus 01-ff] end is updated to 01
[    2.105605] pci 0000:00:00.0: BAR 8: assigned [mem 0x1f00000000-0x1f005fffff]
[    2.112783] pci 0000:01:00.0: BAR 1: assigned [mem 0x1f00000000-0x1f003fffff]
[    2.119971] pci 0000:01:00.0: BAR 2: assigned [mem 0x1f00400000-0x1f0040ffff]
[    2.127155] pci 0000:01:00.0: BAR 0: assigned [mem 0x1f00410000-0x1f00413fff]
[    2.134332] pci 0000:00:00.0: PCI bridge to [bus 01]
[    2.139323] pci 0000:00:00.0:   bridge window [mem 0x1f00000000-0x1f005fffff]
[    2.146495] pci 0000:00:00.0: Max Payload Size set to  256/ 512 (was  128), Max Read Rq  512
[    2.154986] pci 0000:01:00.0: Max Payload Size set to  256/ 256 (was  128), Max Read Rq  512
[    2.163554] pcieport 0000:00:00.0: enabling device (0000 -> 0002)
[    2.169738] pcieport 0000:00:00.0: PME: Signaling with IRQ 38
[    2.175595] pcieport 0000:00:00.0: AER: enabled with IRQ 38
[    2.181315] rp1 0000:01:00.0: bar0 len 0x4000, start 0x1f00410000, end 0x1f00413fff, flags, 0x40200
[    2.190410] rp1 0000:01:00.0: bar1 len 0x400000, start 0x1f00000000, end 0x1f003fffff, flags, 0x40200
[    2.199684] rp1 0000:01:00.0: enabling device (0000 -> 0002)
[    2.206866] rp1 0000:01:00.0: chip_id 0x20001927
[    2.217342] genirq: irq_chip rp1_irq_chip did not update eff. affinity mask of irq 100
[    2.241080] macb 1f00100000.ethernet eth0: Cadence GEM rev 0x00070109 at 0x1f00100000 irq 106 (2c:cf:67:5e:38:58)
[    2.252984] dw_axi_dmac_platform 1f00188000.dma: DesignWare AXI DMA Controller, 8 channels
[    2.261671] xhci-hcd xhci-hcd.0: xHCI Host Controller
[    2.266756] xhci-hcd xhci-hcd.0: new USB bus registered, assigned bus number 1
[    2.274496] xhci-hcd xhci-hcd.0: hcc params 0x0240fe6d hci version 0x110 quirks 0x0000008000000810
[    2.283520] xhci-hcd xhci-hcd.0: irq 131, io mem 0x1f00200000
[    2.289391] xhci-hcd xhci-hcd.0: xHCI Host Controller
[    2.294474] xhci-hcd xhci-hcd.0: new USB bus registered, assigned bus number 2
[    2.301738] xhci-hcd xhci-hcd.0: Host supports USB 3.0 SuperSpeed
[    2.307921] usb usb1: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 6.06
[    2.316229] usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    2.323485] usb usb1: Product: xHCI Host Controller
[    2.328389] usb usb1: Manufacturer: Linux 6.6.63-v8-16k xhci-hcd
[    2.334424] usb usb1: SerialNumber: xhci-hcd.0
[    2.339071] hub 1-0:1.0: USB hub found
[    2.342846] hub 1-0:1.0: 2 ports detected
[    2.347066] usb usb2: New USB device found, idVendor=1d6b, idProduct=0003, bcdDevice= 6.06
[    2.355373] usb usb2: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    2.362636] usb usb2: Product: xHCI Host Controller
[    2.367541] usb usb2: Manufacturer: Linux 6.6.63-v8-16k xhci-hcd
[    2.373586] usb usb2: SerialNumber: xhci-hcd.0
[    2.378247] hub 2-0:1.0: USB hub found
[    2.382028] hub 2-0:1.0: 1 port detected
[    2.386432] xhci-hcd xhci-hcd.1: xHCI Host Controller
[    2.391515] xhci-hcd xhci-hcd.1: new USB bus registered, assigned bus number 3
[    2.399244] xhci-hcd xhci-hcd.1: hcc params 0x0240fe6d hci version 0x110 quirks 0x0000008000000810
[    2.408275] xhci-hcd xhci-hcd.1: irq 136, io mem 0x1f00300000
[    2.414134] xhci-hcd xhci-hcd.1: xHCI Host Controller
[    2.419214] xhci-hcd xhci-hcd.1: new USB bus registered, assigned bus number 4
[    2.426600] xhci-hcd xhci-hcd.1: Host supports USB 3.0 SuperSpeed
[    2.432760] usb usb3: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 6.06
[    2.441184] usb usb3: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    2.448441] usb usb3: Product: xHCI Host Controller
[    2.453343] usb usb3: Manufacturer: Linux 6.6.63-v8-16k xhci-hcd
[    2.459489] usb usb3: SerialNumber: xhci-hcd.1
[    2.464108] hub 3-0:1.0: USB hub found
[    2.467889] hub 3-0:1.0: 2 ports detected
[    2.472093] usb usb4: New USB device found, idVendor=1d6b, idProduct=0003, bcdDevice= 6.06
[    2.480515] usb usb4: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    2.487772] usb usb4: Product: xHCI Host Controller
[    2.492670] usb usb4: Manufacturer: Linux 6.6.63-v8-16k xhci-hcd
[    2.498888] usb usb4: SerialNumber: xhci-hcd.1
[    2.503497] hub 4-0:1.0: USB hub found
[    2.507275] hub 4-0:1.0: 1 port detected
[    2.512435] bcm2712-iommu 1000005100.iommu: bcm2712_iommu_init: DEBUG_INFO = 0x20804774
[    2.520924] platform 1000800000.codec: bcm2712_iommu_probe_device: MMU 1000005100.iommu
[    2.529194] platform 1000800000.codec: bcm2712_iommu_device_group: MMU 1000005100.iommu
[    2.537251] platform 1000800000.codec: Adding to iommu group 0
[    2.543342] platform 1000880000.pisp_be: bcm2712_iommu_probe_device: MMU 1000005100.iommu
[    2.551568] platform 1000880000.pisp_be: bcm2712_iommu_device_group: MMU 1000005100.iommu
[    2.560000] platform 1000880000.pisp_be: Adding to iommu group 0
[    2.566074] platform 1000800000.codec: bcm2712_iommu_attach_dev: MMU 1000005100.iommu
[    2.573942] platform 1000880000.pisp_be: bcm2712_iommu_attach_dev: MMU 1000005100.iommu
[    2.582206] bcm2712-iommu 1000005100.iommu: bcm2712_iommu_probe: Success
[    2.589433] bcm2712-iommu 1000005200.iommu: bcm2712_iommu_init: DEBUG_INFO = 0x20804774
[    2.598119] platform axi:gpu: bcm2712_iommu_probe_device: MMU 1000005200.iommu
[    2.605381] platform axi:gpu: bcm2712_iommu_device_group: MMU 1000005200.iommu
[    2.612852] platform axi:gpu: Adding to iommu group 1
[    2.617966] platform axi:gpu: bcm2712_iommu_attach_dev: MMU 1000005200.iommu
[    2.625096] bcm2712-iommu 1000005200.iommu: bcm2712_iommu_probe: Success
[    2.632500] bcm2712-iommu 1000005280.iommu: bcm2712_iommu_init: DEBUG_INFO = 0x20804774
[    2.640997] bcm2712-iommu 1000005280.iommu: bcm2712_iommu_probe: Success
[    2.648031] vc4-drm axi:gpu: bcm2712_iommu_of_xlate: MMU 1000005200.iommu
[    2.657538] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    2.671235] sdhci-brcmstb 1000fff000.mmc: Got CD GPIO
[    2.671365] mmc1: CQHCI version 5.10
[    2.681765] mmc0: CQHCI version 5.10
[    2.682568] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    2.696106] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    2.706889] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    2.715803] of_cfs_init
[    2.718280] of_cfs_init: OK
[    2.725758] mmc0: SDHCI controller on 1000fff000.mmc [1000fff000.mmc] using ADMA 64-bit
[    2.738234] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    2.832436] mmc0: Tuning failed, falling back to fixed sampling clock
[    2.838913] mmc0: new ultra high speed DDR50 SDHC card at address 0003
[    2.845749] mmcblk0: mmc0:0003 SD4GB 3.68 GiB
[    2.851422]  mmcblk0: p1 p2
[    2.854361] mmcblk0: mmc0:0003 SD4GB 3.68 GiB
[    2.861385] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    2.867441] mmc1: SDHCI controller on 1001100000.mmc [1001100000.mmc] using ADMA 64-bit
[    2.879096] clk: Disabling unused clocks
[    2.891786] ALSA device list:
[    2.894777]   No soundcards found.
[    2.899096] uart-pl011 107d001000.serial: no DMA platform data
[    2.899121] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    2.922936] mmc1: new ultra high speed DDR50 SDIO card at address 0001
[    2.944132] EXT4-fs (mmcblk0p2): orphan cleanup on readonly fs
[    2.950106] EXT4-fs (mmcblk0p2): mounted filesystem 4324987b-4162-4657-9f32-e1e164ca1c32 ro with ordered data mode. Quota mode: none.
[    2.962204] VFS: Mounted root (ext4 filesystem) readonly on device 179:2.
[    2.969311] devtmpfs: mounted
[    2.975906] Freeing unused kernel memory: 5376K
[    2.980544] Run /sbin/init as init process
[    3.243904] systemd[1]: System time before build time, advancing clock.
[    3.335820] NET: Registered PF_INET6 protocol family
[    3.341317] Segment Routing with IPv6
[    3.345013] In-situ OAM (IOAM) with IPv6
[    3.381540] systemd[1]: systemd 255.18^ running in system mode (-PAM -AUDIT -SELINUX -APPARMOR +IMA -SMACK +SECCOMP -GCRYPT -GNUTLS -OPENSSL +ACL +BLKID -CURL -ELFUTILS -FIDO2 -IDN2 -IDN -IPTC +KMOD -LIBCRYPTSETUP +LIBFDISK -PCRE2 -PWQUALITY -P11KIT -QRENCODE -TPM2 -BZIP2 -LZ4 -XZ -ZLIB +ZSTD -BPF_FRAMEWORK +XKBCOMMON +UTMP +SYSVINIT default-hierarchy=unified)
[    3.413627] systemd[1]: Detected architecture arm64.

Welcome to Poky (Yocto Project Reference Distro) 5.0.9 (scarthgap)!

[    3.437148] systemd[1]: Hostname set to <raspberrypi5>.
[    3.447559] systemd[1]: Initializing machine ID from random generator.
[    3.454186] systemd[1]: Installed transient /etc/machine-id file.
[    3.702276] systemd[1]: Queued start job for default target Multi-User System.
[    3.735875] systemd[1]: Created slice Slice /system/getty.
[  OK  ] Created slice Slice /system/getty.
[    3.755313] systemd[1]: Created slice Slice /system/modprobe.
[  OK  ] Created slice Slice /system/modprobe.
[    3.775286] systemd[1]: Created slice Slice /system/serial-getty.
[  OK  ] Created slice Slice /system/serial-getty.
[    3.795175] systemd[1]: Created slice User and Session Slice.
[  OK  ] Created slice User and Session Slice.
[    3.815022] systemd[1]: Started Dispatch Password Requests to Console Directory Watch.
[  OK  ] Started Dispatch Password Requests to Console Directory Watch.
[    3.839000] systemd[1]: Started Forward Password Requests to Wall Directory Watch.
[  OK  ] Started Forward Password Requests to Wall Directory Watch.
[    3.862995] systemd[1]: Expecting device /dev/mmcblk0p1...
         Expecting device /dev/mmcblk0p1...
[    3.882949] systemd[1]: Expecting device /sys/devices/platform/gpu/graphics/fb0...
         Expecting device /sys/devices/platform/gpu/graphics/fb0...
[    3.906980] systemd[1]: Reached target Path Units.
[  OK  ] Reached target Path Units.
[    3.926943] systemd[1]: Reached target Remote File Systems.
[  OK  ] Reached target Remote File Systems.
[    3.946943] systemd[1]: Reached target Slice Units.
[  OK  ] Reached target Slice Units.
[    3.966968] systemd[1]: Reached target Swaps.
[  OK  ] Reached target Swaps.
[    4.001961] systemd[1]: Listening on RPCbind Server Activation Socket.
[  OK  ] Listening on RPCbind Server Activation Socket.
[    4.026983] systemd[1]: Reached target RPC Port Mapper.
[  OK  ] Reached target RPC Port Mapper.
[    4.047645] systemd[1]: Listening on Syslog Socket.
[  OK  ] Listening on Syslog Socket.
[    4.067058] systemd[1]: Listening on initctl Compatibility Named Pipe.
[  OK  ] Listening on initctl Compatibility Named Pipe.
[    4.091338] systemd[1]: Listening on Journal Audit Socket.
[  OK  ] Listening on Journal Audit Socket.
[    4.111103] systemd[1]: Listening on Journal Socket (/dev/log).
[  OK  ] Listening on Journal Socket (/dev/log).
[    4.131213] systemd[1]: Listening on Journal Socket.
[  OK  ] Listening on Journal Socket.
[    4.151209] systemd[1]: Listening on Network Service Netlink Socket.
[  OK  ] Listening on Network Service Netlink Socket.
[    4.171454] systemd[1]: Listening on udev Control Socket.
[  OK  ] Listening on udev Control Socket.
[    4.191084] systemd[1]: Listening on udev Kernel Socket.
[  OK  ] Listening on udev Kernel Socket.
[    4.211102] systemd[1]: Listening on User Database Manager Socket.
[  OK  ] Listening on User Database Manager Socket.
[    4.231144] systemd[1]: Huge Pages File System was skipped because of an unmet condition check (ConditionPathExists=/sys/kernel/mm/hugepages).
[    4.263018] systemd[1]: Mounting POSIX Message Queue File System...
         Mounting POSIX Message Queue File System...
[    4.284027] systemd[1]: Mounting Kernel Debug File System...
         Mounting Kernel[    4.290969] systemd[1]: Mounting Kernel Trace File System...
 Debug File System...
         Mounting Kernel Trace F[    4.312558] systemd[1]: Mounting Temporary Directory /tmp...
ile System...
         Mounting Temporary Dire[    4.332541] systemd[1]: Starting Create List of Static Device Nodes...
ctory /tmp...
         Starting Create List of[    4.356397] systemd[1]: Starting Load Kernel Module configfs...
 Static Device Nodes...
         Starting Load K[    4.376344] systemd[1]: Starting Load Kernel Module drm...
ernel Module configfs...
         Starting Load K[    4.396375] systemd[1]: Starting Load Kernel Module fuse...
ernel Module drm...
         Starting Load Kernel Module fuse...
[    4.418484] systemd[1]: Starting RPC Bind...
         Starting RPC Bi[    4.428197] systemd[1]: Starting File System Check on Root Device...
nd...
[    4.446328] fuse: init (API version 7.39)
         Starting File System Check on Root Devi[    4.462061] systemd[1]: Starting Journal Service...
ce...
         Starting Journal Service...
[    4.484581] systemd[1]: Load Kernel Modules was skipped because no trigger condition checks were met.
[    4.495396] systemd[1]: Starting Generate network units from Kernel command line...
         Starting Genera[    4.517085] systemd[1]: Starting Apply Kernel Variables...
te network units from Kernel command line...
    [    4.527069] systemd[1]: Starting Coldplug All udev Devices...
     Starting Apply Kernel Variables.[    4.537195] systemd[1]: Started RPC Bind.
..
         Starting Co[    4.543447] systemd[1]: Mounted POSIX Message Queue File System.
ldplug All udev Devices...
[[    4.552433] systemd[1]: Mounted Kernel Debug File System.
  OK  ] Started     4.560726] systemd[1]: Mounted Kernel Trace File System.
39mRPC Bind.
[  OK  [    4.569037] systemd[1]: Mounted Temporary Directory /tmp.
] Mounted POSIX Mess[    4.577477] systemd[1]: Finished Create List of Static Device Nodes.
age Queue File System.
[    4.586827] systemd[1]: modprobe@configfs.service: Deactivated successfully.
;32m  OK  ] Mounted [    4.596510] systemd[1]: Finished Load Kernel Module configfs.
Kernel Debug File System systemd[1]: modprobe@drm.service: Deactivated successfully.
[0m.
[  OK  ] Mount[    4.614636] systemd[1]: Finished Load Kernel Module drm.
ed Kernel Trace File Syste[    4.622520] systemd[1]: modprobe@fuse.service: Deactivated successfully.
m.
[  OK   systemd[1]: Finished Load Kernel Module fuse.
[0m] Mounted Temporary Di[    4.639718] systemd[1]: Finished Generate network units from Kernel command line.
rectory /tmp.
[  OK  [    4.650185] systemd[1]: Reached target Preparation for Network.
] Finished Create List of Static Device Nodes.
[  OK  ] Finished Load Kernel Module configf[    4.668181] systemd-journald[130]: Collecting audit messages is enabled.
s.
[  OK  ] Finished L[    4.679069] systemd[1]: Mounting FUSE Control File System...
oad Kernel Module drm.
[  OK [    4.688393] systemd[1]: Mounting Kernel Configuration File System...
 ] Finished Load Kernel Module fuse.
[  [    4.700276] systemd[1]: Starting Create Static Device Nodes in /dev gracefully...
OK  ] Finished Generate netwo[    4.711431] systemd[1]: Finished Apply Kernel Variables.
rk units from Kernel command line systemd[1]: Mounted FUSE Control File System.
[0m.
[  OK  ] Reache[    4.727514] systemd[1]: Mounted Kernel Configuration File System.
d target Preparation for [    4.736519] systemd[1]: Started Journal Service.
Network.
         Mounting FUSE Control File System...
         Mounting Kernel Configuration File System...
         Starting Create Static Device Nodes in /dev gracefully...
[  OK  ] Finished Apply Kernel Variables.
[  OK  ] Mounted FUSE Control File System.
[  OK  ] Mounted Kernel Configuration File System.
[  OK  ] Started Journal Service.
[  OK  ] Finished Create Static Device Nodes in /dev gracefully.
[  OK  ] Finished File System Check on Root Device.
[  OK  ] Finished Coldplug All udev Devices.
         Starting Remount Root and Kernel File Systems...
[    4.929148] EXT4-fs (mmcblk0p2): re-mounted 4324987b-4162-4657-9f32-e1e164ca1c32 r/w. Quota mode: none.
[  OK  ] Finished Remount Root and Kernel File Systems.
         Starting Flush Journal to Persistent Storage...
[    4.994514] systemd-journald[130]: Received client request to flush runtime journal.
         Starting Create System Users...
[  OK  ] Finished Flush Journal to Persistent Storage.
[    5.045723] audit: type=1334 audit(1741187610.795:2): prog-id=6 op=LOAD
[    5.052551] audit: type=1334 audit(1741187610.807:3): prog-id=7 op=LOAD
         Starting User D[    5.059463] audit: type=1334 audit(1741187610.807:4): prog-id=8 op=LOAD
atabase Manager...
[  OK  ] Started User Database Manager.
[  OK  ] Finished Create System Users.
         Starting Create Static Device Nodes in /dev...
[  OK  ] Finished Create Static Device Nodes in /dev.
[  OK  ] Reached target Preparation for Local File Systems.
         Mounting /var/volatile...
[    5.279590] audit: type=1334 audit(1741187611.031:5): prog-id=9 op=LOAD
[    5.286263] audit: type=1334 audit(1741187611.035:6): prog-id=10 op=LOAD
         Starting Rule-based Manager for Device Events and Files...
[  OK  ] Mounted /var/volatile.
         Starting Load/Save OS Random Seed...
[  OK  ] Finished Load/Save OS Random Seed.
[  OK  ] Started Rule-based Manager for Device Events and Files.
[    5.435996] audit: type=1334 audit(1741187611.187:7): prog-id=11 op=LOAD
         Starting Network Configuration...
[    5.509091] rpi-gpiomem 107d508500.gpiomem: window base 0x107d508500 size 0x00000040
[    5.521796] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    5.530256] rpi-gpiomem 107d508500.gpiomem: initialised 1 regions as /dev/gpiomem1
[    5.539706] rpi-gpiomem 107d517c00.gpiomem: window base 0x107d517c00 size 0x00000040
[    5.548487] rpi-gpiomem 107d517c00.gpiomem: initialised 1 regions as /dev/gpiomem2
[    5.556189] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    5.562751] rpi-gpiomem 107d504100.gpiomem: window base 0x107d504100 size 0x00000020
[    5.569290] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    5.574359] rpi-gpiomem 107d504100.gpiomem: initialised 1 regions as /dev/gpiomem3
[    5.586410] rpi-gpiomem 107d510700.gpiomem: window base 0x107d510700 size 0x00000020
[    5.590229] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    5.594439] rpi-gpiomem 107d510700.gpiomem: initialised 1 regions as /dev/gpiomem4
[    5.609736] rpi-gpiomem 1f000d0000.gpiomem: window base 0x1f000d0000 size 0x00030000
[    5.610997] mc: Linux media interface: v0.10
[    5.624175] vc4-drm axi:gpu: bound 107c580000.hvs (ops vc4_hvs_ops)
[    5.624265] brcmstb-i2c 107d508200.i2c:  @97500hz registered in interrupt mode
[    5.624427] input: pwr_button as /devices/platform/pwr_button/input/input0
[    5.625433] rpi-gpiomem 1f000d0000.gpiomem: initialised 1 regions as /dev/gpiomem0
[    5.640352] Registered IR keymap rc-cec
[    5.649665] brcmstb-i2c 107d508280.i2c:  @97500hz registered in interrupt mode
[    5.664682] rc rc0: vc4-hdmi-0 as /devices/platform/soc/107c701400.hdmi/rc/rc0
[    5.678988] input: vc4-hdmi-0 as /devices/platform/soc/107c701400.hdmi/rc/rc0/input1
[    5.692844] input: vc4-hdmi-0 HDMI Jack as /devices/platform/soc/107c701400.hdmi/sound/card0/input2
[    5.703099] vc4-drm axi:gpu: bound 107c701400.hdmi (ops vc4_hdmi_ops)
[    5.717327] Registered IR keymap rc-cec
[    5.721440] rc rc1: vc4-hdmi-1 as /devices/platform/soc/107c706400.hdmi/rc/rc1
[    5.728893] input: vc4-hdmi-1 as /devices/platform/soc/107c706400.hdmi/rc/rc1/input3
[    5.740014] input: vc4-hdmi-1 HDMI Jack as /devices/platform/soc/107c706400.hdmi/sound/card1/input4
[    5.752212] vc4-drm axi:gpu: bound 107c706400.hdmi (ops vc4_hdmi_ops)
[    5.767076] vc4-drm axi:gpu: bound 107c500000.mop (ops vc4_txp_ops)
[  OK  ] Found device /dev/mm[    5.778005] vc4-drm axi:gpu: bound 107c501000.moplet (ops vc4_txp_ops)
cblk0p1.
[    5.787242] vc4-drm axi:gpu: bound 107c410000.pixelvalve (ops vc4_crtc_ops)
[    5.793985] cfg80211: Loading compiled-in X.509 certificates for regulatory database
[    5.794989] vc4-drm axi:gpu: bound 107c411000.pixelvalve (ops vc4_crtc_ops)
[    5.811433] Loaded X.509 cert 'benh@debian.org: 577e021cb980e0e820821ba7b54b4961b8b4fadf'
[    5.817613] [drm] Initialized vc4 0.0.0 20140616 for axi:gpu on minor 0
[    5.819685] [drm] Initialized v3d 1.0.0 20180419 for 1002000000.v3d on minor 1
[    5.820553] Loaded X.509 cert 'romain.perier@gmail.com: 3abbc6ec146e09d1b6016ab9d6cf71dd233f0328'
[    5.821015] Loaded X.509 cert 'sforshee: 00b28ddf47aef9cea7'
[    5.821468] Loaded X.509 cert 'wens: 61c038651aabdcf94bd0ac7ff06c7248db18c600'
[    5.823538] videodev: Linux video capture interface: v2.00
[    5.829551] vc4-drm axi:gpu: [drm] Cannot find any crtc or sizes
[    5.870695] vc4-drm axi:gpu: [drm] Cannot find any crtc or sizes
         Mounting /boot...
[    5.882988] vc4-drm axi:gpu: [drm] Cannot find any crtc or sizes
[  OK  ] Started Network Configuration.
[    5.916486] macb 1f00100000.ethernet eth0: PHY [1f00100000.ethernet-ffffffff:01] driver [Broadcom BCM54213PE] (irq=POLL)
[    5.928101] pispbe 1000880000.pisp_be: bcm2712_iommu_of_xlate: MMU 1000005100.iommu
[    5.936051] macb 1f00100000.ethernet eth0: configuring for phy/rgmii-id link mode
[    5.947560] pps pps0: new PPS source ptp0
[    5.950993] pispbe 1000880000.pisp_be: Runtime PM usage count underflow!
[    5.953439] macb 1f00100000.ethernet: gem-ptp-timer ptp clock registered.
[    5.965273] brcmfmac: brcmf_fw_alloc_request: using brcm/brcmfmac43455-sdio for chip BCM4345/6
[  OK  ] Listening on [    5.974316] usbcore: registered new interface driver brcmfmac
Load/Save RF Kill Switch Status /dev/rfkill Watch.
[    5.987770] brcmfmac mmc1:0001:1: Direct firmware load for brcm/brcmfmac43455-sdio.raspberrypi,5-model-b.bin failed with error -2
[    6.001062] rpivid_hevc: module is from the staging directory, the quality is unknown, you have been warned.
[    6.015343] Bluetooth: Core ver 2.22
[    6.019029] NET: Registered PF_BLUETOOTH protocol family
[    6.024386] Bluetooth: HCI device and connection manager initialized
[    6.030859] Bluetooth: HCI socket layer initialized
[    6.036478] rpivid 1000800000.codec: bcm2712_iommu_of_xlate: MMU 1000005100.iommu
         Starting Virtua[    6.044091] Bluetooth: L2CAP socket layer initialized
[    6.046858] rpivid 1000800000.codec: Device registered as /dev/video19

[    6.052038] Bluetooth: SCO socket layer initialized
[  OK  ] Mounted /boot.
[    6.074732] Bluetooth: HCI UART driver ver 2.3
[    6.079255] Bluetooth: HCI UART protocol H4 registered
[    6.084479] Bluetooth: HCI UART protocol Three-wire (H5) registered
[    6.090986] hci_uart_bcm serial0-0: supply vbat not found, using dummy regulator
[    6.098443] Bluetooth: HCI UART protocol Broadcom registered
[    6.102982] hci_uart_bcm serial0-0: supply vddio not found, using dummy regulator
[  OK  ] Reached target Local File Systems.
         Starting Rebuild Dynamic Linker Cache...
         Starting Commit a transient machine-id on disk...
         Starting Create System Files and Directories...
[  OK  ] Finished Virtual Console Setup.
[  OK  ] Finished Create System Files and Directories.
         Starting Rebuild Journal Catalog...
[    6.359383] brcmfmac: brcmf_c_process_txcap_blob: no txcap_blob available (err=-2)
[    6.367283] brcmfmac: brcmf_c_preinit_dcmds: Firmware: BCM4345/6 wl0: Aug 29 2023 01:47:08 version 7.45.265 (28bca26 CY) FWID 01-b677b91b
[    6.388328] audit: type=1334 audit(1741187612.139:8): prog-id=12 op=LOAD
         Starting Network Name Resolution...
[    6.408345] audit: type=1334 audit(1741187612.159:9): prog-id=13 op=LOAD
         Starting Network Time Synchronization...
         Starting Record System Boot/Shutdown in UTMP...
[    6.475363] Bluetooth: hci0: BCM: chip id 107
[    6.479970] Bluetooth: hci0: BCM: features 0x2f
[    6.485752] Bluetooth: hci0: BCM4345C0
[    6.489531] Bluetooth: hci0: BCM4345C0 (003.001.025) build 0000
[    6.502877] Bluetooth: hci0: BCM4345C0 'brcm/BCM4345C0.hcd' Patch
[  OK  ] Created slice Slice /system/bthelper.
         Starting Load/Save RF Kill Switch Status...
[  OK  ] Finished Record System Boot/Shutdown in UTMP.
[  OK  ] Started Load/Save RF Kill Switch Status.
[    6.586916] rp1-firmware: probe of rp1_firmware failed with error -110
[  OK  ] Finished Commit a transient machine-id on disk.
[  OK  ] Finished Rebuild Journal Catalog.
[  OK  ] Started Network Time Synchronization.
[  OK  ] Started Network Name Resolution.
[  OK  ] Reached target Network.
[  OK  ] Reached target Host and Network Name Lookups.
[  OK  ] Reached target System Time Set.
[  OK  ] Finished Rebuild Dynamic Linker Cache.
         Starting Update is Completed...
[  OK  ] Finished Update is Completed.
[  OK  ] Reached target System Initialization.
[  OK  ] Started Daily Cleanup of Temporary Directories.
[  OK  ] Reached target Timer Units.
[  OK  ] Listening on Avahi mDNS/DNS-SD Stack Activation Socket.
[  OK  ] Listening on D-Bus System Message Bus Socket.
[  OK  ] Reached target Socket Units.
[  OK  ] Reached target Basic System.
         Starting Save/Restore Sound Card State...
         Starting Avahi mDNS/DNS-SD Stack...
[  OK  ] Started Kernel Logging Service.
[  OK  ] Started System Logging Service.
         Starting D-Bus System Message Bus...
[  OK  ] Started Getty on tty1.
         Starting Raspberry Pi bluetooth helper...
         Starting Telephony service...
[  OK  ] Started Serial Getty on ttyAMA10.
[  OK  ] Reached target Login Prompts.
[    7.113751] audit: type=1334 audit(1741187612.863:10): prog-id=14 op=LOAD
[    7.120650] audit: type=1334 audit(1741187612.871:11): prog-id=15 op=LOAD
[    7.127567] audit: type=1334 audit(1741187612.879:12): prog-id=16 op=LOAD
         Starting User Login Management...
[  OK  ] Started D-Bus System Message Bus.
[  OK  ] Finished Save/Restore Sound Card State.
[  OK  ] Reached target Sound Card.
[  OK  ] Started Telephony service.
[    7.216138] Bluetooth: hci0: BCM: features 0x2f
[    7.222111] Bluetooth: hci0: BCM43455 37.4MHz Raspberry Pi 3+-0190
[    7.228408] Bluetooth: hci0: BCM4345C0 (003.001.025) build 0382
[    7.234743] Bluetooth: hci0: BCM: Using default device address (43:45:c0:00:1f:ac)
[  OK  ] Started User Login Management.
[  OK  ] Started Avahi mDNS/DNS-SD Stack.
[  OK  ] Finished Raspberry Pi bluetooth helper.
[  OK  ] Reached target Multi-User System.
         Starting Bluetooth service...
         Starting Record Runlevel Change in UTMP...
[  OK  ] Finished Record Runlevel Change in UTMP.
[  OK  ] Started Bluetooth service.
[    7.423293] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
[    7.428645] Bluetooth: BNEP filters: protocol multicast
[    7.428654] Bluetooth: BNEP socket layer initialized
[  OK  ] Reached target Bluetooth Support.
[    7.445287] Bluetooth: MGMT ver 1.22
[    7.453949] NET: Registered PF_ALG protocol family
[    7.475838] audit: type=1334 audit(1741187613.227:13): prog-id=17 op=LOAD
[    7.482780] audit: type=1334 audit(1741187613.231:14): prog-id=18 op=LOAD
[    7.489700] audit: type=1334 audit(1741187613.231:15): prog-id=19 op=LOAD
[    7.489704] Bluetooth: RFCOMM TTY layer initialized
[    7.501513] Bluetooth: RFCOMM socket layer initialized
[    7.506686] Bluetooth: RFCOMM ver 1.11
         Starting Hostname Service...
[  OK  ] Started Hostname Service.
[    7.867782] hwmon hwmon2: Undervoltage detected!

Poky (Yocto Project Reference Distro) 5.0.9 raspberrypi5 ttyAMA10

raspberrypi5 login: [   16.699173] platform 1f00178000.pio: deferred probe pending
[   19.395386] mmc0: Tuning failed, falling back to fixed sampling clock
[   35.811387] mmc0: Tuning failed, falling back to fixed sampling clock
[   37.678978] audit: type=1334 audit(1741187643.431:16): prog-id=19 op=UNLOAD
[   37.685992] audit: type=1334 audit(1741187643.431:17): prog-id=18 op=UNLOAD
[   37.692994] audit: type=1334 audit(1741187643.431:18): prog-id=17 op=UNLOAD
[   52.227385] mmc0: Tuning failed, falling back to fixed sampling clock
[   68.643387] mmc0: Tuning failed, falling back to fixed sampling clock

raspberrypi5 login: root

```

</details>
