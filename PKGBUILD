# Maintainer: Steven Xu <stevenxxiu@gmail.com>
# Maintainer: Bruno Pagani <archange@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

_pkgname=nemo
pkgname=${_pkgname}-git
pkgver=6.6.3.r22.g66d42992
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
  xapps-git
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
conflicts=('nemo')
provides=('nemo')
source=("git+$url.git")
b2sums=('SKIP')

pkgver() {
  cd $_pkgname
  git describe --tags --match="[0-9]*.[0-9]*.[0-9]*" | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd $_pkgname

  # Patches
  patch --forward --strip=1 --input="${startdir}/0001-feat-sort-hidden-files-the-same-as-normal-files-so-w.patch"
  patch --forward --strip=1 --input="${startdir}/0002-feat-use-g_utf8_collate_key-instead-of-g_utf8_collat.patch"
}

build() {
  arch-meson $_pkgname build \
    --libexecdir=lib/$_pkgname \
    -D gtk_doc=true
  meson compile -C build
}

package() {
  meson install -C build --destdir="$pkgdir"
}
