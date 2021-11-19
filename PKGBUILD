# Maintainer: Sevan Murriguian--Watrin <sevan@cri.epita.fr>
# Compatibility edit for external computers by Victor ABRAHAM--BITTER <victor.abraham-biter@epita.fr>

pkgname=i3lock-PIEscaped
pkgver=2.11.1.PIEscaped
pkgrel=3
pkgdesc="An improved screenlocker based upon XCB and PAM - PIEscaped compatibility patch"
arch=('i686' 'x86_64')
url="https://github.com/abrvham/i3lock-PIEscaped"
license=('MIT')
groups=('i3')
provides=('i3lock')
conflicts=('i3lock')
depends=('xcb-util-image' 'xcb-util-xrm' 'libev' 'cairo' 'libxkbcommon-x11' 'pam' 'systemd')
backup=("etc/pam.d/i3lock")
options=('docs')
makedepends=('git')
source=('git://github.com/abrvham/i3lock-PIEscaped#branch=master')
sha1sums=('SKIP')

_gitname='i3lock-PIEscaped'

build() {
    cd "$_gitname"

  # Fix ticket FS#31544, sed line taken from gentoo
  sed -i -e 's:login:system-auth:' pam/i3lock

  autoreconf --force --install

  rm -rf build/
  mkdir -p build && cd build/

  ../configure \
      --prefix=/usr \
      --sysconfdir=/etc \
      --disable-sanitizers

  # See https://lists.archlinux.org/pipermail/arch-dev-public/2013-April/024776.html
  make CPPFLAGS+="-U_FORTIFY_SOURCE"
}

package() {
    cd "$_gitname"
    cd build/

    make DESTDIR="$pkgdir/" install

    install -Dm644 ../LICENSE \
        "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set ts=4 sw=4 et:
