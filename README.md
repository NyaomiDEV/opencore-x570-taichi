# OpenCore configuration for ASRock X570 Taichi

## Relevant build details:

- ASRock X570 Taichi
- AMD Ryzen 7 3800XT
- AMD Radeon RX 6900 XT 16GB
- Booting from a SATA SSD: Samsung 870 EVO 500GB

## Recommended macOS version(s) to use:

- Ventura.
  Tested and working on versions 13.0 - 13.2

If you need Big Sur (because you probably need the builtin Ethernet to work) check out the [older, unmaintained tree](https://github.com/NyaomiDEV/opencore-x570-taichi/tree/big_sur) which works well enough with it.

## What is NOT working:

### All possible configurations on this board

- The builtin Ethernet does not work reliably. This is down to the AppleIGB kernel extension being really bad, but also being the only kernel extension that's currently available for Monterey onwards.
  The LucyRTL8125Ethernet kernel extension is included to support Realtek PCIe cards based on the RTL8125 chip (and variants), which are usually cheap to get on Amazon. Those also support 2.5Gbps networking (a step up since the builtin Ethernet port is only 1Gbps in speed), so the (small) price to pay is eventually worth it.
  Furthermore, there's HoRNDIS (Android USB tethering kernel extension) included as a last resort, though the Wi-Fi will work both on recovery mode and on the final installed system.

- Microphone and line inputs (AppleALC doesn't support that on AMD systems);

- Onboard RGB controls (you can change your lighting from the BIOS anyway);

- HDMI/DP audio is crackly, and that's due to the PAT fix by Shaneee (you could use algrey's PAT fix but that will make the GPU noticeably slower);

- Software that relies on Apple's hypervisor kernel extension (**Docker**, **Parallels Desktop**, etc.)
  
  You can work around some stuff (for example, you can use Docker under a Linux VM inside VirtualBox);

- 32-bit applications.
  
  This isn't a big concern since Apple dropped 32-bit support themselves, but there are plenty of 64-bit apps that still use 32-bit code paths.
  (**Wine**, **CrossOver**, etc.)

- Applications taking advantage of Intel's MKL (OneAPI).
  They might appear to work, but then they'd hang indefinitely or crash; notable mentions are:
  
  - The (almost) entirety of the **Adobe Creative Cloud suite** (yes, Photoshop, Premiere Pro and After Effects are affected);
  - **Discord** (the Krisp AI noise suppression module, to be specific);
  
  What, you really wanted to use those applications because that's kinda the whole point of hackintoshing for productivity?
  Oh well then great news for you: around the internet there are patched versions of those apps that run magically well on our systems!
  And if you ever get tired of searching patched apps, then [just use the library patcher I made](https://github.com/NyaomiDEV/AMDFriend)
  because that's also what the guys in the forums do to make those patched apps and libs.

### Peculiar configurations:

- Ryzen G series APUs:
  
  - Crackling audio; the only workaround is to buy an external audio card with its own clock circuitry;
  - Onboard graphics is not supported;

- AMD graphics cards newer than the RX Polaris series:
  
  - RX 5000/6000 Series: You have to add `agdpmod=pikera` in boot-args to properly boot. (already added by default)
  - RX 6000 Series: Not all cards are supported! Check your card beforehand.

- Any processor other than the 3800XT I have:
  
  - You have to modify the core count on the kernel patches section of the OpenCore config;
  - You also have to modify the processor name in the RestrictEvents configuration.

## What needs special treatment in order to get working:

- The Thunderbolt 3 expansion card
  (the one ASRock recommends, but also third parties are fine.
  If you're shopping for one just pick one that's known to be moddable and working on macOS)

## What is working:

Pretty much everything else.

## Notes:

- VoodooHDA is an alternative to AppleALC that has mic input and line input working; but the audio quality is noticeably worse.
- iServices DO work, if you provide a legit serial/MKB/ROM combo.

## Honorable mentions:

- Alessandro Zanardi for rebuilding the EFI from scratch because I am dumb
- Baronerosso @ GitHub for finding the USB mapping nobody actually wanted to do

## Final thoughts:

La madonna maiala
