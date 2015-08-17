pkgname=qmplay
pkgver=1.54.06
pkgrel=2
pkgdesc="Polish, cross-platform music player. QMPlay plays music from hard disk, wrzuta.pl or other http streams. Supported formats: AudioCD, MODs, OGG Vorbis, MP3, AAC, FLAC and uncompressed audio."
url="http://zaps166.sourceforge.net/"
license="LGPL"
arch=('i686' 'x86_64')
depends=('qt4' 'mpg123' 'faad2' 'libcdio' 'libcddb' 'curl' 'taglib' 'libvorbis' 'libogg' 'portaudio' 'libsndfile')
optdepends=('pulseaudio')
makedepends=('gcc' 'make')
install=QMPlay.install

build()
{
	cd $pkgdir

	mkdir -p usr/share/applications/
	mkdir -p usr/share/pixmaps/
	mkdir -p usr/bin/
	mkdir opt/

	ln -s ../../opt/qmplay/qmplay $pkgdir/usr/bin/qmplay

	cd $srcdir
	if [ $PWD != $srcdir ]; then
		echo "Error"
		return 1
	fi
	rm -rf *
	wget "http://sourceforge.net/projects/zaps166/files/QMPlay/src/QMPlay-$pkgver.tar.bz2/download" -O qmplay
	tar xf qmplay
	if [ $? != 0 ]; then
		echo "Can't unpack archive, exiting... ;("
		return 1
	fi
	cd "QMPlay"
	./compile_unix
	if [ $? != 0 ]; then
		echo "There are errors, exiting... ;("
		return 1
	fi
	rm -rf qmplay/install
	mv qmplay $pkgdir/opt/

	cp src/qmp_lib/icons/play_64x64.png $pkgdir/usr/share/pixmaps/QMPlay.png
	cp src/qmplay/Unix/install/QMPlay.desktop $pkgdir/usr/share/applications/
	cp src/qmplay/Unix/install/QMPlay_enqueue.desktop $pkgdir/usr/share/applications/
	cp src/qmplay/Unix/install/qplst-qplst.xml $pkgdir/opt/qmplay/

	cd $pkgdir/opt/qmplay

	touch noautoupdates

	return 0
}
