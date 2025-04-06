# Maintainer: 

pkgname=('racket-minimal')
pkgver=8.16
pkgrel=1
pkgdesc='Minimal Racket installation'
arch=('x86_64' 'aarch64')
url='https://racket-lang.org/'
license=('Apache-2.0' 'GPL-3.0-only' 'LGPL-3.0-only' 'custom')
depends=('gtk3' 'libevent' 'libffi' 'libiconv' 'ncurses' 'zlib' 'lz4' 'libtool')
makedepends=('gsfonts' 'sqlite')
options=('!strip' '!emptydirs')
conflicts=('racket')
replaces=('racket')

source=("https://download.racket-lang.org/installers/${pkgver}/${pkgname}-${pkgver}-src.tgz")

sha512sums=('d4b4328e8e876e3840998dbad76666a4b1548b90a72cb5fda172a5bed5ad889ae25cc5b9ca0509f344a7a44d62f114692960ef95ac0c5cb6dc185b15e2f8793f')
b2sums=('ec7c1e722e1e21265aad32571ea54b9b250bb034637e7c73175af64f1b529bd90defa337b51bad309fad72c88e15fca02f56d1566d06f09eae24f4a7d2b9234b')

_basename=racket
_configure_options=('--prefix=/usr --sysconfdir=/etc --enable-libffi --enable-pthread --enable-iconv --enable-curses --enable-csdefault --enable-libz --enable-liblz4 --enable-lt --disable-shared --disable-docs --disable-libs --disable-standalone')

prepare() {
  cd "$_basename-$pkgver"
}

build() {
  cd "$_basename-$pkgver/src"
  [ "$CARCH" == "x86_64" ] && export CFLAGS+=" -fPIC -ffat-lto-objects"
  ./configure $_configure_options
  make JOBS=$(nproc)
}

package_racket-minimal() {
  cd "$_basename-$pkgver/src"
  make DESTDIR="$pkgdir" install

  install -Dm644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE*.txt
}
