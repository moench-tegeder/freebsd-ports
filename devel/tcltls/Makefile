# Created by: mi@aldan.algebra.com
# $FreeBSD$

PORTNAME=	tcltls
PORTVERSION=	1.6
PORTREVISION=	1
CATEGORIES=	devel tcl
MASTER_SITES=	SF/tls/tls/${PORTVERSION}
DISTNAME=	tls${PORTVERSION}-src

MAINTAINER=	mi@aldan.algebra.com
COMMENT=	SSL extensions for TCL; dynamicly loadable

LICENSE=	TclTk
LICENSE_NAME=	Tcl/Tk License
LICENSE_FILE=	${WRKSRC}/license.terms
LICENSE_PERMS=	auto-accept dist-mirror dist-sell pkg-mirror pkg-sell

OPTIONS_DEFINE=	DOCS

USES+=		tcl
USE_OPENSSL=	yes
GNU_CONFIGURE=	yes
CONFIGURE_ARGS+=--exec-prefix=${PREFIX} \
		--with-tcl=${TCL_LIBDIR} \
		--with-ssl-dir=${OPENSSLBASE}

TCLPKG=		tls${PORTVERSION}
WRKSRC=		${WRKDIR}/${TCLPKG}
PLIST_FILES=	lib/${TCLPKG}/lib${TCLPKG}.so \
		lib/${TCLPKG}/pkgIndex.tcl \
		lib/${TCLPKG}/tls.tcl
PLIST_DIRS=	lib/${TCLPKG}
PORTDOCS=	*

.include <bsd.port.options.mk>

post-patch:
	${REINPLACE_CMD} -e \
		's,package require tls.*,load ${WRKSRC}/lib${TCLPKG}.so;\
			source ${WRKSRC}/tls.tcl,' \
		${WRKSRC}/tests/*.test
	# The tests in ciphers.test are meaningless so far:
	${MV} ${WRKSRC}/tests/ciphers.test ${WRKSRC}/tests/ciphers.test.broken

.if ${PORT_OPTIONS:MDOCS}
post-install:
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/tls.htm ${STAGEDIR}${DOCSDIR}
.endif

regression-test:
	cd ${WRKSRC}/tests && ${SETENV} TCL_LIBRARY="${WRKSRC}" \
		tclsh${TCL_VER} all.tcl

.include <bsd.port.mk>
