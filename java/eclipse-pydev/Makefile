# Created by: Nicola Vitale <nivit@FreeBSD.org>
# $FreeBSD$

PORTNAME=	pydev
PORTVERSION=	2.8.2
PORTREVISION=	0
CATEGORIES=	java devel python
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/PyDev%20${PORTVERSION}/
PKGNAMEPREFIX=	eclipse-
DISTNAME=	PyDev%20${PORTVERSION}

MAINTAINER=	nivit@FreeBSD.org
COMMENT=	Eclipse plugin for Python and Jython development

LICENSE=	EPL

RUN_DEPENDS=	eclipse:${PORTSDIR}/java/eclipse

BUNDLES_INFO=	${PREFIX}/lib/eclipse/configuration/org.eclipse.equinox.simpleconfigurator/bundles.info

DISTDATE=	2013090511

JYTHON_DESC=	Use Jython as Python interpreter

NO_WRKSUBDIR=	yes

OPTIONS_DEFINE=	JYTHON

PLUGINDIR=	share/eclipse/dropins/pydev/eclipse/plugins
PYDEV_BUNDLES_INFO=	${PREFIX}/${PLUGINDIR}/bundles.info

USE_PYTHON=	yes
USES=		zip

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MJYTHON}
RUN_DEPENDS+=	jython:${PORTSDIR}/lang/jython
.endif

pre-install:
	@${ECHO_MSG} "===>   Creating bundles.info"
	@PLUGINS=$$(ls -1 ${WRKDIR}/plugins); \
	for d in $${PLUGINS}; do \
	    (${ECHO_CMD} "$${d},../../${PLUGINDIR}/$${d}/,4,false" | \
	    ${SED} -e 's/_\([0-9]\)/,\1/1' -e '/templates/d') >> ${WRKDIR}/plugins/bundles.info; \
	done
	@# ignore javashell.py file, because there is a syntax error
	@# see http://goo.gl/E4epH
	${PYTHON_CMD} -m compileall -x javashell.py -f ${WRKSRC}/plugins
	${PYTHON_CMD} -O -m compileall -x javashell.py -f ${WRKSRC}

add-plist-post:
	@${ECHO_CMD} "@exec ${CAT} ${PYDEV_BUNDLES_INFO} >> ${BUNDLES_INFO}" >> ${TMPPLIST}
	@${ECHO_CMD} "@unexec ${SED} -i '' -E '/^((org)|(com))\.python\.pydev/d' %D/lib/eclipse/configuration/org.eclipse.equinox.simpleconfigurator/bundles.info" >> ${TMPPLIST}

.include "${PORTSDIR}/java/eclipse/Makefile.plugins"

.include <bsd.port.mk>
