# Created by: Pedro Giffuni
# $FreeBSD$

PORTNAME=	CalculiX
PORTVERSION=	2.7
PORTREVISION=	3
CATEGORIES=	cad
MASTER_SITES=	http://www.dhondt.de/
DISTFILES=	${DIST_SOURCES}
.ifdef WITH_EXAMPLES
DISTFILES+=	${DIST_EXAMPLES}
.endif
DIST_SUBDIR=	calculix
EXTRACT_ONLY=	${DIST_SOURCES}
.ifdef WITH_EXAMPLES
EXTRACT_ONLY+=	${DIST_EXAMPLES}
.endif

MAINTAINER=	maho@FreeBSD.org
COMMENT=	Three-Dimensional Structural Finite Element Program

LICENSE=	GPLv2

LIB_DEPENDS=	libarpack.so:${PORTSDIR}/math/arpack	\
		libspooles.so:${PORTSDIR}/math/spooles \
		libtaucs.so:${PORTSDIR}/math/taucs

USE_BZIP2=	yes

DIST_SOURCES=	ccx_${PORTVERSION}.src${EXTRACT_SUFX}	\
		cgx_${PORTVERSION}.all${EXTRACT_SUFX}
DIST_HTM=	ccx_${PORTVERSION}.htm${EXTRACT_SUFX}	\
		cgx_${PORTVERSION}.htm${EXTRACT_SUFX}
DIST_PS=	ccx_${PORTVERSION}.ps${EXTRACT_SUFX}
DIST_PDF=	cgx_${PORTVERSION}.pdf
DIST_EXAMPLES=	ccx_${PORTVERSION}.test${EXTRACT_SUFX}	\
		cgx_${PORTVERSION}.exa${EXTRACT_SUFX}

WRKSRC=		${WRKDIR}/${PORTNAME}
CCX_VER=	ccx_${PORTVERSION}
CGX_VER=	cgx_${PORTVERSION}

USES=		fortran gmake
USE_GCC=	yes
USE_XORG=	xmu
USE_GL=	glut

BROWSER?=	firefox
PSVIEWER?=	gv

OPTIONS_DEFINE= METIS METIS_EDF
OPTIONS_DEFAULT=METIS

.include <bsd.port.options.mk>

.if $(PORT_OPTIONS:MDOCS)
DISTFILES+=	${DIST_HTM} ${DIST_PS} ${DIST_PDF}
EXTRACT_ONLY+=	${DIST_HTM} ccx_${PORTVERSION}.ps${EXTRACT_SUFX}
.endif

.if ${PORT_OPTIONS:MMETIS}
LIB_DEPENDS+= 	libmetis.so:${PORTSDIR}/math/metis4
.endif
.if ${PORT_OPTIONS:MMETIS_EDF}
LIB_DEPENDS+= 	libmetis.so:${PORTSDIR}/math/metis-edf
.endif

.if exists(${LOCALBASE}/lib/libatlas.so) && !defined(WITH_BLAS)
WITH_ATLAS=             yes
.endif
.if defined(WITH_ATLAS)
LIB_DEPENDS+=	libatlas.so:${PORTSDIR}/math/atlas
BLAS_LIBS=	-lf77blas
LAPACK_LIBS=	-lalapack -lcblas
.else
LIB_DEPENDS+=	libblas.so:${PORTSDIR}/math/blas
LIB_DEPENDS+=	liblapack.so:${PORTSDIR}/math/lapack
BLAS_LIBS=	-lblas
LAPACK_LIBS=	-llapack
.endif

.if ${ARCH} == "sparc64"
CFLAGS+=	-fPIC
FFLAGS+=	-fPIC
.else
CFLAGS+=	-fpic
FFLAGS+=	-fpic
.endif

.if !defined(WITH_EXAMPLES)
PLIST_SUB=	WITH_EXAMPLES="@comment "
.else
PLIST_SUB=	WITH_EXAMPLES=""
.endif

.ifndef (WITH_EXAMPLES)
pre-everything::
	@${ECHO} "You can define WITH_EXAMPLES=yes to install example files"
.endif

pre-build:
	@${REINPLACE_CMD} -e 's+%%FC%%+${FC}+g ; s+%%CC%%+${CC}+g ; \
	s+%%BLAS_LIBS%%+${BLAS_LIBS}+ ; \
	s+%%LAPACK_LIBS%%+${LAPACK_LIBS}+ ; \
	s+%%LOCALBASE%%+${LOCALBASE}+g;' \
		${WRKSRC}/${CCX_VER}/src/Makefile
	@${REINPLACE_CMD} -e 's/c++/${CXX}/g;' \
		${WRKSRC}/libSNL/src/makefile
	@${REINPLACE_CMD} -e 's+%%DOCSDIR%%+${DOCSDIR}+g; \
	s+"firefox"+"${BROWSER}"+ ; \
	s+"gv"+"${PSVIEWER}"+ ;' \
		${WRKSRC}/${CGX_VER}/src/cgx.h

do-build:
	@(cd ${WRKSRC}/${CCX_VER}/src; ${SETENV} ${MAKE_ENV} $(GMAKE) )
	@(cd ${WRKSRC}/libSNL/src; ${SETENV} ${MAKE_ENV} $(GMAKE) )
	@(cd ${WRKSRC}/${CGX_VER}/src; ${SETENV} ${MAKE_ENV} $(GMAKE) )

do-install:
	@${INSTALL_PROGRAM} ${WRKSRC}/${CCX_VER}/src/${CCX_VER} \
	  ${STAGEDIR}${PREFIX}/bin/ccx
	@${INSTALL_PROGRAM} ${WRKSRC}/${CGX_VER}/src/cgx \
	  ${STAGEDIR}${PREFIX}/bin/cgx
.if ${PORT_OPTIONS:MDOCS}
	@${MKDIR} ${STAGEDIR}${DOCSDIR}/ccx
	@(cd ${WRKSRC}/${CCX_VER}/doc/ccx && ${COPYTREE_SHARE} . \
	  ${STAGEDIR}${DOCSDIR}/ccx)
	@${MKDIR} ${STAGEDIR}${DOCSDIR}/cgx
	@(cd ${WRKSRC}/${CGX_VER}/doc/cgx && ${COPYTREE_SHARE} . \
	  ${STAGEDIR}${DOCSDIR}/cgx)
	@${INSTALL_DATA} ${WRKSRC}/${CCX_VER}/doc/${CCX_VER}.ps ${STAGEDIR}${DOCSDIR}
	@${GZIP_CMD} ${STAGEDIR}${DOCSDIR}/${CCX_VER}.ps
	@${INSTALL_DATA} ${DISTDIR}/${DIST_SUBDIR}/cgx_${PORTVERSION}.pdf \
	  ${STAGEDIR}${DOCSDIR}
.endif
.ifdef WITH_EXAMPLES
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	@(cd ${WRKSRC}/${CGX_VER}/examples && ${COPYTREE_SHARE} . \
	  ${STAGEDIR}${EXAMPLESDIR})
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}/test
	@(cd ${WRKSRC}/${CCX_VER}/test && ${COPYTREE_SHARE} . \
	  ${STAGEDIR}${EXAMPLESDIR}/test)
.endif

.include <bsd.port.mk>
