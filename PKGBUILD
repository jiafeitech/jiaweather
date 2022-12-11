pkgname=jiaweather
_pkgname=gnome-weather
pkgver=43.0+7+g463624f
pkgrel=1
pkgdesc="Access current weather conditions and forecasts"
url="https://wiki.gnome.org/Apps/Weather"
arch=(any)
license=(GPL)
depends=('gtk3' 'gjs' 'libgweather-4' 'geoclue2')
makedepends=('gobject-introspection' 'appstream-glib' 'git' 'meson')
provides=('gnome-weather')
conflicts=('gnome-weather' 'gnome-weather-git')
groups=('gnome')
source=("git+https://gitlab.gnome.org/GNOME/gnome-weather.git#branch=gnome-43" "desktop.patch" "weather.png")
sha512sums=('SKIP' 'SKIP' 'SKIP')

pkgver() {
  cd $_pkgname
  git describe --tags | sed 's/-/+/g'
}

build() {
  patch $srcdir/$_pkgname/data/org.gnome.Weather.desktop.in.in desktop.patch

  arch-meson $_pkgname build
  ninja -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  mkdir -p ${pkgdir}/usr/share/icons/cvm-ui-icons
  cp ${srcdir}/weather.png ${pkgdir}/usr/share/icons/cvm-ui-icons/
  
  DESTDIR="$pkgdir" meson install -C build
}
