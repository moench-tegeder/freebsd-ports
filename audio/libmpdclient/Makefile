# Created by: Grzegorz Blach <gblach@FreeBSD.org>
# $FreeBSD$

PORTNAME=	libmpdclient
PORTVERSION=	2.9
CATEGORIES=	audio
MASTER_SITES=	http://www.musicpd.org/download/libmpdclient/2/

MAINTAINER=	gblach@FreeBSD.org
COMMENT=	API library for interfacing MPD

GNU_CONFIGURE=	yes
USES=		tar:xz gmake pathfix
USE_LDCONFIG=	yes

OPTIONS_DEFINE=	DOCS

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MDOCS}
BUILD_DEPENDS+=	doxygen:${PORTSDIR}/devel/doxygen
.else
CONFIGURE_ARGS=	--disable-documentation
.endif

.include <bsd.port.mk>
