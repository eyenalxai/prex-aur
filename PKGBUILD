# Maintainer: roehistat <mail at iyxeyl.me>

pkgname=prex
pkgver=0.5.3
pkgrel=1
pkgdesc="Run Windows executables in a running game's Proton prefix"
arch=('x86_64')
url="https://github.com/eyenalxai/${pkgname}"
license=('GPL3')
depends=('gcc-libs' 'sqlite')
makedepends=('cargo')
options=('!debug' 'strip')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('81d36af1e13773e6ae592c9b9e2bfa687ea92cc4b93e0114c5109220baff5c8a')

prepare() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --locked --target host-tuple
}

build() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  cargo build --frozen --release --all-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm0755 -t "$pkgdir/usr/bin/" "target/release/$pkgname"
  install -Dm0644 -t "$pkgdir/usr/share/applications/" "$pkgname.desktop"
  install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE
}
