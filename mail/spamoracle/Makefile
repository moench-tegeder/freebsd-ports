# Created by: Mario Sergio Fujikawa Ferreira <lioux@FreeBSD.org>
# $FreeBSD$

PORTNAME=	spamoracle
PORTVERSION=	1.4
PORTREVISION=	1
CATEGORIES=	mail
MASTER_SITES=	http://cristal.inria.fr/~xleroy/software/

MAINTAINER=	xride@FreeBSD.org
COMMENT=	procmail spam filter written in ML using Bayesian classification

BUILD_DEPENDS=	ocaml:${PORTSDIR}/lang/ocaml

MAN1=	spamoracle.1
MAN5=	spamoracle.conf.5

PLIST_FILES=	bin/spamoracle
.ifndef(NOPORTDOCS)
PORTDOCS=	Changes README
.endif

NO_STAGE=	yes
do-configure:
	@${REINPLACE_CMD} -E -e 's|^(CPP=)gcc[[:space:]]+-E|\1${CPP}|' \
		-e 's|^(MANDIR=).*$$|\1${MANPREFIX}/man|' \
		-e 's|^(BINDIR=).*$$|\1${PREFIX}/bin|' \
		${WRKSRC}/Makefile

post-install:
.ifndef(NOPORTDOCS)
	@${MKDIR} ${DOCSDIR}
.for file in ${PORTDOCS}
	@${INSTALL_DATA} ${WRKSRC}/${file} ${DOCSDIR}
.endfor
.endif

.include <bsd.port.mk>
