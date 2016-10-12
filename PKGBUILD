# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=3.0.6
pkgrel=2
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('i686' 'x86_64')
url="https://github.com/linuxmint/nemo"
license=('GPL')
depends=('libexif' 'gvfs' 'dconf' 'desktop-file-utils' 'exempi' 'python'
         'cinnamon-desktop' 'libnotify' 'libxml2' 'cinnamon-translations')
makedepends=('gtk-doc' 'gobject-introspection' 'intltool' 'gnome-common'
      'python-gobject' 'python-polib' 'python2-gobject')
options=('!emptydirs')
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxmint/nemo/tarball/$pkgver"
        "Fix-GTK-3.21.3-desktop-redraw-issue.patch")
sha256sums=('77d5c47a6657dfbaf66c9f80978ce8650595753138d27bd2adaebbe0e46c3e23'
            'ff2fe4fbf6edbdc51e0c6cef08b3b10ae612718d71701c59b28738ad168387eb')

prepare() {
  cd linuxmint-nemo-*

  # Fix GTK 3.21.3 desktop redraw issue
  # https://github.com/linuxmint/nemo/issues/1231
  patch -Np1 -i ../Fix-GTK-3.21.3-desktop-redraw-issue.patch

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

  # Remove D-Bus activation file to avoid conflict with nautilus-desktop
  rm "$pkgdir/usr/share/dbus-1/services/org.nemo.freedesktop.FileManager1.service"
}
