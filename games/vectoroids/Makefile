# Created by: Kris Kennaway <kris@FreeBSD.org>
# $FreeBSD$

PORTNAME=	vectoroids
PORTVERSION=	1.1.0
PORTREVISION=	15
CATEGORIES=	games
MASTER_SITES=	ftp://ftp.tuxpaint.org/unix/x/vectoroids/src/

MAINTAINER=	games@FreeBSD.org
COMMENT=	Vector-based rock-shooting game similar to Asteroids

LICENSE=	GPLv2

USES=		gmake
USE_SDL=	image mixer sdl

PORTDOCS=	CHANGES.txt README.txt
OPTIONS_DEFINE=	DOCS

DESKTOP_ENTRIES="Vectoroids" "" "${PORTNAME}" \
		"${PORTNAME}" "Game;ArcadeGame;" ""

post-patch:
	@${FIND} ${WRKDIR} -name .xvpics | ${XARGS} ${RM} -fr

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/
.for d in images music sounds
	@(cd ${WRKSRC}/data && ${COPYTREE_SHARE} ${d} ${STAGEDIR}${DATADIR})
.endfor
	${LN} -sf ${DATADIR}/images/icon.png \
		${STAGEDIR}${PREFIX}/share/pixmaps/${PORTNAME}.png
	${INSTALL_MAN} ${WRKSRC}/${PORTNAME}.6 ${STAGEDIR}${MAN6PREFIX}/man/man6/

	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
