# Maintainer: OBeard-Wan Cannoli
pkgname=claude-status
pkgver=1.0.0
pkgrel=1
pkgdesc="System tray app showing live Claude/Anthropic service status as a scrolling history bar"
arch=('any')
url="https://github.com/OBeardWan/claude-status"
license=('MIT')
depends=('python' 'python-gobject' 'gtk3' 'libayatana-appindicator' 'python-cairo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('SKIP')

package() {
  cd "$pkgname-$pkgver"

  install -Dm755 "bin/claude-status" "$pkgdir/usr/bin/claude-status"
  install -Dm644 "data/claude-status.desktop" "$pkgdir/usr/share/applications/claude-status.desktop"
  install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  for size in 16 22 24 32 48 64 128 256; do
    install -Dm644 "data/icons/claude-status-${size}.png" \
      "$pkgdir/usr/share/icons/hicolor/${size}x${size}/apps/claude-status.png"
  done
}
