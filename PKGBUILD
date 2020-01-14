# Maintainer: Steven Xu <stevenxxiu@gmail.com>
# Maintainer: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo-git-better-sorting
pkgver=4.4.2.r3.g18ed0292
pkgrel=1
pkgdesc="Cinnamon file manager (Nautilus fork)"
arch=('x86_64')
url="https://github.com/linuxmint/nemo"
_branch='master'
license=('GPL')
depends=('cinnamon-desktop' 'dconf' 'gvfs' 'exempi' 'libexif' 'libnotify' 'libxml2'
         'python' 'xapps')
optdepends=('cinnamon-translations: i18n'
            'ffmpegthumbnailer: support for video thumbnails')
makedepends=('git' 'meson' 'gobject-introspection' 'intltool')
conflicts=('nemo')
provides=('nemo')
source=("git+$url.git")
sha512sums=('SKIP')

pkgver() {
  cd nemo
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd nemo

  # Rename 'Files' app name to avoid having the same as nautilus
  sed -i '/^\[Desktop Entry/,/^\[Desktop Action/ s/^Name\(.*\)=.*/Name\1=Nemo/' data/nemo.desktop.in

  # Patch to not sort hidden files specially, and to be the same as normal files
  patch --forward --strip=1 --input="${srcdir}/../0001-nemo-file.c-sort-hidden-files-the-same-as-normal-fil.patch"
}

build() {
  mkdir -p "${srcdir}"/nemo/build
  cd "${srcdir}"/nemo/build

  meson --prefix=/usr \
        --libexecdir=lib/${pkgname} \
        --buildtype=plain \
        ..
  ninja
}

package() {
  cd "${srcdir}"/nemo/build

  DESTDIR="${pkgdir}" ninja install
}
