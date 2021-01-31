pkgname=8189fs-git
_pkgname=rtl8189ES_linux
pkgver=r64.c6493c3
pkgrel=1
pkgdesc="Kernel module for Realtek RTL8189FTV SDIO wireless devices."
arch=('aarch64')
url="https://github.com/jwrdegoede/rtl8189ES_linux/tree/rtl8189fs"
license=('GPL')
depends=('linux')
makedepends=('linux-headers' 'git')
source=("git://github.com/jwrdegoede/$_pkgname.git#branch=rtl8189fs")
sha256sums=('SKIP')
install=depmod.install

_extramodules="$(basename $(readlink -f /lib/modules/$(uname -r)/extramodules/))"

pkgver() {
  cd "$_pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "$_pkgname"
  make ARCH=arm64 KSRC="/lib/modules/$(uname -r)/build/"
  gzip -9 8189fs.ko
}

package() {
  install -d "$pkgdir/usr/lib/modules/${_extramodules}/"
  install -m644 "$srcdir/$_pkgname/8189fs.ko.gz" \
    "$pkgdir/usr/lib/modules/${_extramodules}/8189fs.ko.gz"
}
