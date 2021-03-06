# Created by: Jing-Tang Keith Jang <keith@FreeBSD.org>
# $FreeBSD$

PORTNAME=	libtabe
PORTVERSION=	0.2.6
PORTREVISION=	4
CATEGORIES=	chinese
MASTER_SITES=	ftp://cle.linux.org.tw/pub/xcin/cvs/

MAINTAINER=	clsung@FreeBSD.org
COMMENT=	Unified library for Chinese text processing

USES=		gmake
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
USE_BDB=	yes
OBSOLETE_BDB_VAR=	USE_DB2
DATADIR=	${PREFIX}/share/tabe
DOCSDIR=	${PREFIX}/share/doc/tabe
CONFIGURE_ARGS=	--prefix=${PREFIX} \
		--includedir=${PREFIX}/include/tabe \
		--with-db-name=${BDB_LIB_NAME} \
		--with-db-inc=${BDB_INCLUDE_DIR} \
		--with-db-lib=${BDB_LIB_DIR} \
		--with-db-bin=${LOCALBASE}/bin \
		--enable-shared
MAKE_JOBS_UNSAFE=	yes

OPTIONS_DEFINE=	DOCS X11
OPTIONS_DEFAULT=	DOCS

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MX11}
USE_XORG=	x11
PLIST_SUB+=	X11=""
.else
CONFIGURE_ARGS+=	--without-x
PLIST_SUB+=	X11="@comment "
.endif

pre-everything::
.if defined(WITH_BDB_VER)
pre-everything::
	@${ECHO_CMD} ""
	@${ECHO_CMD} "WARNING:"
	@${ECHO_CMD} "	You have defined WITH_BDB_VER. Make sure you use the same"
	@${ECHO_CMD} "	db version for all ports that use libtabe, such as xcin."
	@${ECHO_CMD} "	Otherwise, ports that use libtabe may not work correctly."
	@${ECHO_CMD} ""
.endif

post-patch:
	${REINPLACE_CMD} -e '/objformat/s/echo aout/echo elf/' ${WRKSRC}/configure
.if !${PORT_OPTIONS:MX11}
	${REINPLACE_CMD} -e '/all:/s/ bims//; /bims/d' ${WRKSRC}/src/Makefile.in
.endif

post-install:
.if ${PORT_OPTIONS:MDOCS}
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/tsi-src/README ${STAGEDIR}${DOCSDIR}/README.tsi
.if ${PORT_OPTIONS:MX11}
	${INSTALL_DATA} ${WRKSRC}/src/supports/bims/README ${STAGEDIR}${DOCSDIR}/README.bims
.endif
.for DOC in BoPoMoFo.shtml Changes Changes.pre-0.1 TODO ZuYinCode.txt \
		et26.txt libtabe.sgml
	${INSTALL_DATA} ${WRKSRC}/doc/${DOC} ${STAGEDIR}${DOCSDIR}
.endfor
.endif

.include <bsd.port.mk>
