# Created by: J.R. Oldroyd <fbsd@opal.com>
# $FreeBSD$

PORTNAME=	kaa-metadata
PORTVERSION=	0.7.7
PORTREVISION=	10
CATEGORIES=	multimedia python
MASTER_SITES=	SF/freevo/${PORTNAME}/${PORTVERSION}
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	fbsd@opal.com
COMMENT=	Kaa Media Repository - media file metadata parser

LIB_DEPENDS=	libdvdread.so:${PORTSDIR}/multimedia/libdvdread
BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}kaa-base>0:${PORTSDIR}/multimedia/py-kaa-base \
		${PYTHON_PKGNAMEPREFIX}exiv2>0:${PORTSDIR}/graphics/py-exiv2
RUN_DEPENDS:=	${BUILD_DEPENDS}

USE_PYTHON=	2
USE_PYDISTUTILS=	yes
PYDISTUTILS_AUTOPLIST=	yes

CFLAGS+=	-I${PREFIX}/include
LDFLAGS+=	-L${PREFIX}/lib

.include <bsd.port.mk>
