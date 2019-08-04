pkgname=pidgin-sipe-media-git
pkgver=1.24.0.r76.g6028919c
pkgrel=1
pkgdesc="Third-party Pidgin plugin for Microsoft Office 365/Lync/LCS/OCS - With patches from Tieto"
arch=('x86_64')
license=('GPL2')
url="http://sipe.sf.net"
# depends as I need them, some are in theory optional.
depends=('gmime3' 'libpurple' 'glib2' 'libxml2' 'nss' 'dbus' 'farstream' 'gstreamer' 'gst-plugins-base' 'gst-plugins-bad' 'libnice-git' 'freerdp')
makedepends=('git' 'intltool' 'pkg-config' 'flex')
source=('git+https://repo.or.cz/siplcs.git#branch=mob'
        '0001-media-move-filtering-of-broken-codecs-to-SIPE-core.patch'
        '0002-media-enable-SIREN-in-SfB-conferences.patch'
        '0003-conf-parse-media-source-id-of-participant-video-stre.patch'
        '0004-msrtp-configurable-media-source-id-in-VSR.patch'
        '0005-media-set-stream-media-source-id-for-video-streams.patch'
        '0006-conf-join-conference-video-call.patch'
        '0007-media-increase-connection-timeout-to-120s.patch'
        '0008-sipmsg-insert-line-breaks-between-paragraphs.patch'
        '0009-config-Use-one-equal-sign-for-tests-in-configure.ac.patch')
sha256sums=('SKIP'
            'b26729fa8d6afd8f81b53c63948b437e494a0322a4be385b3abb020e5059def5'
            '92e3430566bcc1533e169f4abe3aac043484a85ab31e38fa66ba6d31fa5208b5'
            '33afd7860018150e00758ae4ef92956eb822e0071f3c9fb84f68187fec34b489'
            '61fe5a860ddcfe7d30f4910ee6b2683334acb915b6b1cc0d6486a89517524433'
            'e3714417f5fb43726231a7d99b651fa8fc4d509a432d06e6dfb79c87af4aec0f'
            '9b7746165d9536f00b4e421078288edceabb4a37543371e9e4bcff0014da26aa'
            '18c6f6684f432db5b72dc9d96be4fc524801f4c123bb429264ebbfe5fb7a2eb4'
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

  patch -Np1 -i "${srcdir}/0001-media-move-filtering-of-broken-codecs-to-SIPE-core.patch"
  patch -Np1 -i "${srcdir}/0002-media-enable-SIREN-in-SfB-conferences.patch"
  patch -Np1 -i "${srcdir}/0003-conf-parse-media-source-id-of-participant-video-stre.patch"
  patch -Np1 -i "${srcdir}/0004-msrtp-configurable-media-source-id-in-VSR.patch"
  patch -Np1 -i "${srcdir}/0005-media-set-stream-media-source-id-for-video-streams.patch"
  patch -Np1 -i "${srcdir}/0006-conf-join-conference-video-call.patch"
  patch -Np1 -i "${srcdir}/0007-media-increase-connection-timeout-to-120s.patch"

  patch -Np1 -i "${srcdir}/0008-sipmsg-insert-line-breaks-between-paragraphs.patch"
  patch -Np1 -i "${srcdir}/0009-config-Use-one-equal-sign-for-tests-in-configure.ac.patch"

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
