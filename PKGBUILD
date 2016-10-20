# Maintainer: jun7 <jun7@hush.com>
# Contributor: Florian pritz <bluewind@xinu.at>
# Contributor: Bartłomiej Piotrowski <nospam@bpiotrowski.pl>
# Contributor: Brad Fanella <bradfanella@archlinux.us>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: tobias <tobias@archlinux.org>

pkgname=openbox-1pixelwm
pkgver=3.6.1
pkgrel=3
branch=1pixel
pkgdesc='Highly configurable and lightweight X11 window manager'
arch=('i686' 'x86_64')
url='http://openbox.org'
license=('GPL')
confricts=('openbox')
depends=('startup-notification' 'libxml2' 'libxinerama' 'libxrandr'
         'libxcursor' 'pango' 'imlib2' 'librsvg' 'libsm')
optdepends=('plasma-workspace: for the KDE/Openbox xsession'
            'python2-xdg: for the openbox-xdg-autostart script')
groups=('lxde' 'lxde-gtk3' 'lxqt')
backup=('etc/xdg/openbox/menu.xml' 'etc/xdg/openbox/rc.xml'
        'etc/xdg/openbox/autostart' 'etc/xdg/openbox/environment')
source=("git://github.com/jun7/openbox.git#branch=$branch")
md5sums=('SKIP')

prepare() {
  cd "$srcdir/openbox"

  sed -i 's|/usr/bin/env python|/usr/bin/env python2|' \
    data/autostart/openbox-xdg-autostart
}

build() {
  cd "$srcdir/openbox"

  ./bootstrap

  ./configure --prefix=/usr \
    --with-x \
    --enable-startup-notification \
    --sysconfdir=/etc \
    --libexecdir=/usr/lib/openbox
  make
}

package() {
  cd "$srcdir/openbox"
  make DESTDIR="$pkgdir" install

  # GNOME Panel is no longer available in the official repositories
  rm -r "$pkgdir"/usr/bin/{gdm-control,gnome-panel-control,openbox-gnome-session} \
    "$pkgdir"/usr/share/gnome{,-session} \
    "$pkgdir"/usr/share/man/man1/openbox-gnome-session.1 \
    "$pkgdir"/usr/share/xsessions/openbox-gnome.desktop

  sed -i 's:startkde:/usr/bin/\0:' \
    "$pkgdir"/usr/share/xsessions/openbox-kde.desktop
}
