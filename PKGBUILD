# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=2.0.0
pkgrel=2
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('i686' 'x86_64')
url="https://github.com/linuxmint/nemo"
license=('GPL')
depends=('libexif' 'gvfs' 'dconf' 'desktop-file-utils' 'exempi' 'python2'
         'cinnamon-desktop' 'gnome-icon-theme' 'libnotify' 'libtracker-sparql' 'libxml2')
makedepends=('gtk-doc' 'gobject-introspection' 'intltool' 'gnome-common' 'cinnamon-translations')
optdepends=('gksu: Open as Root')
options=('!emptydirs' '!libtool')
install=nemo.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxmint/nemo/tarball/$pkgver")
sha256sums=('3848d55a20134826aa6512898c78b05a953f5d2f353817e7003c1a4f6286e31c')

prepare() {
  cd linuxmint-nemo-*

  # Python2 fix
  sed -i 's/bin\/python/bin\/python2/g' files/usr/share/nemo/actions/myaction.py

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
      --disable-gtk-doc-html \
      --disable-schemas-compile
  make
}

package() {
  cd linuxmint-nemo-*

  make DESTDIR="$pkgdir/" install

  # Autostart only in Cinnamon to avoid conflict with GNOME Classic session
  cp "$pkgdir/etc/xdg/autostart/nemo-autostart.desktop" \
    "$pkgdir/etc/xdg/autostart/nemo-autostart2d.desktop"
  sed -i 's/^AutostartCondition=.*/AutostartCondition=GNOME3 if-session cinnamon/' \
    "$pkgdir/etc/xdg/autostart/nemo-autostart.desktop"
  sed -i 's/^AutostartCondition=.*/AutostartCondition=GNOME3 if-session cinnamon2d/' \
    "$pkgdir/etc/xdg/autostart/nemo-autostart2d.desktop"
}
