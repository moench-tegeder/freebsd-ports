# $FreeBSD$

PORTNAME=	meek
PORTVERSION=	0.5
CATEGORIES=	security
MASTER_SITES=	http://c-s.li/ports/

MAINTAINER=	cs@FreeBSD.org
COMMENT=	Pluggable transport proxy that relays through third-party server

BUILD_DEPENDS=	${LOCALBASE}/${GO_LIBDIR}/git.torproject.org/pluggable-transports/goptlib.git.a:${PORTSDIR}/security/goptlib

PLIST_FILES=	bin/meek-client bin/meek-server man/man1/meek-client.1.gz man/man1/meek-server.1.gz
SUB_FILES=	pkg-message
GO_PKGNAME=	git.torproject.org/pluggable-transports/${PORTNAME}.git
GO_TARGET=	${GO_PKGNAME}/${PORTNAME}-server \
		${GO_PKGNAME}/${PORTNAME}-client

post-extract:
	@${MKDIR} ${GO_WRKSRC:H}
	@${LN} -sf ${WRKSRC} ${GO_WRKSRC}

post-install:
	${INSTALL_MAN} ${WRKSRC}/doc/meek-server.1 ${STAGEDIR}${PREFIX}/man/man1
	${INSTALL_MAN} ${WRKSRC}/doc/meek-client.1 ${STAGEDIR}${PREFIX}/man/man1

.include <bsd.port.pre.mk>
.include "${PORTSDIR}/lang/go/files/bsd.go.mk"
.include <bsd.port.post.mk>
