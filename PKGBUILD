# Maintainer: Gimmeapill <gimmeapill[at]gmail[dot]com>

pkgname=modulyzer-svn
pkgver=78
pkgrel=1
pkgdesc="SDL GUI for Armstrong (early alpha stage)"
url="http://batman.no/gui2/"
arch=('x86_64' 'i686')
license=('LPGL')
depends=('fbgui-svn' 'lua')
optdepends=()
makedepends=('subversion')
provides=(modulyzer)
conflicts=()
replaces=()
backup=()
install=
source=(modulyzer-launcher)
md5sums=('b374ae79637c0770ce5ec3462a387b5c')

_svntrunk="svn://anders-e.com/fbgui/trunk/modulyzer"
_svnmod="modulyzer"


build() {

  msg "Starting SVN checkout..."
  cd ${srcdir}
    if [ -d $_svnmod/.svn ]; then
      (cd $_svnmod && svn up -r $pkgver)
    else
      svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
    fi
  msg "SVN checkout done or server timeout"

  cd ${srcdir}/$_svnmod
  
  #fix the path to lua in Makefile.am
  sed -i s/lua5.2/lua/ Makefile.am
 
  autoreconf -vi
  ./configure --prefix=/usr
  make
}    

package() {
  mkdir -p /$pkgdir/usr/bin	
  mkdir -p /$pkgdir/usr/lib/modulyzer
  cp -r ${srcdir}/$_svnmod/Gear /$pkgdir/usr/lib/modulyzer
  cp ${srcdir}/$_svnmod/modulyzer /$pkgdir/usr/lib/modulyzer
  cp modulyzer-launcher /$pkgdir/usr/bin
}



