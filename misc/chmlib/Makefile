# Created by: ijliao
# $FreeBSD$

PORTNAME=	chmlib
PORTVERSION=	0.40
CATEGORIES=	misc
MASTER_SITES=	http://www.jedrea.com/chmlib/

MAINTAINER=	fluffy@FreeBSD.org
COMMENT=	A library for dealing with Microsoft ITSS/CHM format files

USES=		gmake tar:bzip2
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--disable-io64 --disable-pread --exec-prefix=${PREFIX} --disable-static --enable-examples
USE_LDCONFIG=	yes

post-patch:
	@${REINPLACE_CMD} -e "s,-lpthread,${PTHREAD_LIBS}," ${WRKSRC}/configure

.include <bsd.port.mk>
