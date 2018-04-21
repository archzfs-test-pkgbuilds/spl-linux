# Maintainer: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
# ! WARNING !
#
# The archzfs packages are kernel modules, so these PKGBUILDS will only work with the kernel package they target. In this
# case, the archzfs-linux packages will only work with the default linux package! To have a single PKGBUILD target many
# kernels would make for a cluttered PKGBUILD!
#
# If you have a custom kernel, you will need to change things in the PKGBUILDS. If you would like to have AUR or archzfs repo
# packages for your favorite kernel package built using the archzfs build tools, submit a request in the Issue tracker on the
# archzfs github page.
#
pkgbase="spl-linux"
pkgname=("spl-linux" "spl-linux-headers")

pkgver=0.7.8.4.16.3.1
pkgrel=1
makedepends=("linux-headers=4.16.3-1" "libelf" "git")
arch=("x86_64")
url="http://zfsonlinux.org/"
source=("https://github.com/zfsonlinux/zfs/releases/download/zfs-0.7.8/spl-0.7.8.tar.gz")
sha256sums=("f6c9fe37d149da7fec34ee3bf32302a16b4cfcd84b8c6aa3d764ceb816587636")
license=("GPL")
depends=("spl-utils-common=0.7.8" "kmod" "linux=4.16.3-1")

build() {
    cd "${srcdir}/spl-0.7.8"
    ./autogen.sh
    ./configure --prefix=/usr --libdir=/usr/lib --sbindir=/usr/bin \
                --with-linux=/usr/lib/modules/4.16.3-1-ARCH/build \
                --with-linux-obj=/usr/lib/modules/4.16.3-1-ARCH/build \
                --with-config=kernel
    make
}

package_spl-linux() {
    pkgdesc="Solaris Porting Layer kernel modules."
    install=spl.install
    provides=("spl")
    groups=("archzfs-linux")
    conflicts=('spl-linux-git')
    replaces=("spl-git")
    cd "${srcdir}/spl-0.7.8"
    make DESTDIR="${pkgdir}" install
    mv "${pkgdir}/lib" "${pkgdir}/usr/"
    # Remove src dir
    rm -r "${pkgdir}"/usr/src
}

package_spl-linux-headers() {
    pkgdesc="Solaris Porting Layer kernel headers."
    conflicts=('spl-archiso-linux-headers' 'spl-archiso-linux-git-headers' 'spl-linux-hardened-headers' 'spl-linux-hardened-git-headers' 'spl-linux-lts-headers' 'spl-linux-lts-git-headers'  'spl-linux-git-headers' 'spl-linux-vfio-headers' 'spl-linux-vfio-git-headers' 'spl-linux-zen-headers' 'spl-linux-zen-git-headers' )
    cd "${srcdir}/spl-0.7.8"
    make DESTDIR="${pkgdir}" install
    rm -r "${pkgdir}/lib"
    # Remove reference to ${srcdir}
    sed -i "s+${srcdir}++" ${pkgdir}/usr/src/spl-*/4.16.3-1-ARCH/Module.symvers
}
