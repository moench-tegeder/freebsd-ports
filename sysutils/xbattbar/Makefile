# Created by: sumikawa
# $FreeBSD$

PORTNAME=	xbattbar
PORTVERSION=	1.4.2
PORTREVISION=	7
CATEGORIES=	sysutils
MASTER_SITES=	http://iplab.aist-nara.ac.jp/member/suguru/
DISTNAME=	${PORTNAME}_${PORTVERSION}

MAINTAINER=	sumikawa@FreeBSD.org
COMMENT=	Simple battery meter

USES=		imake
USE_XORG=	x11 xext
WRKSRC=		${WRKDIR}/xbattbar-${PORTVERSION}
PLIST_FILES=	bin/xbattbar \
		man/man1/xbattbar.1.gz

.include <bsd.port.mk>
