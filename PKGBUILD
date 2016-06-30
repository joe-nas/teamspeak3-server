# Maintainer: Malte Rabenseifner <mail@malte-rabenseifner.de>
# Contributor: EnteEnteEnte <ducksource@duckpond.ch>

pkgname='teamspeak3-server'
pkgver='3.0.12.4'
pkgrel=1
pkgdesc='A proprietary VoIP conference software'
license=('custom')
arch=('i686' 'x86_64')
url="http://www.teamspeak.com"
depends=('glibc')
optdepends=('mariadb-connector-c: for MariaDB backend')
backup=(etc/default/teamspeak3-server)
install='teamspeak3-server.install'
source=('teamspeak3-server.ini'
        'teamspeak3-server.service')
source_i686=("http://teamspeak.gameserver.gamed.de/ts3/releases/$pkgver/teamspeak3-server_linux_x86-$pkgver.tar.bz2")
source_x86_64=("http://teamspeak.gameserver.gamed.de/ts3/releases/$pkgver/teamspeak3-server_linux_amd64-$pkgver.tar.bz2")
md5sums=('SKIP'
            'SKIP')
sha256sums_i686=('6c1138abc8e849d956793ddbf4fda79777c5311627239f7bac2a1c08d66373a7')
sha256sums_x86_64=('6bb0e8c8974fa5739b90e1806687128342b3ab36510944f576942e67df7a1bd9')

if [ "$CARCH" == "x86_64" ]; then
  _TSARCH='amd64'
elif [ "$CARCH" == "i686" ]; then
  _TSARCH='x86'
fi

package() {
    cd "$srcdir"

    install -Dm 644 teamspeak3-server.ini "$pkgdir/etc/teamspeak3-server.ini"
    install -Dm 644 teamspeak3-server.service "$pkgdir/usr/lib/systemd/system/teamspeak3-server.service"

    install -Dm 755 "teamspeak3-server_linux_$_TSARCH/ts3server" "$pkgdir/usr/bin/ts3server"
    install -Dm 644 "teamspeak3-server_linux_$_TSARCH/libts3db_mariadb.so" "$pkgdir/usr/lib/libts3db_mariadb.so"
    install -Dm 644 "teamspeak3-server_linux_$_TSARCH/libts3db_sqlite3.so" "$pkgdir/usr/lib/libts3db_sqlite3.so"
    install -Dm 644 "teamspeak3-server_linux_$_TSARCH/LICENSE" "$pkgdir/usr/share/licenses/teamspeak3-server/LICENSE"

    mkdir -p "$pkgdir/usr/share/doc/teamspeak3-server" \
             "$pkgdir/usr/share/teamspeak3-server" \
             "$pkgdir/var/lib/teamspeak3-server" \
             "$pkgdir/var/log/teamspeak3-server"

    cp -a "teamspeak3-server_linux_$_TSARCH/doc/" "$pkgdir/usr/share/doc/teamspeak3-server/"
    cp -a "teamspeak3-server_linux_$_TSARCH/sql/" "$pkgdir/usr/share/teamspeak3-server/"

    find "$pkgdir/usr/share/teamspeak3-server" -type d -exec chmod 755 {} \;
    find "$pkgdir/usr/share/teamspeak3-server" -type f -exec chmod 644 {} \;
    find "$pkgdir/usr/share/doc/teamspeak3-server" -type d -exec chmod 755 {} \;
    find "$pkgdir/usr/share/doc/teamspeak3-server" -type f -exec chmod 644 {} \;

    chmod 750 "$pkgdir/var/lib/teamspeak3-server" \
              "$pkgdir/var/log/teamspeak3-server"
}
