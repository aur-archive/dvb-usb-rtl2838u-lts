# Maintainer: Sarkasper <echo a2FzcGVyLm1lbnRlbkBnbXguY29tCg== | base64 -d>
# Based on dvb-usb-rtl2832u-stv20, Jesus Lazaro Plaza <jesuslazaro84 at gmail.com>
# Based on dvb-usb-rtl2838u-arch, Peter Ivanov <ivanovp at gmail.com>

pkgname=dvb-usb-rtl2838u-lts
_kernelname="-lts"
_kversion="3.0.24"
pkgver=1.1_${_kversion}
pkgrel=1
pkgdesc="Linux-lts kernel module for the RTL2832U, RTL2836U and RTL2838U DVB-T USB2.0 devices"
arch=('any')
url="http://dev.ivanov.eu/projects/rtl2838/"
license=('GPL')
depends=("linux-lts")
makedepends=("linux-lts-headers")
conflicts=('dvb-usb-rtl2838u-arch' 'dvb-usb-rtl2832u-arch' 'rtl2832u-git' 'dvb-usb-rtl2832u-stv20')
install="${pkgname}.install"
source=("dvb-usb-rtl2838u.tar.gz::http://dev.ivanov.eu/projects/rtl2838/dvb-usb-rtl2838u.tar.gz")
md5sums=('f767d22de33e4eb3de0effff7bba7bd7')
sha256sums=('2bd8bea9cda586ee5dcb2d48c4a1b3eeae7f6ce71166bcff5a74af835951e17e')

build() {
  local _KERNEL="${_kversion}-${pkgrel}${_kernelname}"
  # set KERNEL_VERSION
  sed -e "s#KERNEL_VERSION=.*#KERNEL_VERSION=${_KERNEL}#g" -i "${startdir}/${install}"

  cd ${srcdir}/dvb-usb-rtl2832u

  export KBUILD_SRC="/usr/src/linux-${_KERNEL}"
  export INSTALL_MOD_PATH="${pkgdir}"
  export INSTALL_MOD_DIR=kernel/drivers/media/dvb/dvb-usb
  make -C "${KBUILD_SRC}" M="$PWD" modules
  make -C "${KBUILD_SRC}" M="$PWD" modules_install
}

package() {
   make -C "${KBUILD_SRC}" M="${srcdir}/dvb-usb-rtl2832u" modules_install
} 
