# Created by: Jorge Niedbalski <niedbalski@gmail.com>
# $FreeBSD$

PORTNAME=	latex-supertabular
PORTVERSION=	1
PORTREVISION=	4
CATEGORIES=	print
MASTER_SITES=	ftp://tug.ctan.org/pub/tex-archive/macros/latex/contrib/supertabular/
DISTFILES=	supertabular.dtx supertabular.ins ${DOC_FILES}
DIST_SUBDIR=	${PORTNAME}

MAINTAINER=	niedbalski@gmail.com
COMMENT=	A LaTeX package for a tabular that spans multiple pages

USE_TEX=	latex
PLIST_SUB=	TEXMFLOCAL=${TEXMFLOCAL} MKTEXLSR=${MKTEXLSR} \
		CLASSDIR=${CLASSDIR}
USES=		gmake
TEXMFLOCAL=	share/texmf-local
TEXMFLOCAL_LSR=	${LOCALBASE}/${TEXMFLOCAL}/ls-R
MKTEXLSR=	${LOCALBASE}/bin/mktexlsr
TEX_BIN=	${LOCALBASE}/bin/latex
CLASSDIR=	${TEXMFLOCAL}/tex/latex/${PORTNAME:S/^latex-//}
WRKSRC=		${WRKDIR}/${PORTNAME:S/^latex-//}
CLASS_FILES=	supertabular.dtx supertabular.sty supertabular.ins
DOC_FILES=	README MANIFEST CATALOG supertabular.pdf

NO_STAGE=	yes
do-extract:
	${MKDIR} ${WRKSRC}
	cd ${DISTDIR}/${DIST_SUBDIR} && ${CP} ${DISTFILES} ${WRKSRC}

do-build:
	cd ${WRKSRC} && ${TEX_BIN} supertabular.ins

do-install:
	${MKDIR} ${PREFIX}/${CLASSDIR}
	${INSTALL_DATA} ${CLASS_FILES:S@^@${WRKSRC}/@} ${PREFIX}/${CLASSDIR}
.if !defined(NOPORTDOCS)
	${MKDIR} ${DOCSDIR}
	${INSTALL_DATA} ${DOC_FILES:S@^@${WRKSRC}/@} ${DOCSDIR}
.endif

post-install:
	@${MKTEXLSR} ${TEXMFLOCAL}

.include <bsd.port.mk>
