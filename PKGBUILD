# Maintainer: tinywrkb <tinywrkb@gmail.com>
# Contributor: Morten Linderud <foxboron@archlinux.org>
# Contributor: Maxim Baz <rofi at maximbaz dot com>
# Contributor: Anatol Pomozov
# Contributor: Benjamin Chrétien <chretien + aur [at] lirmm [dot] fr>
# Contributor: Eric Engestrom <aur [at] engestrom [dot] ch>
# Contributor: Rasi <rasi@xssn.at>
# Contributor: Sean Pringle <sean.pringle@gmail.com>
# Contributor: SanskritFritz (gmail)
# Contributor: Jonas Strassel <info@jonas-strassel.de>

pkgname=rofi-wayland
pkgver=1.7.0
_gitname=rofi
pkgrel=1
pkgdesc='A window switcher, application launcher and dmenu replacement (Wayland fork)'
arch=(x86_64 aarch64)
url='https://github.com/lbonn/rofi'
license=(MIT)
depends=(libxdg-basedir startup-notification libxkbcommon-x11 xcb-util-cursor xcb-util-wm
         xcb-util-xrm librsvg wayland)
makedepends=(check git meson wayland-protocols)
provides=(rofi)
conflicts=("rofi" "rofi-lbonn-wayland-git")
source=("${_gitname}::git+${url}.git#tag=$pkgver-wayland")
sha256sums=('SKIP')
prepare() {
  cd rofi
  git submodule update --init
}

build() {
  local meson_options=(
    -D wayland=enabled
    -D check=enabled
  )
  arch-meson rofi build "${meson_options[@]}"
  meson compile -C build
}

package() {
  meson install -C build --destdir="$pkgdir"

  cd rofi
  install -Dm644 -t "$pkgdir"/usr/share/licenses/$pkgname/ COPYING
  install -Dm755 -t "$pkgdir"/usr/share/doc/rofi/examples/ Examples/*.sh
}
