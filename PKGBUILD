# Maintainer: xiretza <xiretza+aur@xiretza.xyz>
# Contributor: Harry Beadle <harrybeadle@protonmail.com>

_pkgname=vtr-verilog-to-routing
_commit=c012f19d3b892e5680a73311f4645b4236044850
pkgname=vtr-git
pkgver=8.1.0.dev.c012f19d3
pkgrel=1
pkgdesc='Open Source CAD Flow for FPGA Research'
arch=(x86_64)
url='https://verilogtorouting.org'
license=(custom)
makedepends=('git' 'cmake')
depends=('gcc-libs')
provides=("${pkgname%%-git}=$pkgver")
conflicts=("${pkgname%%-git}")
source=("git+https://github.com/verilog-to-routing/vtr-verilog-to-routing.git#commit=${_commit}"
        "0001-tbb_and_cstdint.patch")
sha256sums=('3b087d52b3eca230b755ddc48f5f1483d4839b8c9e46dbf291f270a9bdf510fd'
            '29f3d0e9573e28cfa9609e6f107da67f8f163fd098832f17cd6c2d6b99b8af7e')

#pkgver() {
#	cd "$_pkgname"
#
#	git describe | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
#}

prepare() {
	cd "${srcdir}/${_pkgname}"
    patch -Np1 -i "${srcdir}/0001-tbb_and_cstdint.patch"
}

build() {
	cmake -B build -S "$_pkgname" \
		-DCMAKE_BUILD_TYPE=None \
		-DCMAKE_INSTALL_PREFIX=/usr
	make -C build
}

check() {
	make -C build test || warning "Test(s) Failed"
}

package() {
	make -C build DESTDIR="$pkgdir" install

	install -Dm 644 "$_pkgname/LICENSE.md" "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}

