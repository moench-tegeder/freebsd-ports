# Created by: bauerm
# $FreeBSD$

PORTNAME=	ntl
PORTVERSION=	6.0.0
CATEGORIES=	math
MASTER_SITES=	http://www.shoup.net/ntl/

MAINTAINER=	bf@FreeBSD.org
COMMENT=	Victor Shoup's Number Theory Library

# ntl is faster with libgmp4, but you can disable it
.if !defined(WITHOUT_GMP)
LIB_DEPENDS=	libgmp.so:${PORTSDIR}/math/gmp

CONFIGURE_ARGS=	NTL_GMP_LIP=on
.endif

USES=		perl5
USE_PERL5=	build
HAS_CONFIGURE=	yes
CONFIGURE_ARGS+=	AR="${AR}" \
		CC="${CC}" CFLAGS="${CFLAGS}" \
		CXX="${CXX}" CXXFLAGS="${CXXFLAGS}" \
		DEF_PREFIX="${LOCALBASE}" \
		LDFLAGS="${LDFLAGS}" NTL_STD_CXX=on \
		PREFIX="${PREFIX}" RANLIB="${RANLIB}"

CFLAGS+=	-fPIC
WRKSRC=		${WRKDIR}/${DISTNAME}/src
MAKEFILE=	makefile

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/include/NTL
	${INSTALL_DATA} ${WRKSRC}/../include/NTL/* ${STAGEDIR}${PREFIX}/include/NTL/
	${INSTALL_DATA} ${WRKSRC}/ntl.a ${STAGEDIR}${PREFIX}/lib/libntl.a

post-install:
.if !defined(NOPORTDOCS)
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/../doc/* ${STAGEDIR}${DOCSDIR}
.endif

test: build
	@(cd ${WRKSRC}; ${SETENV} ${MAKE_ENV} ${MAKE} \
		${MAKE_FLAGS} ${MAKEFILE} ${MAKE_ARGS} check)

.include <bsd.port.mk>
