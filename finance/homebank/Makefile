# $FreeBSD$

PORTNAME=	homebank
PORTVERSION=	4.5.6
CATEGORIES=	finance
MASTER_SITES=	http://homebank.free.fr/public/

MAINTAINER=	pawel@FreeBSD.org
COMMENT=	Free, easy, personal accounting for everyone

LICENSE=	GPLv2

LIB_DEPENDS=	libosp.so:${PORTSDIR}/textproc/opensp

GNU_CONFIGURE=	yes
USES=		desktop-file-utils gmake pkgconfig shared-mime-info
USE_GNOME=	gnomehier gtk20
INSTALLS_ICONS=	yes

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib -pthread

PORTDOCS=	AUTHORS ChangeLog NEWS README

OPTIONS_DEFINE=	DOCS OFX
OFX_DESC=	OFX file format support
OPTIONS_DEFAULT=OFX

OFX_CONFIGURE_WITH=	ofx
OFX_LIB_DEPENDS=	libofx.so:${PORTSDIR}/finance/libofx

post-extract:
	@${CHMOD} ${BINMODE} ${WRKSRC}/install-sh

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
