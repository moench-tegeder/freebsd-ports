# Created by: Uffe Jakobsen <uffe@uffe.org>
# $FreeBSD$

PORTNAME=	libsigrok
PORTVERSION=	0.2.2
PORTREVISION=	1
CATEGORIES=	devel
MASTER_SITES=	http://sigrok.org/download/source/libsigrok/

MAINTAINER=	uffe@uffe.org
COMMENT=	Framework for hardware logic analyzers, core library

LICENSE=	GPLv3

LIB_DEPENDS=	libzip.so:${PORTSDIR}/archivers/libzip

GNU_CONFIGURE=	yes
USES=		gmake libtool pathfix pkgconfig
USE_GNOME=	gtk20
INSTALL_TARGET=	install-strip
MAKE_JOBS_UNSAFE=	yes
LDFLAGS+=	-L/usr/lib -lusb
USE_LDCONFIG=	yes

# Workaround for libusb not knowing LIBUSB_CLASS_APPLICATION
CFLAGS+=	-DLIBUSB_CLASS_APPLICATION=0xfe

.include <bsd.port.mk>
