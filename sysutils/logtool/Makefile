# Created by: Ying-Chieh Liao <ijliao@csie.nctu.edu.tw>
# $FreeBSD$

PORTNAME=	logtool
PORTVERSION=	1.3.1
CATEGORIES=	sysutils
MASTER_SITES=	http://xjack.org/logtool/download/

MAINTAINER=	dhn@FreeBSD.org
COMMENT=	Parse ASCII logfiles into ANSI, CSV, HTML formats

USES=		gmake

GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--sysconfdir=${PREFIX}/etc/${PORTNAME}

PKGMESSAGE=	${WRKDIR}/pkg-message

MAN1=		logtool.1
DOCS=		CHANGES CREDITS README TODO doc/logtool.txt

NO_STAGE=	yes
do-build:
	cd ${WRKSRC}/src && ${GMAKE} INCLUDES="${CPPFLAGS}"

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/src/logtool ${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/doc/logtool.1 ${MANPREFIX}/man/man1
	@${MKDIR} ${EXAMPLESDIR} ${EXAMPLESDIR}/scripts
	${INSTALL_DATA} ${WRKSRC}/conf/* ${EXAMPLESDIR}
	@${RM} ${EXAMPLESDIR}/logtool.conf.in
	${INSTALL_DATA} ${WRKSRC}/scripts/* ${EXAMPLESDIR}/scripts
.if !defined(NOPORTDOCS)
	@${MKDIR} ${DOCSDIR}
	cd ${WRKSRC} && ${INSTALL_DATA} ${DOCS} ${DOCSDIR}
.endif
	@${SED} -e 's!PREFIX!${PREFIX}!' ${.CURDIR}/pkg-message > ${PKGMESSAGE}
	${CAT} ${PKGMESSAGE}

.include <bsd.port.mk>
