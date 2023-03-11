pkgname=minetest-mapserver
pkgver=4.6.1
pkgrel=1
pkgdesc="Minetest realtime mapserver, written in go"
arch=('i686' 'x86_64')
url="https://github.com/minetest-mapserver/mapserver"
license=('MIT')
makedepends=('go' 'rollup')
source=(
  https://github.com/minetest-mapserver/mapserver/archive/refs/tags/v"${pkgver}".tar.gz
  minetest-mapserver.service
)
sha256sums=(
  'e4e7fd8eb35fef9122aa32952f8bbcf8a34eb048115124bb03332f48d625b8d7'
  '06ccaea993e9ba43d8ce98916c46fb377d99686175a211d089a626ef4e2907f3'
)

build() {
  cd "${srcdir}"/mapserver-"${pkgver}"
  go build
  cd public
  rollup -c rollup.config.js
}

package() {
  echo package
  cd "${srcdir}"/mapserver-"${pkgver}"/
  install -D -m755 mapserver "${pkgdir}"/usr/bin/"${pkgname}"
  install -D -m644 license.txt "${pkgdir}"/usr/share/licenses/$pkgname/license.txt
  install -D -m644 "${startdir}"/"${pkgname}".service "${pkgdir}"/usr/lib/systemd/system/"${pkgname}".service
}

post_install() {
  echo "
  if you want to change the default configuration do the following:
  $ cd /var/lib/minetest/0/
  $ minetest-mapserver --createconfig

  to install the mod do the following:

  $ cd /var/lib/minetest/0/
  $ mkdir worldmods
  $ cd worldmods
  $ git clone https://github.com/minetest-mapserver/mapserver_mod
  $ cd ..
  $ chown -R minetest:minetest worldmods
  then add the following to your minetest.conf
    secure.http_mods = mapserver
    mapserver.url = http://127.0.0.1:8080
    mapserver.key = ZJoSpysiKGlYexof  

}
