# Created by: Yen-Ming Lee <leeym@FreeBSD.org>
# $FreeBSD$

PORTNAME=	autossh
PORTVERSION=	1.4c
CATEGORIES=	security
MASTER_SITES=	http://www.harding.motd.ca/autossh/
EXTRACT_SUFX=	.tgz

MAINTAINER=	leeym@FreeBSD.org
COMMENT=	Automatically restart SSH sessions and tunnels

GNU_CONFIGURE=	yes

PORTDOCS=	CHANGES README

post-patch:
	@${REINPLACE_CMD} -e 's,cp autossh.1 ,$$\{BSD_INSTALL_MAN\} autossh.1 ,g' ${WRKSRC}/${MAKEFILE}.in
	@${REINPLACE_CMD} -e 's,cp autossh ,$$\{BSD_INSTALL_PROGRAM\} autossh ,g' ${WRKSRC}/${MAKEFILE}.in
	@${REINPLACE_CMD} -e 's,cp ,$$\{BSD_INSTALL_DATA\} ,g' ${WRKSRC}/${MAKEFILE}.in
.if defined(NOPORTDOCS)
	@${REINPLACE_CMD} -Ee '/doc/d' ${WRKSRC}/${MAKEFILE}.in
.endif

.include <bsd.port.mk>
