# Maintainer: Stephan Peters <speters33w аt gmail dоt cоm>
# Contributor: Alejandro Villanueva <awewanwo at disroot dot org>

_include_webfonts=false
# true to include webfonts with ttf or otf installation.
# explicitly installing webfonts overrides this value to true.

_webfontdir=$HOME/www/fonts/
# Directory to copy webfonts to.

fontname=d-din
# pkgname=("otf-$fontname" "ttf-$fontname" "webfonts-$fontname")
pkgname=("webfonts-$fontname")  # Install single package.
pkgver=1.12
pkgrel=1.12
name="$fontname-fonts" # Fedora package name
version=1.0            # Font release version
release=12             # Fedora release
dist=fc38              # Fedora dist
pkgdesc="A sans-serif typeface family derived from German DIN by Charles Nix."
# url=https://www.datto.com/fonts/d-din/  # Datto no longer hosts file.
url=https://packages.fedoraproject.org/pkgs/d-din-fonts/
arch=(any)
license=("custom:SIL Open Font License v1.1")
depends=()
makedepends=()
optdepends=()
conflicts=()
rpmname="$name-$version-$release.$dist.src.rpm"
zipfile="D-DIN_complete-v$version.zip"
source=(https://download.fedoraproject.org/pub/fedora/linux/development/rawhide/Everything/source/tree/Packages/d/"$rpmname")
sha256sums=('61978241c40bb60d8353ff408066138243d11e4cec6a4fd2316b9d1323e49ee3')

prepare(){
  bsdtar xvf $rpmname  # d-din-fonts-1.0-12.fc38.src.rpm
  bsdtar xvf $zipfile  # D-DIN_complete-v1.0.zip
  cd "$srcdir"
}
  
install_license(){
  if [ ! -f "/usr/share/licenses/$name/OFL-1.1.txt" ] ; then
    mkdir -p "$pkgdir"/usr/share/licenses/"$name"
    install -Dm644 -t "$pkgdir"/usr/share/licenses/"$name" COPYING.txt
    install -Dm644 -t "$pkgdir"/usr/share/licenses/"$name" OFL-1.1.txt
    install -Dm644 -t "$pkgdir"/usr/share/licenses/"$name" README
    install -Dm644 -t "$pkgdir"/usr/share/licenses/"$name" FONTLOG.txt
  fi
}

install_fonts(){
  mkdir -p "$pkgdir"/usr/share/fonts/"$name"
  install -Dm644 -t "$pkgdir"/usr/share/fonts/"$name" ./*."$1"
}

install_webfonts(){
  if [ "$_include_webfonts" = true ] ; then
    mkdir -p "$pkgdir"/"$_webfontdir"
    if [ ! -f "$_webfontdir/D-DIN.woff" ] ; then 
      install -Dm644 -t "$pkgdir"/"$_webfontdir"/ ./*.woff
    fi
    if [ ! -f "$_webfontdir/D-DIN.woff2" ] ; then
      install -Dm644 -t "$pkgdir"/"$_webfontdir"/ ./*.woff2 
    fi
  echo -e "\e[32mWebfonts will be installed in ${_webfontdir}.\e[0m" 
  fi  
}

package_ttf-d-din() {
  conflicts+=(otf-d-din)
  install_license
  install_fonts ttf
  install_webfonts
}

package_otf-d-din() {
  conflicts+=(ttf-d-din)
  install_license
  install_fonts otf
  install_webfonts
}

package_webfonts-d-din() {
  _include_webfonts=true
  install_license
  install_webfonts
}


