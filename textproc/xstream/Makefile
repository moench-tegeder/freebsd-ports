# Created by: Alex Dupre <ale@FreeBSD.org>
# $FreeBSD$

PORTNAME=	xstream
PORTVERSION=	1.4.3
CATEGORIES=	textproc java
MASTER_SITES=	https://nexus.codehaus.org/content/repositories/releases/com/thoughtworks/xstream/xstream-distribution/${PORTVERSION}/
DISTFILES=	${PORTNAME}-distribution-${PORTVERSION}-bin${EXTRACT_SUFX}

MAINTAINER=	ale@FreeBSD.org
COMMENT=	A simple library to serialize Java objects to XML

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

OPTIONS_DEFINE=	DOCS

USES=		zip
USE_JAVA=	yes
NO_BUILD=	yes

PLIST_FILES=	%%JAVAJARDIR%%/${PORTNAME}.jar

PORTDOCS=	*

.include <bsd.port.options.mk>

do-install:
	@${ECHO_MSG} -n ">> Installing JAR as ${JAVAJARDIR}/${PORTNAME}.jar..."
	@${INSTALL_DATA} ${WRKSRC}/lib/${DISTNAME}.jar \
		${STAGEDIR}${JAVAJARDIR}/${PORTNAME}.jar
	@${ECHO_MSG} " [ DONE ]"
.if ${PORT_OPTIONS:MDOCS}
	@${ECHO_MSG} -n ">> Installing documentation in ${DOCSDIR}..."
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	@${INSTALL_DATA} ${WRKSRC}/README.txt ${STAGEDIR}${DOCSDIR}/
	@${ECHO_MSG} " [ DONE ]"
.endif

.include <bsd.port.mk>
