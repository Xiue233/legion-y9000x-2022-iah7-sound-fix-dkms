_pkgbase=legion-y9000x-2022-iah7-sound-fix
pkgname=${_pkgbase}-dkms
pkgver=0.3.0
pkgrel=1
pkgdesc="DKMS package to fix internal speakers for Legion Y9000X 2022 IAH7 (which has cs35l41 amps identified as 17AA386E)"
arch=(any)
url="https://alampy.com/2024/04/19/use-dkms-to-patch-linux-kernel-mod/"
license=('GPL2')
depends=(dkms curl libarchive)
makedepends=()

source=('dkms-patchmodule.sh'
        'dkms.conf'
        'v3-1-2-ALSA-cs35l41-obey-the-trigger-type-from-DSDT.patch::https://patchwork.kernel.org/project/alsa-devel/patch/TYCP286MB253538FE76C93C032DB55212C40E2@TYCP286MB2535.JPNP286.PROD.OUTLOOK.COM/raw/'
        'v3-2-2-ALSA-hda-realtek-Fix-internal-speakers-for-Legion-Y9000X-2022-IAH7.patch::https://patchwork.kernel.org/project/alsa-devel/patch/TYCP286MB25359B61BB685A4B3110BB44C40E2@TYCP286MB2535.JPNP286.PROD.OUTLOOK.COM/raw')
sha256sums=('SKIP'
            'SKIP'
            '880a2ead1f744dd71b64188e964164be1fd8c40122adc5f726e9e49797a0bf3f'
            'e5b237c9ad9662684586a9ed52f7938486055d334072ad79534059de43cc803f')

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
