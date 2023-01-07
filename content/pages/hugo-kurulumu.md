---
title: Böyle Bir Siteye Sahip Olmak İster Misiniz?
date: 2022-12-17
tags: ["proje"]
draft: false
---
# Github Pages Üzerinde Hugo
Herkese selam, uzun uğraşlar sonucu Hugo'yu halledebildim bugün ise github-pages üzerinde Hugo kurulumunu anlatacağım.

# 1-) Github Deposu Oluşturma
Github üzerinde kullanıcıadı.github.io şeklinde yeni bir repo oluşturuyoruz.

# 2-) Hugo Kurulumu
Linux kullanıyorsanız paket yöneticinizi kullanarak Hugo paketini yükleyin.
-    Arch : `sudo pacman -S hugo`
-   Debian / Ubuntu : `sudo apt install hugo`
-   Fedora : `sudo dnf install hugo`
-   Gentoo : `sudo emerge --ask www-apps/hugo`
-   OpenSUSE : `sudo zypper in hugo`

# 3-) Git Kurulumu
Linux kullanıyorsanız paket yöneticinizi kullanarak Git paketini yükleyin.
-   Arch : `sudo pacman -S git`
-   Debian / Ubuntu : `sudo apt install git`
-   Fedora : `sudo dnf install git`
-   Gentoo : `sudo emerge --ask dev-vcs/git`
-   OpenSUSE : `sudo zypper in git`

# 4-) Hugo Repo üzerinde kurulum
Araçlarımızı yüklediğimize göre kuruluma geçelim öncelikle karmaşıklık olmasın için Documents/Belgeler kısmında bu işlemleri uygulayabilirsiniz.

```bash
git clone https://github.com/kullanıcıadı/kullanıcıadı.github.io
```
- Sonrasında hugo’yu repo içine kuralım.
```bash
hugo new site kullanıcıadı.github.io --force
cd kullanıcıadı.github.io
```
- Hugo yapılandırma işlemi için `config.toml` içine bunları ekleyin örnek için kendi config dosyamı paylaşıyorum. baseURL kısmını kendinize göre düzenleyin ondan sonra isteğinize göre yapılandırma yapabilirsiniz.

```yml
baseURL = 'http://kullaniciadi.github.io/'
languageCode = 'tr-tr'
title = 'Boranity Blog'
theme = 'PaperMod'
paginate = "5"
DefaultContentLanguage = "tr"
enableInlineShortcodes = true
enableRobotsTXT = true
buildDrafts = false
buildFuture = false
buildExpired = false
enableEmoji = true

[Author]
  name = "Boranity"
  telegram = "@boranity"
  mastodon = "@boranity@mastodon.com.tr"


 [params]
  favicon = "img/favicon.ico"
  dateFormat = "January 2, 2006"
  rss = true
  defaultTheme = "auto"
  ShowPostNavLinks = true
  env = "production"
  ShowReadingTime = true
  ShowCodeCopyButtons = true



  [privacy.youtube]
  disabled = false
  privacyEnhanced = true

  [params.homeInfoParams]
  Title = "Boranity Blog 👋"
  Content = "Linux, özgür yazılım gibi kendi deneyimlemiş olduğum ve arada günlük hayatımdaki yaşanmış olayı anlatabileceğim bir blog."

  [[params.socialIcons]]
  name = "github"
  url = "https://github.com/boranityy"
  html_attributes = "rel=\"me\""

  [[params.socialIcons]]
  name = "telegram"
  url = "https://t.me/boranity"
  html_attributes = "rel=\"me\""

  [[params.socialIcons]]
  name = "twitter"
  url = "https://twitter.com/@boranits"
  html_attributes = "rel=\"me\""

  [[params.socialIcons]]
  name = "mastodon"
  url = "https://mastodon.com.tr/@boranity"
  html_attributes = "rel=\"me\""

  [[params.socialIcons]]
  name = "reddit"
  url = "https://www.reddit.com/user/Boranity0"
  html_attributes = "rel=\"me\""

  [[params.socialIcons]]
  name = "RsS"
  url = "index.xml"

```
Dosyayı kaydedip çıktıktan sonra kendi sitemdeki PaperMod temasını kurmayı anlatacağım isterseniz farklı tema seçebilirsiniz ona göre komutları değiştirirsiniz.

```bash
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

- Şimdi ise her gönderi paylaştığımız da sitemizi yenileyecek kodu yazalım.
```bash
$ mkdir .github/workflows -p
$ nano .github/workflows/gh-pages.yml          #içine alttakileri yazın

name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public

```
Kaydedip çıkalım. Şimdi ise yaptığımız şeyleri Repo'muza yükleyeceğiz. Ama öncelikle bize Github Tokeni lazım onun için [Buradan](https://github.com/settings/tokens) yeni token oluşturun tokeni bir yere kaydedin.

```bash
hugo                                   # Son durumu kaydedelim
git add .
git commit -m "Hugo"
git push -u origin main -f               # Sizden kullanıcı adı ve şifre isteyecek. Kullanıcı adınızı Github'daki yazın ve
                                         # Şifre kısmına ghp ile başlayan tokeni giriniz
```

Dosyalar yüklendikten sonra bu işlemi uygulayın.
![](https://i.hizliresim.com/f6ta4c4.jpg)
