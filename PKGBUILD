# Maintainer: Runnytu < runnytu at gmail dot com >
# OldMaintainer: Alexey Kharlamov <der@2-47.ru>
# Contributor: David Dufberg Tøttrup <david at dufberg dot se>
# Contributor: Jordi De Groof <jordi(dot)degroof(at)gmail(dot)com>
# Contributor: pyther <pyther@pyther.net>
# Contributor: z3ntu <WEI16416@spengergasse.at>
# Edited by: A.Alanov, Y.Yepishenko specially for CFUV people

pkgname=packettracer
pkgver=8.0.1
pkgrel=1
pkgdesc="A cross-platform visual simulation tool designed by Cisco Systems that allows users to create network topologies and imitate modern computer network"
arch=( 'x86_64' )
depends=('openssl>=1.0' 'dbus' 'icu' 'glib2' 'libxml2' 'libjpeg-turbo' 'nss' 'libxss' 'java-runtime>=1.7.0' 'qt6-multimedia' 'qt6-webengine' 'qt6-svg' 'qt6-networkauth' 'qt6-websockets' 'qt5-script' 'qt5-speech')
options=('!strip' '!emptydirs')
url="https://www.netacad.com/courses/packet-tracer"
license=('custom')

source=('local://CiscoPacketTracer_801_Ubuntu_64bit.deb'
	'packettracer.sh'
	'cisco-pt.desktop'
	'cisco-ptsa.desktop')
sha512sums=('541743d823b6bbe4ac86491fa2361d2de62761f4bbefe52c832706dff807c80342b4dbd5c9f8dbfebcda1a502cfe11257af98728053ccab20fefebfa7701309c'
            '47d575abf87ff26917ced452922ae6030b548e0deecca66397dbd4e22c032e217fcb4219b1bc783e6efa5fcbc4472dbe75b0d26f9d07de63a63d720475eb5122'
            '739ca68e39072e036d9e055222c3b4c8433d10fd8425d1a3f555ffa012e6f2b90f019975192f991368aff06abe29509f92085159525f5c95c37960da9a91099f'
            '90068e517607900ab0937974d1204e780463216cea4e377b1fb93d9d79bd78eee980da5943a54dcca7908d7b2362d2012b4db610bd72c373c84184c8fa917cef')

package() {

	tar xf data.tar.xz -C "${pkgdir}"
	chown -R 0:0 "${pkgdir}"
	mv "${pkgdir}/opt/pt/" "${pkgdir}/opt/packettracer/"
	mkdir -p "${pkgdir}/usr/share/applications/"
	mv "${srcdir}/cisco-pt.desktop" "${pkgdir}/usr/share/applications/cisco-pt.desktop"
	mv "${srcdir}/cisco-ptsa.desktop" "${pkgdir}/usr/share/applications/cisco-ptsa.desktop"
	chmod a+x "${pkgdir}/usr/share/applications/cisco-pt.desktop"
	chmod a+x "${pkgdir}/usr/share/applications/cisco-ptsa.desktop"
	mkdir -p "${pkgdir}/usr/bin/"

	find "${pkgdir}" -type d -exec chmod 755 {} \;
	find "${pkgdir}/opt/packettracer/help/" -type d -exec chmod 777 {} \;
	find "${pkgdir}/opt/packettracer/saves/" -type d -exec chmod 555 {} \;
	find "${pkgdir}/opt/packettracer/art/html/network_controller/" -type d -exec chmod 775 {} \;
	find "${pkgdir}/opt/packettracer/art/RackView/CablePegboard/" -type d -exec chmod 775 {} \;
	find "${pkgdir}/opt/packettracer/bin/xcbglintegrations/" -type d -exec chmod 775 {} \;
	find "${pkgdir}/opt/packettracer/help/default/NetconRestAPI/" -type d -exec chmod 775 {} \;
	
	ln -s /opt/packettracer/packettracer "${pkgdir}/usr/bin/packettracer"

	ln -s /usr/lib/libdouble-conversion.so "${pkgdir}/opt/packettracer/bin/libdouble-conversion.so.1"

	sed -i 's|/opt/pt|/opt/packettracer|' "${pkgdir}/opt/packettracer/linguist" "${pkgdir}/opt/packettracer/packettracer"

	install -D -m755 "${srcdir}/packettracer.sh" "${pkgdir}/etc/profile.d/packettracer.sh"

	install -D -m644 "${pkgdir}/opt/packettracer/help/default/copyrights.htm" "${pkgdir}/usr/share/licenses/${pkgname}/COPYRIGHT"

}
