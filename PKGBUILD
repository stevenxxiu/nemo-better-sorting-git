# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=2.2.0
pkgrel=2
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('i686' 'x86_64')
url="https://github.com/linuxmint/nemo"
license=('GPL')
depends=('libexif' 'gvfs' 'dconf' 'desktop-file-utils' 'exempi' 'python2'
         'cinnamon-desktop' 'gnome-icon-theme' 'libnotify' 'libxml2'
         'cinnamon-translations')
makedepends=('gtk-doc' 'gobject-introspection' 'intltool' 'gnome-common' 'python2-gobject' 'python2-polib')
options=('!emptydirs')
install=nemo.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxmint/nemo/tarball/$pkgver"
        "adwaita_style.patch")
sha256sums=('d909354fb5378804eb9abcfe04e3f4b4e482e7afbec018cacc35b3e845cce466'
            '6faa6a5a7042832fb1230a5d21ebe8572c100798e724fcd72fee86dc01d69290')

prepare() {
  cd linuxmint-nemo-*

  # Fix white text on breadcrumb with Adwaita theme
  patch -Np1 -i ../adwaita_style.patch

  # Python2 fix
  sed -i 's/bin\/python/bin\/python2/g' files/usr/share/nemo/actions/myaction.py
  find -type f | xargs sed -i 's@^#!.*python$@#!/usr/bin/python2@'

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
      --disable-packagekit \
      --disable-tracker \
      --disable-gtk-doc-html \
      --disable-schemas-compile
  make
}

package() {
  cd linuxmint-nemo-*

  make DESTDIR="$pkgdir/" install
}
