# Maintainer: Samuel Tilly <samuel.tilly AT gmail DOT com>
# Contributor: Anton Bazhenov <anton.bazhenov at gmail>
# Contributor: Christopher Rogers <slaxemulator@gmail.com>
# Contributor: J. W. Birdsong <jwbirdsong AT gmail DOT com> 

pkgname=wordwarvi-git
pkgver=20120722
pkgrel=1
pkgdesc="Word War vi is a retro-styled old school side scrolling shooter reminiscent of Defender or Scramble"
arch=('i686' 'x86_64')
url="http://smcameron.github.com/wordwarvi/"
license=('GPL'  'CCPL')
depends=('gtk2' 'libvorbis' 'portaudio' 'hicolor-icon-theme')
makedepends=('git')
provides=('wordwarvi')
conflicts=('wordwarvi')
install=wordwarvi.install
source=(wordwarvi.desktop)

md5sums=('cff0eecbe7166f42d35240725b586e76')

_gitroot=git://github.com/smcameron/wordwarvi.git
_gitname=wordwarvi

build() {
  cd $srcdir

  # download source
  msg "connecting to github's GIT server...."
  if [ -d $startdir/src/$_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot
  fi
  msg "GIT checkout done"

  # make and install
  cd "$srcdir/$_gitname"
  make || return 1
  make DESTDIR="$pkgdir" install || return 1

  # install license and .desktop files
  install -Dm644 sounds/Attribution.txt "$pkgdir"/usr/share/licenses/$_gitname/COPYING_SOUNDS
  install -Dm644 ../$_gitname.desktop "$pkgdir"/usr/share/applications/$_gitname.desktop

  # install icons
  for _width in '16' '22' '32' '48' '64' '128'; do
    install -Dm644 icons/${_gitname}_icon_${_width}x${_width}.png \
      "$pkgdir"/usr/share/icons/hicolor/${_width}x${_width}/apps/$_gitname.png
  done
}
md5sums=('7e04f54cc1d8688fc68663a8b5309d31')
