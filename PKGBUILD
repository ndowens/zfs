pkgname=zfs-dkms
pkgdesc="Kernel modules for the Zettabyte File System."
pkgver=0.8.3
pkgrel=2.1
makedepends=(git)
arch=("x86_64")
url="https://zfsonlinux.org/"
source=("git+https://github.com/ndowens/zfs-1.git#tag=5a42ef04fd390dc96fbbf31bc9f3d05695998211"
        "linux-5.5-compat-blkg_tryget.patch")
sha256sums=('SKIP'
            'daae58460243c45c2c7505b1d88dcb299ea7d92bcf3f41d2d30bc213000bb1da')
license=("CDDL")
depends=("lsb-release" "dkms")
provides=("zfs" "zfs-headers" "spl" "spl-headers")
conflicts=("zfs" "zfs-headers" "spl" "spl-headers")

prepare() {
    cd "$srcdir"/zfs-1
    ./autogen.sh
}

build() {
    cd "$srcdir"/zfs-1

    ./scripts/dkms.mkconf -n ${pkgname%-dkms} -v ${pkgver} -f dkms.conf
}

package() {
    depends=("zfs-utils=${pkgver}" 'dkms')

    cd "$srcdir"/zfs-1
    dkmsdir="${pkgdir}/usr/src/${pkgname%-dkms}-${pkgver}"
    install -d "${dkmsdir}"/{config,scripts,cmd,contrib,etc,lib,man,rpm,tests,udev}
    cp -a configure dkms.conf Makefile.in META ${pkgname%-dkms}_config.h.in ${pkgname%-dkms}.release.in include/ module/ "${dkmsdir}"/
    cp config/config.* config/missing config/*sh "${dkmsdir}"/config/
    cp -r cmd/* "$dkmsdir"/cmd
    cp -r contrib/* "$dkmsdir"/contrib
    cp -r etc/* "$dkmsdir"/etc
    cp -r lib/* "$dkmsdir"/lib
    cp -r udev/* "$dkmsdir"/udev
    cp -r man/* "$dkmsdir"/man
    cp -r rpm/* "$dkmsdir"/rpm
    cp -r tests/* "$dkmsdir"/tests
    cp -r scripts/* "$dkmsdir"/scripts
}
