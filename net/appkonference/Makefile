# Created by: Alex Deiter <Alex.Deiter@Gmail.COM>
# $FreeBSD$

PORTNAME=	appkonference
PORTVERSION=	2.1
CATEGORIES=	net
MASTER_SITES=	SF

MAINTAINER=	alex.deiter@gmail.com
COMMENT=	High-performance Asterisk voice/video conferencing plugin

BUILD_DEPENDS=	asterisk:${PORTSDIR}/net/asterisk
RUN_DEPENDS=	asterisk:${PORTSDIR}/net/asterisk

USE_CSTD=	gnu89
USES=		gmake
WRKSRC=		${WRKDIR}/${PORTNAME}/konference

PLIST_FILES=	lib/asterisk/modules/app_konference.so

ONLY_FOR_ARCHS=		amd64 arm i386 ia64
ONLY_FOR_ARCHS_REASON=	not yet ported to this architecture

NO_STAGE=	yes
.include <bsd.port.mk>
