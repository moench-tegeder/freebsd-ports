# $FreeBSD$

PORTNAME=	jicmp6
PORTVERSION=	1.2.2
CATEGORIES=	net java
MASTER_SITES=	SF/opennms/JICMP6/stable-1.2

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Java native interface (JNI) to ICMPv6

USES=		libtool
USE_JAVA=	yes
JAVA_VERSION=	1.6
JAVA_VENDOR=	openjdk
JAVA_BUILD=	yes
JAVA_RUN=	yes
GNU_CONFIGURE=	yes
CONFIGURE_ENV=	JAVA_HOME=${JAVA_HOME}

PLIST_FILES=	lib/libjicmp6.so \
		share/java/jicmp6.jar

.include <bsd.port.mk>
