# Maintainer: Bruno Pagani <archange@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=6.6.1
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
makedepends=(git meson gobject-introspection intltool libgsf glib2-devel)
source=(git+${url}#tag=$pkgver)
sha512sums=('6da5994e817779ad84b8f30d25b87a18f4e9c23bd0d49c528d88269cca13c8e15a2889c625aaf7c8542e91f4ce23ec9d8ca30f925af94b401c12cda2e91acaeb')
b2sums=('652e563d0efdd3144536044527e0f5469b2b68fca1670894ccc9039a4f6a62d8f67b7efb54b06106490a9bdc9abc4e35c1b583ad4dc69147efe930a3d5a58aef')

prepare() {
  cd ${pkgname}
  # Rename 'Files' app name to avoid having the same as nautilus
  sed -i '/^\[Desktop Entry/,/^\[Desktop Action/ s/^Name\(.*\)=.*/Name\1=Nemo/' data/nemo.desktop.in
}

build() {
  arch-meson --libexecdir=lib/${pkgname} ${pkgname} build
  meson compile -C build
}

package() {
  meson install -C build --destdir="$pkgdir"
}
