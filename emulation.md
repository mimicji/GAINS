# IoT Hardware Emulation/Simulate
## Table of contents
- [Complete Hardware Emulation](#complete-hardware-emulation)
- [Emulate OS-based (Linux-based) Device](#emulate-os-based-linux-based-device)
	- [Hybrid Emulation Approach](#hybrid-emulation-approach)
	- [Fully Emulated Environment](#fully-emulated-environment)
- [Emulate non-Linux-based (bare-metal) IoT device](#emulate-non-linux-based-bare-metal-iot-device)
- [Emulate Network/Device](#emulate-networkdevice)


## Complete Hardware Emulation
Analyze device drivers by relying on an emulated PCI bus and network card that return symbolic values.
This approach has the main drawback that it requires to emulate the device properly. While this is not much of a problem for well-understood devices, like a PCI network card supported by most PC emulation software, it can be a real challenge in embedded systems and can be just impossible when the hardware is not documented. Unfortunately, lack of documentation is the rule in the embedded world, especially in complex proprietary SoCs.

#### Literature
1. Chipounov, Vitaly, and George Candea. "Reverse engineering of binary device drivers with RevNIC." Proceedings of the 5th European conference on Computer systems. 2010.

2. Kuznetsov, Volodymyr, Vitaly Chipounov, and George Candea. "Testing closed-source binary device drivers with DDT." USENIX Annual Technical Conference. No. CONF. 2010.


## Emulate OS-based (Linux-based) Device
### Hybrid Emulation Approach
1. Zaddach, Jonas, et al. "**AVATAR**: A Framework to Support Dynamic Security Analysis of Embedded Systems' Firmwares." NDSS. Vol. 14. 2014.
	- Hybrid way: emulator with hardware
	- Other methods: complete hardware emulation, hardware over-approximation, firmware adaption  

2. Talebi, Seyed Mohammadjavad Seyed, et al. "**Charm**: Facilitating dynamic analysis of device drivers of mobile systems." 27th {USENIX} Security Symposium ({USENIX} Security 18). 2018.
	- Decouples the execution of the device driver from the mobile system hardware. Enable the device driver to run in a virtual machine on a different physical machine
	- Now only supports open-source device drivers
	- Makes a claim: Emulating the I/O device hardware for the virtual machine in software requires prohibitive engineering effort due to the diversity of I/O devices in mobile systems

3. Koscher, Karl, Tadayoshi Kohno, and David Molnar. "**SURROGATES**: Enabling near-real-time dynamic analyses of embedded systems." 9th {USENIX} Workshop on Offensive Technologies ({WOOT} 15). 2015.
	- By using a custom FPGA bridge between the host and target, it enables near-real-time emulation of the target system
	- Similar to Avatar (improves the forwarding performance of Avatar via customized hardware)

4. Muench, Marius, et al. "**Avatar2**: A multi-target orchestration platform." Proc. Workshop Binary Anal. Res.(Colocated NDSS Symp.). Vol. 18. 2018.
	- Extends Avatar to allow replay of forwarded peripheral I/O without using real devices

5. Kammerstetter, Markus, Christian Platzer, and Wolfgang Kastner. "**Prospect**: peripheral proxying supported embedded code testing." Proceedings of the 9th ACM symposium on Information, computer and communications security. 2014.
	- Forwards peripheral accesses at the syscall level (which does not exist on bare-metal MCU devices)

6. Kammerstetter, Markus, Daniel Burian, and Wolfgang Kastner. "Embedded security testing with peripheral device caching and runtime program state approximation." 10th International Conference on Emerging Security Information, Systems and Technologies (SECUWARE). 2016.
	- Uses cached peripheral accesses to approximate firmware states for analysis (over-approximate?)

### Fully Emulated Environment
1. Chen, Daming D., et al. "Towards Automated Dynamic Analysis for Linux-based Embedded Firmware." NDSS. Vol. 16. 2016. (**FIRMADYNE**)
	- Targets Linux-based firmware on network-connected COTS devices
	- Uses the pre-compiled kernels
	- Dynamic analysis as a proof-of-concept application to find out the vulnerability

2. Renzelmann, Matthew J., Asim Kadav, and Michael M. Swift. "**SymDrive**: testing drivers without devices." Presented as part of the 10th {USENIX} Symposium on Operating Systems Design and Implementation ({OSDI} 12). 2012.
	- The system uses symbolic execution to remove the need for hardware

3. Costin, Andrei, Apostolis Zarras, and Aurélien Francillon. "Automated dynamic firmware analysis at scale: a case study on embedded web interfaces." Proceedings of the 11th ACM on Asia Conference on Computer and Communications Security. 2016.

4. Zheng, Yaowen, et al. "**FIRM-AFL**: high-throughput greybox fuzzing of iot firmware via augmented process emulation." 28th {USENIX} Security Symposium ({USENIX} Security 19). 2019.
	- Combines user-mode emulation and system-mode emulation to fuzz the firmware. Enter the user-mode (host machine kernel) when encountering predefined fuzzing points
	- Based on the Firmadyne to emulate the firmware and AFL to fuzz

5. Song, Dokyung, et al. "**Periscope**: An effective probing and fuzzing framework for the hardware-os boundary." NDSS. 2019.
	- Passively monitor and log traffic between device drivers and their corresponding hardware, or mutate the data stream on-the-fly using a fuzzing component, PERIFUZZ, thus mimicking an active adversarial attack.

## Emulate non-Linux-based (bare-metal) IoT device
1. Feng, Bo, Alejandro Mera, and Long Lu. "**P2IM**: Scalable and Hardware-independent Firmware Testing via Automatic Peripheral Interface Modeling." Proceedings of the 29th USENIX Security Symposium. 2020.
	- Automatically models the I/O behaviors of a wide range of peripherals while treating the peripherals themselves as black boxes
	- To fuzz the firmware (not for fuzzing exclusively)
	- Not specific to the ARM architecture (they only do it on ARM???)
	- Other types of dynamic firmware analysis that do not require fully accurate output from firmware can use P2IM

2. Gustafson, Eric, et al. "Toward the analysis of embedded firmware through automated re-hosting." 22nd International Symposium on Research in Attacks, Intrusions and Defenses ({RAID} 2019). 2019. (**PRETENDER**) 

3. Clements, Abraham A., et al. "**HALucinator**: Firmware Re-hosting Through Abstraction Layer Emulation." 29th USENIX Security Symposium (USENIX Sec). 2020.

## Emulate Network/Device
1. Bagula, B. A., and Zenville Erasmus. "Iot emulation with **cooja**." ICTP-IoT workshop. 2015.
	- Only-targeted the Contiki OS - Contiki is an operating system for networked, memory-constrained systems with a focus on low-power wireless Internet of Things devices (e.g. Z1 mote https://github.com/Zolertia/Resources/wiki/The-Z1-mote)
	- Have an MCU inside

2. Brady, Shane, et al. "Towards an emulated IoT test environment for anomaly detection using NEMU." 2017 Global Internet of Things Summit (GIoTS). IEEE, 2017.
	- This is to emulate the network IoT environment (a testbed of inter-connected, emulated Raspberry Pi devices)
	- NEMU - realistic virtual dynamic networks
	- QEMU - used to emulate the IoT devices (run the Pi’s OS in QEMU)
	- It also does an anomaly detection by using logs



