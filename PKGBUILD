# Maintainer: Bardia Moshiri <fakeshell@bardia.tech>

pkgname=ofono-hybris
provides=('ofono=1.29')
conflicts=('ofono')
_pkgbase=ofono
pkgver=10097.3afa0876
pkgrel=3
arch=('armv7h' 'aarch64' 'x86' 'x86_64')
url="https://github.com/sailfishos/ofono"
license=('GPL2')
depends=('libglibutil' 'dbus' 'systemd')
makedepends=('git' 'pkgconfig' 'libwspcodec' 'automake' 'autoconf' 'dbus-glib' 'mobile-broadband-provider-info')
source=("ofono::git+https://github.com/sailfishos/ofono.git"
	"ril_subscription.conf")
md5sums=('SKIP'
	 'SKIP')
options=(debug !strip)

pkgver() {
  cd "${srcdir}/${_pkgbase}"
  echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

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

  install -Dm644 "${srcdir}/ril_subscription.conf" "${pkgdir}/etc/ofono/ril_subscription.conf"
}
