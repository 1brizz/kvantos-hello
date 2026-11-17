# Maintainer: KvantOS Project
pkgname=kvantos-hello
pkgver=1.0.0
pkgrel=2
pkgdesc="Welcome screen for KvantOS (fork of cachyos-welcome)"
arch=('x86_64')
url="https://github.com/KvantOS/kvantos-hello"
license=('GPL-3.0-or-later')
depends=('gtk3' 'glib2' 'gdk-pixbuf2' 'pacman' 'hicolor-icon-theme')
makedepends=('meson' 'ninja' 'cargo' 'python')
source=("${pkgname}-${pkgver}.tar.gz")
sha256sums=('SKIP')

build() {
    # -march=native/-flto из makepkg.conf ломают сборку C-библиотеки aws-lc
    unset CFLAGS CXXFLAGS LDFLAGS CPPFLAGS RUSTFLAGS
    meson setup build "${srcdir}" --prefix=/usr -Dwerror=false
    ninja -C build
}

package() {
    # custom_target cargo-build помечен build_always_stale: ninja install
    # пересобирал бы cargo под fakeroot и падал бы на aws-lc
    DESTDIR="${pkgdir}" meson install -C build --no-rebuild
    install -Dm755 kvantos-mode "${pkgdir}/usr/bin/kvantos-mode"
}
