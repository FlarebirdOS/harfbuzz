pkgname=(
    harfbuzz
    harfbuzz-icu
    harfbuzz-utils
)
pkgbase=harfbuzz
pkgver=11.4.1
pkgrel=1
pkgdesc="OpenType text shaping engine"
arch=('x86_64')
url="https://harfbuzz.github.io"
license=('MIT')
depends=(
    'freetype2'
    'graphite2'
    'glibc'
    'glib2'
)
makedepends=(
    'glib2-devel'
    'gobject-introspection'
    'help2man'
    'icu'
    'meson'
    'python'
)
source=(https://github.com/harfbuzz/harfbuzz/releases/download/${pkgver}/${pkgbase}-${pkgver}.tar.xz)
sha256sums=(7aafab93115eb56cdc9a931ab7d19ff60d7f2937b599d140f17236f374e32698)

build() {
    cd ${pkgbase}-${pkgver}

    local meson_args=(
        -D graphite2=enabled
        -D cpp_std=c++17
        -D chafa=disabled
    )

    CFLAGS=${CFLAGS/-fexceptions/}
    CXXFLAGS=${CXXFLAGS/-fexceptions/}

    ${meson_options} "${meson_args[@]}"

    ${meson_build}
}

package_harfbuzz() {
    cd ${pkgbase}-${pkgver}

    ${meson_install} ${pkgdir}

    _pick hb-icu ${pkgdir}/usr/lib64/libharfbuzz-icu*
    _pick hb-icu ${pkgdir}/usr/lib64/pkgconfig/harfbuzz-icu.pc
    _pick hb-icu ${pkgdir}/usr/include/harfbuzz/hb-icu.h

    _pick hb-utils ${pkgdir}/usr/bin
}

package_harfbuzz-icu() {
    pkgdesc+=" - ICU integration"
    depends=(
        'glibc'
        'harfbuzz'
        'icu'
    )

    mv hb-icu/* ${pkgdir}
}

package_harfbuzz-utils() {
    pkgdesc+=" - Utilities"
    depends=(
        'freetype2'
        'glib2'
        'glibc'
        'harfbuzz'
    )

    mv hb-utils/* ${pkgdir}
}
