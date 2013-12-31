# Maintainer: Neng Xu <neng2.xu2@gmail.com>

pkgname=gnucash-latest
pkgver=2.6.0
pkgrel=1
pkgdesc="A personal and small-business financial-accounting application"
arch=('i686' 'x86_64')
url="http://www.gnucash.org"
license=("GPL")
depends=('gtkhtml' 'slib' 'goffice0.8' 'libgnomeui' 'libdbi-drivers' 'aqbanking' 'desktop-file-utils')
makedepends=('intltool')
optdepends=('evince: for print preview'
            'perl-finance-quote: for stock information lookups'
            'perl-date-manip: for stock information lookups')
options=('!libtool' '!makeflags' '!emptydirs')
conflicts=('gnucash' 'gnucash-devel')
provides=('gnucash')
install=gnucash.install
source=(http://downloads.sourceforge.net/sourceforge/gnucash/gnucash-${pkgver}.tar.bz2)
md5sums=('52edee40b03120d2646a47463f675d9a')

build() {
  cd "${srcdir}/gnucash-${pkgver}"
  ./configure --prefix=/usr --mandir=/usr/share/man --sysconfdir=/etc \
    --libexecdir=/usr/lib --disable-schemas-install --enable-ofx --enable-aqbanking
  make
}

package() {
  cd "${srcdir}/gnucash-${pkgver}"
  make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR="${pkgdir}" install
  cd src/doc/design
  make DESTDIR="${pkgdir}" install-info

  install -dm755 "${pkgdir}/usr/share/gconf/schemas"
  gconf-merge-schema "${pkgdir}/usr/share/gconf/schemas/gnucash.schemas" --domain gnucash "${pkgdir}"/etc/gconf/schemas/*.schemas
  rm -f "${pkgdir}"/etc/gconf/schemas/*.schemas
}
