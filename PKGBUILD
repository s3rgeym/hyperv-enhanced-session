#!/bin/bash
# shellcheck disable=SC2034,SC2154,SC2164

# Maintainer: Sergey M <yamldevelope@proton.me>
# Based on:
# https://github.com/microsoft/linux-vm-tools/blob/master/arch/install-config.sh

# ПОМНИ: версия пакета на сервере не обновится (файл .SRCINFO), пока не изменится какой-нибудь source
# ЭТО ПРОСТО ЗАЕБАЛО, ПОЭТОМУ ВМЕСТО ПРОВЕРКИ ЧЕКСУМ ПРОЩЕ ПИСАТЬ SKIP!!!
pkgname="hyperv-enhanced-session"
# AUR не поддерживает теги как и любые ветки кроме master
pkgver=1
pkgrel=0
#arch=('x86_64')
arch=('any')
pkgdesc="Enables Hyper-V Enhanced Session via systemd."
url="https://github.com/s3rgeym/hyperv-enhanced-session"
license=('GPL')

provides=("$pkgname.service")

depends=(
  base{,-devel}
  xorg-xinit
  hyperv
  {xorg,}xrdp-git
)

optdepends=(
  'hyperv: hyper-v tools'
  'xf86-video-fbdev: frame buffer xorg driver fix resolution issue'
)

source=('git+https://github.com/s3rgeym/hyperv-enhanced-session.git')

sha256sums=('SKIP')

pkgver() {
  # Сначала клонируется репо, а потом он крпмруется в src
  cd "$pkgname"
  git describe --abbrev=0 --tags
}

prepare() {
  :
}

build() {
  :
}

package() {
  cd "$srcdir/$pkgname"
  cd ./install-files
  readarray -t install_files < <(find . -type f)
  for file in "${install_files[@]}"; do
    install -CDm644 "$file" "$pkgdir/$file"
  done
  cd ../

  install -Dm644 README.md -t "$pkgdir"/usr/share/doc/$pkgname/README.md

  #printf '%.0s-' {1..78}

  fold -w 78 -s <<-EOF
	==============================================================================
	You will have to configure ~/.xinitrc to start your windows manager, see https://wiki.archlinux.org/index.php/Xinit
	Run "sudo systemctl enable --now $pkgname.service" to enable enhanced session.
	==============================================================================
	EOF
}
