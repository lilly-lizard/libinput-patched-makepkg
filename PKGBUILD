# Maintainer: Andreas Radke <andyrtr@archlinux.org>

pkgname=libinput-patched
pkgver=1.21.0
pkgrel=2
pkgdesc="Input device management and event handling library"
url="https://gitlab.freedesktop.org/libinput"
arch=(x86_64)
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
provides=('libinput')
conflicts=('libinput')
# upstream doesn't recommend building docs
makedepends=('gtk4' 'meson' 'wayland-protocols' 'check') # 'doxygen' 'graphviz' 'python-sphinx' 'python-recommonmark'
optdepends=('gtk4: libinput debug-gui'
            'python-pyudev: libinput measure'
            'python-libevdev: libinput measure')
source=(https://gitlab.freedesktop.org/libinput/libinput/-/archive/$pkgver/libinput-$pkgver.tar.bz2 libinput_draglock_timeout.patch)
sha512sums=('SKIP' 'SKIP')

#sha512sums=('145b0e0760929137ab442b2030b4b42f6df54a3ae61c47c929e1a74857a170f0f2a56bb7522b7d1d9c0943028ac54c7728cf8d66a0c384f6118f31d6625ab44c')
#sha512sums=('SKIP')
#source=(https://freedesktop.org/software/$pkgname/$pkgname-$pkgver.tar.xz{,.sig})
#sha512sums=('f4b776d0da78c687ba21b430a04941ac6b43f68970c82ec9f7360358fdea5ed6a873948ce66a25bcdd64d4b95fa4bf705cc24dbc25c7c0f5fd2d0efbd763f298'
#            'SKIP')
#validpgpkeys=('3C2C43D9447D5938EF4551EBE23B7E70B467F0BF') # Peter Hutterer (Who-T) <office@who-t.net>

prepare() {
  patch --directory="libinput-$pkgver" --forward --strip=2 --input="${srcdir}/libinput_draglock_timeout.patch"
}

build() {
  arch-meson libinput-$pkgver build \
    -D udev-dir=/usr/lib/udev \
    -D documentation=false

  # Print config
  meson configure build

  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  meson install -C build --destdir "$pkgdir"

  install -Dvm644 libinput-$pkgver/COPYING \
    "$pkgdir/usr/share/licenses/libinput/LICENSE"
}
