# Created by: Sahil Tandon <sahil@FreeBSD.org>
# $FreeBSD$

PORTNAME=	graphy
PORTVERSION=	1.0
CATEGORIES=	graphics python
MASTER_SITES=	GOOGLE_CODE
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
DISTNAME=	${PORTNAME}_${PORTVERSION}

MAINTAINER=	sahil@FreeBSD.org
COMMENT=	Simple chart library for Python

USE_BZIP2=	yes
USE_PYTHON_RUN=	yes

PORTDOCS=	README
PORTEXAMPLES=	*

NO_BUILD=	yes
NO_INSTALL_MANPAGES=	yes

.include <bsd.port.pre.mk>

post-patch:
	@${REINPLACE_CMD} -e 's|python2.4|${PYTHON_VERSION}|' \
		${WRKSRC}/examples/*.py \
		${WRKSRC}/${PORTNAME}/*.py
	@${FIND} ${WRKSRC} -name '.svn' -or -name '*.bak' | \
		${XARGS} ${RM} -rf

do-install:
	@${MKDIR} ${STAGEDIR}${PYTHON_SITELIBDIR}/${PORTNAME}
	@(cd ${WRKSRC}/${PORTNAME}/ && \
	     ${COPYTREE_SHARE} \* ${STAGEDIR}${PYTHON_SITELIBDIR}/${PORTNAME})
.if !defined(NOPORTDOCS)
	@${INSTALL} -o ${DOCOWN} -g ${DOCGRP} -m 555 -d ${STAGEDIR}${DOCSDIR}
	@${INSTALL_DATA} ${WRKSRC}/${PORTDOCS} ${STAGEDIR}${DOCSDIR}
.endif
.if !defined(NOPORTEXAMPLES)
	@${INSTALL} -o ${SHAREOWN} -g ${SHAREGRP} -m 555 -d ${STAGEDIR}${EXAMPLESDIR}
	@(cd ${WRKSRC}/examples/ && ${COPYTREE_SHARE} \* ${STAGEDIR}${EXAMPLESDIR})
.endif

.include <bsd.port.post.mk>
