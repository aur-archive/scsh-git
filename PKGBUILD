# Maintainer: Jérémy Autran <jeremy.autran@gmail.com>
pkgname=scsh-git
_gitname=scsh
pkgver=240.768ef5e
pkgrel=1
pkgdesc="Scsh is a unix shell embedded in Scheme"
arch=('i686' 'x86_64')
url="http://www.scsh.net/"
license=('BSD')
depends=('glibc' 'scheme48>=1.9')
source=('git+git://github.com/scheme/scsh.git')
md5sums=('SKIP')

pkgver() {
    cd $_gitname
    echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

build() {
    cd "$srcdir/$_gitname"
    git submodule update --init
    autoreconf
    ./configure --prefix=/usr
    make
}

package() {
    cd "$srcdir/$_gitname"
    sed -i 's,"$(LIB)/","$(DESTDIR)$(LIB)/",g' Makefile
    sed -i 's,$(DESTDIR)$$dir,$(DESTDIR)/$$dir,g' Makefile
    sed -i 's,install -c,install -D,g' Makefile
    make DESTDIR="$pkgdir" install
}
