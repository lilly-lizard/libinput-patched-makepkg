# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot

pkgname=libinput
pkgver=0.21.0
pkgrel=2
pkgdesc="library that handles input devices for display servers and other applications that need to directly deal with input devices."
arch=(i686 x86_64)
url="http://www.freedesktop.org/wiki/Software/libinput/"
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev')
install=libinput.install
options=('!libtool')
source=(http://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig})
sha256sums=('7cce7a9e510dfe5c4a19ad00e9350808d4f59f8611fd2b5e87213c507283f550'
            'SKIP')
validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

prepare() {
  cd $pkgname-$pkgver
}

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr --disable-static
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
  install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
