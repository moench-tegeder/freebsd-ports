# Created by: Stacey D. Son <sds@son.org>
# $FreeBSD$

PORTNAME=	aoe
PORTVERSION=	1.2.0
CATEGORIES=	net kld
MASTER_SITES=	http://www.son.org/download/
DISTNAME=	${PORTNAME}-freebsd-${PORTVERSION}

MAINTAINER=	fjoe@FreeBSD.org
COMMENT=	FreeBSD driver for ATA over Ethernet (AoE)

NO_PACKAGE=	Should be in sync with the kernel to work correctly
SSP_UNSAFE=	kernel module does not support ssp

WRKSRC=		${WRKDIR}/dev/aoe
MAN4=		aoe.4
USE_RC_SUBR=	aoe

NO_STAGE=	yes
pre-everything::
	@if [ ! -f /usr/src/sys/Makefile ]; then \
		${ECHO_MSG} ">> The AoE port needs FreeBSD kernel source code to compile."; \
		${ECHO_MSG} ">> Please install FreeBSD kernel source code in /usr/src/sys."; \
		${FALSE}; \
	fi

do-install:
	${MKDIR} ${PREFIX}/lib/aoe
	${INSTALL_KLD} ${WRKSRC}/aoe.ko ${PREFIX}/lib/aoe
	${INSTALL_MAN} ${WRKDIR}/aoe.4 ${PREFIX}/man/man4
	${CAT} ${PKGMESSAGE}

.include <bsd.port.mk>
