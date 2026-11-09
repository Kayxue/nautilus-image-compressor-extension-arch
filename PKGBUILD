# Maintainer: Kay <s0990006@gmail.com>

pkgname=nautilus-image-compressor-extension
pkgver=0.1.0
pkgrel=1
pkgdesc="Modern Nautilus 43+ context menu extension to compress images"
arch=('x86_64' 'aarch64')
url="https://github.com/Kayxue/nautilus-image-compressor-extension"
license=('MIT')
depends=(
  'gcc-libs'
  'glib2'
  'glibc'
  'libnautilus-extension'
  'nautilus'
)
makedepends=(
  'cargo'
  'git'
  'pkgconf'
)
optdepends=(
  'nautilus-image-compressor: companion CLI/GUI application to perform image compression'
)
install="$pkgname.install"
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('SKIP')

prepare() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  CFLAGS+=" -ffat-lto-objects"
  cargo build --frozen --release
}

check() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 "target/release/libnautilus_image_compressor_extension.so" \
    "$pkgdir/usr/lib/nautilus/extensions-4/libnautilus_image_compressor_extension.so"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
