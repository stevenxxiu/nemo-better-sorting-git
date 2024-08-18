# Maintainer: Bruno Pagani <archange@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=6.2.8
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
sha512sums=('cd943603cfb14cc9d50466872607d191a3af7ff61f05549407caa5d9dfe606e080d6eb40d17bbcdf3a9e810bcc493f3be087b1eac6c8272746cd72c9751822af')
b2sums=('fc74ab19e5aef65ba279f212f505cab91aa0dc92b19d31d4ae2f44b3222bd2278fbdf0df0bc36fa3973b91c9c06fab2c211b58c8d840deef5e60d5dbcbfa4dd7')

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
