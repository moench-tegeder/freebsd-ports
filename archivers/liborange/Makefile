# Created by: Sam Lawrance <boris@brooknet.com.au>
# $FreeBSD$

PORTNAME=	liborange
PORTVERSION=	0.4
PORTREVISION=	2
CATEGORIES=	archivers
MASTER_SITES=	SF/synce/Orange/${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Library to extract CAB files from self-extracting installers

RUN_DEPENDS=	cabextract:${PORTSDIR}/archivers/cabextract \
		unzip:${PORTSDIR}/archivers/unzip

OPTIONS_DEFINE=	LIBSYNCE LIBDYNAMITE LIBUNSHIELD INNO VISE MSI
OPTIONS_DEFAULT=	LIBSYNCE LIBDYNAMITE LIBUNSHIELD
LIBSYNCE_DESC=		Build with libsynce support
LIBDYNAMITE_DESC=	Build with libdynamite support
LIBUNSHIELD_DESC=	Build with libunshield support
INNO_DESC=		Build with expermential Inno Setup support
VISE_DESC=		Build with expermential VISE support
MSI_DESC=		Build with expermential MSI support

GNU_CONFIGURE=	yes
USES=		iconv libtool pathfix pkgconfig
CFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
USE_LDCONFIG=	yes

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MLIBSYNCE}
CONFIGURE_ARGS+=	--without-libsynce
REQUIRES+=	libsynce
.else
LIB_DEPENDS+=		libsynce.so:${PORTSDIR}/palm/synce-libsynce
CONFIGURE_ARGS+=	--with-libsynce
.endif

.if ${PORT_OPTIONS:MLIBDYNAMITE}
CONFIGURE_ARGS+=	--without-libdynamite
REQUIRES+=	libdynamite
.else
LIB_DEPENDS+=		libdynamite.so:${PORTSDIR}/archivers/libdynamite
CONFIGURE_ARGS+=	--with-libdynamite
.endif

.if ${PORT_OPTIONS:MLIBUNSHIELD}
CONFIGURE_ARGS+=	--without-libunshield
REQUIRES+=	libunshield
.else
LIB_DEPENDS+=		libunshield.so:${PORTSDIR}/archivers/unshield
CONFIGURE_ARGS+=	--with-libunshield
.endif

.if ${PORT_OPTIONS:MINNO}
CONFIGURE_ARGS+=	--enable-inno
.endif

.if ${PORT_OPTIONS:MVISE}
CONFIGURE_ARGS+=	--enable-vise
.endif

.if ${PORT_OPTIONS:MMSI}
CONFIGURE_ARGS+=	--enable-msi --with-libgsf
LIB_DEPENDS+=		libgsf-1.so.114:${PORTSDIR}/devel/libgsf
.endif

post-patch:
.for req in ${REQUIRES}
	@${REINPLACE_CMD} -e 's|${req}||' ${WRKSRC}/${PORTNAME}.pc.in
.endfor

.include <bsd.port.mk>
