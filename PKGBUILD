# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=3.0.5
pkgrel=1
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('i686' 'x86_64')
url="https://github.com/linuxmint/nemo"
license=('GPL')
depends=('libexif' 'gvfs' 'dconf' 'desktop-file-utils' 'exempi' 'python'
         'cinnamon-desktop' 'libnotify' 'libxml2' 'cinnamon-translations')
makedepends=('gtk-doc' 'gobject-introspection' 'intltool' 'gnome-common'
      'python-gobject' 'python-polib' 'python2-gobject')
options=('!emptydirs')
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxmint/nemo/tarball/$pkgver")
sha256sums=('67a4607e0f311db3b71c2014ab2be4c0d4c14f272fc019d381c77acf8442ad77')

prepare() {
  cd linuxmint-nemo-*

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
