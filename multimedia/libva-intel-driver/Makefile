# Created by: Manuel Creach <manuel.creach@me.com>
# $FreeBSD$

PORTNAME=	libva-intel-driver
PORTVERSION=	1.3.1
CATEGORIES=	multimedia
MASTER_SITES=	http://www.freedesktop.org/software/vaapi/releases/${PORTNAME}/

MAINTAINER=	manuel.creach@me.com
COMMENT=	VAAPI intel driver

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libva.so:${PORTSDIR}/multimedia/libva
BUILD_DEPENDS=	${LOCALBASE}/include/linux/videodev2.h:${PORTSDIR}/multimedia/v4l_compat

USES=		gmake libtool:keepla pkgconfig tar:bzip2
USE_GL=		gl
USE_AUTOTOOLS=	aclocal autoheader automake autoconf libtoolize
ACLOCAL_ARGS=	-I.
AUTOMAKE_ARGS=	--add-missing
USE_LDCONFIG=	yes

CPPFLAGS+=	-isystem${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

PLIST_FILES=	lib/va/i965_drv_video.so \
		lib/va/i965_drv_video.la

.include <bsd.port.pre.mk>

.if defined(WITH_NEW_XORG)
pre-configure:
.if !exists(${LOCALBASE}/lib/libkms.so)
	@${ECHO} "${PKGNAME}: Rebuild graphics/libdrm with the KMS option enabled."
	@${FALSE}
.endif
.else
IGNORE=		this port needs libdrm version that is available when WITH_NEW_XORG is set
.endif

post-patch:	.SILENT
	${REINPLACE_CMD} -e 's/-ldl//' \
		${WRKSRC}/src/Makefile.am
	${REINPLACE_CMD} -e 's|driverdir|& --define-variable prefix=${PREFIX}|' \
		${WRKSRC}/configure.ac

.include <bsd.port.post.mk>
