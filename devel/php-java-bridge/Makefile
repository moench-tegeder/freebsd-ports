# Created by: chinsan
# $FreeBSD$

PORTNAME=	php-java-bridge
PORTVERSION=	5.4.3
PORTREVISION=	1
CATEGORIES=	devel java
MASTER_SITES=	SF/${PORTNAME}/OldFiles
DISTNAME=	${PORTNAME}_${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	PHP module wich connects the PHP object with the Java/ECMA 335 object

USE_AUTOTOOLS=	autoconf:env automake:env libtool:env
GNU_CONFIGURE=	yes
USES=		gmake
USE_JAVA=	yes
JAVA_BUILD=	jdk

USE_PHP=	session
USE_PHPIZE=	yes
USE_PHPEXT=	yes
PHP_MODNAME=	java
DEFAULT_PHP_VER=53
IGNORE_WITH_PHP=5

WRKSRC=		${WRKDIR}/${PORTNAME}-${PORTVERSION}

NO_STAGE=	yes
do-configure:
	(cd ${WRKSRC}; ${SETENV} ${SCRIPTS_ENV} ${PHPBASE}/bin/phpize)
	(cd ${WRKSRC}; ./configure --with-java="${JAVA_HOME}")

post-install:
	${INSTALL_DATA} ${WRKSRC}/modules/JavaBridge.jar \
		${PREFIX}/lib/php/${PHP_EXT_DIR}
	${INSTALL_PROGRAM} ${WRKSRC}/modules/RunJavaBridge \
		${PREFIX}/lib/php/${PHP_EXT_DIR}
	${INSTALL_PROGRAM} ${WRKSRC}/modules/libnatcJavaBridge.so \
		${PREFIX}/lib/php/${PHP_EXT_DIR}
	${ECHO_CMD} "lib/php/${PHP_EXT_DIR}/JavaBridge.jar" \
		>> ${TMPPLIST}
	${ECHO_CMD} "lib/php/${PHP_EXT_DIR}/RunJavaBridge" \
		>> ${TMPPLIST}
	${ECHO_CMD} "lib/php/${PHP_EXT_DIR}/libnatcJavaBridge.so" \
	 	>> ${TMPPLIST}

.include <bsd.port.mk>
