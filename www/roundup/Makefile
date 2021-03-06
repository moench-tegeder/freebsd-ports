# Created by: nbm
# $FreeBSD$

PORTNAME=	roundup
PORTVERSION=	1.4.21
CATEGORIES=	www python
MASTER_SITES=	CHEESESHOP

MAINTAINER=	sbz@FreeBSD.org
COMMENT=	Issue-Tracking System for Knowledge Workers

LICENSE=	PSFL

USES=		gettext
USE_PYTHON=	yes
USE_PYDISTUTILS=yes

OPTIONS_DEFINE=	SQLITE PGSQL MYSQL NLS
OPTIONS_DEFAULT=SQLITE NLS

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MSQLITE}
RUN_DEPENDS+=	${PYTHON_PKGNAMEPREFIX}sqlite3>0:${PORTSDIR}/databases/py-sqlite3
.endif

.if ${PORT_OPTIONS:MPGSQL}
RUN_DEPENDS+=	${PYTHON_SITELIBDIR}/psycopgmodule.so:${PORTSDIR}/databases/py-psycopg
.endif

.if ${PORT_OPTIONS:MMYSQL}
RUN_DEPENDS+=	${PYTHON_PKGNAMEPREFIX}MySQLdb>=0:${PORTSDIR}/databases/py-MySQLdb
.endif

.if ${PORT_OPTIONS:MNLS}
PLIST_SUB+=	NLS=""
.else
PLIST_SUB+=	NLS="@comment "
.endif

SCRIPTS=	roundup-admin roundup-demo roundup-gettext roundup-mailgw \
		roundup-server roundup-xmlrpc-server

post-install:
	${INSTALL_SCRIPT} ${SCRIPTS:S,^,${WRKSRC}/build/scripts-${PYTHON_VER}/,} ${STAGEDIR}${PREFIX}/bin
.for f in roundup-admin roundup-demo roundup-mailgw roundup-server
	${INSTALL_MAN} ${WRKSRC}/share/man/man1/${f}.1 ${STAGEDIR}${PREFIX}/man/man1
.endfor
.if ${PORT_OPTIONS:MNLS}
	@(cd ${WRKSRC}/build/share/locale/ && ${COPYTREE_SHARE} \* ${STAGEDIR}${PREFIX}/share/locale/)
.endif

.include <bsd.port.mk>
