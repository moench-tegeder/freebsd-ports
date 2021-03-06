# Created by: Vanilla I. Shu <vanilla@MinJe.com.TW>
# $FreeBSD$
#    $MCom: ports/x11-toolkits/gtk12/Makefile,v 1.3 2006/10/09 19:31:53 ahze Exp $

PORTNAME=	gtk
PORTVERSION=	1.2.10
PORTREVISION=	22
CATEGORIES=	x11-toolkits
MASTER_SITES=	GNOME
MASTER_SITE_SUBDIR=	sources/gtk+/1.2
PKGNAMESUFFIX=	1
DISTNAME=	gtk+-${PORTVERSION}

MAINTAINER=	gnome@FreeBSD.org
COMMENT=	Gimp Toolkit for X11 GUI (previous stable version)

USES=		perl5
USE_PERL5=	build
USE_XORG=	x11 ice xext sm inputproto xi
USE_GNOME=	glib12
USE_LDCONFIG=	yes
USE_AUTOTOOLS=	libtool
CONFIGURE_ARGS=	--includedir=${PREFIX}/include/gtk12 --with-native-locale \
		--with-xinput=xfree
CPPFLAGS+=	-I${LOCALBASE}/include
LIBS+=		-L${LOCALBASE}/lib

INFO=		gdk gtk
.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MNLS}
USES+=		gettext
PLIST_SUB+=	NLS=""
.else
CONFIGURE_ARGS+=--disable-nls
PLIST_SUB+=	NLS="@comment "
.endif

pre-build:
	${RM} -rf ${WRKSRC}/docs/gtk.info*

post-install:
	@${MKDIR} ${STAGEDIR}${PREFIX}/lib/gtk/themes/engines
	@${LN} -sf ${PREFIX}/bin/gtk-config ${STAGEDIR}${PREFIX}/bin/gtk12-config
.for lib in gdk gtk
	@${RM} ${STAGEDIR}${PREFIX}/lib/lib${lib}.la ${STAGEDIR}${PREFIX}/lib/lib${lib}.so
	@${MV} ${STAGEDIR}${PREFIX}/lib/lib${lib}.a ${STAGEDIR}${PREFIX}/lib/lib${lib}-12.a
.endfor

.include <bsd.port.mk>
