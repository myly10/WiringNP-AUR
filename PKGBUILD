# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# The following guidelines are specific to BZR, GIT, HG and SVN packages.
# Other VCS sources are not natively supported by makepkg yet.

# Maintainer: Your Name <youremail@domain.com>
pkgname=WiringNP-git
pkgver=r20.0464ba6
pkgrel=1
pkgdesc=""
arch=(aarch64)
url="http://wiki.friendlyarm.com/wiki/index.php/WiringNP:_NanoPi_NEO/NEO2/Air_GPIO_Programming_with_C"
license=('unknown')
groups=()
depends=(linux-aarch64-headers)
makedepends=('git') # 'bzr', 'git', 'mercurial' or 'subversion'
provides=("${pkgname%-VCS}")
conflicts=("${pkgname%-VCS}")
replaces=()
backup=()
options=()
install=
source=('git://github.com/friendlyarm/WiringNP.git' patch-wiringPi patch-devLib patch-gpio patch-boardtype)
noextract=()
md5sums=('SKIP' SKIP SKIP SKIP SKIP)

# Please refer to the 'USING VCS SOURCES' section of the PKGBUILD man page for
# a description of each element in the source array.

pkgver() {
	cd "$srcdir/${pkgname%-git}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    cd "$srcdir/${pkgname%-git}"
    patch wiringPi/Makefile < ../patch-wiringPi
    patch devLib/Makefile < ../patch-devLib
    patch gpio/Makefile < ../patch-gpio
    patch wiringPi/boardtype_friendlyelec.c < ../patch-boardtype
}

build() {
	cd "$srcdir/${pkgname%-git}"
    mkdir -p $srcdir/installcache/usr/local/bin
    mkdir -p $srcdir/installcache/usr/local/lib
    mkdir -p $srcdir/installcache/usr/local/include

    echo Building wiringPi
    cd wiringPi
    make -j$(nproc --all)
    make DESTDIR="../../installcache/usr" install

    echo Building devLib
    cd ../devLib
    make DESTDIR="../../installcache/usr" -j$(nproc --all)
    make DESTDIR="../../installcache/usr" install

    echo Building gpio
    cd ../gpio
    make DESTDIR="../../installcache/usr" -j$(nproc --all)
    make DESTDIR="../../installcache/usr" install
}

#check() {
#}

package() {
	cd "$srcdir/${pkgname%-git}"
    cp -r ../installcache/* $pkgdir
}
