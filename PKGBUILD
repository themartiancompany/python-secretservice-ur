# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Patrice Peterson <runiq at archlinux dot us>
# Contributor: JonnyJD <arch@JonnyJD.net>

pkgbase=python-secretstorage
pkgname=(python-secretstorage python2-secretstorage)
pkgver=2.3.1
pkgrel=1
pkgdesc="Securely store passwords and other private data using the SecretService DBus API"
arch=('any')
url="https://pypi.python.org/pypi/SecretStorage"
license=('BSD')
makedepends=('python-dbus' 'python2-dbus' 'python-crypto' 'python2-crypto' 'dbus-glib'
             'python-cryptography' 'python2-cryptography')
checkdepends=('gnome-keyring' 'xorg-server-xvfb' 'dbus-glib')
source=("https://pypi.io/packages/source/S/SecretStorage/SecretStorage-${pkgver}.tar.gz")
md5sums=('3b9465831b069e2622973afb7deb7bc2')

prepare() {
  cp -a SecretStorage-$pkgver{,-py2}
}

check() {
  cd SecretStorage-$pkgver
  dbus-launch xvfb-run -a python -m unittest discover -s tests || warning "Tests failed"

  cd ../SecretStorage-$pkgver-py2
  dbus-launch xvfb-run -a python2 -m unittest discover -s tests || warning "Tests failed"
}

package_python-secretstorage() {
  depends=('python-dbus' 'python-crypto' 'dbus-glib' 'python-cryptography')

  cd SecretStorage-$pkgver
  python setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_python2-secretstorage() {
  depends=('python2-dbus' 'python2-crypto' 'dbus-glib' 'python2-cryptography')

  cd SecretStorage-$pkgver-py2
  python2 setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
