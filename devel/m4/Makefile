# Created by: mr
# $FreeBSD$

PORTNAME=	m4
PORTVERSION=	1.4.17
PORTREVISION=	1
PORTEPOCH=	1
CATEGORIES=	devel
MASTER_SITES=	GNU

MAINTAINER=	johans@FreeBSD.org
COMMENT=	GNU m4

USES=		tar:bzip2
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--program-prefix=g
CONFIGURE_ENV=	MAKEINFO="makeinfo --no-split"

INFO=	m4

EXAMPLESDIR=	share/examples/gm4

OPTIONS_DEFINE=		LIBSIGSEGV
LIBSIGSEGV_DESC=	Use libsigsegv for better diagnostics
LIBSIGSEGV_LIB_DEPENDS=		libsigsegv.so:${PORTSDIR}/devel/libsigsegv
LIBSIGSEGV_CONFIGURE_ON=	--with-libsigsegv-prefix=${LOCALBASE}
LIBSIGSEGV_CONFIGURE_OFF=	--without-libsigsegv-prefix

post-install:
	@${MKDIR} ${STAGEDIR}${PREFIX}/${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/examples/*.m4 \
		${STAGEDIR}${PREFIX}/${EXAMPLESDIR}

.include <bsd.port.mk>
