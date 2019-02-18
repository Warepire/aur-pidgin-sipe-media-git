pkgname=pidgin-sipe-media-git
pkgver=1.24.0.r18.g2085b4ae
pkgrel=1
pkgdesc="Third-party Pidgin plugin for Microsoft Office 365/Lync/LCS/OCS - Tieto media fork"
arch=('x86_64')
license=('GPL2')
url="https://github.com/tieto/sipe"
# depends as I need them, some are in theory optional.
depends=('gmime' 'libpurple' 'glib2' 'libxml2' 'nss' 'dbus' 'farstream' 'gstreamer' 'gst-plugins-base' 'gst-plugins-bad' 'libnice-git' 'freerdp-with-shadow-server')
makedepends=('intltool' 'pkg-config')
source=('git+https://github.com/tieto/sipe.git#branch=launchpad-next'
        '0001-sipmsg-insert-line-breaks-between-paragraphs.patch'
        '0002-config-Use-one-equal-sign-for-tests-in-configure.ac.patch')
sha256sums=('SKIP'
            '4456cc3c079be9332e6367eeb5e2771d0fe166ef2bfce9d231e5552b221c6eb5'
            '44a3aec703f7c905e57902e502ffef0f0f9538b284c53f316d195394dc26b594')
provides=(pidgin-sipe)
conflicts=(pidgin-sipe)

pkgver() {
  cd sipe
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd sipe

  patch -Np1 -i "${srcdir}/0001-sipmsg-insert-line-breaks-between-paragraphs.patch"
  patch -Np1 -i "${srcdir}/0002-config-Use-one-equal-sign-for-tests-in-configure.ac.patch"

  ./autogen.sh
}

build() {
  cd sipe

  ./configure --prefix=/usr --disable-telepathy --without-krb5 --without-gssapi

  make
}

package() {
  cd sipe

  make DESTDIR="$pkgdir" install
}
