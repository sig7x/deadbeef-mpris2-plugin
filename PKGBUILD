pkgname=deadbeef-mpris2-plugin-git
pkgver=1.14.1
pkgrel=1
pkgdesc='MPRISv2 plugin for the DeaDBeeF music player'
url='https://github.com/sig7x/deadbeef-mpris2-plugin'
arch=('x86_64')
license=('GPL2')
depends=('deadbeef>=1.9.0')
makedepends=('git' 'glib2' 'automake')
source=("$pkgname::git+$url.git#branch=db-1.9")
b2sums=('SKIP')

pkgver() {
  cd "$pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  # deadbeef install places artwork.h in the same dir as deadbeef.h while it is trying to include "../../deadbeef.h"
  sed 's|"../../deadbeef.h"|<deadbeef/deadbeef.h>|' /usr/include/deadbeef/artwork.h > "$srcdir/$pkgname/src/artwork.h"
}

build() {
  cd "$srcdir/$pkgname"
  autoreconf --install
  ./configure --prefix=/usr
  make
}

package() {
  cd "$srcdir/$pkgname"
  make DESTDIR="$pkgdir" install
}
