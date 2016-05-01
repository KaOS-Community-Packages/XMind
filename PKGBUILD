pkgname=xmind
pkgver=3.6.1
pkgrel=1
pkgdesc='Professional and powerful mind mapping software'
arch=('x86_64')
url="www.xmind.net"
license=('EPL' 'LGPL')
depends=('openjdk' 'webkitgtk2' 'lame' 'glib2')
source=('http://dl2.xmind.net/xmind-downloads/xmind-7-update1-linux_amd64.deb')
md5sums=('d3e8e76766fa6bc6cdf62a8a5f3c3b95')

package() {
tar -xf data.tar.gz -C $pkgdir
rm -r $pkgdir/usr/share/doc
}
