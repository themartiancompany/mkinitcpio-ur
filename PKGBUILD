# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Maintainer: Morten Linderud <foxboron@archlinux.org>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=41
pkgrel=1
pkgdesc="Modular initramfs image creation utility"
arch=('any')
url='https://gitlab.archlinux.org/archlinux/mkinitcpio/mkinitcpio'
license=('GPL-2.0-only')
depends=('awk' 'mkinitcpio-busybox' 'kmod' 'util-linux' 'libarchive' 'coreutils'
         'bash' 'binutils' 'diffutils' 'findutils' 'grep' 'gzip' 'filesystem' 'zstd' 'systemd')
checkdepends=('bats' 'bats-assert' 'lzop')
makedepends=('meson')
optdepends=('xz: Use lzma or xz compression for the initramfs image'
            'bzip2: Use bzip2 compression for the initramfs image'
            'lzop: Use lzo compression for the initramfs image'
            'lz4: Use lz4 compression for the initramfs image'
            'mkinitcpio-nfs-utils: Support for root filesystem on NFS'
            'systemd-ukify: alternative UKI generator')
provides=('initramfs')
backup=('etc/mkinitcpio.conf')
source=("https://sources.archlinux.org/other/$pkgname/$pkgname-$pkgver.tar.xz"{,.sig})
sha512sums=('bb0955214d037e645c2cae34423a31a1baae5d9864bce56a4477dfe5a38151057f643dc34ec51de0ed9f420ec922f974a6cbec18f9d5c65813ca1e5896362776'
            'SKIP')
b2sums=('39d95a41b0da67e4d7e376083cc21a3c2b91ff262bd7096956457b2d0baee4e61342e022eb5ab05fb8ab189ef57d92c2a8e1f34a4b11deda4c1385e6cd553fa2'
        'SKIP')
validpgpkeys=('ECCAC84C1BA08A6CC8E63FBBF22FB1D78A77AEAB'    # Giancarlo Razzolini
              'C100346676634E80C940FB9E9C02FF419FECBE16')   # Morten Linderud

build(){
  cd $pkgname-$pkgver
  arch-meson \
    -Dsystemd_hooks=true \
    ../build
  meson compile -C ../build
}

check() {
  cd $pkgname-$pkgver
  meson test -C ../build
}

package() {
  cd $pkgname-$pkgver
  DESTDIR="$pkgdir" meson install -C ../build
}
