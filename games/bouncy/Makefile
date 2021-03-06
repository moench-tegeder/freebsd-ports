# Created by: Rusmir Dusko <nemysis@FreeBSD.org>
# $FreeBSD$

PORTNAME=	bouncy
PORTVERSION=	r6
PORTREVISION=	1
CATEGORIES=	games python
MASTER_SITES=	http://media.pyweek.org/dl/3/bouncy/ \
		SF/nemysisfreebsdp/games/${PORTNAME}/:icons
DISTFILES=	${PORTNAME}-post-${DISTVERSION}.tgz \
		${PORTNAME}.png:icons
DIST_SUBDIR=	python
EXTRACT_ONLY=	${PORTNAME}-post-${DISTVERSION}.tgz

MAINTAINER=	games@FreeBSD.org
COMMENT=	You are a hungry rabbit. Eat food to complete the level

LICENSE=	GPLv2

RUN_DEPENDS=	${PYGAME} \
		${PYTHON_PKGNAMEPREFIX}opengl>=0:${PORTSDIR}/graphics/py-opengl

WRKSRC=		${WRKDIR}/${PORTNAME}-post-${DISTVERSION}

USE_PYTHON=	2

PORTDOCS=	README.txt

OPTIONS_DEFINE=	DOCS SHADER
SHADER_DESC=	Hardware shader support
OPTIONS_DEFAULT=	SHADER

INSTALLS_ICONS=	yes

SUB_FILES=	${PORTNAME}

DESKTOP_ENTRIES="Bouncy the Hungry Rabbit" "" "${PORTNAME}" \
		"${PORTNAME}" "Game;ArcadeGame;" ""

.include <bsd.port.options.mk>

post-patch:
	@${FIND} ${WRKSRC} -name '*.py' | ${XARGS} \
		${REINPLACE_CMD} -e 's|^.*#!.*python.*$$|#!${PYTHON_CMD}|'
	@${FIND} ${WRKSRC} -name "*.bak" -delete

.if ${PORT_OPTIONS:MSHADER}
	@${REINPLACE_CMD} -i '' '/#try/,/#    print/s/#//' ${WRKSRC}/objects.py
.endif

do-build:
	@${PYTHON_CMD} -m compileall ${WRKSRC}
	@${PYTHON_CMD} -O -m compileall ${WRKSRC}

do-install:
	@${REINPLACE_CMD} -e 's|%%PYTHON_CMD%%|${PYTHON_CMD}|' \
		${WRKDIR}/${PORTNAME}
	${INSTALL_SCRIPT} ${WRKDIR}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/

.for d in data pyglyph
	@(cd ${WRKSRC} && ${COPYTREE_SHARE} ${d} ${STAGEDIR}${DATADIR})
.endfor
.for f in *.py *.pyc *.pyo
	${INSTALL_SCRIPT} ${WRKSRC}/${f} ${STAGEDIR}${DATADIR}
.endfor

	${INSTALL_DATA} ${_DISTDIR}/${PORTNAME}.png \
		${STAGEDIR}${PREFIX}/share/pixmaps/

	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
