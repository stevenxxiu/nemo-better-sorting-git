# Maintainer: Steven Xu <stevenxxiu@gmail.com>
# Maintainer: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Alexandre Filgueira <alexfilgueira@cinnarch.com>
# Contributor: Ner0

pkgname=nemo-git
pkgver=6.2.0.r0.gf67bfd31
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
makedepends=('git' 'meson' 'glib2-devel' 'gobject-introspection' 'intltool')
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

  # Patches
  patch --forward --strip=1 --input="${startdir}/0001-feat-sort-hidden-files-the-same-as-normal-files-so-w.patch"
  patch --forward --strip=1 --input="${startdir}/0002-feat-use-g_utf8_collate_key-instead-of-g_utf8_collat.patch"
  patch --forward --strip=1 --input="${startdir}/0003-feat-always-open-in-existing-window-for-SmartGit.patch"
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
