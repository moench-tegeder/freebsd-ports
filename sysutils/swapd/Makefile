# Created by: Yen-Ming Lee <leeym@FreeBSD.org>
# $FreeBSD$

PORTNAME=	swapd
PORTVERSION=	1.0.5
CATEGORIES=	sysutils
MASTER_SITES=	http://www.rkeene.org/files/oss/swapd/

MAINTAINER=	leeym@FreeBSD.org
COMMENT=	A daemon that watches free memory and manages swap files

LIB_DEPENDS=	libstatgrab.so:${PORTSDIR}/devel/libstatgrab

USES=		gmake pkgconfig
GNU_CONFIGURE=	yes

USE_RC_SUBR=	swapd

post-patch:
	@${REINPLACE_CMD} -e "s,%%PREFIX%%,${PREFIX},g" ${WRKSRC}/${CONFIGURE_SCRIPT}

post-install:
.for f in swapd_swapon swapd_swapoff
	${INSTALL_SCRIPT} ${FILESDIR}/${f} ${STAGEDIR}${PREFIX}/sbin
.endfor

.include <bsd.port.mk>
