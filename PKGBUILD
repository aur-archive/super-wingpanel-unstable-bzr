# Maintainer: quequotion <quequotion@bugmenot.com>
# Contributor: ernest21 <ernest2193 at gmail dot com>

pkgname=super-wingpanel-unstable-bzr
pkgver=r189
pkgrel=2
pkgdesc='A super sexy space-saving top panel (unstable bzr version + compatibility patches)'
arch=('i686' 'x86_64')
url="https://code.launchpad.net/~heathbar/super-wingpanel/unstable"
license=('GPL3')
depends=('granite-bzr' lib{indicator3-bzr,wnck3,gee})
optdepends=(indicator-{application,datetime,messages,printers,session,sound}-pantheon-bzr": Tray applet"
            "indicator-power-bzr: Tray applet"
            "network-manager-applet-ubuntu: Tray applet"
            "glippy-bzr: Simple, powerful clipboard manager"
            "indicator-powersave: On the fly power savings and performance toggles"
            "pantheon-notify-bzr: Popup notifications (freedesktop standard compliant)"
            "pantheon-print-bzr: Printer dialog (integrates with contractor-enabled applications)")
makedepends=('bzr' 'cmake' 'vala')
provides=(super-wingpanel{,-unstable}{,-bzr}=$pkgver)
conflicts=(super-wingpanel{,-unstable}{,-bzr})
install='super-wingpanel.install'
source=("bzr+lp:/~heathbar/super-wingpanel/unstable"
	'libgee-0.8.patch'
	'super-unity-indicators.patch'
        'vala-syntax-update.patch'
        'gtk-3.14-margins.patch'
        '24px-pixbuff-limit.patch')
sha256sums=('SKIP'
            '038cef670fb57be8180d5b5bbb6280b0a50a1a15b0086d7f53fcb548e88e0ad7'
            '7fe49833c8d952169cb074e7f59220304a35defd64c332bd1f82e4fc8affa813'
            '58f5df7fc3f511bdc1bcad2d2c9e3031364800bfd6311f3cdde0d4b43e63e2d2'
            'fd349a84a9b87137aff0f60abb56e2766510052a88e580a04be7dd1d7310b3b6'
            'f57989ed805edb6e1854d83e2cf76355ca5c01074c9de04ff98072eeb6d9eae8')

pkgver() {
  cd unstable

  printf "r%s" "$(bzr revno)"
}

build() {
  cd unstable

  patch -Np2 < "${srcdir}/libgee-0.8.patch"
  patch -Np2 < "${srcdir}/super-unity-indicators.patch"
  patch -Np2 < "${srcdir}/vala-syntax-update.patch"
  patch -Np2 < "${srcdir}/gtk-3.14-margins.patch"
  patch -Np2 < "${srcdir}/24px-pixbuff-limit.patch"

  if [[ -d build ]]; then
    rm -rf build
  fi
  mkdir build && cd build

  cmake .. -DCMAKE_BUILD_TYPE='Release' -DCMAKE_INSTALL_PREFIX='/usr' -DGSETTINGS_COMPILE='OFF'
  make 
}

package() {
  cd unstable/build

  make DESTDIR="${pkgdir}" install
}
