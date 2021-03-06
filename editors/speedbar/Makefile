# Created by: Kimura Fuyuki <fuyuki@mj.0038.net>
# $FreeBSD$

PORTNAME=	speedbar
PORTVERSION=	0.14.b4
PORTREVISION=	8
CATEGORIES=	editors elisp
MASTER_SITES=	SF/cedet/${PORTNAME}/1.4beta4 \
		http://dryice.name/computer/FreeBSD/distfiles/

PKGNAMESUFFIX=	-${EMACS_PORT_NAME}
DISTNAME=	${PORTNAME}-${PORTVERSION:S/.b/beta/}

MAINTAINER=	dryice@dryice.name
COMMENT=	Quick access to files and tags in an Emacs frame

USE_EMACS=	yes
EMACS_PORT_NAME?=	emacs21

USES=		gmake
CONFLICTS=	cedet*

LISPDIR=	${PREFIX}/${EMACS_VERSION_SITE_LISPDIR}/speedbar

# We need to recompile these el's because of some incompatible changes
# in speedbar.
MUST_BE_RECOMPILED=	gud.el info.el rmail.el vhdl-mode.el

EMACS_ARGS=	 -batch -l speedbar-compile-script -f batch-byte-compile

NO_STAGE=	yes
pre-everything::
	@${ECHO_MSG} ""
	@${ECHO_MSG} "New version of speedbar is now in devel/cedet."
	@${ECHO_MSG} "Hit C-c now if you want the new version."
	@${ECHO_MSG} ""

pre-build:
.for i in ${MUST_BE_RECOMPILED}
	${CP} `${FIND} ${PREFIX}/${EMACS_LIBDIR_WITH_VER}/lisp -name ${i}` \
		${WRKSRC}
	${REINPLACE_CMD} -e 's/speedbar-attached-frame/dframe-attached-frame/' \
		${WRKSRC}/${i}
.endfor

post-build:
	cd ${WRKSRC}; ${EMACS_CMD} ${EMACS_ARGS} ${MUST_BE_RECOMPILED}

do-install:
	${MKDIR} ${LISPDIR}
.for i in *.el *.elc *.xpm
	${INSTALL_DATA} ${WRKSRC}/${i} ${LISPDIR}
.endfor
	${INSTALL_DATA} ${WRKSRC}/speedbar.info ${PREFIX}/info
	install-info ${PREFIX}/info/speedbar.info ${PREFIX}/info/dir

.include <bsd.port.mk>
