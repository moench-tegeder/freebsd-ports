# Created by: taguchi@tohoku.iij.ad.jp
# $FreeBSD$

PORTNAME=	tcl
PORTVERSION=	8.0.5
PORTREVISION=	2
CATEGORIES=	japanese lang tcl
MASTER_SITES=	${MASTER_SITE_TCLTK}
MASTER_SITE_SUBDIR=tcl8_0
DISTNAME=	${PORTNAME}${PORTVERSION}

PATCH_SITES=	ftp://ftp.sra.co.jp/pub/lang/tcl/jp/
PATCHFILES=	${PORTNAME}${PORTVERSION}jp1.7.patch.gz

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Japanized Tool Command Language, version 8.0

VERSION=	${PORTVERSION:R}
TOPDIR=		${WRKDIR}/${DISTNAME}
WRKSRC=		${TOPDIR}/unix
.if defined(PATCH_DEBUG)
PATCH_DIST_ARGS=-d ${TOPDIR} -E ${PATCH_DIST_STRIP}
.else
PATCH_DIST_ARGS=-d ${TOPDIR} --forward --quiet -E ${PATCH_DIST_STRIP}
.endif
USE_AUTOTOOLS=	autoconf213
CONFIGURE_ARGS=	--enable-shared
RANLIB=		ranlib
PKGINSTALL=	${PORTSDIR}/lang/tcl82/pkg-install.tclsh
PKGDEINSTALL=	${PORTSDIR}/lang/tcl82/pkg-deinstall.tclsh
USE_LDCONFIG=	yes

NO_STAGE=	yes
.include <bsd.port.pre.mk>

.if ${ARCH} == "sparc64"
BROKEN=		Does not compile on sparc64 (needs -fPIC)
.elif ${OSVERSION} >= 900000
BROKEN=		does not build
.endif

.if !defined(NOPORTDOCS)
post-patch:
	@${CP} ${FILESDIR}/README.FreeBSD.in ${TOPDIR}/README.FreeBSD.JP.in
	@${SED} -e 's%AC_OUTPUT(Makefile tclConfig.sh)%AC_OUTPUT(Makefile tclConfig.sh ../README.FreeBSD.JP)%' \
	  < ${WRKSRC}/configure.in \
	  > ${WRKSRC}/configure.in.tmp
	@${MV} -f ${WRKSRC}/configure.in.tmp ${WRKSRC}/configure.in
.endif

post-install:
.if !defined(NOPORTDOCS)
	@${MKDIR} ${PREFIX}/share/doc/tcl${VERSION}jp
	@(cd ${TOPDIR}; \
	  ${INSTALL_DATA} README changes README.FreeBSD.JP README.JP \
		changes.JP \
		Incompat80jp ${PREFIX}/share/doc/tcl${VERSION}jp; \
	 )
.endif
.if exists(${PKGINSTALL})
	${SETENV} PKG_PREFIX=${PREFIX} ${SH} ${PKGINSTALL}
.endif
	@${CAT}	${PKGMESSAGE}

test:
	cd ${WRKSRC} && ${MAKE} test

install-man:
	cd ${WRKSRC} && ${MAKE} install-man

.include <bsd.port.post.mk>
