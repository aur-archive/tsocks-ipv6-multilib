# Maintainer: maz-1 <loveayawaka at gmail dot com>
pkgname=tsocks-ipv6-multilib
pkgver=1.8beta6
GIT_COMMIT=be36c83a7326c75123fa019a4cb53792ecd8f689
pkgrel=1
pkgdesc='Transparent SOCKS proxying library, with IPv6 support.This is the multilib version for x86_64.'
url='https://github.com/Elysion-tcfa/tsocks'
license=('GPL')
arch=('x86_64')
makedepends=('gcc-multilib')
source=("https://github.com/Elysion-tcfa/tsocks/archive/${GIT_COMMIT}.tar.gz"
  "fix-mkinstalldirs.patch")
md5sums=('170e2115c29544b9ffd553dd78f63d6b'
         'b85f664abe7e6afdb908c94fbfd17602')
conflicts=("tsocks" "tsocks-ipv6")
provides=("tsocks" "tsocks-ipv6")


build() {
	cp -a "${srcdir}/tsocks-${GIT_COMMIT}" ${srcdir}/tsocks-32
	cp -a "${srcdir}/tsocks-${GIT_COMMIT}" ${srcdir}/tsocks-64
	
	cd "${srcdir}/tsocks-64"
	export CPPFLAGS=
        patch -p1 < ../fix-mkinstalldirs.patch
	./configure --prefix=/usr --sysconfdir=/etc --mandir=/usr/share/man --libdir=/usr/lib
	make
	
	cd "${srcdir}/tsocks-32"
	export CPPFLAGS=
        patch -p1 < ../fix-mkinstalldirs.patch
	CC='gcc -m32' ./configure --prefix=/usr --sysconfdir=/etc --mandir=/usr/share/man --libdir=/usr/lib32
	make
}

package() {
	cd "${srcdir}/tsocks-64"
	make DESTDIR="${pkgdir}" install
	
	cd "${srcdir}/tsocks-32"
	make DESTDIR="${pkgdir}" install
	
	
	install -d "${pkgdir}/usr/share/${pkgname}"
	install -m644 tsocks.conf.{simple,complex}.example "${pkgdir}/usr/share/${pkgname}"
}
