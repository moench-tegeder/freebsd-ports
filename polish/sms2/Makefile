# Created by: Krzysztof Kowalewski <pyzmen@kam.pl>
# $FreeBSD$

PORTNAME=	sms
PORTVERSION=	2.1.0
PORTREVISION=	6
CATEGORIES=	polish
MASTER_SITES=	http://ceti.pl/~miki/komputery/download/sms/ \
		http://radioemiter.pl/~mjd/slackware/sms2/ \
		http://pyzmen.kam.pl/sms/ \
		ftp://ftp.ma.krakow.pl/pub/sms/

MAINTAINER=	pyzmen@kam.pl
COMMENT=	Send SMS to cellular phones in Poland (Idea, ERA, Plus)

DEPRECATED=	sms2 is no longer being developed, consider using alternative software.
EXPIRATION_DATE=2014-06-30

LIB_DEPENDS=	curl:${PORTSDIR}/ftp/curl \
		pcre.3:${PORTSDIR}/devel/pcre \
		gdbm.4:${PORTSDIR}/databases/gdbm \
		pcre\\+\\+.0:${PORTSDIR}/devel/pcre++

LATEST_LINK=	sms2

USES=		gmake

NO_STAGE=	yes
.include <bsd.port.mk>
