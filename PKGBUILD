pkgname=pidgin-sipe-media-git
pkgver=1.25.0.r12.gad0d885d
pkgrel=1
pkgdesc="Third-party Pidgin plugin for Microsoft Office 365/Lync/LCS/OCS - With patches from Tieto"
arch=('x86_64')
license=('GPL2')
url="https://github.com/tieto/sipe"
# depends as I need them, some are in theory optional.
depends=('gmime3' 'libpurple' 'glib2' 'libxml2' 'nss' 'dbus' 'farstream' 'gstreamer' 'gst-plugins-base' 'gst-plugins-bad' 'libnice-git' 'freerdp')
makedepends=('git' 'intltool' 'pkg-config' 'flex')
source=('git+https://github.com/tieto/sipe.git#branch=launchpad-next'
        '0008-sipmsg-insert-line-breaks-between-paragraphs.patch'
        '0009-config-Use-one-equal-sign-for-tests-in-configure.ac.patch')
sha256sums=('SKIP'
            'f0e9cbd5a0541228f5a136dc1ec2d961c3077ea4ff27bd0cc954dd7d2acd038c'
            '44a3aec703f7c905e57902e502ffef0f0f9538b284c53f316d195394dc26b594')
provides=(pidgin-sipe)
conflicts=(pidgin-sipe)

pkgver() {
  cd sipe
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd sipe

  patch -Np1 -i "${srcdir}/0008-sipmsg-insert-line-breaks-between-paragraphs.patch"
  patch -Np1 -i "${srcdir}/0009-config-Use-one-equal-sign-for-tests-in-configure.ac.patch"

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
