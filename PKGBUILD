pkgname=xmind
pkgver=3.7.0
pkgrel=1
pkgdesc="The most popular Mind Mapping Software on the planet"
arch=('x86_64')
url="https://www.xmind.net"
license=('EPL' 'LGPL')
depends=('jdk' 'gtk2>=2.8' 'webkitgtk2')
optdepends=('lame: needed for the feature audio notes')
install=${pkgname}.install
source=("https://www.xmind.net/xmind/downloads/${pkgname}-8-linux.zip"
        "XMind.png")
md5sums=('1ea5acf1edcf628629f21bf73dd18358'
         'b0249518575eeb2f48f5d857346fecfc')

prepare() {
  # patch XMind.ini
  sed \
    -e '1i -vm\n/opt/java/bin/java' \
    -e 's|\.\/configuration|\@user\.home/\.xmind\/configuration|' \
    -e 's|\.\.\/workspace|\@user\.home\/\.xmind\/workspace-cathy|' \
    -e "s|\.\.\/plugins|\/opt\/${pkgname}\/plugins|g" \
    -e '$i -Dosgi.instance.area=@user.home/.xmind/workspace-cathy' \
    -e '$i -Dosgi.configuration.area=@user.home/.xmind/configuration' \
    -i ${srcdir}/XMind_amd64/XMind.ini

  #create desktop file
  cat > ${srcdir}/${pkgname}.desktop << EOF
[Desktop Entry]
Type=Application
Version=3.7.0
Encoding=UTF-8
Name=XMind
Comment=Launch XMind 8
Icon=XMind
Exec=/opt/xmind/XMind_amd64/XMind
Terminal=false
StartupNotify=true
Categories=Office;
MimeType=application/xmind;x-scheme-handler/xmind;
EOF
}

package() {
  # install fonts
  install -Dm755 -d ${pkgdir}/usr/share/fonts/truetype/${pkgname}/
  install -Dm644 ${srcdir}/fonts/*.ttf ${pkgdir}/usr/share/fonts/truetype/${pkgname}/

  # install menu entry
  install -Dm644 ${srcdir}/${pkgname}.desktop ${pkgdir}/usr/share/applications/${pkgname}.desktop
  install -Dm644 ${srcdir}/XMind.png ${pkgdir}/usr/share/pixmaps/XMind.png

  # install xmind
  install -Dm755 -d ${pkgdir}/opt/${pkgname}/
  install -Dm644 ${srcdir}/*.{xml,html,txt} ${pkgdir}/opt/${pkgname}/
  install -Dm644 ${srcdir}/configuration/config.ini ${pkgdir}/opt/${pkgname}/configuration/config.ini
  for folder in 'features' 'plugins' 'XMind_amd64'; do
    cp -R "${srcdir}/${folder}" "${pkgdir}/opt/${pkgname}/${folder}"
    chmod -R u+rwX,go+rX,go-w "${pkgdir}/opt/${pkgname}/${folder}"
  done

  # make executable
  chmod 755 "${pkgdir}/opt/${pkgname}/XMind_amd64/XMind"
}
