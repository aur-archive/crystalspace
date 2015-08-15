# Maintainer: Harley Laue <losinggeneration@gmail.com>
# Contributor: Martin Sandsmark <sandsmark@iskrembilen.com>
# Contributor: Matt McDonald <metzen@gmail.com>

pkgname=crystalspace
pkgver=2.0
pkgrel=3
pkgdesc="Free and portable 3D Game Development Kit written in C++"
url="http://www.crystalspace3d.org"
arch=('i686' 'x86_64')
license=('LGPL')
depends=('cegui' 'freetype2' 'libgl' 'libxcursor' 'libxrender')
makedepends=('alsa-lib' 'boost' 'cairomm' 'cal3d' 'ftjam-stable' 'lcms'
             'lib3ds'  'libmng' 'libvorbis' 'nvidia-cg-toolkit' 'openal'
             'python2' 'speex' 'wxgtk')
optdepends=('alsa-lib: Audio plugin'
'cairomm: Image plugin'
'cal3d: Models plugin'
'lcms: Image plugin'
'lib3ds: Models plugin'
'libmng: Image plugin'
'libvorbis: Audio plugin'
'nvidia-cg-toolkit: Rendering plugin'
'openal: Audio  plugin'
'python2: Bindings plugin'
'speex: Audio plugin'
'wxgtk: GUI plugin')
source=(http://www.crystalspace3d.org/downloads/release/${pkgname}-src-${pkgver}.tar.bz2
        crystalspace.profile)
md5sums=('e6c65d666e5cc75357c95e243d3cfbc9'
         'f0bdbbc6200ce99186d0dd7968735b50')

build() {
  cd "$srcdir/crystalspace-src-${pkgver}"

  # Bullet, ODE, Perl, & Java all fail to compile
  PYTHON=python2 \
  CXXFLAGS='-fpermissive' \
  ./configure --prefix=/opt/crystalspace \
              --sysconfdir=/etc \
              --disable-make-emulation \
              --without-bullet \
              --without-ode \
              --without-perl \
              --without-java

  jam "${MAKEFLAGS}"
}

package() {
  cd "$srcdir/crystalspace-src-${pkgver}"
  jam DESTDIR="$pkgdir/" install
  install -D -m755 "${srcdir}"/crystalspace.profile "${pkgdir}"/etc/profile.d/crystalspace.sh

  install -d -m755 "${pkgdir}"/usr/lib
  mv "${pkgdir}"/opt/crystalspace/lib/python* "${pkgdir}"/usr/lib

  install -d -m755 "${pkgdir}"/etc/ld.so.conf.d/
  echo '/opt/crystalspace/lib' > "${pkgdir}"/etc/ld.so.conf.d/crystalspace.conf
}
