PORTNAME=	mt7601u-firmware
PORTVERSION=	1.0
CATEGORIES=	net
MASTER_SITES=	https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/plain/mediatek/
PKGNAMESUFFIX=	-kmod
DISTNAME=	${FWNAME}
EXTRACT_SUFX=

MAINTAINER=	jsm@FreeBSD.org
COMMENT=	Mediatek 7601U IEEE 802.11b/g Firmware Kernel Module
WWW=		https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/

FWNAME=		mt7601u.bin

USES=		kmod uidfix
DRIVERNAME=	mt7601u_fw
FIRMS=		mt7601u.bin
BUILD_WRKSRC=	${WRKSRC}
INSTALL_WRKSRC=	${WRKSRC}
KMODVERSION=	${FWVERSION:C/^(...)$/\1.0/:S/.//g}
PLIST_FILES=	${KMODDIR}/${DRIVERNAME}.ko
CFLAGS+=	-D_KERNEL
do-extract:
	${MKDIR} ${WRKSRC}
	${CP} ${DISTDIR}/${DISTNAME} ${WRKSRC}/
post-patch:
	${ECHO_CMD} "KMOD= ${DRIVERNAME}" > ${WRKSRC}/Makefile
	${ECHO_CMD} "FIRMWS= ${FIRMS:C/:.*//}:${DRIVERNAME}:${KMODVERSION}" >> \
		${WRKSRC}/Makefile
	${ECHO_CMD} ".include <bsd.kmod.mk>" >> \
		${WRKSRC}/Makefile

.include <bsd.port.mk>
