# Maintainer: Bruno Pagani <archange@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=6.6.2
pkgrel=2
pkgdesc='File manager for Cinnamon (Nautilus fork)'
arch=(x86_64)
url='https://github.com/linuxmint/nemo'
license=('GPL-3.0-or-later AND LGPL-2.1-or-later')
depends=(
  at-spi2-core
  bash
  cairo
  cinnamon-desktop
  dconf
  exempi
  gcc-libs
  gdk-pixbuf2
  glib2
  glibc
  gtk3
  gvfs
  hicolor-icon-theme
  json-glib
  libexif
  libx11
  libxmlb
  pango
  python
  python-cairo
  python-gobject
  xapp
)
optdepends=(
  'catdoc: search helpers support for legacy MS Word files'
  'cinnamon-translations: i18n'
  'ffmpegthumbnailer: support for video thumbnails'
  'ghostscript: search helpers support for PostScript files'
  'libgsf: search helpers support for MS Office files'
  'libreoffice: search helpers support for legacy MS PowerPoint files'
  'poppler: search helpers support for PDF files'
  'python-xlrd: search helpers support for legacy MS Excel files'
)
makedepends=(
  git
  glib2-devel
  gobject-introspection
  gtk-doc
  intltool
  libgsf
  meson
)
source=("git+https://github.com/linuxmint/nemo.git#tag=$pkgver")
b2sums=(175852456cdd845608ec994a34f2a419ff4d086db59f4a98b6c3aa5ab0ca89acacb66701861c35a35bda021ff1f0ee005798978f7b24d4a10e4cbe2b883505ea)

build() {
  arch-meson $pkgname build \
    --libexecdir=lib/$pkgname \
    -D gtk_doc=true
  meson compile -C build
}

package() {
  meson install -C build --destdir="$pkgdir"
}
