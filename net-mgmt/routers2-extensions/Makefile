# Created by: Xavier Beaudouin <kiwi@oav.net>
# $FreeBSD$

PORTNAME=	routers2-extensions
PORTVERSION=	2.19
PORTREVISION=	2
CATEGORIES=	net-mgmt
MASTER_SITES=	http://www.steveshipway.org/software/rrd/ \
		ftp://ftp.oav.oav.net/routers2/
DISTNAME=	routers2-v${PORTVERSION}

MAINTAINER=	kiwi@oav.net
COMMENT=	Extensions of routers2 frontend

RUN_DEPENDS=	${LOCALBASE}/www/routers2/routers2.cgi:${PORTSDIR}/net-mgmt/routers2 \
		p5-Net-Telnet-Cisco>=0:${PORTSDIR}/net-mgmt/p5-Telnet-Cisco \
		${LOCALBASE}/bin/htmldoc:${PORTSDIR}/textproc/htmldoc

WRKSRC=		${WRKDIR}/routers2-v${PORTVERSION}/extensions

USES=		perl5

NO_BUILD=	YES

NO_STAGE=	yes
post-patch:
	for file in *.cgi ; do \
		${REINPLACE_CMD} -e 's|%%LOCALBASE%%|${LOCALBASE}|' ${WRKSRC}/$$file; \
	done

do-install:
		${MKDIR} -m 755 ${PREFIX}/www/routers2/extensions

.if !defined(NOPORTDOCS)
		${MKDIR} -m 755 ${DOCSDIR}
		for file in README *.txt extension.cgi.pl; do \
			${INSTALL_DATA} ${WRKSRC}/$$file ${DOCSDIR}; \
		done
.endif
		for file in *.cgi; do \
			${INSTALL_SCRIPT} ${WRKSRC}/$$file ${PREFIX}/www/routers2/extensions; \
		done

.include <bsd.port.mk>
