# Created by: trasz <trasz@pin.if.uz.zgora.pl>
# $FreeBSD$

PORTNAME=	hexter
PORTVERSION=	1.0.2
PORTREVISION=	1
CATEGORIES=	audio
MASTER_SITES=	SF/dssi/${PORTNAME}/${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	DSSI softsynth that models the sound generation of a Yamaha DX7

LICENSE=	GPLv2

LIB_DEPENDS=	libdssialsacompat.so:${PORTSDIR}/audio/libdssialsacompat \
		liblo.so:${PORTSDIR}/audio/liblo \
		libjack.so:${PORTSDIR}/audio/jack
BUILD_DEPENDS=	${LOCALBASE}/include/dssi.h:${PORTSDIR}/audio/dssi

USES=		gmake pkgconfig
GNU_CONFIGURE=	yes
USE_GNOME=	gtk20

PORTDOCS=	AUTHORS ChangeLog README
OPTIONS_DEFINE=	DOCS

post-patch:
	@${REINPLACE_CMD} -e 's|-finline-limit=5000||' ${WRKSRC}/configure

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/dssi/hexter.so

	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
