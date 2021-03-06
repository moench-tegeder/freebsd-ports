# Created by: Sunpoet Po-Chuan Hsieh <sunpoet@FreeBSD.org>
# $FreeBSD$

PORTNAME=	npm
PORTVERSION=	1.4.12
CATEGORIES=	www
MASTER_SITES=	LOCAL/sunpoet

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Node package manager

LICENSE=	MIT

OPTIONS_DEFINE=	NODE_DEVEL
NODE_DEVEL_DESC=Use www/node-devel instead of www/node

NO_BUILD=	yes
USES=		tar:xz

MAKE_ARGS=	npm_config_prefix=${STAGEDIR}${PREFIX}
REINPLACE_ARGS=	-i ''

MANPREFIX=	${PREFIX}/lib/node_modules/npm

NODE_DEVEL_RUN_DEPENDS=	node-devel>=0.8.0:${PORTSDIR}/www/node-devel
NODE_DEVEL_RUN_DEPENDS_OFF=	node>=0.8.0:${PORTSDIR}/www/node

post-patch:
	@${REINPLACE_CMD} -e 's|node cli.js|& --cache ${WRKDIR}/.cache|; /^install: / s| docclean||' ${WRKSRC}/Makefile
	@${REINPLACE_CMD} -e 's|linkBins, linkMans|linkBins|' ${WRKSRC}/lib/build.js
	@${ECHO_CMD} "MANPATH ${MANPREFIX}/man" > ${WRKDIR}/npm.conf

post-install:
	@${INSTALL_DATA} ${WRKDIR}/npm.conf ${STAGEDIR}${PREFIX}/etc/man.d/npm.conf
	@${CHMOD} +x ${STAGEDIR}${PREFIX}/lib/node_modules/npm/bin/node-gyp-bin/node-gyp

# maintainer section:
# require: bash, git, gmake, perl, node

MS_DISTNAME=	${PORTNAME}-${MS_VERSION}
MS_TAGS=	${MS_WRKSRC}/tags
MS_VERSION=	`${CAT} ${MS_VERSIONFILE}`
MS_VERSIONFILE=	${MS_WRKSRC}/.version
MS_WRKSRC=	${WRKSRC}/tmp

GITHUB_PROJECT=	${PORTNAME}
GITHUB_TAGSURL=	https://github.com/npm/npm/tags
GITHUB_TARBALL=	https://github.com/${GITHUB_USER}/${GITHUB_PROJECT}/archive/${GITHUB_VERSION}.tar.gz
GITHUB_USER=	npm
GITHUB_VERSION=	v${MS_VERSION}

maketar: do-clean
	@${MKDIR} ${MS_WRKSRC}/
	@${FETCH_BINARY} ${FETCH_ARGS:C/A//} -o ${MS_WRKSRC}/tags ${GITHUB_TAGSURL}
	@${GREP} -o '/${GITHUB_USER}/${GITHUB_PROJECT}/archive/[^"]*\.tar\.gz' ${MS_WRKSRC}/tags | ${HEAD} -1 | ${CUT} -d/ -f5 | ${SED} 's|^v||; s|\.tar\.gz$$||' > ${MS_VERSIONFILE}
	@${ECHO_MSG} "*** Updating from ${PORTVERSION} to ${MS_VERSION} ..."
	@${FETCH_BINARY} ${FETCH_ARGS:C/A//} -o ${MS_WRKSRC}/${MS_DISTNAME}.tar.gz ${GITHUB_TARBALL}
	@${MKDIR} ${MS_WRKSRC}/${MS_DISTNAME}/
	@${TAR} -xf ${MS_WRKSRC}/${MS_DISTNAME}.tar.gz -C ${MS_WRKSRC}/${MS_DISTNAME}/ --strip-components 1
	@${REINPLACE_CMD} -e 's|ronn|marked|g' ${MS_WRKSRC}/${MS_DISTNAME}/Makefile ${MS_WRKSRC}/${MS_DISTNAME}/scripts/doc-build.sh
	@${REINPLACE_CMD} -e '/manRoot/ s|, "share"||' ${MS_WRKSRC}/${MS_DISTNAME}/lib/build.js ${MS_WRKSRC}/${MS_DISTNAME}/lib/unbuild.js
	@${REINPLACE_CMD} -e '1 s|#!/bin/bash|#!${LOCALBASE}/bin/bash|; s|make|gmake|; s|perl -pi|perl -p|' ${MS_WRKSRC}/${MS_DISTNAME}/scripts/doc-build.sh
	@${GREP} -lr share/man ${MS_WRKSRC}/${MS_DISTNAME}/doc/ ${MS_WRKSRC}/${MS_DISTNAME}/scripts/ | ${XARGS} -I % ${REINPLACE_CMD} 's|share/man|man|g' %
	@cd ${MS_WRKSRC}/${MS_DISTNAME}/ && ${GMAKE}
	@${FIND} ${MS_WRKSRC}/${MS_DISTNAME}/ -type d -exec ${CHMOD} 755 '{}' \;
	@${FIND} ${MS_WRKSRC}/${MS_DISTNAME}/ -type f -exec ${CHMOD} 644 '{}' \;
	@${FIND} ${MS_WRKSRC}/${MS_DISTNAME}/ -type f -name '*.sh' -exec ${CHMOD} 755 '{}' \;
	@cd ${MS_WRKSRC}/ && ${TAR} -Jcf ${MS_DISTNAME}.tar.xz ${MS_DISTNAME}/
	@${REINPLACE_CMD} -e '/^PORTVERSION=/ s|${PORTVERSION}|'${MS_VERSION}'|; /^PORTREVISION=/d' ${.CURDIR}/Makefile
	@sudo ${INSTALL} -m 644 ${MS_WRKSRC}/${PORTNAME}-${MS_VERSION}.tar.xz ${DISTDIR}/
	@cd ${.CURDIR}/ && ${MAKE_CMD} makesum

.include <bsd.port.mk>
