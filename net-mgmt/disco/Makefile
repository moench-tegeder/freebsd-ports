# Created by: Kirill Ponomarew <ponomarew@oberon.net>
# $FreeBSD$

PORTNAME=	disco
PORTVERSION=	1.2
PORTREVISION=	1
CATEGORIES=	net-mgmt
MASTER_SITES=	SF/${PORTNAME}ipd/DISCO/${PORTNAME}-${PORTVERSION}.tar.gz

MAINTAINER=	jadawin@FreeBSD.org
COMMENT=	IP discovery and fingerprinting utility

GNU_CONFIGURE=	yes
CPPFLAGS+=	-I${LOCALBASE}/include
LIBS+=		-L${LOCALBASE}/lib

WRKSRC=		${WRKDIR}/${PORTNAME}

PLIST_FILES=	bin/disco bin/disco.fp

OPTIONS_DEFINE=	DOCS

.include <bsd.port.options.mk>

post-install:
.if ! ${PORT_OPTIONS:MDOCS}
	${MKDIR} ${STAGEDIR}${DOCSDIR}
.for i in README
	${INSTALL_DATA} ${WRKSRC}/${i} ${STAGEDIR}${DOCSDIR}
.endfor
.endif

.include <bsd.port.mk>
