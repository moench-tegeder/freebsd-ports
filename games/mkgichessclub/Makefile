# Created by: Nicola Vitale	<nivit@FreeBSD.org>
# $FreeBSD$

PORTNAME=	mkgichessclub
PORTVERSION=	2.2.0
#PORTREVISION=	0
CATEGORIES=	games
MASTER_SITES=	SF
DISTNAME=	MKGIChessClub-${PORTVERSION}

MAINTAINER=	nivit@FreeBSD.org
COMMENT=	Chess playing server with a pure web interface

OPTIONS_DEFINE=	GNUCHESS PHALANX
GNUCHESS_DESC=	Install gnuchess robot
PHALANX_DESC=	Install phalanx robot

OPTIONS_DEFAULT=	GNUCHESS PHALANX

NO_BUILD=	yes

SUB_FILES=	pkg-message

USE_MYSQL=	server
USE_PHP=	mysql pcre session
USE_PYTHON=	yes
GNUCHESS_RUN_DEPENDS=	gnuchess:${PORTSDIR}/games/gnuchess
PHALANX_RUN_DEPENDS=	phalanx:${PORTSDIR}/games/phalanx

WRKSRC=	${WRKDIR}/MKGIChessClub-${PORTVERSION}

.include <bsd.port.options.mk>

do-install:
	${MKDIR} ${STAGEDIR}${DATADIR}; cd ${WRKSRC}; \
	${INSTALL_DATA} database/* ${STAGEDIR}${DATADIR}; \
	${MKDIR} ${STAGEDIR}${WWWDIR}; cd www; ${CP} -R . ${STAGEDIR}${WWWDIR}

.if ${PORT_OPTIONS:MDOCS}
	${MKDIR} ${STAGEDIR}${DOCSDIR}; \
	${INSTALL_DATA} ${WRKSRC}/README.INSTALL ${STAGEDIR}${DOCSDIR}
.endif

.include <bsd.port.mk>
