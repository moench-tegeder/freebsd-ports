# Created by: Gea-Suan Lin <gslin@ccca.nctu.edu.tw>
# $FreeBSD$

PORTNAME=	zsync
PORTVERSION=	0.6.2
CATEGORIES=	net
MASTER_SITES=	http://zsync.moria.org.uk/download/

MAINTAINER=	lippe@FreeBSD.org
COMMENT=	A file transfer program

USE_BZIP2=	yes
GNU_CONFIGURE=	yes

PORTDOCS=	COPYING INSTALL NEWS README
PLIST_FILES=	bin/zsync bin/zsyncmake \
		man/man1/zsync.1.gz man/man1/zsyncmake.1.gz

MANPAGE=	zsync.1 zsyncmake.1
BINS=		zsync zsyncmake

OPTIONS_DEFINE=	DOCS

do-install:
	${INSTALL_PROGRAM} ${BINS:S,^,${WRKSRC}/,} ${STAGEDIR}${PREFIX}/bin
	${INSTALL_MAN} ${MANPAGE:S,^,${WRKSRC}/doc/,} \
		${STAGEDIR}${MANPREFIX}/man/man1
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S,^,${WRKSRC}/,} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
