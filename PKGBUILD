# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=3.4.5
pkgrel=1
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('i686' 'x86_64')
url="https://github.com/linuxmint/nemo"
license=('GPL')
depends=('libexif' 'gvfs' 'dconf' 'desktop-file-utils' 'exempi' 'python'
         'cinnamon-desktop' 'libnotify' 'libxml2' 'cinnamon-translations')
optdepends=('ffmpegthumbnailer: support for video thumbnails')
makedepends=('gtk-doc' 'gobject-introspection' 'intltool' 'gnome-common'
             'python-gobject' 'python-polib' 'python2-gobject')
options=('!emptydirs')
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxmint/nemo/tarball/$pkgver")
sha512sums=('911dcc22bbf6e8810c7acab6e3e7ce9b587257549c3654a0808c61940ab2fe85879ff183583c3686d423af97588bc6e038f3167f43c13b4f8c92bc13c074f943')

prepare() {
  cd linuxmint-nemo-*

  # Rename 'Files' app name to avoid having the same as nautilus
  sed -i '/^\[Desktop Entry/,/^\[Desktop Action/ s/^Name\(.*\)=.*/Name\1=Nemo/' data/nemo.desktop.in.in
}

build() {
  cd linuxmint-nemo-*

  ./autogen.sh --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --disable-static \
      --libexecdir=/usr/lib/nemo \
      --disable-update-mimedb \
      --disable-tracker \
      --disable-gtk-doc-html \
      --disable-schemas-compile \
      --disable-selinux

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
