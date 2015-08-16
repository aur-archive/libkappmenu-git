pkgname=libkappmenu-git
pkgver=20120908
pkgrel=1
pkgdesc="lib for kded-appmenu module"
arch=('i686' 'x86_64')
url='https://projects.kde.org/projects/playground/base/kded-appmenu'
license=('GPL')
provides=('libkappmenu')
conflicts=('libkappmenu')
depends=('libdbusmenu-qt' 'kdelibs' 'kded-appmenu')
makedepends=('git' 'cmake' 'automoc4')

_gitroot=git://gitorious.org/libkappmenu/libkappmenu.git
_gitname=libkappmenu

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  mkdir build
  cd build
  cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=`kde4-config --prefix`
  make
}

package() {
  cd "$srcdir/$_gitname-build/build"
  make DESTDIR="$pkgdir/" install
}
