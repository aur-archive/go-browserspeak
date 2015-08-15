# Maintainer: Alexander Rødseth <rodseth@gmail.com>

pkgname=go-browserspeak
pkgver=20121220
pkgrel=1
pkgdesc='Web template generator'
arch=('x86_64' 'i686')
url='https://github.com/xyproto/browserspeak'
license=('MIT')
makedepends=('go' 'go-check' 'go-web')
options=('!strip' '!emptydirs')
_gourl=github.com/xyproto/browserspeak

build() {
  cd "$srcdir"
  GOPATH="$srcdir" go get -v -x ${_gourl}
}

check() {
  source /etc/profile.d/go.sh
  GOPATH="$GOPATH:$srcdir" go test -v -x ${_gourl}
}

package() {
  source /etc/profile.d/go.sh
  mkdir -p "$pkgdir/$GOPATH"
  cp -Rv --preserve=timestamps ${srcdir}/{src,pkg} "${pkgdir}/$GOPATH"

  # Package license (if available)
  for f in LICENSE COPYING; do
    if [ -e "$srcdir/src/$_gourl/$f" ]; then
      install -Dm644 "$srcdir/src/$_gourl/$f" \
        "$pkgdir/usr/share/licenses/$pkgname/$f"
    fi
  done

  # Remove duplicate go-web files
  find "$pkgdir" -depth -type d -name hoisie -exec rm -r {} \;
}

# vim:set ts=2 sw=2 et:
