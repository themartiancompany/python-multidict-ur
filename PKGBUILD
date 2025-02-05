# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: renek <aur@spaceshore.net>

_os="$( \
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
fi
_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
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
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_libc}"
)
makedepends=(
  'cython'
  "${_py}-setuptools"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-cov"
  "${_py}-pytest"
  "${_py}-psutil"
  "${_py}-perf"
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
