# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=2.4.3
pkgrel=1
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('i686' 'x86_64')
url="https://github.com/linuxmint/nemo"
license=('GPL')
depends=('libexif' 'gvfs' 'dconf' 'desktop-file-utils' 'exempi' 'python2'
         'cinnamon-desktop' 'libnotify' 'libxml2' 'cinnamon-translations')
makedepends=('gtk-doc' 'gobject-introspection' 'intltool' 'gnome-common' 'python2-gobject' 'python2-polib')
options=('!emptydirs')
install=nemo.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxmint/nemo/tarball/$pkgver"
        "desktop-theme.patch")
sha256sums=('c3a0537d5c45fcf0cb3863caeb92f48cafa9076f3130c43735c7eb4a2e8cded7'
            'SKIP')

prepare() {
  cd linuxmint-nemo-*

  # Python2 fix
  find -type f | xargs sed -i 's@^#!.*python$@#!/usr/bin/python2@'

  # Add application-specific theme for Adwaita
  patch -Np1 -i ../desktop-theme.patch

  # Fix build
  sed -i '/AC_SUBST(DISABLE_DEPRECATED_CFLAGS)/d' configure.in

  # Rename 'Files' app name to avoid having the same as nautilus
  sed -i 's/^Name\(.*\)=.*/Name\1=Nemo/' data/nemo.desktop.in.in
}

build() {
  cd linuxmint-nemo-*

  ./autogen.sh --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --disable-static \
      --libexecdir=/usr/lib/nemo \
      --disable-update-mimedb \
      --disable-tracker \
      --disable-gtk-doc-html \
      --disable-schemas-compile
  make
}

package() {
  cd linuxmint-nemo-*

  make DESTDIR="$pkgdir/" install
}
