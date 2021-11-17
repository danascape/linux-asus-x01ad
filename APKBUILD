# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm64/configs/(CHANGEME!)

pkgname=linux-asus-x01ad
pkgver=4.9.267
pkgrel=0
pkgdesc="Asus Max M2 kernel fork"
arch="aarch64"
_carch="arm64"
_flavor="asus-x01ad"
url="https://kernel.org"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="
	bash
	bc
	bison
	devicepkg-dev
	flex
	openssl-dev
	perl
"

# Source
_repository="android_kernel_asus_X01AD"
_commit="c3e365429f70ec6fea174ef0f92437283abcb938"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/LineageOS/$_repository/archive/$_commit.tar.gz
	$_config
	always-boot-to-initramfs.patch
"
builddir="$srcdir/$_repository-$_commit"
_outdir="out"

prepare() {
	default_prepare
	. downstreamkernel_prepare
}

build() {
	unset LDFLAGS
	make O="$_outdir" ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
	downstreamkernel_package "$builddir" "$pkgdir" "$_carch" "$_flavor" "$_outdir"
}

sha512sums="
3c6e12d7050fc9bd89b252b753ae1d78c5fbdcb1bf510b27c5fc5e609afc8588b3ef9cc6ac4f5ec799f5e80df0b41a7c73656d9efb9c1eaa77f1a5ce464c13ed  linux-asus-x01ad-c3e365429f70ec6fea174ef0f92437283abcb938.tar.gz
9bdd094214fbfb5a5720896b7ce846874500eb2c7186b17ca36e4fc9aa0794f66cacbb03c6279a47bcef667788a735cbc8b816f14662e9096d7fcbc138c60c48  config-asus-x01ad.aarch64
8c10d536075009ef3fc636db50c706820751eebf8c581c06e16f2e68776b73e7c2369fcfc0c7bbb7f4be462df39fd82234efaacd7654de96367aaf117a98fd5a  always-boot-to-initramfs.patch
"
