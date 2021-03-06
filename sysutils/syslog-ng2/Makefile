# Created by: Ivan Lago <ivan.lago@ifom-ieo-campus.it>
# $FreeBSD$

PORTNAME=	syslog-ng
PORTVERSION=	2.0.10
PORTREVISION=	1
CATEGORIES=	sysutils
MASTER_SITES=	http://www.balabit.com/downloads/files/syslog-ng/sources/2.0/src/
PKGNAMESUFFIX=	2

MAINTAINER=	ivan.lago@ifom.eu
COMMENT=	A powerful syslogd replacement

LIB_DEPENDS=	net:${PORTSDIR}/net/libnet \
		evtlog.0:${PORTSDIR}/sysutils/eventlog

MAN5=		syslog-ng.conf.5
MAN8=		syslog-ng.8

USE_RC_SUBR=	syslog-ng
USES=		pkgconfig
GNU_CONFIGURE=	yes
USE_GNOME=	glib20
SUB_FILES=	pkg-message

LIBNET_CONFIG?=	${LOCALBASE}/bin/libnet11-config

CONFIGURE_ARGS=	--sysconfdir=${LOCALBASE}/etc --localstatedir=/var/db \
		--enable-dynamic-linking --with-libnet=${LOCALBASE}/bin
LDFLAGS+=	`${LIBNET_CONFIG} --libs`
CFLAGS+=	`${LIBNET_CONFIG} --cflags`

NO_STAGE=	yes
.include <bsd.port.pre.mk>

.if ${OSVERSION} > 900007
BROKEN=		fails to build with new utmpx
.endif

.if defined(WITH_TCP_WRAPPERS)
CONFIGURE_ARGS+=--enable-tcp-wrapper
.endif

post-patch:
	@${REINPLACE_CMD} -e 's:__PREFIX__:${PREFIX}:g' ${WRKSRC}/src/syslog-ng.h
	@${REINPLACE_CMD} -e 's:libnet-config:libnet11-config:g' ${WRKSRC}/configure

post-install:
.if !defined(NOPORTDOCS)
	${INSTALL} -d -o ${SHAREOWN} -g ${SHAREGRP} \
			${PREFIX}/share/doc/syslog-ng \
			${PREFIX}/share/doc/syslog-ng/sgml
	${INSTALL_DATA} ${WRKSRC}/AUTHORS ${PREFIX}/share/doc/syslog-ng
	${INSTALL_DATA} ${WRKSRC}/COPYING ${PREFIX}/share/doc/syslog-ng
	${INSTALL_DATA} ${WRKSRC}/ChangeLog ${PREFIX}/share/doc/syslog-ng
	${INSTALL_DATA} ${WRKSRC}/NEWS ${PREFIX}/share/doc/syslog-ng
	${INSTALL_DATA} ${WRKSRC}/README ${PREFIX}/share/doc/syslog-ng
.endif
	@if [ ! -f ${PREFIX}/etc/syslog-ng/syslog-ng.conf.sample ]; then \
		${INSTALL} -d -o ${SHAREOWN} -g ${SHAREGRP} ${PREFIX}/etc/syslog-ng; \
		${INSTALL_DATA} ${FILESDIR}/syslog-ng.conf.sample ${PREFIX}/etc/syslog-ng; \
	fi
	@${CAT} ${PKGMESSAGE}

.include <bsd.port.post.mk>
