# Created by: Oliver Braun <obraun@informatik.unibw-muenchen.de>
# $FreeBSD$

PORTNAME=	nhc98
PORTVERSION=	1.18
PORTREVISION=	2
CATEGORIES=	lang haskell
MASTER_SITES=	ftp://ftp.cs.york.ac.uk/pub/haskell/${PORTNAME}/
DISTFILES=	${PORTNAME}src-${PORTVERSION}${EXTRACT_SUFX} ${PORTNAME}-${PORTVERSION}-library-interfaces${EXTRACT_SUFX}
DIST_SUBDIR=	nhc98
PATCH_SITES=	${MASTER_SITES}
PATCHFILES=	patch-1.18-newtype

MAINTAINER=	haskell@FreeBSD.org
COMMENT=	A fully-fledged compiler for Haskell 98

ONLY_FOR_ARCHS=	i386

WRKSRC=		${WRKDIR}/${PORTNAME}-${PORTVERSION}

USES=		gmake
HAS_CONFIGURE=	yes
CONFIGURE_ARGS+=--prefix=${PREFIX} --buildwith=gcc

OPTIONS_DEFINE=		DOCS
OPTIONS_DEFAULT=	DOCS

NO_STAGE=	yes
.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MDOCS}
CONFIGURE_ARGS+=	--docdir=${DOCSDIR} +docs
.else
CONFIGURE_ARGS+=	-docs
.endif

MAN1=		harch.1 hmake.1 hp2graph.1 nhc98.1 hi.1

CONFLICTS=	hs-hmake-[0-9]* hs-cpphs-[0-9]*

post-patch:
	@${REINPLACE_CMD} -e 's|-O3|${CFLAGS}|' ${WRKSRC}/Makefile.inc
	@${REINPLACE_CMD} -e 's|$$(CC)|gcc|g' ${WRKSRC}/Makefile

post-configure:
	@${ECHO} "LIBDIR=${PREFIX}/lib/nhc98" \
		>> ${WRKSRC}/targets/ix86-FreeBSD/config.cache

post-install:
	${SED} -e "s#/usr/doc/nhc98#${PREFIX}/share/doc/nhc98#" \
	       < ${WRKSRC}/man/nhc98.1 > ${WRKSRC}/man/nhc98.1.fix
	${INSTALL_MAN} ${WRKSRC}/man/nhc98.1.fix ${PREFIX}/man/man1/nhc98.1
	${RM} ${WRKSRC}/man/nhc98.1.fix
.if ${PORT_OPTIONS:MDOCS}
.for directory in . bugs examples hmake implementation-notes libs
	${RM} -r ${DOCSDIR}/${directory}/CVS
.endfor
.endif

.include <bsd.port.mk>
