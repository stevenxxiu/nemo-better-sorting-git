# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=1.7.4
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
md5sums=('fc5595a2489ed28f274c5f79ce95d5de'
         '9e170cc74eee901634b3367b06a209c6'
         'f10af52377e44e1efe8ec4934aa4d4d2')

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
}
