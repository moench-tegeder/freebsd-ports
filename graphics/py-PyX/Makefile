# Created by: Ying-Chieh Liao <ijliao@FreeBSD.org>
# $FreeBSD$

PORTNAME=	PyX
PORTVERSION=	0.13
CATEGORIES=	graphics python
MASTER_SITES=	SF
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	mva@FreeBSD.org
COMMENT=	Python package for creating encapsulated PostScript figures

LICENSE=	GPLv2

USE_PYTHON=		3
USE_PYDISTUTILS=	yes
PYDISTUTILS_AUTOPLIST=	yes
USE_TEX=	latex:build

OPTIONS_DEFINE=		T1CODE KPATHSEA
OPTIONS_DEFAULT=	T1CODE KPATHSEA
T1CODE_DESC=		Fast t1 font encoding/decoding
KPATHSEA_DESC=		Python wrapper around kpathsea

T1CODE_CFLAGS=		-I${LOCALBASE}/include
KPATHSEA_CFLAGS=	-I${LOCALBASE}/include
KPATHSEA_LDFLAGS=	-L${LOCALBASE}/lib

.include <bsd.port.options.mk>

post-patch:
.if ${PORT_OPTIONS:MT1CODE}
	@${REINPLACE_CMD} -e 's|build_t1code=0|build_t1code=1|' ${WRKSRC}/setup.cfg
.endif
.if ${PORT_OPTIONS:MKPATHSEA}
	@${REINPLACE_CMD} -e 's|build_pykpathsea=0|build_pykpathsea=1|' ${WRKSRC}/setup.cfg
.endif

.include <bsd.port.mk>
