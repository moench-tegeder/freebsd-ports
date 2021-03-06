# $FreeBSD$

PORTNAME=	open-motif
PORTVERSION=	2.3.4
PORTREVISION=	1
CATEGORIES=	x11-toolkits
# MASTER_SITES=	SF/${PORTNAME}/Motif%202.3.4%20Source%20Code/
MASTER_SITES=	SF/motif/Motif%202.3.4%20Source%20Code/
DISTNAME=	motif-${PORTVERSION}-src
EXTRACT_SUFX=	.tgz

MAINTAINER=	m.tsatsenko@gmail.com
COMMENT=	Motif X11 Toolkit (industry standard GUI (IEEE 1295))

LICENSE=	LGPL21
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libpng15.so:${PORTSDIR}/graphics/png \
		libjpeg.so:${PORTSDIR}/graphics/jpeg

MAKE_JOBS_UNSAFE=	yes
CONFLICTS=	lesstif-[0-9]*
# WRKSRC=		${WRKDIR}/${PORTNAME}-${PORTVERSION}
WRKSRC=		${WRKDIR}/motif-${PORTVERSION}

USES=		gmake iconv libtool:keepla pkgconfig
USE_AUTOTOOLS=	libtoolize aclocal autoconf autoheader automake
ACLOCAL_ARGS=	-I.
AUTOMAKE_ARGS=	-a -c -f --foreign
LIBTOOLIZE_ARGS=-i -c -f
USE_XORG=	xaw xbitmaps xft
GNU_CONFIGURE=	yes
USE_LDCONFIG=	yes
MAKE_ENV=	LANG=C
CPPFLAGS+=	-DCSRG_BASED -DXUSE_MTSAFE_API -DXNO_MTSAFE_PWDAPI -I${PREFIX}/include
USE_CSTD=	gnu89

OPTIONS_DEFINE=	DOCS

.include <bsd.port.options.mk>

post-patch:
# fix sections
	@${FIND} ${WRKSRC}/doc/man/man1 -name '*.1' -maxdepth 1 | \
		${XARGS} ${REINPLACE_CMD} -e 's|user cmd|1|'
	@${FIND} ${WRKSRC}/doc/man/man3 -name '*.3' -maxdepth 1 | \
		${XARGS} ${REINPLACE_CMD} -e 's|library call|3|'
# mwmrc is not a kernel interface!!
	@cd ${WRKSRC}/doc/man && ${CP} -f man4/mwmrc.4 man5/mwmrc.5
	@${FIND} ${WRKSRC}/doc/man/man5 -name '*.5' -maxdepth 1 | \
		${XARGS} ${REINPLACE_CMD} -e 's|special file|5| ; \
		 s|file formats|5|'
	@${REINPLACE_CMD} -e 's|/usr/local|${LOCALBASE}|' ${WRKSRC}/configure.ac

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
.for i in BUGREPORT README RELNOTES
	${INSTALL_DATA} ${WRKSRC}/${i} ${STAGEDIR}${DOCSDIR}
.endfor

.include <bsd.port.mk>
