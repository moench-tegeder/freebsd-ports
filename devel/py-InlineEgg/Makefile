# Created by: Sofian Brabez <sbrabez@gmail.com>
# $FreeBSD$

PORTNAME=	InlineEgg
PORTVERSION=	1.08
PORTREVISION=	1
CATEGORIES=	devel security python
MASTER_SITES=	http://corelabs.coresecurity.com/index.php?module=Wiki&action=attachment&type=tool&page=InlineEgg&file=
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sbz@FreeBSD.org
COMMENT=	Python module for writing inline assembler programs

FETCH_BEFORE_ARGS=-o ${DISTFILES}
USES=		dos2unix shebangfix
SHEBANG_FILES=	examples/*.py
python_CMD=	${PYTHON_CMD}
USE_PYTHON=	yes
USE_PYDISTUTILS=	yes
PYDISTUTILS_AUTOPLIST=	yes

PORTDOCS=	InlineEgg.html Changelog README
PORTEXAMPLES=	*

OPTIONS_DEFINE=	DOCS EXAMPLES

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA}  ${PORTDOCS:S,^,${WRKSRC}/,} ${STAGEDIR}${DOCSDIR}
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_SCRIPT} ${WRKSRC}/examples/* ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.mk>
