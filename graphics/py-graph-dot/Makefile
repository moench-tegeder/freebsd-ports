# Created by: Yi-Jheng Lin <yzlin@cs.nctu.edu.tw>
# $FreeBSD$

PORTNAME=	graph-dot
PORTVERSION=	1.8.2
CATEGORIES=	graphics python
MASTER_SITES=	GOOGLE_CODE
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
DISTNAME=	python-${PORTNAME}-${PORTVERSION}

MAINTAINER=	demon@FreeBSD.org
COMMENT=	Library for working with graphs in Python, dot module

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pydot>=0:${PORTSDIR}/graphics/py-pydot \
		${PYTHON_PKGNAMEPREFIX}graph-core>=${PORTVERSION}:${PORTSDIR}/graphics/py-graph-core

PROJECTHOST=	python-graph
USE_PYTHON=	yes
USE_PYDISTUTILS=	easy_install
PYDISTUTILS_PKGNAME=	python_graph_dot
PYDISTUTILS_AUTOPLIST=	yes

.include <bsd.port.mk>
