# Created by: Eduard Martinescu
# $FreeBSD$

PORTNAME=	smartmontools
PORTVERSION=	6.2
PORTREVISION=	2
CATEGORIES=	sysutils
MASTER_SITES=	SF

MAINTAINER=	samm@os2.kiev.ua
COMMENT=	S.M.A.R.T. disk monitoring tools

LICENSE=	GPLv2

CONFLICTS=	smartmontools-devel-[0-9]*

OPTIONS_DEFINE=	DOCS
DOCS_CONFIGURE_OFF=	--without-docdir --without-exampledir
DOCS_CONFIGURE_ON=	--with-docdir=${DOCSDIR}

USES=		gmake
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--disable-dependency-tracking \
		--enable-drivedb --enable-sample \
		--with-initscriptdir=${PREFIX}/etc/rc.d

SUB_FILES=	pkg-message smart
USE_RC_SUBR=	smartd

PORTDOCS=	*

post-patch:
	@${REINPLACE_CMD} -e 's| install-initdDATA| |' ${WRKSRC}/Makefile.in

post-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/periodic/daily
	${INSTALL_SCRIPT} ${WRKDIR}/smart \
		${STAGEDIR}${PREFIX}/etc/periodic/daily

.include <bsd.port.mk>
