# Created by: Yonatan <onatan@gmail.com>
# $FreeBSD$

PORTNAME=	pft
PORTVERSION=	1.3
CATEGORIES=	security
MASTER_SITES=	http://www.phenoelit-us.org/hp/
DISTNAME=	libPJL-${PORTVERSION}-src
EXTRACT_SUFX=	.tgz

MAINTAINER=	onatan@gmail.com
COMMENT=	Printer Job Language library and tool

NO_WRKSUBDIR=	yes
ALL_TARGET=	libPJL.a
USES=		gmake

PLIST_FILES=	bin/pft lib/libPJL.a

NO_STAGE=	yes
post-patch:
	@${REINPLACE_CMD} -e 's|g++|${CXX} ${CXXFLAGS}|' \
		${WRKSRC}/pft/Makefile

post-build:
	@(cd ${WRKSRC}/pft; ${SETENV} ${MAKE_ENV} ${GMAKE} pft)

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/pft/pft ${PREFIX}/bin
	${INSTALL_DATA} ${WRKSRC}/libPJL.a ${PREFIX}/lib

.include <bsd.port.mk>
