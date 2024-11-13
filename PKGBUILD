# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>
# Contributor: Patrice Peterson <runiq at archlinux dot us>
# Contributor: JonnyJD <arch@JonnyJD.net>

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
_pkg=secretstorage
_pkgname=SecretStorage
pkgname="${_py}-${_pkg}"
pkgver=3.3.3
pkgrel=5
_pkgdesc=(
  "Securely store passwords and other private"
  "data using the SecretService DBus API"
)
arch=(
  'any'
)
_http="https://github.com"
_ns="mitya57"
url="${_http}/${_ns}/${_pkg}"
license=(
  'BSD-3-Clause'
)
depends=(
  "${_py}-cryptography"
  "${_py}-jeepney"
)
makedepends=(
  "${_py}-setuptools"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
)
checkdepends=(
  'org.freedesktop.secrets'
  'xorg-server-xvfb'
)
_pypa="https://pypi.io/packages/source"
source=(
  "${_pypa}/${_pkgname:0:1}/${_pkgname}/${_pkgname}-${pkgver}.tar.gz"
)
sha512sums=(
  '9a048c8245cfb01babebdd85dbbe84f9634b9b28188f7d11d3abad841109cfa307861de05e529199e409e595864ff3e097fcc961fcff210040d214a50f932f6e'
)

build() {
  cd \
    "${_pkgname}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_pkgname}-${pkgver}"
  dbus-launch \
    xvfb-run \
    -a \
      python \
    -m \
      unittest \
    discover \
      -s \
        tests
}

package() {
  cd \
    "${_pkgname}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    "LICENSE" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}
