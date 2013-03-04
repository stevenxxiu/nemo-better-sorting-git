# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=1.7.1
pkgrel=2
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('i686' 'x86_64')
url="https://github.com/linuxmint/nemo"
license=('GPL')
depends=('libexif' 'gvfs' 'dconf' 'desktop-file-utils' 'exempi' 'python2'
         'gnome-desktop' 'gnome-icon-theme' 'libnotify' 'libtracker-sparql')
makedepends=('gtk-doc' 'gobject-introspection' 'intltool' 'gnome-common')
optdepends=('gksu: Open as Root')
provides=('nemo-fm')
replaces=('nemo-fm')
conflicts=('nemo-fm')
options=('!emptydirs' '!libtool')
install=nemo.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxmint/nemo/tarball/$pkgver"
        "gnome-autogen.sh"
        "use-terminal-config.patch")
md5sums=('b348b6e340e055bef3163555b99621bb'
         'a925691c9b57a6a884dcf07da057fd1f'
         '6cca080cc8fe3df7e725c0f8cd5fa485')

build() {
  cd linuxmint-nemo-*

  # Read the default terminal app from GSettings
  patch -Np1 -i ../use-terminal-config.patch

  cp ${srcdir}/gnome-autogen.sh .
  sed -i 's/\ --warn-all\ --warn-error//' src/Makefile.am
  sed -i 's/gnome-autogen.sh/.\/gnome-autogen.sh/g' autogen.sh
  chmod +x gnome-autogen.sh

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

  # Python2 fix
  sed -i 's/bin\/python/bin\/python2/g' "${pkgdir}/usr/share/nemo/actions/myaction.py"
}
