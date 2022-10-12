# Maintainer: Muflone http://www.muflone.com/contacts/english/

pkgname=4kvideodownloader
pkgver=4.21.7.5040
pkgrel=1
pkgdesc="Quickly download videos from YouTube in high-quality"
arch=('x86_64')
url="https://www.4kdownload.com/products/product-videodownloader"
license=('custom:eula')
depends=('openssl')
makedepends=('chrpath')
source=("${pkgname}_${pkgver}_amd64.tar.bz2"::"https://dl.4kdownload.com/app/${pkgname}_${pkgver%.*}_amd64.tar.bz2"
        "${pkgname}.desktop"
        "${pkgname}.svg"
        "fix_symlink_path.patch")
sha256sums=('56da901036f46afc1f409ae7d5a8c6c2a7d8419c0a8f8abf714fdbc1eace24e4'
            '78bdc7becf7124e2917547a0b66ec6e10ec397900cb49a685ca589dba5321967'
            '5c169ea486d1d9b50e0f510d6bc90901ff72162e3996b60f70ce574e58d173cb'
            '2b5a9c262ff7b832eafbfb0e027b676a8be44f9c527b99ac00bd8379fc709668')

prepare() {
  cd "${pkgname}"
  # Remove insecure RPATH
  chrpath --delete "${pkgname}-bin"
  # Fix symlink path
  patch -p1 -i "${srcdir}/fix_symlink_path.patch"
}

package() {
  # Install desktop file
  install -m 755 -d "${pkgdir}/usr/share/applications"
  install -m 755 -t "${pkgdir}/usr/share/applications" "${pkgname}.desktop"
  # Install icon file
  install -m 755 -d "${pkgdir}/usr/share/pixmaps"
  install -m 644 -t "${pkgdir}/usr/share/pixmaps" "${pkgname}.svg"
  # Install files
  install -m 755 -d "${pkgdir}/usr/lib"
  cp -r "${pkgname}" "${pkgdir}/usr/lib"
  chown root.root "${pkgdir}/usr/lib/${pkgname}"
  # Install launcher file
  install -m 755 -d "${pkgdir}/usr/bin"
  ln -s "/usr/lib/${pkgname}/${pkgname}.sh" "${pkgdir}/usr/bin/${pkgname}"
  # Install license file
  install -m 755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m 644 -t "${pkgdir}/usr/share/licenses/${pkgname}" "${pkgname}/doc/eula"
}
