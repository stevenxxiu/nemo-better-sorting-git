# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=2.0.8
pkgrel=2
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('i686' 'x86_64')
url="https://github.com/linuxmint/nemo"
license=('GPL')
depends=('libexif' 'gvfs' 'dconf' 'desktop-file-utils' 'exempi' 'python2'
         'cinnamon-desktop' 'gnome-icon-theme' 'libnotify' 'libtracker-sparql' 'libxml2'
         'cinnamon-translations')
makedepends=('gtk-doc' 'gobject-introspection' 'intltool' 'gnome-common')
options=('!emptydirs')
install=nemo.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxmint/nemo/tarball/$pkgver"
        "Fix_rename_entry_position.patch")
sha256sums=('6a40868e46fd2ed6c27e694e76c160996d16e2d27681bf5126e6b0e647c24033'
            '07e81aaeeff9ae8c6de76fe2b87b28b89323577ef425596241b96e94b4e04750')

prepare() {
  cd linuxmint-nemo-*

  # Rename files and directory : invisible field: https://bugzilla.redhat.com/show_bug.cgi?id=1045181
  patch -Np1 -i ../Fix_rename_entry_position.patch

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
}
