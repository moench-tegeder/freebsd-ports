# Created by: tundra
# $FreeBSD$

PORTNAME=	tconfpy
PORTVERSION=	2.112
CATEGORIES=	devel python
MASTER_SITES=	http://www.tundraware.com/Software/tconfpy/
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
DISTNAME=	py-${PORTNAME}-${PORTVERSION}

MAINTAINER=	tconfpy@tundraware.com
COMMENT=	Python Configuration File Parser

USE_PYTHON=	yes
INSTALLS_EGGINFO=	yes
PYDISTUTILS_PKGNAME=	tconfpy
PYDISTUTILS_PKGVERSION=	0.0.0

MANCOMPRESSED=	yes
MAN1=		test-tc.1
MAN3=		tconfpy.3
PORTDOCS=	READ-1ST.txt WHATSNEW.txt tconfpy-license.txt tconfpy.html tconfpy.pdf tconfpy.ps tconfpy.txt test-tc.html test-tc.pdf test-tc.ps test-tc.txt

NO_STAGE=	yes

post-patch:
	@${REINPLACE_CMD} -e 's|python setup.py|${PYTHON_CMD} setup.py|' \
		${WRKSRC}/Makefile

post-install:
.if !defined(NOPORTDOCS)
	@${MKDIR} ${DOCSDIR}
.for f in ${PORTDOCS}
	@${INSTALL_DATA} ${WRKSRC}/${f} ${DOCSDIR}
.endfor
.endif

.include <bsd.port.mk>
