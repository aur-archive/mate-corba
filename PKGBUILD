# Maintainer: Perberos <perberos@gmail.com>
pkgname=mate-corba
pkgver=20130101
pkgrel=1
pkgdesc="Thin/fast CORBA ORB"
url="https://github.com/mate-desktop/mate-corba"
arch=('i686' 'x86_64')
license=('LGPL' 'GPL')
depends=('libidl2>=0.8.11')
makedepends=('git' 'pkgconfig' 'mate-common' 'gtk-doc')
options=('!emptydirs' '!libtool')
groups=('mate')
source=()
sha256sums=()

_gitroot=git://github.com/mate-desktop/mate-corba.git
_gitname=mate-corba

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

  ./autogen.sh \
    --prefix=/usr \
    --disable-static || return 1
  make || return 1
}

package() {
  cd "$srcdir/$_gitname-build"
  
  make DESTDIR="${pkgdir}" install || return 1
}
