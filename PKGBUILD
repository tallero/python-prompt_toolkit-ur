# Maintainer: Morten Linderud <foxboron@archlinux.org>
# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Contributor: Kyle Keen <keenerd@gmail.com>
# Contributor: Andy Weidenbaum <archbaum@gmail.com>

pkgname=python-prompt_toolkit
pkgver=3.0.46
pkgrel=1
pkgdesc='Library for building powerful interactive command lines in Python'
arch=('any')
url='https://github.com/prompt-toolkit/python-prompt-toolkit'
license=('BSD')
depends=(
  'python'
  'python-pygments'
  'python-wcwidth'
)
makedepends=(
  'git'
  'python-build'
  'python-installer'
  'python-wheel'
  'python-setuptools'
)
checkdepends=('python-pytest')
source=("$pkgname::git+$url#tag=$pkgver")
b2sums=('2afa4a80a0d1df7bee12e75c3dcef5684e32da44d4bc70975302abcd9d01c9742b9494cb0b62ba92b0808800c08cc9140cdb08305a14eeff4ac1216b936a5843')

build() {
  cd "$pkgname"

  python -m build --wheel --no-isolation
}

check() {
  cd "$pkgname"

  PYTHONPATH=build/lib pytest -v
}

package() {
  cd "$pkgname"

  python -m installer --destdir="$pkgdir" dist/*.whl

  # symlink license file
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "$pkgdir/usr/share/licenses/$pkgname"
  ln -s "$site_packages/${pkgname#python-}-$pkgver.dist-info/LICENSE" \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
