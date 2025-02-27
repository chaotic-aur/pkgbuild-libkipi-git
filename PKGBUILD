pkgname=libkipi-git
pkgver=r1278.4ec0a9a
pkgrel=1
pkgdesc='An interface to use kipi-plugins from a KDE application'
arch=('i686' 'x86_64')
url='http://www.kde.org'
license=('GPL' 'LGPL' 'FDL')
depends=('qt5-base' 'hicolor-icon-theme' 'kxmlgui' 'kservice-git')
makedepends=('git' 'extra-cmake-modules-git' 'kdoctools')
conflicts=('libkipi')
provides=('libkipi')
groups=('digikamsc-git')
source=("git+https://invent.kde.org/graphics/libkipi")
md5sums=('SKIP')
install=libkipi-git.install

#pkgver() {
#  cd "${srcdir}/libkipi"
#  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
#}

pkgver() {
  cd ${pkgname%-git}
  _major_ver="$(grep -m1 'set.*(.*_LIB_MAJOR_VERSION' CMakeLists.txt | cut -d '"' -f2)"
  _minor_ver="$(grep -m1 'set.*(.*_LIB_MINOR_VERSION' CMakeLists.txt | cut -d '"' -f2)"
  _patch_ver="$(grep -m1 'set.*(.*_LIB_PATCH_VERSION' CMakeLists.txt | cut -d '"' -f2)"
  echo "${_major_ver}.${_minor_ver}.${_patch_ver}_r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}

prepare() {
if [[ -d "${srcdir}/build" ]]; then
      msg "Cleaning the previous build directory..."
      rm -rf "${srcdir}/build"
  fi
  mkdir "${srcdir}/build"
}

build() {
  cd "${srcdir}/build"
  cmake "${srcdir}/libkipi" -DCMAKE_BUILD_TYPE=Release \
                -DCMAKE_INSTALL_PREFIX=/usr \
                -DLIB_INSTALL_DIR=lib \
                -DKDE_INSTALL_USE_QT_SYS_PATHS=ON \
                -DBUILD_TESTING=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}" install
}

source=("git+https://invent.kde.org/graphics/libkipi")
