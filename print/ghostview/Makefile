# Created by: jkh
# $FreeBSD$

PORTNAME=	ghostview
PORTVERSION=	1.5
PORTREVISION=	3
CATEGORIES=	print
MASTER_SITES=	http://ftp.gnu.org/old-gnu/ghostview/ \
		http://ftp.sunet.se/pub/text-processing/postscript/interpreters/ghostscript/gnu/ghostview/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	X11 front-end for ghostscript, the GNU postscript previewer

LICENSE=	GPLv2 # (or later)

DEPRECATED=	project dead nearly a decade ago; use print/gv instead
EXPIRATION_DATE=2014-07-31

USES=		imake
USE_XORG=	xbitmaps xaw
USE_GHOSTSCRIPT_RUN=	yes
CFLAGS+=	-Wno-error=return-type

MAN1=		ghostview.1
PLIST_FILES=	bin/ghostview \
		lib/X11/app-defaults/Ghostview

NO_STAGE=	yes
post-install:
	@${SH} ${PKGINSTALL} ${PKGNAME} POST-INSTALL

.include <bsd.port.mk>
