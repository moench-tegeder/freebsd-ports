# Created by: gahr
# $FreeBSD$

PORTNAME=	catch
PORTVERSION=	1.0.47
CATEGORIES=	devel

MAINTAINER=	gahr@FreeBSD.org
COMMENT=	Header-only test framework for C++

LICENSE=	BSL

USE_GITHUB=	yes
GH_ACCOUNT=	gahr
GH_PROJECT=	Catch
GH_COMMIT=	48fac9c

NO_BUILD=	yes

PLIST_FILES=	include/catch.hpp

do-install:
	${INSTALL_DATA} ${WRKSRC}/single_include/catch.hpp \
	    ${STAGEDIR}${PREFIX}/include

.include <bsd.port.mk>
