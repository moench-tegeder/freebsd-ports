# Created by: Martin Matuska <mm@FreeBSD.org>
# $FreeBSD$

PORTNAME=	binutils
PORTVERSION=	2.24
CATEGORIES=	devel
MASTER_SITES=	${MASTER_SITE_SOURCEWARE}
MASTER_SITE_SUBDIR=	binutils/releases

MAINTAINER=	zeising@FreeBSD.org
COMMENT=	GNU binary tools

LICENSE=	GPLv3 LGPL3
LICENSE_COMB=	multi

BUILD_DEPENDS=	${LOCALBASE}/lib/libgmp.so:${PORTSDIR}/math/gmp \
		${LOCALBASE}/lib/libmpfr.so:${PORTSDIR}/math/mpfr

CONFLICTS=	libbfd-[0-9]*

OPTIONS_DEFINE=	NLS

LICENSE_FILE_GPLv3=	${WRKSRC}/COPYING3
LICENSE_FILE_LGPL3=	${WRKSRC}/COPYING3.LIB

USES=		bison tar:bzip2 gmake
GNU_CONFIGURE=	yes

CFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
CONFIGURE_ARGS+=	--with-system-zlib \
			--with-sysroot=/ \
			--disable-werror \
			--with-gmp=${LOCALBASE} \
			--with-mpfr=${LOCALBASE}

INFO=		as \
		binutils \
		standards \
		gprof \
		bfd \
		configure \
		ld

.include <bsd.port.options.mk>

# Actual earliest version may differ slightly
.if ${ARCH} != ia64 && ${OSVERSION} >= 900044
CONFIGURE_ARGS+=	--enable-gold --enable-plugins
PLIST_SUB+=	GOLD=""
.else
PLIST_SUB+=	GOLD="@comment "
.endif

.if ${PORT_OPTIONS:MNLS}
USES+=		gettext
PLIST_SUB+=	NLS=""
.else
CONFIGURE_ARGS+=	--disable-nls
PLIST_SUB+=	NLS="@comment "
.endif

.if ${ARCH} == "amd64"
CONFIGURE_TARGET=	x86_64-portbld-freebsd${OSREL}
.else
CONFIGURE_TARGET=	${ARCH}-portbld-freebsd${OSREL}
.endif

post-install:
.if ${OSVERSION} >= 900044
	${INSTALL_DATA} ${WRKSRC}/include/plugin-api.h ${STAGEDIR}${PREFIX}/include/
.endif
	@${FIND} -ds ${STAGEDIR}${PREFIX}/${CONFIGURE_TARGET} ! -type d | \
		${SED} -e 's,^${STAGEDIR}${PREFIX}/,,' >> ${TMPPLIST}
	@${FIND} -ds ${STAGEDIR}${PREFIX}/${CONFIGURE_TARGET} -type d | \
		${SED} -e 's,^${STAGEDIR}${PREFIX}/,@dirrm ,' >> ${TMPPLIST}
	${RM} ${STAGEDIR}${PREFIX}/include/ansidecl.h

.include <bsd.port.mk>
