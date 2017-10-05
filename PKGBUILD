pkgname=xmind
pkgver=3.7.5
pkgrel=1
pkgdesc="The most popular Mind Mapping Software on the planet"
arch=('x86_64')
url="https://www.xmind.net"
license=('EPL' 'LGPL')
depends=('openjdk>=8u' 'gtk2>=2.8' 'webkitgtk2')
optdepends=('lame: needed for the feature audio notes')
install=${pkgname}.install
source=("https://www.xmind.net/xmind/downloads/${pkgname}-8-update5-linux.zip"
        "XMind.png")
sha256sums=('7e23e113a96b95ca8f73e10e6a6a3a54520e99069fc69dccf33990bc7eb7295a'
            '67cda22286ea8350eda083456eeddabbcbc8ad419624be7e64bb601ec9352191')

prepare() {
  # patch XMind.ini
  sed \
    -e 's|\.\/configuration|\@user\.home/\.xmind\/configuration|' \
    -e 's|\.\.\/workspace|\@user\.home\/\.xmind\/workspace-cathy|' \
    -e "s|\.\.\/plugins|\/opt\/${pkgname}\/plugins|g" \
    -e '$ i -Dosgi.instance.area=@user.home/.xmind/workspace-cathy' \
    -e '$ i -Dosgi.configuration.area=@user.home/.xmind/configuration' \
    -i ${srcdir}/XMind_amd64/XMind.ini

  #create desktop file
  cat > ${srcdir}/${pkgname}.desktop << EOF
[Desktop Entry]
Encoding=UTF-8
Type=Application
Categories=Office;
Name=XMind
Version=3.7.2
Comment=Launch XMind 8 Update 2
Icon=XMind
Exec=SWT_GTK3=0 /opt/xmind/XMind_amd64/XMind
Terminal=false
StartupNotify=true
MimeType=application/xmind;x-scheme-handler/xmind;
EOF
}

package() {
  # install fonts
  install -Dm755 -d ${pkgdir}/usr/share/fonts/truetype/${pkgname}/
  install -Dm644 ${srcdir}/fonts/*.ttf ${pkgdir}/usr/share/fonts/truetype/${pkgname}/

  # install menu entry
  install -Dm755 ${srcdir}/${pkgname}.desktop ${pkgdir}/usr/share/applications/${pkgname}.desktop
  install -Dm644 ${srcdir}/XMind.png ${pkgdir}/usr/share/icons/hicolor/32x32/apps/XMind.png

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
