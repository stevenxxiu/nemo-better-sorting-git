# Maintainer: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=4.0.0
pkgrel=1
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('x86_64')
url="https://github.com/linuxmint/${pkgname}"
license=('GPL')
depends=('cinnamon-desktop' 'dconf' 'gvfs' 'exempi' 'libexif' 'libnotify' 'libxml2' 'python' 'xapps')
optdepends=('cinnamon-translations: i18n'
            'ffmpegthumbnailer: support for video thumbnails')
makedepends=('meson' 'gobject-introspection' 'intltool')
source=("$pkgname-$pkgver.tar.gz::${url}/archive/${pkgver}.tar.gz")
sha512sums=('0f98af1785c5533148b8d2813fa832aa5d0ea54d7475a3d4a4baff027131c1076af35dba3ca1136e80719084d30716e41604b0ded0c9ede9e0b34ee3e7e6f7f9')

prepare() {
    cd "${srcdir}"/${pkgname}-${pkgver}

    # Rename 'Files' app name to avoid having the same as nautilus
    sed -i '/^\[Desktop Entry/,/^\[Desktop Action/ s/^Name\(.*\)=.*/Name\1=Nemo/' data/nemo.desktop.in
}

build() {
    mkdir -p "${srcdir}"/${pkgname}-${pkgver}/build
    cd "${srcdir}"/${pkgname}-${pkgver}/build

    meson --prefix=/usr \
          --libexecdir=lib/${pkgname} \
          --buildtype=plain \
          ..
    ninja
}

package() {
    cd "${srcdir}"/${pkgname}-${pkgver}/build

    DESTDIR="${pkgdir}" ninja install
}
