# Created by: issei <issei@jp.FreeBSD.org>
# $FreeBSD$

PORTNAME=	xchadance
PORTVERSION=	1.0
PORTREVISION=	2
CATEGORIES=	games
MASTER_SITES=	ftp://ftp.mk.bsdclub.org/pub/FreeBSD/distfiles/
DISTFILES=	xchada01.lzh

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Display a dancing girl "ChaCha."

USES=		lha
USE_XORG=	x11
MAKEFILE=	makefile
NO_WRKSUBDIR=	yes

RESTRICTED=	'contains commercial character data'

post-patch:
	@cd ${WRKSRC}; \
	${PATCH} < ${WRKSRC}/xchada01.bug

post-install:
.if !defined(NOPORTOCS)
	@${MKDIR} ${STAGEDIR}${PREFIX}/share/doc/xchadance
	@${INSTALL_DATA} ${WRKSRC}/README.jp ${STAGEDIR}${PREFIX}/share/doc/xchadance
	@${INSTALL_DATA} ${WRKSRC}/README.eng ${STAGEDIR}${PREFIX}/share/doc/xchadance
.endif

.include <bsd.port.mk>
