# Created by: Ying-Chieh Liao <ijliao@FreeBSD.org>
# $FreeBSD$

PORTNAME=	sng
PORTVERSION=	1.0.5
PORTREVISION=	1
CATEGORIES=	graphics
MASTER_SITES=	SF/${PORTNAME}/${PORTVERSION}/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Compiler/decompiler for Scriptable Network Graphics

BUILD_DEPENDS=	${LOCALBASE}/lib/X11/rgb.txt:${PORTSDIR}/x11/rgb
RUN_DEPENDS=	${LOCALBASE}/lib/X11/rgb.txt:${PORTSDIR}/x11/rgb
LIB_DEPENDS=	libpng15.so:${PORTSDIR}/graphics/png

GNU_CONFIGURE=	yes
CFLAGS+=	-I${LOCALBASE}/include/libpng15
LDFLAGS+=	-L${LOCALBASE}/lib
CONFIGURE_ARGS=	--with-png-inc=${LOCALBASE}/include \
		--with-rgbtxt=${LOCALBASE}/lib/X11/rgb.txt

PLIST_FILES=	bin/sng bin/sng_regress man/man1/sng.1.gz

no-pre-patch:
	@${REINPLACE_CMD} -e 's|-static||g' ${WRKSRC}/Makefile.in
	@${REINPLACE_CMD} -e '33,34s|^static ||' ${WRKSRC}/sngd.c

post-install:
	${INSTALL_SCRIPT} ${WRKSRC}/sng_regress ${STAGEDIR}${PREFIX}/bin

.include <bsd.port.mk>
