# Created by: Gea-Suan Lin <gslin@gslin.org>
# $FreeBSD$

PORTNAME=	sharedance
PORTVERSION=	0.6
PORTREVISION=	3
CATEGORIES=	databases
MASTER_SITES=	http://download.pureftpd.org/pub/sharedance/

MAINTAINER=	gslin@gslin.org
COMMENT=	Daemon to centralize keys and associated data

LIB_DEPENDS=	libevent-2.0.so:${PORTSDIR}/devel/libevent2

CONFIGURE_ARGS=	--with-largefile
GNU_CONFIGURE=	yes
USE_BZIP2=	yes
CFLAGS+=	-I${LOCALBASE}/include/event2/compat \
		-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib/event2

post-patch:
	@${REINPLACE_CMD} -e "s/-levent/-levent-2.0/g" ${WRKSRC}/configure

post-install:
	@${MKDIR} ${STAGEDIR}${DATADIR}
	${INSTALL_SCRIPT} ${WRKSRC}/php/*.php ${STAGEDIR}${DATADIR}

.include <bsd.port.mk>
