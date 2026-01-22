pkgname=prex
pkgver=0.5.2
pkgrel=1
pkgdesc="Run Windows executables in a running game's Proton context"
arch=('x86_64')
url="https://github.com/eyenalxai/${pkgname}"
license=('MIT')
depends=('gcc-libs' 'sqlite')
makedepends=('cargo')
options=('!debug' 'strip')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('d13bd660a0db2aeda08e2191760d36bf27d5ee9b3722c7d7af79705f46406b74')

prepare() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
}
