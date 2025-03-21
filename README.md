# OpenCore configuration for ASRock X570 Taichi

## Relevant build details:

- ASRock X570 Taichi
- AMD Ryzen 9 5950X
- AMD Radeon RX 6900 XT 16GB
- Booting from a SATA SSD: Samsung 870 EVO 500GB

## Recommended macOS version(s) to use:

- Ventura.
  Tested and working on versions 13.0 - 13.2

If you need Big Sur (because you probably need the builtin Ethernet to work) check out the [older, unmaintained tree](https://github.com/NyaomiDEV/opencore-x570-taichi/tree/big_sur) which works well enough with it.

## What is NOT working:

### All possible configurations on this board

- Onboard RGB controls (you can change your lighting from the BIOS anyway);

- HDMI/DP audio is crackly, and that's due to the PAT fix by Shaneee (you could use algrey's PAT fix but that will make the GPU noticeably slower);

- Software that relies on Apple's hypervisor kernel extension (**Docker**, **Parallels Desktop**, etc.)
  
  You can work around some stuff (for example, you can use Docker under a Linux VM inside VirtualBox);

- 32-bit applications.
  
  This isn't a big concern since Apple dropped 32-bit support themselves, but there are plenty of 64-bit apps that still use 32-bit code paths.
  (**Wine**, **CrossOver**, etc.)

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
