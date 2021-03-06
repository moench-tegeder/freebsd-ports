# Created by: Yukihiro Nakai <nakai@FreeBSD.org>
# $FreeBSD$

PORTNAME=	sawfish
PORTVERSION=	1.10
PORTREVISION=	1
PORTEPOCH=	3
CATEGORIES=	x11-wm
MASTER_SITES=	http://download.tuxfamily.org/sawfish/%SUBDIR%/
MASTER_SITE_SUBDIR=	. Archive

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Lisp configurable window manager

LICENSE=	ART20 GPLv2
LICENSE_COMB=	multi

BUILD_DEPENDS=	rep-gtk2>=0.90:${PORTSDIR}/x11-toolkits/rep-gtk2
LIB_DEPENDS=	librep.so:${PORTSDIR}/lang/librep
RUN_DEPENDS=	rep-gtk2>=0.90:${PORTSDIR}/x11-toolkits/rep-gtk2

USES=		gettext gmake pathfix pkgconfig tar:xz libtool
USE_XORG=	ice sm x11 xft xinerama xrandr xtst
USE_GNOME=	cairo gnomehier gtk20
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--localstatedir=${PREFIX}/share \
		--datadir=${PREFIX}/share
INSTALLS_ICONS=	yes

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

INFO=		sawfish

post-patch:
	@${REINPLACE_CMD} -e \
		'/dnsdomainname/d' ${WRKSRC}/build-info
	@${REINPLACE_CMD} -e \
		'/KDEDIR/s|^|#|g' ${WRKSRC}/Makefile.in
	@${REINPLACE_CMD} -e \
		's|/share/man/|/man/|g' ${WRKSRC}/man/Makefile.in
	@${REINPLACE_CMD} -e \
		's|prog_name|program_name|g' ${WRKSRC}/src/main.c

.include <bsd.port.mk>
