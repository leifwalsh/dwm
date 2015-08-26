# $Id: PKGBUILD 60970 2011-12-19 21:33:58Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.0
pkgrel=5
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
        01-statuscolors.patch
        02-pertag.patch
        03-systray.patch
        04-config-colors.patch
        05-config-font.patch
        06-config-keys.patch
        07-config-tags.patch
        dwm.desktop
        dwmstart)
md5sums=('8bb00d4142259beb11e13473b81c0857'
         '76706fdeda50e0a9f8367079efee7149'
         'd2ff4c32286bb5fec5c9bee8c7aac91b'
         '967174d90cc7d99508f4285fedf301a8'
         'bc65904864bcda50ce397b1962f9d66d'
         '22dcb7b1d762837dcdef54a815323915'
         'bcf6dd303e03c9e490b602a2fb453ffe'
         '2380a9a7473b4c026135bd035ce5c2f3'
         '1fd6ee7c7d66741480aa5256849ddd6b'
         'c8e286dc3b77c76f5b088bcb66dfcd14')

build() {
  cd $srcdir/$pkgname-$pkgver
  for patch in $srcdir/*.patch; do
    echo "=> $patch"
    patch -p1 < $patch
  done
  cp $srcdir/dwmstart dwmstart
  sed -i 's/CPPFLAGS =/CPPFLAGS +=/g' config.mk
  sed -i 's/^CFLAGS = -g/#CFLAGS += -g/g' config.mk
  sed -i 's/^#CFLAGS = -std/CFLAGS += -std/g' config.mk
  sed -i 's/^LDFLAGS = -g/#LDFLAGS += -g/g' config.mk
  sed -i 's/^#LDFLAGS = -s/LDFLAGS += -s/g' config.mk
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m755 -D dwmstart $pkgdir/usr/bin/dwmstart
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
