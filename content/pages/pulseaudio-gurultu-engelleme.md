---
title: Linux PulseAudio Mikrofon Gürültü Engelleme
date: 2023-01-04
tags: ["linux"]
draft: false
---
PulseAudio için mikrofonda gürültü nasıl engellenir buna kısaca değineceğim.
'sudo nano /etc/pulse/default.pa' config dosyasının içine girip en alta bu kodları ekliyoruz.
```
load-module module-filter-heuristics
load-module module-filter-apply
load-module module-echo-cancel aec_args="analog_gain_control=0 digital_gain_control=0"
```
Ondan sonra `pulseaudio -k` komutunu çalıştırıyoruz ses ayarlarından mikrofon için (echo cancelled) ile başlayanı seçiyoruz. Herkeste aynı etkiyi gösterecek diye durum yok tabii ki eğer hoşunuza gitmezse ses, pulseeffects aracını indirip ekolayzer yapabilirsiniz.
