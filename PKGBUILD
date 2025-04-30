# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
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
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Morten Linderud <foxboron@archlinux.org>
# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Contributor: Kyle Keen <keenerd@gmail.com>
# Contributor: Andy Weidenbaum <archbaum@gmail.com>

_pkg=prompt_toolkit
_Pkg=prompt-toolkit
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
pkgname="${_py}-${_pkg}"
pkgver=3.0.51
pkgrel=1
_pkgdesc=(
  'Library for building powerful'
  'interactive command lines in Python'
)
arch=(
  'any'
)
_http="https://github.com"
_ns="prompt-toolkit"
url="${_http}/${_ns}/${_py}-${_Pkg}"
license=('BSD')
depends=(
    "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-wcwidth"
)
makedepends=(
  'git'
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
)
optdepends=(
  "${_py}-pygments: for its color schemes and lexers"
)
provides=(
  "${_py}-${_Pkg}=${pkgver}"
)
source=(
  "${pkgname}::git+${url}#tag=${pkgver}"
)
b2sums=(
  '962da5c4f2ef5abeb592995241a270d9cd7b11dd967ab2437123975c9f88acf3048a840f308f91918a948732258bf14b02aff1e5cd9ce56d88b7823f9aa26fac'
)

build() {
  cd \
    "${pkgname}"
  "${_py}" \
    -m \
      "build" \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${pkgname}"
  "${_py}" \
    -m \
      "venv" \
    --system-site-packages \
      "test-env"
  "test-env/bin/${_py}" \
    -m \
       "installer" \
    "dist/"*".whl"
  "test-env/bin/${_py}" \
    -m \
      "pytest" \
      -v
}

package() {
  local \
    _site_packages
  _site_packages="$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")"
  cd \
    "${pkgname}"
  "${_py}" \
    -m \
      "installer" \
    --destdir="${pkgdir}" \
      "dist/"*".whl"
  # symlink license file
  install \
    -d \
      "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${_site_packages}/${_pkg}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
