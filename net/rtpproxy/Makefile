# Created by: sobomax
# $FreeBSD$

PORTNAME=	rtpproxy
PORTVERSION=	1.2.1
PORTREVISION=	1
CATEGORIES=	net
MASTER_SITES=	http://www.rtpproxy.org/chrome/site/

MAINTAINER=	sobomax@FreeBSD.org
COMMENT=	High-performance RTP proxy server for the SIP Express Router (SER)

LIB_DEPENDS=	gsm.1:${PORTSDIR}/audio/gsm

GNU_CONFIGURE=	yes
CPPFLAGS+=	-I${LOCALBASE}/include
LIBS+=		-L${LOCALBASE}/lib
MAN8=		rtpproxy.8

USERS=		${PORTNAME}
GROUPS=		${PORTNAME}

NO_STAGE=	yes
post-build:
	${SED} 's|%%PREFIX%%|${PREFIX}|g ; s|%%RC_SUBR%%|/etc/rc.subr|g' \
	    ${WRKSRC}/freebsd/rtpproxy.in > ${WRKDIR}/rtpproxy

post-install:
	${INSTALL_SCRIPT} ${WRKDIR}/rtpproxy ${PREFIX}/etc/rc.d/rtpproxy

.include <bsd.port.mk>
