# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>
# Contributor: Patrice Peterson <runiq at archlinux dot us>
# Contributor: JonnyJD <arch@JonnyJD.net>

pkgbase=python-secretstorage
_pkgname=SecretStorage
pkgname=(python-secretstorage python2-secretstorage)
pkgver=3.0.1
pkgrel=4
pkgdesc="Securely store passwords and other private data using the SecretService DBus API"
arch=('any')
url="https://github.com/mitya57/secretstorage"
license=('BSD')
makedepends=('python-setuptools' 'python2-setuptools')
checkdepends=('gnome-keyring' 'xorg-server-xvfb' 'python-cryptography' 'python-jeepney' 'python2-cryptography')
source=("https://pypi.io/packages/source/${_pkgname:0:1}/$_pkgname/$_pkgname-$pkgver.tar.gz")
sha512sums=('830f8de1a300d4a334ce7c2fa494ac1d8f1e36a8518f3df6df2b352ac3377bcdb84293b1c809b18bc774a61188b91f31fa30c15109b7aec180a2d1f522f2a165')

prepare() {
  cp -a $_pkgname-$pkgver{,-py2}
}

build() {
  echo "Building python-secretstorage $pkgver"
  cd "$srcdir"/$_pkgname-$pkgver
  python setup.py build

  echo "Building python2-secretstorage $pkgver"
  cd "$srcdir"/$_pkgname-$pkgver-py2
  python2 setup.py build
}

check() {
  echo "Running tests on python-secretstorage $pkgver"
  cd "$srcdir"/$_pkgname-$pkgver
  dbus-launch xvfb-run -a python -m unittest discover -s tests || warning "Tests failed on python-secretstorage $pkgver"

  echo "Running tests on python2-secretstorage $pkgver"
  cd "$srcdir"/$_pkgname-$pkgver-py2
  dbus-launch xvfb-run -a python2 -m unittest discover -s tests || warning "Tests failed on python2-secretstorage $pkgver"
}

package_python-secretstorage() {
  depends=('python-cryptography' 'python-jeepney')
  cd $_pkgname-$pkgver

  python setup.py install --root="$pkgdir" --optimize=1 --skip-build
  install -Dm 644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-secretstorage() {
  depends=('python2-cryptography')
  cd $_pkgname-$pkgver-py2

  python2 setup.py install --root="$pkgdir" --optimize=1 --skip-build
  install -Dm 644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
