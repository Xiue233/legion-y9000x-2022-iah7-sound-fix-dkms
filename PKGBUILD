_pkgbase=legion-y9000x-2022-iah7-sound-fix
pkgname=${_pkgbase}-dkms
pkgver=0.4.0
pkgrel=2
pkgdesc="DKMS package to fix internal speakers for Legion Y9000X 2022 IAH7 (which has cs35l41 amps identified as 17AA386E)"
arch=(any)
url="https://alampy.com/2024/04/19/use-dkms-to-patch-linux-kernel-mod/"
license=('GPL2')
depends=(dkms curl libarchive)
makedepends=()

source=('dkms-patchmodule.sh'
        'dkms.conf'
        'ignore_irqs_error.patch::https://github.com/torvalds/linux/commit/762eba7096e3d4d81faefffcc57074a82b53613d.patch'
        '17aa_386e_quirk.patch')
sha256sums=('SKIP'
            'SKIP'
            '9f222a486f8c2fb5068f5408268dd2bebd884415fbcbf16d6610aa99e390c8a5'
            '69681c7bbc2e692f5a040f955bf1f2d785b3c61308992c5c77b88320de22595d')

package() {
    install -Dm644 dkms.conf "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf
    sed -e "s/@_PKGBASE@/${_pkgbase}/" \
        -e "s/@PKGVER@/${pkgver}/" \
        -i "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf
    for src in "${source[@]}"; do
        src="${src%%::*}"
        src="${src##*/}"
        [[ $src = *.patch ]] || continue
        install -Dm644 "${src}" "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/${src}
    done
    install -Dm755 dkms-patchmodule.sh "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms-patchmodule.sh
}
