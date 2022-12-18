---
title: Linux'ta Chromium Tarayıcılarda Koyu Mod Aktif Etme
date: 2022-12-18
tags: ["linux"]
draft: false
showtoc: true
---

Kısa bir içerik olacak fakat Chromium tarayıcıların bazılarında ayarlarda koyu modu açamıyorsunuz bunlardan biri Google Chrome. Bu kodu terminaliniz de çalıştırınız. Örnek olarak Google Chrome için kod paylaşacağım. `google-chrome-stable` yazan yeri kullandığınız tarayıca göre düzenleyebilirsiniz eğer yapamazsanız ana sayfadan bana telegramdan ulaşabilirsiniz.

```bash
sudo sed -i 's;/usr/bin/google-chrome-stable;/usr/bin/google-chrome-stable --enable-features=WebUIDarkMode --force-dark-mode;g' /usr/share/applications/google-chrome.desktop
```
