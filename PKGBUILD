# Maintainer: Leif Warner <abimelech@gmail.com>
_hkgname=swish
pkgname=haskell-swish
pkgver=0.9.0.12
pkgrel=1
pkgdesc="A semantic web toolkit."
url="http://hackage.haskell.org/package/${_hkgname}"
license=('LGPL')
arch=('i686' 'x86_64')
depends=('haskell-containers' 'haskell-directory' 'haskell-filepath' 'haskell-hashable<1.3' 'haskell-intern' 'haskell-mtl' 'haskell-network' 'haskell-old-locale' 'haskell-polyparse<=2.0' 'haskell-semigroups<0.13' 'haskell-text' 'haskell-time')
options=('staticlibs')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
md5sums=('2cc41c2d3bfb8f5f9d19ac01535b3ffd')
install=${pkgname}.install
build() {
    cd ${_hkgname}-${pkgver}
    runhaskell Setup configure -O ${PKGBUILD_HASKELL_ENABLE_PROFILING:+-p } --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
}
