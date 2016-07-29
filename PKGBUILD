pkgname=xmind
pkgver=3.6.51
pkgrel=1
pkgdesc='Professional and powerful mind mapping software'
arch=('x86_64')
url="www.xmind.net"
license=('EPL' 'LGPL')
depends=('openjdk' 'webkitgtk2' 'lame' 'glib2')
source=('http://www.xmind.net/${pkgname}/downloads/${pkgname}-7.5-update1-linux_amd64.deb')
md5sums=('64fb4bf0dfed84701432bc0bc8a47b16')

package() {
tar -xf data.tar.gz -C $pkgdir
rm -r $pkgdir/usr/share/{doc,lintian}
}
