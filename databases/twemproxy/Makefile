# Created by: Steven Kreuzer <skreuzer@FreeBSD.org>
# $FreeBSD$

PORTNAME=	twemproxy
PORTVERSION=	0.3.0
CATEGORIES=	databases
MASTER_SITES=	GOOGLE_CODE
DISTNAME=	nutcracker-${PORTVERSION}

MAINTAINER=	skreuzer@FreeBSD.org
COMMENT=	Fast, light-weight proxy for memcached and redis

LICENSE=	APACHE20

LIB_DEPENDS=	libexecinfo.so:${PORTSDIR}/devel/libexecinfo

CFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib -lexecinfo

PLIST_FILES=	sbin/nutcracker \
		man/man8/nutcracker.8.gz \
		etc/nutcracker.yml.sample

USE_GCC=	yes
HAS_CONFIGURE=	yes

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/src/nutcracker ${STAGEDIR}${PREFIX}/sbin
	${INSTALL_MAN} ${WRKSRC}/man/nutcracker.8 ${STAGEDIR}${MANPREFIX}/man/man8/
	${INSTALL_DATA} ${WRKSRC}/conf/nutcracker.yml ${STAGEDIR}${PREFIX}/etc/nutcracker.yml.sample

.include <bsd.port.mk>
