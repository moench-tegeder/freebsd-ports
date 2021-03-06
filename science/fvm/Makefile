# Created by: thierry@pompo.net
# $FreeBSD$

PORTNAME=	fvm
PORTVERSION=	0.15.3
PORTREVISION=	6
CATEGORIES=	science parallel
MASTER_SITES=	http://research.edf.com/fichiers/fckeditor/Commun/Innovation/logiciels/code_saturne/Releases/
DISTNAME=	${PORTNAME}-${PORTVERSION:S/.//g}

MAINTAINER=	thierry@FreeBSD.org
COMMENT=	Code_Saturne Finite Volume Mesh

LICENSE=	LGPL21

LIB_DEPENDS=	libmed.so:${PORTSDIR}/french/med	\
		libbft.so:${PORTSDIR}/science/bft	\
		libhdf5.so:${PORTSDIR}/science/hdf5	\
		libcgns.so:${PORTSDIR}/science/cgnslib

WRKSRC=		${WRKDIR}/${PORTNAME}-${PORTVERSION}

USES=		zip
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-bft=${LOCALBASE}	\
		--with-hdf5=${LOCALBASE}	\
		--with-cgns=${LOCALBASE}	\
		--with-med=${LOCALBASE}
CONFIGURE_ENV=	PTHREAD_LIBS=${PTHREAD_LIBS}

.if defined(WITH_LAM)
BUILD_DEPENDS+=	${LOCALBASE}/lib/liblam.a:${PORTSDIR}/net/lam
RUN_DEPENDS+=	${LOCALBASE}/bin/lamboot:${PORTSDIR}/net/lam
CONFIGURE_ARGS+=	--with-mpi=${LOCALBASE}
.elif defined(WITH_OPENMPI)
BUILD_DEPENDS+=	${LOCALBASE}/mpi/openmpi/bin/mpicc:${PORTSDIR}/net/openmpi
RUN_DEPENDS+=	${LOCALBASE}/mpi/openmpi/bin/mpirun:${PORTSDIR}/net/openmpi
CONFIGURE_ARGS+=	--with-mpi=${LOCALBASE}/mpi/openmpi
.else
BUILD_DEPENDS+=	${LOCALBASE}/bin/mpicc:${PORTSDIR}/net/mpich2
RUN_DEPENDS+=	${LOCALBASE}/bin/mpirun:${PORTSDIR}/net/mpich2
CONFIGURE_ARGS+=	--with-mpi=${LOCALBASE}
.endif

.if defined(WITH_DEBUG)
CONFIGURE_ARGS+=	--enable-debug
.endif

TESTSBIN=	fvm_file_test fvm_interface_test fvm_selector_postfix_test fvm_selector_test

pre-configure:
	${REINPLACE_CMD} -e 's|-lmpich|-lmpich -lmpl|'	\
		${WRKSRC}/${CONFIGURE_SCRIPT}
	# No useful doc there
	${REINPLACE_CMD} -e 's|tests doc|tests|' ${WRKSRC}/Makefile.in

regression-test:
.for pg in ${TESTSBIN}
	(cd ${WRKSRC}/tests; ./${pg})
.endfor

.include <bsd.port.mk>
