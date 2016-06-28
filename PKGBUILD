# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Patrice Peterson <runiq at archlinux dot us>
# Contributor: JonnyJD <arch@JonnyJD.net>

pkgbase=python-secretstorage
pkgname=(python-secretstorage python2-secretstorage)
pkgver=2.2.1
pkgrel=1
pkgdesc="Securely store passwords and other private data using the SecretService DBus API"
arch=('any')
url="https://pypi.python.org/pypi/SecretStorage"
license=('BSD')
makedepends=('python-dbus' 'python2-dbus' 'python-crypto' 'python2-crypto' 'dbus-glib')
checkdepends=('gnome-keyring' 'xorg-server-xvfb' 'dbus-glib')
source=("https://pypi.io/packages/source/S/SecretStorage/SecretStorage-${pkgver}.tar.gz")
md5sums=('9a6f9e4c9962e6cd616624c331fce1ab')

prepare() {
  cp -a SecretStorage-$pkgver{,-py2}
}

check() {
  cd SecretStorage-$pkgver
  xvfb-run -a python -m unittest discover -s tests || warning "Tests failed"

  cd ../SecretStorage-$pkgver-py2
  xvfb-run -a python2 -m unittest discover -s tests || warning "Tests failed"
}

package_python-secretstorage() {
  depends=('python-dbus' 'python-crypto' 'dbus-glib')

  cd SecretStorage-$pkgver
  python setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_python2-secretstorage() {
  depends=('python2-dbus' 'python2-crypto' 'dbus-glib')

  cd SecretStorage-$pkgver-py2
  python2 setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
