# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=2.2.4
pkgrel=2
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
sha256sums=('7dea1a9e1360b00840fe6cf3248c888eba09c3c1003c36aece3d40699787934a'
            'cb5a1e6f27d1e5901faf90a21c0ff199080c0c0d7912dbaa461b01dd6b521f51')

prepare() {
  cd linuxmint-nemo-*

  # Python2 fix
  sed -i 's/bin\/python/bin\/python2/g' files/usr/share/nemo/actions/myaction.py
  find -type f | xargs sed -i 's@^#!.*python$@#!/usr/bin/python2@'

  # Add better style for the desktop with GNOME 3.14
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
