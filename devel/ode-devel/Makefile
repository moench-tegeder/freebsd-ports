# Created by: David Yeske <dyeske@yahoo.com>
# $FreeBSD$

PORTNAME=	ode
DISTVERSION=	${ODEVER}-060223
PORTREVISION=	4
CATEGORIES=	devel
MASTER_SITES=	http://opende.sourceforge.net/snapshots/
PKGNAMESUFFIX=	-devel
DISTNAME=	${PORTNAME}-${DISTVERSION:S/${ODEVER}-//}

MAINTAINER=	acm@FreeBSD.org
COMMENT=	Articulated rigid body dynamics library (devel)

DEPRECATED=	Outdated by devel/ode
EXPIRATION_DATE=2014-06-27

ODEVER=		0.5

CONFLICTS=	ode-[0-9].*

USE_GL=		yes
USES=		gmake
MAKE_JOBS_UNSAFE=	yes

OPTIONS_DEFINE=	OPCODE
OPTIONS_DEFAULT=	OPCODE
OPCODE_DESC=	Enable code required by TriList (trimesh) class

.include <bsd.port.pre.mk>

.if ${ARCH} == "amd64" || ${ARCH} == "ia64"
CFLAGS+=	-fPIC -DPIC
.endif

post-patch:
	@${REINPLACE_CMD} -e 's|malloc.h|stdlib.h|g' \
		${WRKSRC}/configurator.c

	@${REINPLACE_CMD} -e 's|g++|${CXX}|; s|-Wall||g; s|-L/usr/X11/lib|-lXext|; \
		s|-L/usr/lib/X11R6||; s|-L/usr/lib/X11||; s|-L/usr/X11R6/lib|-L${LOCALBASE}/lib|; \
		s|-fno-rtti||; s|-ffast-math|${CXXFLAGS} -I${LOCALBASE}/include|' \
		${WRKSRC}/config/makefile.unix-gcc
.if ${PORT_OPTIONS:MOPCODE}
	@${REINPLACE_CMD} -e 's/^#OPCODE_DIRECTORY/OPCODE_DIRECTORY/' \
		${WRKSRC}/config/user-settings
.endif

do-configure:
	cd ${WRKSRC} ; ${GMAKE} configure
	@${REINPLACE_CMD} -e '/include.*values.h/d' ${WRKSRC}/include/ode/config.h

do-install:
	@${INSTALL_DATA} ${WRKSRC}/lib/libode.a ${STAGEDIR}${PREFIX}/lib
	@${INSTALL_DATA} ${WRKSRC}/lib/libdrawstuff.a ${STAGEDIR}${PREFIX}/lib
	@${MKDIR} ${STAGEDIR}${PREFIX}/include/ode
	@${INSTALL_DATA} ${WRKSRC}/include/ode/*.h ${STAGEDIR}${PREFIX}/include/ode

.include <bsd.port.post.mk>
