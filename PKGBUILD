# Maintainer: Martin Rys <rys.pw/contact>

# Previous maintainers:
#   Brian Li <brian14708@gmail.com>
#   Denys Zariaiev <denys.zariaiev@gmail.com>

pkgname=chitubox-free-bin
pkgver=2.0.0

pkgrel=1
pkgdesc="CHITUBOX Basic - All-in-one SLA/DLP/LCD Slicer"

makedepends=('icoutils')

url="https://www.chitubox.com/download.html"
arch=("x86_64")
license=("Commercial")

# Config
RUNFILE="CHITUBOX_Basic_Linux_Installer_V2.0.run"

options=(!strip)

source=(
	"$pkgname-$pkgver.tar.gz::https://sac.chitubox.com/software/download.do?softwareId=17839&softwareVersionId=v${pkgver}&fileName=CHITUBOX_V${pkgver}.tar.gz"
	"local://chitubox-free.desktop"
	"local://chitubox-free.xml"
)

sha256sums=(
	'0231fd7183342c6ca5395bd738935bb10abb46c1704e2b13aaf3f73ca9ce7b75'
	'376b2b3805788b856b61c77760a736f57d40cc28de6a1b0266efb3e25dea6942'
	'8bd846e6e12e293c8fe9a9c78e59658397dd078e1d697d72cda339ccd6ba06b2'
)

package()
{
	INSTALL_ROOT="${srcdir}/opt/${pkgname}"
	OPT_DIR="${pkgdir}/opt"
	APP_DIR="${OPT_DIR}/${pkgname}"
	
	# Run installer, which unfortunately doesn't run without root privileges. So it's not possible to put the install in build().
	${srcdir}/${RUNFILE} --root "${INSTALL_ROOT}" --accept-licenses --no-size-checking --accept-messages --confirm-command install

	# Little clean up
	rm ${INSTALL_ROOT}/Uninstall*

	# binary data
	install -d "${OPT_DIR}"
	mv "${INSTALL_ROOT}" "${OPT_DIR}/"

	# Extract icon
	icotool --extract "${APP_DIR}/bin/Resources/Image/SoftwareIcon/freeIcon.ico" --output .
	install -Dm644 freeIcon_1_256x256x32.png "${pkgdir}/usr/share/icons/hicolor/256x256/apps/chitubox-free.png"

	# desktop file
	install -Dm644 chitubox-free.desktop "${pkgdir}/usr/share/applications/chitubox-free.desktop"

	# mime/associations - see https://manual.chitubox.com/user-manual-pro/requirements/
	install -Dm644 chitubox-free.xml "${pkgdir}/usr/share/mime/packages/chitubox-free.xml"
}
