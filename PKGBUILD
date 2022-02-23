# Maintainer: LAHFA Samy <samy@lahfa.xyz>
pkgname=metacall-git
pkgver=0.5.7
pkgrel=1
pkgdesc='A library for providing inter-language foreign function interface calls'
arch=('x86_64')
url='https://github.com/metacall/core'
license=('Apache')
makedepends=('cmake' 'git') # Build deps
optdepends=('dotnet-sdk-bin' 'python' 'ruby' 'clang' 'jre-openjdk-headless' 'nodejs' 'typescript') # optional runtime deps
provides=('metacall')
source=(${pkgname}::git+${url})
sha256sums=('SKIP')

prepare() {
    echo "Set METACALL_LOADER_language=on in order to build metacall with support of a specific language."
    echo "See https://github.com/metacall/core/blob/develop/docs/README.md#21-loaders-backends for current available loaders."
}

build() {
    # All commented variables are still under developpement
    METACALL_LOADER_C="${METACALL_LOADER_C:=off}"
    METACALL_LOADER_CS="${METACALL_LOADER_CS:=off}"
    METACALL_LOADER_COB="${METACALL_LOADER_COB:=off}"
    METACALL_LOADER_JAVA="${METACALL_LOADER_JAVA:=off}"
    METACALL_LOADER_FILE="${METACALL_LOADER_FILE:=off}"
    METACALL_LOADER_NODE="${METACALL_LOADER_NODE:=off}"
    METACALL_LOADER_JS="${METACALL_LOADER_JS:=off}"
    METACALL_LOADER_PY="${METACALL_LOADER_PY:=off}"
    METACALL_LOADER_RB="${METACALL_LOADER_RB:=off}"
    METACALL_LOADER_TS="${METACALL_LOADER_TS:=off}"
    cmake -B build -S "${pkgname}" \
        -DCMAKE_BUILD_TYPE='Release' \
        -DCMAKE_INSTALL_PREFIX='/usr' \
        -DOPTION_BUILD_LOADERS_C=$METACALL_LOADER_C \
        -DOPTION_BUILD_LOADERS_COB=$METACALL_LOADER_COB \
        -DOPTION_BUILD_LOADERS_JAVA=$METACALL_LOADER_JAVA \
        -DOPTION_BUILD_LOADERS_NODE=$METACALL_LOADER_NODE \
        -DOPTION_BUILD_LOADERS_JS=$METACALL_LOADER_JS \
        -DOPTION_BUILD_LOADERS_PY=$METACALL_LOADER_PY \
        -DOPTION_BUILD_LOADERS_RB=$METACALL_LOADER_RB \
        -DOPTION_BUILD_LOADERS_TS=$METACALL_LOADER_TS \
        -DOPTION_BUILD_LOADERS_MOCK=off \
        -Wno-dev

    cmake --build build
}

#check() {
#    cd build
#    ctest --output-on-failure
#}

package() {
    DESTDIR="$pkgdir" cmake --install build
    echo "In order to have a specific language support, rebuild with a set ENVIRONNEMENT variable METACALL_LOADER_language=on"
    echo "See https://github.com/metacall/core/blob/develop/docs/README.md#21-loaders-backends for current available loaders."
}
