# Created by: Palle Girgensohn <girgen@pingpong.net>
# $FreeBSD$

PORTNAME=	postgresql
PORTREVISION=	1
CATEGORIES=	databases
PKGNAMESUFFIX?=	${DISTVERSION:R:S/.//}${COMPONENT}

MAINTAINER=	pgsql@FreeBSD.org
COMMENT=	The contrib utilities from the PostgreSQL distribution

LIB_DEPENDS=	libxslt.so:${PORTSDIR}/textproc/libxslt \
		libxml2.so:${PORTSDIR}/textproc/libxml2

USE_PGSQL=	yes
DEFAULT_VERSIONS=pgsql=94
MASTERDIR=	${.CURDIR}/../postgresql94-server

USES=		bison

BUILD_DIRS=	src/port src/common contrib
INSTALL_DIRS=	contrib

SLAVE_ONLY=	yes
COMPONENT=	-contrib
CONFIGURE_ARGS+=--with-libxslt --with-libxml --with-openssl --disable-nls
LDFLAGS+=	${PTHREAD_LIBS} -L${PREFIX}/lib

post-install:
	@- ${INSTALL_DATA} ${WRKSRC}/contrib/README ${STAGEDIR}${DOCSDIR}/extension/README

.include "${MASTERDIR}/Makefile"
