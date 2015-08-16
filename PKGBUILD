# Maintainer: Andrea Scarpino <andrea@archlinux.org>

pkgname=kde-runtime-git
pkgver=r20723.23598aa
pkgrel=1
pkgdesc='Plugins and applications necessary for the running of KDE applications'
arch=('i686' 'x86_64')
url='https://projects.kde.org/projects/kde/kde-runtime'
license=('LGPL')
depends=('khtml-git' 'kross-git' 'kcmutils-git' 'kdelibs4support-git' 'kemoticons-git' 'kdesu-git' 'plasma-framework-git' 'threadweaver-git' 'knewstuff-git' 'knotifyconfig-git' 'kinit-git' 'kidletime-git' 'kitemmodels-git' 'kdnssd-git')
makedepends=('extra-cmake-modules-git' 'git' 'networkmanager' 'kdoctools-git')
provides=('kde-runtime')
conflicts=('kde-runtime')
source=('git://anongit.kde.org/kde-runtime.git#branch=frameworks')
md5sums=('SKIP')

pkgver() {
  cd kde-runtime
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  mkdir -p build

  # fix conflicts
  sed -i 's|add_subdirectory(kcontrol)|#add_subdirectory(kcontrol)|' kde-runtime/CMakeLists.txt
  sed -i 's|add_subdirectory(solid-networkstatus)|#add_subdirectory(solid-networkstatus)|' kde-runtime/CMakeLists.txt
  sed -i 's|add_subdirectory(knewstuff)|#add_subdirectory(knewstuff)|' kde-runtime/CMakeLists.txt

}

build() {
  cd build
  export XDG_DATA_DIRS="/opt/kf5/share:$XDG_DATA_DIRS"
  cmake ../kde-runtime \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/opt/kf5 \
    -DLIB_INSTALL_DIR=lib \
    -DBUILD_TESTING=OFF
#    -DSYSCONF_INSTALL_DIR=/etc
  make
}

package() {
  cd build
  make DESTDIR="${pkgdir}" install
}
