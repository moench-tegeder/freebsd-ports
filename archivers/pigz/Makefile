# Created by: Gea-Suan Lin <gslin@gslin.org>
# $FreeBSD$

PORTNAME=	pigz
PORTVERSION=	2.3.1
CATEGORIES=	archivers
MASTER_SITES=	http://www.zlib.net/pigz/ \
		http://freebsd.unixfreunde.de/sources/

MAINTAINER=	gslin@gslin.org
COMMENT=	Parallel GZIP

USES=		gmake

PLIST_FILES=	bin/pigz bin/pigzn bin/pigzt bin/unpigz
.if !defined(NO_INSTALL_MANPAGES)
PLIST_FILES+=	man/man1/pigz.1.gz
.endif

post-patch:
	${REINPLACE_CMD} -e 's/ -lz/ -lm -lz/g' ${WRKSRC}/Makefile

do-install:
.for FILE in pigz pigzn pigzt unpigz
	${INSTALL_PROGRAM} ${WRKSRC}/${FILE} ${STAGEDIR}${PREFIX}/bin
.endfor
.if !defined(NO_INSTALL_MANPAGES)
	${INSTALL_MAN} ${WRKSRC}/pigz.1 ${STAGEDIR}${MAN1PREFIX}/man/man1/
.endif

.include <bsd.port.mk>
