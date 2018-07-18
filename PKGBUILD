# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Patrice Peterson <runiq at archlinux dot us>
# Contributor: JonnyJD <arch@JonnyJD.net>

pkgname=python-secretstorage
pkgver=3.0.1
pkgrel=2
pkgdesc="Securely store passwords and other private data using the SecretService DBus API"
arch=('any')
url="https://pypi.org/project/SecretStorage/"
license=('BSD')
depends=('python-cryptography' 'python-jeepney')
checkdepends=('gnome-keyring' 'xorg-server-xvfb')
source=("https://pypi.io/packages/source/S/SecretStorage/SecretStorage-${pkgver}.tar.gz")
sha512sums=('830f8de1a300d4a334ce7c2fa494ac1d8f1e36a8518f3df6df2b352ac3377bcdb84293b1c809b18bc774a61188b91f31fa30c15109b7aec180a2d1f522f2a165')

build() {
  cd SecretStorage-$pkgver
  python setup.py build
}

check() {
  cd SecretStorage-$pkgver
  dbus-launch xvfb-run -a python -m unittest discover -s tests || warning "Tests failed"
}

package() {
  cd SecretStorage-$pkgver
  python setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
