# Created by: Bartek Rutkowski <r@robakdesign.com>
# $FreeBSD$

PORTNAME=	jggtrans
PORTVERSION=	2.2.4
PORTREVISION=	2
CATEGORIES=	net-im polish
MASTER_SITES=	http://jggtrans.jajcus.net/downloads/ \
		http://freebsd.e.pl/distfiles/

MAINTAINER=	mg@fork.pl
COMMENT=	Jabberd XMPP to GG instant messaging service gateway

LIB_DEPENDS=	libidn.so:${PORTSDIR}/dns/libidn \
		libexpat.so:${PORTSDIR}/textproc/expat2 \
		libgadu.so:${PORTSDIR}/polish/libgadu

GNU_CONFIGURE=	yes
USES=		gettext gmake pkgconfig
USE_GNOME=	glib20
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
CFLAGS+=	-I${LOCALBASE}/include

USE_RC_SUBR=	jggtrans

OPTIONS_DEFINE=	DEBUG EJABBERD
EJABBERD_DESC=	transport with ejabberd
DEBUG_CONFIGURE_ENABLE=debug

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MEJABBERD}
JABBER_USER?=	ejabberd
SUB_LIST+=	JABBER_REQUIRE=ejabberd
.else
JABBER_USER?=	jabber
SUB_LIST+=	JABBER_REQUIRE=jabberd
.endif

SUB_LIST+=	JABBER_USER=${JABBER_USER}

post-install:
	@${INSTALL_DATA} ${WRKSRC}/jggtrans.xml ${STAGEDIR}${PREFIX}/etc/jggtrans.xml.sample

.include <bsd.port.mk>
