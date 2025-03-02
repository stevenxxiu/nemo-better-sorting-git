# Maintainer: Bruno Pagani <archange@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=6.4.5
pkgrel=1
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=(x86_64)
url="https://github.com/linuxmint/${pkgname}"
license=(GPL)
depends=(cinnamon-desktop dconf gvfs exempi libexif libnotify libxml2
         python xapp)
optdepends=('cinnamon-translations: i18n'
            'ffmpegthumbnailer: support for video thumbnails'
            'catdoc: search helpers support for legacy MS Office files'
            'ghostscript: search helpers support for PostScript files'
            'libgsf: search helpers support for MS Office files'
            'libreoffice: search helpers support for legacy MS Office powerpoint files'
            'odt2txt: search helpers support for LibreOffice files'
            'poppler: search helpers support for PDF')
makedepends=(meson samurai gobject-introspection intltool libgsf glib2-devel)
source=(${url}/archive/${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha512sums=('4163dafe0d2c581468b70bf78d928b42d4e71823d698b6e8c5f86e48d148f29fcc7b02f451eba6018ae21c6e3f6ec876c5460ddeff16a8a30613ee19fcec496a')
b2sums=('48a620f6aed0c4652f734ce9ee7e0d9a9d5946ab7f2398baba079825dc4a18d829bc2bb0c59796534970f829adc15a9e60c62e9baebed94a2104aac080f77ef3')

prepare() {
  cd ${pkgname}-${pkgver}
  # Rename 'Files' app name to avoid having the same as nautilus
  sed -i '/^\[Desktop Entry/,/^\[Desktop Action/ s/^Name\(.*\)=.*/Name\1=Nemo/' data/nemo.desktop.in
}

build() {
  arch-meson --libexecdir=lib/${pkgname} ${pkgname}-${pkgver} build
  samu -C build
}

package() {
  DESTDIR="${pkgdir}" samu -C build install
}
