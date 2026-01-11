# Maintainer: Bruno Pagani <archange@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=6.6.3
pkgrel=1
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
b2sums=('ced1a9421a4e37226ab9d1d828b4562be983a598b781c8d1af7891c5b7f9148316f2a5bdaf4427e3bcc923a79d832ee8bc85e7d10414dd2b965d3e0b517590a5')

build() {
  arch-meson $pkgname build \
    --libexecdir=lib/$pkgname \
    -D gtk_doc=true
  meson compile -C build
}

package() {
  meson install -C build --destdir="$pkgdir"
}
