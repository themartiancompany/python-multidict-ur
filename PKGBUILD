# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: renek <aur@spaceshore.net>

_py="python"
_pkg=multidict
pkgname="${_py}-${_pkg}"
pkgver=6.0.5
pkgrel=2
pkgdesc='Asyncio-based multidict implementation for Python'
_http="https://github.com"
_ns="aio-libs"
url="${_http}/${_ns}/${_pkg}"
arch=(
  'x86_64'
  'arm'
  'i686'
  'mips'
  'armv7l'
  'aarch64'
  'pentium4'
  'powerpc'
)
license=(
  'Apache-2.0'
)
depends=(
  "${_py}"
  'glibc'
)
makedepends=(
  'cython'
  "${_py}-setuptools"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
)
checkdepends=(
  'python-pytest'
  'python-pytest-cov'
  'python-pytest'
  'python-psutil'
  'python-perf'
)
source=(
  "${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha512sums=(
  '500d3b2a139d40442462a2b49f9dd0c01631643ef9905367d8b7c472a1030437c26a042a28e11ba94058a17821628d96f19ec6ca479d5831e2f1263ff0069871'
)
b2sums=(
  '668b5db8174c0dbc6651eae281f777d5c1dfb59a4f4d9d5301355148bf40063e33e26844d2f8ff543ebe7b9c91cf7fffb4abd57ca6786684757f50af27b7df56'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m venv \
    --system-site-packages \
    test-env
  test-env/bin/"${_py}" \
    -m \
      installer \
    dist/*.whl
  cd tests
  ../test-env/bin/"${_py}" \
    -m \
      pytest \
    -v
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
}

# vim: ts=2 sw=2 et:
