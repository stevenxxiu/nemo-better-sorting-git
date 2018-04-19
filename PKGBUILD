# Maintainer: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo
pkgver=3.6.5
pkgrel=1
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('x86_64')
url="https://github.com/linuxmint/${pkgname}"
license=('GPL')
depends=('cinnamon-desktop' 'dconf' 'gvfs' 'exempi' 'libexif' 'libnotify' 'libxml2' 'python' 'xapps')
optdepends=('cinnamon-translations: i18n'
            'ffmpegthumbnailer: support for video thumbnails')
makedepends=('gobject-introspection' 'gnome-common' 'gtk-doc' 'intltool')
#options=('!emptydirs')
source=("$pkgname-$pkgver.tar.gz::${url}/archive/${pkgver}.tar.gz")
sha512sums=('6a8652633c0d71e910aad1447cae1cc09de67e6325ff4c7b1515e653e354be80ec2b9889f92bbe3fa011132152729e8aacf95698c079ff00d6b8e737a9cd25f1')

prepare() {
    cd "${srcdir}"/${pkgname}-${pkgver}

    # Rename 'Files' app name to avoid having the same as nautilus
    sed -i '/^\[Desktop Entry/,/^\[Desktop Action/ s/^Name\(.*\)=.*/Name\1=Nemo/' data/nemo.desktop.in.in

    NOCONFIGURE=1 ./autogen.sh
}

build() {
    cd "${srcdir}"/${pkgname}-${pkgver}

    ./configure --prefix=/usr \
                --sysconfdir=/etc \
                --localstatedir=/var \
                --disable-static \
                --libexecdir=/usr/lib/nemo \
                --disable-update-mimedb \
                --disable-tracker \
                --disable-gtk-doc-html \
                --disable-schemas-compile \
                --disable-selinux

    #https://bugzilla.gnome.org/show_bug.cgi?id=656231
    sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool

    make
}

package() {
    cd "${srcdir}"/${pkgname}-${pkgver}

    make DESTDIR="${pkgdir}" install
}
