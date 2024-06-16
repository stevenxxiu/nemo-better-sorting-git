# Maintainer: Bruno Pagani <archange@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=6.2.0
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
sha512sums=('9842d986e955b931ac199332b4f4470f7194f2ec2b151f82c63a7abe6e0458bfd347ece94c394ed618f57e31a3f8c028b2b645f98df456720e4877cc7b3899ad')
b2sums=('262944d8fe9b7624b6926dc9b34a23b6182ef7d940eef6e1ef2b14ca6114ddb1df6a16d887c91903603ca2dd4b17d6ffab378bdc6332f2d81698b357f946b785')

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
