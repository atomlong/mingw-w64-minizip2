pkgname=mingw-w64-minizip2
pkgver=2.9.2
pkgrel=1
pkgdesc='ZIP file extraction library (mingw-w64)'
url='https://github.com/nmoinvaz/minizip'
license=('ZLIB' 'custom')
arch=('any')
makedepends=('mingw-w64-cmake')
options=('!buildflags' 'staticlibs' '!strip')
conflicts=('mingw-w64-minizip')
depends=('mingw-w64-zlib')
source=(minizip-ng-${pkgver}.tar.gz::"https://github.com/nmoinvaz/minizip/archive/${pkgver}.tar.gz")
sha256sums=('e0f715273dbf4d40bf2ee2ec122778a30adde52a2d27ca93fa84e219ec555d07')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  cd minizip-ng-${pkgver}
  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
    ${_arch}-cmake ..
    make
    popd
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "$srcdir/minizip-ng-${pkgver}/build-${_arch}"
    make install DESTDIR="$pkgdir"
    ${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
    ${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a
  done
}
