# Created by: John Nielsen <john@jnielsen.net>
# $FreeBSD$

PORTNAME=	hotwayd
PORTVERSION=	0.8.4
PORTREVISION=	2
PORTEPOCH=	1
CATEGORIES=	mail
MASTER_SITES=	SF

MAINTAINER=	john@jnielsen.net
COMMENT=	A Hotmail -> POP3 gateway

DEPRECATED=	yes
EXPIRATION_DATE=2014-06-30

LIB_DEPENDS=	sasl2:${PORTSDIR}/security/cyrus-sasl2

USE_BZIP2=	yes
GNU_CONFIGURE=	yes
USES=		iconv gmake
USE_GNOME=	libxml2

MAN1=		hotwayd.1 \
		hotsmtpd.1

PORTDOCS=	AUTHORS COPYING ChangeLog INSTALL NEWS README VERSION
PLIST_FILES=	sbin/hotwayd sbin/hotsmtpd

post-install:	install-doc-files display-message

NO_STAGE=	yes
install-doc-files:
.if !defined(NOPORTDOCS)
	@${MKDIR} ${DOCSDIR}
.for f in ${PORTDOCS}
	@${INSTALL_DATA} ${WRKSRC}/${f} ${DOCSDIR}
.endfor
.endif

display-message:
	@${ECHO_MSG}
	@${CAT} ${PKGMESSAGE}
	@${ECHO_MSG}

.include <bsd.port.mk>
