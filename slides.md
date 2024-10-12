---
marp: true
theme: cybertopia
class: invert
paginate: true
header: '**Logiciel libre & Cybersécurité** - **Alexandre ZANNI** alias **noraj**'
footer: '19/10/204 - Open Source Immersion (OSI) 2024'
---

<!-- _header: '' -->
<!-- _footer: '' -->

## Open Source Immersion 2024
### Logiciel libre & Cybersécurité

![bg blur:3px](assets/code.png)

---

## Présentation

- Alexandre ZANNI (@noraj)
- Ingénieur en test d'intrusion
- Recherche et développement
- Contributeur logiciel libre
- Mainteneur BlackArch Linux

![bg contain right:20%](assets/noraj-qrcode.png)

---

## Plan

1. BlackArch
2. Rawsec Cybersecurity Inventory
3. Anecdotes et écosystème
4. Synacktiv : recherche et développement

---

![bg left:33% blur:3px](assets/code_cropped.png)

## BlackArch

---

![bg contain right:50%](assets/ba-logo-transp.png)
![bg contain](assets/blackarch-qrcode.png)

Distribution GNU/Linux en source ouverte pensée pour le test d'intrusion et plus généralement pour la cybersécurité technique. Basée sur ArchLinux.


---

<!-- _header: '' -->
<!-- _footer: '' -->

![bg](assets/ba-slider2.png)

2920 outils (08/10/2024)

---

![bg contain](assets/wordcloud-categories-blackarch.png)

---

<!-- _header: '' -->
<!-- _footer: '' -->

2009-2024

![bg contain left](assets/blackarch-contribs.png)

---

#### Installation

- ISO : Full (22 GO), Slim (5.5 Go), NetInstall (815 Mo)
- VM : OVA (29 Go)
- par-dessus ArchLinux comme dépôt additionnel
- HTTP, HTTPS, FTP, rsync, torrent
- miroirs : 🇦🇺🇦🇹🇨🇦🇨🇳🇩🇰🇪🇨🇫🇷🇩🇪🇬🇷🇬🇧🇭🇺🇮🇳🇮🇷🇮🇹🇯🇵🇰🇷🇲🇩🇳🇱🇳🇿🇵🇱🇵🇹🇷🇺🇸🇬🇸🇪🇨🇭🇹🇷🇹🇼🇺🇸

---

<!-- _header: '' -->
<!-- _footer: '' -->

#### Statistiques

![bg left contain](assets/blackarch-star-history.svg)

- 562 fourches (forks)
- 2,8k étoiles (stars)
- 99 contributeurs
- 4-5 membres actifs
- 24313 archivages (commits)
- 1635 fusiodemandes (merge requests)
- 2535 tickets (issues)

---

###### PKGBUILD

```bash
# This file is part of BlackArch Linux ( https://www.blackarch.org/ ).
# See COPYING for license details.

pkgname=ffuf
pkgver=v2.1.0.r3.gde9ac86
pkgrel=1
epoch=1
groups=('blackarch' 'blackarch-webapp' 'blackarch-fuzzer')
pkgdesc='Fast web fuzzer written in Go.'
arch=('x86_64' 'aarch64')
url='https://github.com/ffuf/ffuf'
license=('MIT')
makedepends=('git' 'go')
options=('!strip')
source=("git+https://github.com/ffuf/$pkgname.git")
sha512sums=('SKIP')
```

---

```bash
pkgver() {
  cd $pkgname

  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd $pkgname

  GOPATH="$srcdir" go mod download
  GOPATH="$srcdir" go build \
    -trimpath \
    -buildmode=pie \
    -mod=readonly \
    -modcacherw \
    -ldflags "-s -w" \
    -o $pkgname .
}

package() {
  cd $pkgname

  install -Dm 755 $pkgname "$pkgdir/usr/bin/$pkgname"
  install -Dm 644 "${pkgname}rc.example" \
    "$pkgdir/usr/share/$pkgname/${pkgname}rc.example"
  install -Dm 644 -t "$pkgdir/usr/share/doc/$pkgname/" *.md
}
```

---

#### Le travail d'un mainteneur

- Empaqueter des nouveaux outils
- Corriger les bogues / améliorer
- MAJ les outils
- MAJ / ajouter des modèles de PKGBUILD
- Autres : ISO, torrents, support à la communauté reddit / Matrix / Github / courriel, ajout mirroirs de dépôts
- Site web, outils comme wordlistctl, webshells

---

