# Maintainer: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=1.7.1
pkgrel=1
pkgdesc="Cinnamon file manager (Nautilus fork), stable version"
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
        "gnome-autogen.sh")
md5sums=('b348b6e340e055bef3163555b99621bb'
         'a925691c9b57a6a884dcf07da057fd1f')

build() {
  cd linuxmint-nemo-*

  # Get default terminal value
  _terminal=$(gsettings get org.gnome.desktop.default-applications.terminal exec | tr -d "'")

  # Set "Open in Terminal" to default terminal (Arch doesn't use x-terminal-emulator)
  sed -i "s/x-terminal-emulator/$_terminal/" src/nemo-view.c

  cp ${srcdir}/gnome-autogen.sh .
  sed -i 's/\ --warn-all\ --warn-error//' src/Makefile.am
  sed -i 's/gnome-autogen.sh/.\/gnome-autogen.sh/g' autogen.sh
  chmod +x gnome-autogen.sh

  ./autogen.sh --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --disable-static \
      --libexecdir=/usr/lib/nemo \
      --disable-nst-extension \
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
