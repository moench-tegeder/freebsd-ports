# Created by: Andrey Slusar <anray@FreeBSD.org>
# $FreeBSD$

PORTNAME=	imagick
DISTVERSION=	3.1.2
PORTREVISION=	1
CATEGORIES=	graphics
MASTER_SITES=	http://pecl.php.net/get/
PKGNAMEPREFIX=	pecl-
EXTRACT_SUFX=	.tgz
DIST_SUBDIR=	PECL

MAINTAINER=	mm@FreeBSD.org
COMMENT=	Provides a wrapper to the ImageMagick/GraphicsMagick library

LICENSE=	PHP301

.if !defined(WITHOUT_X11)
LIB_DEPENDS=	libMagickWand-6.Q*.so:${PORTSDIR}/graphics/ImageMagick
.else
LIB_DEPENDS=	libMagickWand-6.Q*.so:${PORTSDIR}/graphics/ImageMagick-nox11
.endif

USES=		pkgconfig
USE_PHP=	yes
USE_PHPEXT=	yes

CONFIGURE_ARGS=	--with-imagick=${LOCALBASE}

.include <bsd.port.mk>
