# Created by: lbartoletti <coder@tuxfamily.org>
# $FreeBSD$

PORTNAME=	freexl
DISTVERSION=	1.0.0g
CATEGORIES=	textproc
MASTER_SITES=	http://www.gaia-gis.it/gaia-sins/freexl-sources/

MAINTAINER=	coder@tuxfamily.org
COMMENT=	Library to extract valid data from within an Excel (.xls) spreadsheet

GNU_CONFIGURE=	yes
USES=		iconv gmake

CFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib ${ICONV_LIB}
CONFIGURE_ARGS+=CFLAGS="${CFLAGS}" LDFLAGS="${LDFLAGS}"
USE_LDCONFIG=	yes

post-patch:
	@${REINPLACE_CMD} -e 's|(libdir)/pkgconfig|(prefix)/libdata/pkgconfig|g' \
		${WRKSRC}/Makefile.in

.include <bsd.port.mk>
