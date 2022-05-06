# Maintainer Erik Inkinen <erik.inkinen@gmail.com>
pkgname=ofono-hybris
provides=('ofono=1.29')
conflicts=('ofono')
_pkgbase=ofono
pkgver=1.29+git3
pkgrel=1
arch=('armv7h' 'aarch64' 'x86' 'x86_64')
url="https://github.com/sailfishos/ofono"
license=('GPL2')
depends=('libglibutil' 'dbus' 'systemd')
makedepends=('git' 'pkgconfig' 'libwspcodec' 'automake' 'autoconf' 'dbus-glib' 'mobile-broadband-provider-info')
source=("ofono::git+https://github.com/sailfishos/ofono.git#tag=$pkgver")
md5sums=('SKIP')
options=(debug !strip)

build() {
  cd "${srcdir}/${_pkgbase}/ofono"
  autoreconf --force --install
  ./configure --disable-static \
    --enable-sailfish-bt \
    --enable-sailfish-provision \
    --enable-sailfish-pushforwarder \
    --enable-rilmodem \
    --disable-add-remove-context \
    --disable-isimodem \
    --disable-qmimodem \
    --prefix=/usr --mandir=/usr/share/man --libdir=/usr/lib \
    --sysconfdir=/etc --localstatedir=/var --sbindir=/usr/bin \
    --with-systemdunitdir=/usr/lib/systemd/system
  make KEEP_SYMBOLS=1 all
}

package() {
  cd "${srcdir}/${_pkgbase}/ofono"
  make DESTDIR="$pkgdir" install
}
