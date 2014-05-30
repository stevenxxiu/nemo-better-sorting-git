# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=2.2.2
pkgrel=1
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
sha256sums=('452b3720eceb7ae591ce9e1875cb555f531822d8ba73184ea241561d8ad624b2'
            '21555779bc9d2cc87f73042039bcffd43a3d858a7f1f3a93ec27c91cdf69d4ce')

prepare() {
  cd linuxmint-nemo-*

  # Python2 fix
  sed -i 's/bin\/python/bin\/python2/g' files/usr/share/nemo/actions/myaction.py
  find -type f | xargs sed -i 's@^#!.*python$@#!/usr/bin/python2@'

  # Fix white text on breadcrumb with Adwaita theme
  patch -Np1 -i ../adwaita_style.patch

  # Fix desktop style with Adwaita theme
  sed -i 's/add_class (\(.*\), "nemo-/add_class (\1, "nautilus-/' \
    libnemo-private/nemo-icon-{canvas-item,container}.c

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
