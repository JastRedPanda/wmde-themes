# Maintainer: WMDE <https://wmde.fun>
#
# The WMDE theme: every default that decides how the desktop looks. Data-only, no Rust
# build - the files are baked by tools/wmde-theme-gen and committed here.
#
# This package is what makes a CLEAN INSTALL and a NEW USER look like WMDE without a
# single line of code having run: cosmic-config reads /usr/share/wmde/<id>/v<N>/<key> as
# the system default whenever the user has no value of their own.
#
# Mandatory on purpose - wmde-desktop depends on it. A stack without it falls back to the
# values compiled into libcosmic, which are upstream COSMIC's and drift on every merge.
pkgname=wmde-themes
pkgver=1.0.0
pkgrel=1
pkgdesc="WMDE theme - the palettes, fonts, metrics, panel, dock and wallpaper defaults"
arch=('any')
url="https://wmde.fun"
license=('GPL-3.0-only')
# No depends: these are data files read through cosmic-config by whichever component
# wants them. The built-in theme points its wallpaper at the image wmde-bg ships, but
# declaring that here would invert the relationship - the theme names a path, it does not
# own the daemon that draws it.
depends=()
makedepends=('just' 'git')
source=("$pkgname::git+https://github.com/Lin-WMDE/wmde-themes.git#branch=wmde")
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/$pkgname"
  # WMDE unified version: 1.5 (libcosmic base) . <commits since nearest tag> . g<short>.
  local desc
  desc=$(git describe --long --tags --abbrev=7 2>/dev/null || true)
  if [ -n "$desc" ]; then
    printf '1.5.%s.g%s' "$(printf '%s' "$desc" | sed -E 's/.*-([0-9]+)-g[0-9a-f]+$/\1/')" "$(git rev-parse --short=7 HEAD)"
  else
    printf '1.5.%s.g%s' "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
  fi
}

package() {
  cd "$srcdir/$pkgname"
  just rootdir="$pkgdir" install
}
