# Created by: Vladimir Chukharev
# $FreeBSD$

PORTNAME=	robotframework-ride
PORTVERSION=	1.3
CATEGORIES=	devel www python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	Vladimir.Chukharev@gmail.com
COMMENT=	Test data editor for Robot Framework

LICENSE=	APACHE20

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}robotframework>=2.7.5:${PORTSDIR}/devel/py-robotframework \
		${PYTHON_PKGNAMEPREFIX}robotframework-selenium2library>=1.1.0:${PORTSDIR}/devel/py-robotframework-selenium2library \
		${PYTHON_PKGNAMEPREFIX}pygments>0:${PORTSDIR}/textproc/py-pygments

USE_PYTHON=	2
USE_PYDISTUTILS=	yes
PYDISTUTILS_AUTOPLIST=	yes
USE_WX=		2.8+
WX_COMPS=	python:run

.include <bsd.port.mk>
