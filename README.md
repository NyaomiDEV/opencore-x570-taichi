# Big Sus on my X570 Taichi

## What is NOT working:

- Microphone and line inputs
- The Thunderbolt 3 expansion card. I do not have one so I can't even test it, but no SSDTs are there to support it anyway

## What is working:

- Pretty much everything else.

## Notes:

- VoodooHDA is an alternative to AppleALC that has mic input and line input working; but the audio quality is noticeably worse. I'd suggest buying an external audio card, and a good one at that, so that you can also benefit from it in the long term.
- The front panel headphone output has some kinda weird compression effect applied to it. I can't say if it's AppleALC's fault or macOS' but I can sure say this is annoying.
- Try to avoid applications compiled with Intel C++ compiler, such as the Adobe suite, some VSTs for audio production, and basically all AI processing stuff with TensorFlow and whatever else; reason being the Intel C++ compiler, or anything related to Intel's MKL, just assumes that the CPU is an Intel one, and this causes problems down the line with proprietary Intel CPU instruction calls. Library and executable patches for the most famous suites (such as the Adobe one) are out there in the wild, though. Also, here's hoping for an OpenCore patch or a Lilu plugin that can work around this issue...
- iServices DO work, if you provide a legit serial/MKB/ROM combo.

## Honorable mentions:

- Alessandro Zanardi for rebuilding the EFI from scratch because I am dumb
- Baronerosso @ GitHub for finding the USB mapping nobody actually wanted to do

## Relevant build details:

- ASRock X570 Taichi
- AMD Ryzen 7 3800XT
- AMD Radeon RX 580 8GB
- Booting from a SATA SSD: Samsung 870 EVO 500GB

## Final thoughts:

La madonna maiala
