pkgname=perl-gtk3-imageview
_pkgname=perl-gtk3-imageview
_gituser=carygrave
_gitname=gtk3-imageview
pkgver=10.r4.g984cafa
pkgrel=1
pkgdesc="Image viewer widget for Gtk3"
arch=('i686' 'x86_64')
url="https://metacpan.org/release/Gtk3-ImageView"
license=('LGPL')
depends=('imagemagick' 'perl-gtk3')
makedepends=('git')
options=('!emptydirs')
conflicts=($_pkgname)
provides=($_pkgname)
source=('perl-gtk3-imageview::git+https://github.com/carygravel/gtk3-imageview.git')
md5sums=('SKIP')

pkgver() {
  cd "$_pkgname"
  ( set -o pipefail
    git describe --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build() {
  cd $_pkgname
  PERL_MM_USE_DEFAULT=1 perl Makefile.PL INSTALLDIRS=vendor
  make
}

_perl_depends() {
# template start; name=perl-binary-module-dependency; version=1;
if [[ $(find "$pkgdir/usr/lib/perl5/" -name "*.so") ]]; then
	_perlver_min=$(perl -e '$v = $^V->{version}; print $v->[0].".".($v->[1]);')
	_perlver_max=$(perl -e '$v = $^V->{version}; print $v->[0].".".($v->[1]+1);')
	depends+=("perl>=$_perlver_min" "perl<$_perlver_max")
fi
# template end;
}

package() {
  cd $_pkgname
  make DESTDIR="$pkgdir" install
  find "$pkgdir" -name '.packlist' -delete
  find "$pkgdir" -name '*.pod' -delete
  _perl_depends
}
