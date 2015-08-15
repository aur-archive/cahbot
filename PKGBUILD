pkgname=cahbot
pkgver=20130117
pkgrel=1
pkgdesc="An IRC bot which lets you play Card Against Humanity. Written in Nimrod."
arch=(i686 x86_64)
url="https://github.com/dom96/c4hbot"
license=("BSD")
makedepends=(nimrod git)
_gitroot="https://github.com/dom96/c4hbot.git"
_gitname="c4hbot"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  nimrod c -d:release cahbot.nim
}

package() {
  cd "$srcdir/$_gitname-build"
  mkdir -p "$pkgdir/usr/bin"
  install -Dm755 "cahbot" "$pkgdir/opt/cahbot/cahbot"
  install -Dm644 "decks/default.deck" "$pkgdir/opt/cahbot/decks/default.deck"
  ln -s "/opt/cahbot/cahbot" "$pkgdir/usr/bin/cahbot"
}
