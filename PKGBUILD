# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>
# Contributor: Patrice Peterson <runiq at archlinux dot us>
# Contributor: JonnyJD <arch@JonnyJD.net>

pkgname=python-secretstorage
_pkgname=SecretStorage
pkgver=3.1.0
pkgrel=1
pkgdesc="Securely store passwords and other private data using the SecretService DBus API"
arch=('any')
url="https://github.com/mitya57/secretstorage"
license=('BSD')
depends=('python-cryptography' 'python-jeepney')
checkdepends=('gnome-keyring' 'xorg-server-xvfb')
source=("https://pypi.io/packages/source/${_pkgname:0:1}/$_pkgname/$_pkgname-$pkgver.tar.gz")
sha512sums=('a044009480b359aecb0c8782f04e4d02c3c1c0e682f72733896c98f386562c43766318963452d60028d0a92d02903130278cf26a5c206f5f0909e106bdb2d133')

build() {
  cd $_pkgname-$pkgver

  python setup.py build
}

check() {
  cd $_pkgname-$pkgver

  dbus-launch xvfb-run -a python -m unittest discover -s tests || warning "Tests failed"
}

package() {
  cd $_pkgname-$pkgver

  python setup.py install --root="$pkgdir" -O1
  install -Dm 644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
