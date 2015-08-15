#Maintainer Alex Ferrando <alferpal@gmail.com>

_firefox_dir='/usr/lib/firefox'
_extension_id='{9533f794-00b4-4354-aa15-c2bbda6989f8}'

pkgname=firefox-firetray-svn
pkgver=144
pkgrel=3
pkgdesc="A firefox system tray extension for linux"
arch=('i686' 'x86_64')
url="http://code.google.com/p/firetray/"
license=('GPL')
depends=('firefox')
makedepends=('xulrunner=11.0' 'scons' 'svn' 'unzip')
provides=('firefox-firetray')
conflicts=('firefox-firetray')
source=('generate_install_rdf.sh.patch'
        'SConscript.patch')


md5sums=('a1ebf4dc133ec382180e78a2af16e824'
         '32ad360336cbee9d5a1cd3e9a64b56b4')

_svntrunk=http://firetray.googlecode.com/svn/trunk/
_svnmod=firetray

build() {
	
	cd $startdir/src
	if [ -d $_svnmod/.svn ]; then
		( cd $_svnmod && svn up )
	else
		svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
	fi

	msg "SVN checkout done or sever timeout"
	msg "Starting make..."

	cp -r $_svnmod $_svnmod-build
	cd $_svnmod-build

	#patch -Np0 -i ${srcdir}/generate_install_rdf.sh.patch || return 1
	patch -Np0 -i ${srcdir}/SConscript.patch || return 1

	./build.sh
	mkdir -p "${pkgdir}"/"${_firefox_dir}"/extensions/"${_extension_id}"
	unzip firetray*.xpi -d "${pkgdir}"/"${_firefox_dir}"/extensions/"${_extension_id}"
}
