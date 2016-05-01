pkgname=xmind
pkgver=3.6.1
pkgrel=1
pkgdesc="The most popular Mind Mapping Software on the planet"
arch=('x86_64')
url="https://www.xmind.net"
license=('EPL' 'LGPL')
depends=('openjdk' 'gtk2>=2.8' 'webkitgtk2')
optdepends=('lame: needed for the feature audio notes')
source=('http://www.xmind.net/xmind/downloads/xmind-7-update1-linux_amd64.deb')
md5sums=('d3e8e76766fa6bc6cdf62a8a5f3c3b95')

package() {
  tar -xf data.tar.gz -C $pkgdir
  rm -r $pkgdir/usr/share/lintian/
}
