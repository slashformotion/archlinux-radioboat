pkgname=radioboat
pkgver=0.1.0
pkgrel=1
pkgdesc="A terminal web radio client, built with simplicity in mind"
arch=('x86_64')
url="https://github.com/slashformotion/radioboat"
license=('APACHE')
makedepends=('go' 'git')
depends=('mpv')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('8f378fdda91166d3c5d091e077fc7b49b9f1e8fcceb681c7c36f5c43616e4b32')
provides=('radioboat')
prepare() {
  cd "$pkgname-$pkgver"
  export GOPATH="$srcdir/gopath"

  # create directory for build output
  mkdir -p build

  # download dependencies
  go mod download -x
}

build() {
  cd "$pkgname-$pkgver"
  export GOPATH="$srcdir/gopath"
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -mod=readonly -modcacherw"
  go build -v -o build .
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 "build/$pkgname" "$pkgdir/usr/bin/$pkgname"
}