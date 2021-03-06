# Created by: bf <bf@FreeBSD.org>
# $FreeBSD$

PORTNAME=	libranlip
DISTVERSION=	1.0
PORTREVISION= 	1
CATEGORIES=	math
MASTER_SITES=	LOCAL/bf \
		http://www.deakin.edu.au/~gleb/

MAINTAINER=	bf@FreeBSD.org
COMMENT=	A random variate generator for Lipschitz-continuous densities

USES=		libtool
GNU_CONFIGURE=	yes
USE_LDCONFIG=	yes

INFO=	ranlip
PLIST_FILES=	include/ranlip.h include/ranlipdist.h include/ranlipproc.h lib/libranlip.so.1.0.0 \
		lib/libranlip.so.1 lib/libranlip.so lib/libranlip.a
PORTDOCS=	ranlip.ps
PORTEXAMPLES=	makefile ranliptest.cpp ranliptestproc.cpp
TESTPROGS=	static_example static_example2 static_example3 shared_example

.include <bsd.port.pre.mk>

post-install:
.if !defined(NOPORTDOCS)
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_MAN} ${WRKSRC}/docs/ranlip.ps ${STAGEDIR}${DOCSDIR}
.endif
.if !defined(NOPORTEXAMPLES)
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
.for _file in ${PORTEXAMPLES}
	${INSTALL_DATA} ${WRKSRC}/examples/${_file} ${STAGEDIR}${EXAMPLESDIR}
.endfor
.endif

test: build
	@(cd ${WRKSRC}/examples; ${SETENV} ${MAKE_ENV} ${MAKE} ${_MAKE_JOBS} ${MAKE_ARGS} all)
.for _prog in ${TESTPROGS}
	@(cd ${WRKSRC}/examples && ./${_prog})
.endfor

.if ${OSVERSION} < 700000
BROKEN=		fails to build
.endif

.include <bsd.port.post.mk>
