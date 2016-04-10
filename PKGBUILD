# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=2.8.7
pkgrel=3
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
        "deep-count-one-filesystem.patch"
        "0001-Fix-fallback-style-for-GTK-3.20.patch")
sha256sums=('21f290212bcfb4ac58f7bdc17e9dccfafb59d9fd52a7540a7e199e252a7c2fe4'
            '1acd384b7e345d4e2815c51a94b4ffbb802ee376004c3db75cc871eef551cbfa'
            'cb5aa9ec771afd5380cee08e1dd17ef35b6d6502ab8c778d85e88350a30ddfc5')

prepare() {
  cd linuxmint-nemo-*

  # Python2 fix
  find -type f | xargs sed -i 's@^#!.*python$@#!/usr/bin/python2@'

  # directory: limit deep scount (folder contents and size) to one filesystem (FS#47480)
  # https://github.com/linuxmint/nemo/pull/1083
  patch -Np1 -i ../deep-count-one-filesystem.patch

  # Fix fallback style for GTK 3.20
  # https://github.com/linuxmint/nemo/pull/1138
  patch -Np1 -i ../0001-Fix-fallback-style-for-GTK-3.20.patch

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

  #https://bugzilla.gnome.org/show_bug.cgi?id=656231
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool

  make
}

package() {
  cd linuxmint-nemo-*

  make DESTDIR="$pkgdir" install
}
