# Created by: Christophe Labouisse <christophe@labouisse.org>
# $FreeBSD$

PORTNAME=	jdresolve
PORTVERSION=	0.6.1
PORTREVISION=	1
CATEGORIES=	www
MASTER_SITES=	http://www.jdrowell.com/projects/jdresolve/
PATCH_SITES=	${MASTER_SITES}
PATCHFILES=	patch-0.6.2b1.diff

MAINTAINER=	christophe@labouisse.org
COMMENT=	A IP addresse to hostname program for httpd log files

BUILD_DEPENDS=	p5-Net-DNS>=0:${PORTSDIR}/dns/p5-Net-DNS
RUN_DEPENDS:=	${BUILD_DEPENDS}

USES=		perl5
NO_BUILD=	yes

DOC1=	AUTHORS BUGS CHANGELOG COPYING CREDITS INSTALL README TODO

do-install:
.for file in jdresolve rhost
	${INSTALL_SCRIPT} ${WRKSRC}/${file} ${STAGEDIR}${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/${file}.1 ${STAGEDIR}${MAN1PREFIX}/man/man1
.endfor

post-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/share/doc/jdresolve
.for i in ${DOC1}
	${INSTALL_DATA} ${WRKSRC}/${i} ${STAGEDIR}${PREFIX}/share/doc/jdresolve
.endfor

.include <bsd.port.mk>
