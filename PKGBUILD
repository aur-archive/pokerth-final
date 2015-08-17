# $Id: PKGBUILD 74006 2012-12-27

pkgname=pokerth-final
_realname=PokerTH
pkgver=1.0
pkgrel=2
pkgdesc="Poker game written in C++/QT4"
arch=('i686' 'x86_64')
url="http://www.pokerth.net/"
license=('GPL' 'custom')
depends=('curl' 'boost-libs' 'gsasl' 'gnutls' 'protobuf'
         'qt' 'sdl_mixer' 'libircclient' 'tinyxml')
makedepends=('boost')
source=(http://downloads.sourceforge.net/sourceforge/pokerth/1.0/$_realname-$pkgver-src.tar.bz2)
md5sums=('1d8686b8968475cfc76e873a17a53efc')
#
build() {
  cd "$srcdir/$_realname-$pkgver-src"

  mv pokerth.pro pokerth-final.pro

  sed -i '1 i #include <unistd.h>' src/third_party/qtsingleapplication/qtlocalpeer.cpp

  sed -i '23 i #include <libircclient/libirc_rfcnumeric.h>' src/net/common/ircthread.cpp

  # fix g++: error: unrecognized option '-no_dead_strip_inits_and_terms'
  sed \
    -e 's/QMAKE_LFLAGS += -no_dead_strip_inits_and_terms//' \
    -i zlib_compress.pro pokerth_game.pro pokerth_server.pro

  qmake $pkgname.pro
  make
}

package() {
  cd "$srcdir/$_realname-$pkgver-src"

  make INSTALL_ROOT="$pkgdir" install

  install -D pokerth "$pkgdir/usr/bin/pokerth"
  install -D -m644 docs/pokerth.1 "$pkgdir/usr/share/man/man1/pokerth.1"
  install -D -m644 data/data-copyright.txt "$pkgdir/usr/share/licenses/pokerth/data-copyright.txt"
  rm -f "$pkgdir/usr/share/pokerth/data/data-copyright.txt"
}
