# Created by: Kevin Zheng <kevinz5000@gmail.com>
# $FreeBSD$

PORTNAME=	gnomint
PORTVERSION=	1.2.1
PORTREVISION=	2
CATEGORIES=	security
MASTER_SITES=	SF

MAINTAINER=	kevinz5000@gmail.com
COMMENT=	X.509 Certification Authority management tool

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libgcrypt.so:${PORTSDIR}/security/libgcrypt \
		libgnutls.so:${PORTSDIR}/security/gnutls \
		libsqlite3.so:${PORTSDIR}/databases/sqlite3

GNU_CONFIGURE=	yes
USES=		gmake perl5 pkgconfig
USE_GNOME=	gconf2 gdkpixbuf2 glib20 gtk20

CFLAGS:=	${CFLAGS:C/-Werror//}

OPTIONS_DEFINE=	NLS

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MNLS}
PLIST_SUB+=	NLS=""
.else
CONFIGURE_ARGS+=	--disable-nls
PLIST_SUB+=	NLS="@comment "
.endif

.include <bsd.port.mk>
