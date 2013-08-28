# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=1.8.5
pkgrel=1
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('i686' 'x86_64')
url="https://github.com/linuxmint/nemo"
license=('GPL')
depends=('libexif' 'gvfs' 'dconf' 'desktop-file-utils' 'exempi' 'python2'
         'gnome-desktop' 'gnome-icon-theme' 'libnotify' 'libtracker-sparql')
makedepends=('gtk-doc' 'gobject-introspection' 'intltool' 'gnome-common')
optdepends=('gksu: Open as Root')
options=('!emptydirs' '!libtool')
install=nemo.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxmint/nemo/tarball/$pkgver"
        "tracker-0.16.patch"
        "remove-desktop-background.patch")
sha256sums=('ba43794293c66ebc31a9c4145d6e7a8326321a4f0e58b28fe4f3d56a8fe39874'
            '2b86f486add84e3affb0b14eb84425443e7cf5e593738d10d02e9c2ac0f17626'
            '0bd07fd931ad701442358cdcbd26e0c5d57717ffadfd39a1cba137e36def1aa5')

build() {
  cd linuxmint-nemo-*

  # Python2 fix
  sed -i 's/bin\/python/bin\/python2/g' files/usr/share/nemo/actions/myaction.py

  # https://github.com/linuxmint/nemo/pull/258
  patch -Np1 -i ../tracker-0.16.patch

  # https://github.com/linuxmint/nemo/pull/263
  patch -Np1 -i ../remove-desktop-background.patch

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

  # Rename 'Files' app name to avoid having the same as nautilus
  sed -i 's/^Name\(.*\)=.*/Name\1=Nemo/' "$pkgdir/usr/share/applications/nemo.desktop"

  # Autostart only in Cinnamon to avoid conflict with GNOME Classic session
  cp "$pkgdir/etc/xdg/autostart/nemo-autostart.desktop" \
    "$pkgdir/etc/xdg/autostart/nemo-autostart2d.desktop"
  sed -i 's/^AutostartCondition=.*/AutostartCondition=GNOME3 if-session cinnamon/' \
    "$pkgdir/etc/xdg/autostart/nemo-autostart.desktop"
  sed -i 's/^AutostartCondition=.*/AutostartCondition=GNOME3 if-session cinnamon2d/' \
    "$pkgdir/etc/xdg/autostart/nemo-autostart2d.desktop"
}
