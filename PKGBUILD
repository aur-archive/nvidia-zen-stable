# Maintainer : Muhammed Uluyol <muhammedu@gmail.com>

pkgname=nvidia-zen-stable
pkgver=185.18.36
_kernver='2.6.30-zen'
pkgrel=1
pkgdesc="NVIDIA drivers for kernel26zen."
arch=('i686' 'x86_64')
[ "$CARCH" = "i686"   ] && ARCH=x86
[ "$CARCH" = "x86_64" ] && ARCH=x86_64
url="http://www.nvidia.com/"
depends=('kernel26zen>=2.6.30' 'kernel26zen<2.6.31' 'nvidia-utils=185.18.36')
conflicts=('nvidia-96xx' 'nvidia-173xx')
license=('custom')
install=nvidia-zen-stable.install
source=("http://download.nvidia.com/XFree86/Linux-$ARCH/${pkgver}/NVIDIA-Linux-$ARCH-${pkgver}-pkg0.run")
md5sums=('cf40656600b8a587e82a801f05fa2d95')
[ "$CARCH" = "x86_64" ] && md5sums=('c9827059697001fa61518e56fdc24e93')
build() {
	cd $srcdir
	sh NVIDIA-Linux-$ARCH-${pkgver}-pkg0.run --extract-only
	cd NVIDIA-Linux-$ARCH-${pkgver}-pkg0

	cd usr/src/nv/
	ln -s Makefile.kbuild Makefile
	make SYSSRC=/lib/modules/${_kernver}/build module || return 1

	mkdir -p $pkgdir/lib/modules/${_kernver}/kernel/drivers/video/
	install -m644 nvidia.ko $pkgdir/lib/modules/${_kernver}/kernel/drivers/video/

	sed -i -e "s/KERNEL_VERSION='.*'/KERNEL_VERSION='${_kernver}'/" $startdir/nvidia-zen-stable.install
}
