# $Id: PKGBUILD 60970 2011-12-19 21:33:58Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.1
pkgrel=2
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
        01-systray.patch
        02-pertag.patch
        03-statuscolors.patch
        04-status2dleif.patch
        05-config-colors.patch
        06-config-font.patch
        07-config-keys.patch
        08-config-tags.patch
        dwm.desktop
        dwmstart)
md5sums=('f0b6b1093b7207f89c2a90b848c008ec'
         'b059f5abfb7ac17c18bc1d69e102c5d0'
         'c9413139eb527560fd742420f455cd7f'
         '09ded45a4d861db58d18ed2e63aa69f0'
         '096a47a8b979c585221adc4c3677eeaf'
         '58f30564eea68300a375cdbfbcc5c61f'
         '15222918fd0193435499c61dd3dc6d29'
         'd137a34852b9018790583109fe7166aa'
         '8af427ba13e14d06531ad858f335571a'
         '1fd6ee7c7d66741480aa5256849ddd6b'
         'c8e286dc3b77c76f5b088bcb66dfcd14')

build() {
  cd $srcdir/$pkgname-$pkgver
  for patch in $srcdir/*.patch; do
    echo "=> $patch"
    patch -p1 < $patch
  done
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
  install -m755 -D $srcdir/dwmstart $pkgdir/usr/bin/dwmstart
}
