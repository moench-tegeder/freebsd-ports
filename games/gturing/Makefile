# Created by: Juan Salaverria <rael@vectorstar.net>
# $FreeBSD$

PORTNAME=	gturing
PORTVERSION=	0.1.1
PORTREVISION=	18
CATEGORIES=	games gnome
MASTER_SITES=	ftp://ftp.gnome.org/pub/gnome/sources/gturing/0.1/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Simple Turing machine simulator for GNOME 2

USE_GNOME=	gnomeprefix gnomehack libgnomeui
USES=		gettext gmake pkgconfig
USE_AUTOTOOLS=	libtool
CPPFLAGS+=	-I${LOCALBASE}/include
LIBS+=		-L${LOCALBASE}/lib
INSTALLS_OMF=	yes

PORTDOCS=	AUTHORS COPYING NEWS ChangeLog TODO README INSTALL
PORTEXAMPLES=	*

NO_STAGE=	yes
post-patch:
	@${REINPLACE_CMD} -e 's|-D.*_DISABLE_DEPRECATED||g' \
		${WRKSRC}/configure
post-install:
.if !defined(NOPORTDOCS)
	${MKDIR} ${DOCSDIR}
.for docs in ${PORTDOCS}
	${INSTALL_DATA} ${WRKSRC}/${docs} ${DOCSDIR}
.endfor
.endif

.if !defined(NOPORTEXAMPLES)
	${MKDIR} ${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/tapes/* ${EXAMPLESDIR}
.endif

.include <bsd.port.mk>
