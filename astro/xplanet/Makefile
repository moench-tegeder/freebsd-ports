# Created by: darius@dons.net.au
# $FreeBSD$

PORTNAME=	xplanet
PORTVERSION=	1.3.0
PORTREVISION=	4
CATEGORIES=	astro geography
MASTER_SITES=	SF

MAINTAINER=	novel@FreeBSD.org
COMMENT=	Draw pictures of the earth textured by an image

GNU_CONFIGURE=	yes
USES=		iconv
USE_XORG=	xt xscrnsaver
CONFIGURE_ARGS=	--with-map-extension=jpg
CPPFLAGS+=	-I${LOCALBASE}/include
LIBS+=		-L${LOCALBASE}/lib -lm

OPTIONS_DEFINE=	FREETYPE PANGO GIF JPEG PNG PNM TIFF
OPTIONS_DEFAULT= FREETYPE PANGO GIF JPEG PNG PNM TIFF

FREETYPE_CONFIGURE_WITH=	--with-freetype
FREETYPE_LIB_DEPENDS=	libfreetype.so:${PORTSDIR}/print/freetype2
PANGO_CONFIGURE_WITH=	pango
PANGO_USE=	GNOME=pango
GIF_CONFIGURE_WITH=	gif
GIF_LIB_DEPENDS=	libgif.so:${PORTSDIR}/graphics/giflib
JPEG_CONFIGURE_WITH=	jpeg
JPEG_LIB_DEPENDS=	libjpeg.so:${PORTSDIR}/graphics/jpeg
PNG_CONFIGURE_WITH=	png
PNG_LIB_DEPENDS+=	libpng15.so:${PORTSDIR}/graphics/png
PNM_CONFIGURE_WITH=	pnm
PNM_LIB_DEPENDS=	libnetpbm.so:${PORTSDIR}/graphics/netpbm
TIFF_CONFIGURE_WITH=	tiff
TIFF_LIB_DEPENDS=	libtiff.so:${PORTSDIR}/graphics/tiff

post-extract:
	@${REINPLACE_CMD} -e "s/default/default.sample/g" ${WRKSRC}/Makefile.in
	@${REINPLACE_CMD} -e "s/PrintGifError();/GifError();/g" \
		${WRKSRC}/src/libimage/gif.c
	@${MV} ${WRKSRC}/xplanet/config/default ${WRKSRC}/xplanet/config/default.sample

.include <bsd.port.mk>
