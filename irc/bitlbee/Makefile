# $FreeBSD$

PORTNAME=	bitlbee
PORTVERSION=	3.2.1
PORTREVISION=	2
CATEGORIES=	irc
MASTER_SITES=	http://get.bitlbee.org/src/ \
		${MASTER_SITE_LOCAL}
MASTER_SITE_SUBDIR=	brix

MAINTAINER=	brix@FreeBSD.org
COMMENT=	IRC to other chat networks gateway

LICENSE=	GPLv2

SUB_FILES=	pkg-message
PORTDOCS=	AUTHORS CHANGES CREDITS FAQ README
PORTEXAMPLES=	bitlbee.conf motd.txt

GNU_CONFIGURE=	yes
USES=		gmake pkgconfig
USE_GNOME=	glib20
USE_RC_SUBR=	bitlbee
PKGMESSAGE=	${WRKDIR}/pkg-message

OPTIONS_DEFINE=		DEBUG DOCS EXAMPLES IPV6 OTR

OPTIONS_SINGLE=		SSL
OPTIONS_SINGLE_SSL=	OPENSSL GNUTLS

OPTIONS_MULTI=		PROTO
OPTIONS_MULTI_PROTO=	JABBER LIBPURPLE MSN OSCAR TWITTER YAHOO

OTR_DESC=		Off-the-Record Messaging support (Requires GnuTLS)
LIBPURPLE_DESC=		Use libpurple for protocol support
MSN_DESC=		Microsoft Messenger support
OSCAR_DESC=		OSCAR (ICQ, AIM) support
TWITTER_DESC=		Twitter support
YAHOO_DESC=		Yahoo! Messenger support

OPTIONS_DEFAULT=	GNUTLS JABBER MSN OSCAR TWITTER YAHOO

CONFIGURE_ARGS=	--config=/var/db/bitlbee --strip=0

USERS=		bitlbee
GROUPS=		bitlbee

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MOPENSSL} && ${PORT_OPTIONS:MOTR}
IGNORE=Off-the-Record Messaging support requires GnuTLS support
.endif

.if ${PORT_OPTIONS:MDEBUG}
CONFIGURE_ARGS+=--debug=1
.else
CONFIGURE_ARGS+=--debug=0
.endif

.if ${PORT_OPTIONS:MIPV6}
CONFIGURE_ARGS+=--ipv6=1
.else
CONFIGURE_ARGS+=--ipv6=0
.endif

.if ${PORT_OPTIONS:MOPENSSL}
CONFIGURE_ARGS+=--ssl=openssl
.elif ${PORT_OPTIONS:MGNUTLS}
CONFIGURE_ARGS+=--ssl=gnutls
LIB_DEPENDS+=	libgnutls.so:${PORTSDIR}/security/gnutls \
		libgcrypt.so:${PORTSDIR}/security/libgcrypt
.endif

.if ${PORT_OPTIONS:MOTR}
CONFIGURE_ARGS+=--otr=1
LIB_DEPENDS+=	libotr.so.2:${PORTSDIR}/security/libotr3
.else
CONFIGURE_ARGS+=--otr=0
.endif

.if ${PORT_OPTIONS:MMSN}
CONFIGURE_ARGS+=--msn=1
.else
CONFIGURE_ARGS+=--msn=0
.endif

.if ${PORT_OPTIONS:MJABBER}
CONFIGURE_ARGS+=--jabber=1
.else
CONFIGURE_ARGS+=--jabber=0
.endif

.if ${PORT_OPTIONS:MOSCAR}
CONFIGURE_ARGS+=--oscar=1
.else
CONFIGURE_ARGS+=--oscar=0
.endif

.if ${PORT_OPTIONS:MYAHOO}
CONFIGURE_ARGS+=--yahoo=1
.else
CONFIGURE_ARGS+=--yahoo=0
.endif

.if ${PORT_OPTIONS:MTWITTER}
CONFIGURE_ARGS+=--twitter=1
.else
CONFIGURE_ARGS+=--twitter=0
.endif

.if ${PORT_OPTIONS:MLIBPURPLE}
CONFIGURE_ARGS+=--purple=1
LIB_DEPENDS+=	libpurple.so:${PORTSDIR}/net-im/libpurple
.else
CONFIGURE_ARGS+=--purple=0
.endif

post-patch:
	@${REINPLACE_CMD} \
		-e "s|^EFLAGS=|EFLAGS=${LDFLAGS}|" \
		${WRKSRC}/configure

	@${REINPLACE_CMD} \
		-e "s:/etc/bitlbee/motd.txt:${PREFIX}/etc/bitlbee/motd.txt:" \
		-e "s:/var/lib/bitlbee:/var/db/bitlbee:" \
		${WRKSRC}/bitlbee.conf
	@${REINPLACE_CMD} \
		-e "s:/var/lib/bitlbee:/var/db/bitlbee:" \
		${WRKSRC}/doc/bitlbee.8

post-install:
	${MKDIR} ${STAGEDIR}/${PREFIX}/etc/bitlbee
.if ${PORT_OPTIONS:MDOCS}
	${MKDIR} ${STAGEDIR}/${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S@^@${WRKSRC}/doc/@} ${STAGEDIR}/${DOCSDIR}
.endif
.if ${PORT_OPTIONS:MEXAMPLES}
	${MKDIR} ${STAGEDIR}/${EXAMPLESDIR}
	${INSTALL_DATA} ${PORTEXAMPLES:S@^@${WRKSRC}/@} ${STAGEDIR}/${EXAMPLESDIR}
.endif

.include <bsd.port.mk>
