# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=3.6.3
pkgrel=1
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('x86_64')
url="https://github.com/linuxmint/nemo"
license=('GPL')
depends=('libexif' 'gvfs' 'dconf' 'desktop-file-utils' 'exempi' 'python'
         'cinnamon-desktop' 'libnotify' 'libxml2' 'cinnamon-translations' 'xapps')
optdepends=('ffmpegthumbnailer: support for video thumbnails')
makedepends=('gtk-doc' 'gobject-introspection' 'intltool' 'gnome-common'
             'python-gobject' 'python-polib' 'python2-gobject')
options=('!emptydirs')
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxmint/nemo/tarball/$pkgver")
sha512sums=('55b37abb4358317656c04b71e8f794128da03c38026be52dde82902f0d1497bdaedc25bd15a22ddd301b4a61b528e56b40c6f6b44c2f493530230d142b0d716c')

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
  rm "$pkgdir/usr/share/dbus-1/services/nemo.FileManager1.service"
}
