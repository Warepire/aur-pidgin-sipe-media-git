pkgname=pidgin-sipe-media-git
pkgver=1.24.0.r46.g99622659
pkgrel=1
pkgdesc="Third-party Pidgin plugin for Microsoft Office 365/Lync/LCS/OCS - With patches from Tieto"
arch=('x86_64')
license=('GPL2')
url="http://sipe.sf.net"
# patches will be generated from launchpad-next branch of https://github.com/tieto/sipe
# depends as I need them, some are in theory optional.
depends=('gmime3' 'libpurple' 'glib2' 'libxml2' 'nss' 'dbus' 'farstream' 'gstreamer' 'gst-plugins-base' 'gst-plugins-bad' 'libnice-git' 'freerdp-with-shadow-server')
makedepends=('git' 'intltool' 'pkg-config' 'flex')
source=('git+https://repo.or.cz/siplcs.git#branch=mob'
        'https://github.com/tieto/sipe/commit/ac09f5eb7137c022370aa7ef24e02d08117eef12.patch'
        'https://github.com/tieto/sipe/commit/d375fbf2174016e37341bf59a6888870ea4cea14.patch'
        'https://github.com/tieto/sipe/commit/0c899fc87fcfd4edff3d5fcf1cadff0ca12e62d6.patch'
        'https://github.com/tieto/sipe/commit/895390ab32a5b0cd7ee99efa58a0b4bfc2e2c376.patch'
        'https://github.com/tieto/sipe/commit/2ea7325e39c0698ce585918d005642318ba8aefa.patch'
        'https://github.com/tieto/sipe/commit/7ed3cde8ebaed8a9bfbe455ccaf75a43166f0be9.patch'
        'https://github.com/tieto/sipe/commit/2085b4ae009b667ed391a9ef3c57469ac704f31c.patch'
        '0001-sipmsg-insert-line-breaks-between-paragraphs.patch'
        '0002-config-Use-one-equal-sign-for-tests-in-configure.ac.patch')
sha256sums=('SKIP'
            'e7b858a5d1ad62cae82a50dee8adcbb9813e4673f8a80b5cd58cc93fe665f5d7'
            '299ea79bbcfeb373c5f1f5c43bdf3481dfc38a132f64c3a3c0b65dba14140223'
            '630a7baa519af9df81d379c9216d443e5c69573fe0fb12c80a153a2c09ec9337'
            'a9d09efa0ccac7a100b84abbcbd3656dbd638eafc18561b19d1ffddb8230165c'
            '02538d436d209de09b3d2f018d56b2679f68e4b1efb3d5df7132175c66a03560'
            'dde5bf85a986f59209cdced385cb1136f55d66861a8b7f956fad3e12f63ca765'
            '9a8804ba7a7603b89492479aab8fd315da4d4a4b8f2609371c3f0fe767d0d181'
            'f0e9cbd5a0541228f5a136dc1ec2d961c3077ea4ff27bd0cc954dd7d2acd038c'
            '44a3aec703f7c905e57902e502ffef0f0f9538b284c53f316d195394dc26b594')
provides=(pidgin-sipe)
conflicts=(pidgin-sipe)

pkgver() {
  cd siplcs
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd siplcs

  patch -Np1 -i "${srcdir}/ac09f5eb7137c022370aa7ef24e02d08117eef12.patch"
  patch -Np1 -i "${srcdir}/d375fbf2174016e37341bf59a6888870ea4cea14.patch"
  patch -Np1 -i "${srcdir}/0c899fc87fcfd4edff3d5fcf1cadff0ca12e62d6.patch"
  patch -Np1 -i "${srcdir}/895390ab32a5b0cd7ee99efa58a0b4bfc2e2c376.patch"
  patch -Np1 -i "${srcdir}/2ea7325e39c0698ce585918d005642318ba8aefa.patch"
  patch -Np1 -i "${srcdir}/7ed3cde8ebaed8a9bfbe455ccaf75a43166f0be9.patch"
  patch -Np1 -i "${srcdir}/2085b4ae009b667ed391a9ef3c57469ac704f31c.patch"

  patch -Np1 -i "${srcdir}/0001-sipmsg-insert-line-breaks-between-paragraphs.patch"
  patch -Np1 -i "${srcdir}/0002-config-Use-one-equal-sign-for-tests-in-configure.ac.patch"

  ./autogen.sh
}

build() {
  cd siplcs

  ./configure --prefix=/usr --disable-telepathy --without-krb5 --without-gssapi

  make
}

package() {
  cd siplcs

  make DESTDIR="$pkgdir" install
}
