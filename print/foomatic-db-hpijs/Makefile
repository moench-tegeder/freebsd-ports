# Created by: Michael Nottebrock <lofi@FreeBSD.org>
# $FreeBSD$

PORTNAME=	foomatic-db-hpijs
PORTVERSION=	1.4
CATEGORIES=	print
MASTER_SITES=	${MASTER_SITE_LOCAL}
MASTER_SITE_SUBDIR=lofi
DISTNAME=	${PORTNAME}-${PORTVERSION}-1

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Foomatic data for the HPIJS printer drivers

BUILD_DEPENDS=	${LOCALBASE}/share/foomatic/db/oldprinterids:${PORTSDIR}/print/foomatic-db
RUN_DEPENDS=	${LOCALBASE}/share/foomatic/db/oldprinterids:${PORTSDIR}/print/foomatic-db

GNU_CONFIGURE=	yes
USES=		gmake

post-patch:
	${REINPLACE_CMD} -e 's|%%PREFIX%%|${PREFIX}|g' \
			 -e 's|%%LOCALBASE%%|${LOCALBASE}|g' ${WRKSRC}/configure

.include <bsd.port.mk>
