# Created by: Nicola Vitale <nivit@FreeBSD.org>
# $FreeBSD$

PORTNAME=	jspacker
DISTVERSION=	1.00b
CATEGORIES=	www
MASTER_SITES=	http://nivi.interfree.it/distfiles/${PORTNAME}/ \
		http://deanedwards.googlecode.com/svn/trunk/download/
DISTNAME=	packer2.perl

MAINTAINER=	nivit@FreeBSD.org
COMMENT=	JavaScript compressor/obfuscator (Perl version)

JSPACKER=	jsPacker.pl

NO_BUILD=	yes
NO_WRKSUBDIR=	yes

USES=		perl5 zip
USE_PERL5=	run

SUB_FILES=	${PORTNAME}
SUB_LIST=	JSPACKER=${JSPACKER} \
		PERL5=${PERL5}

do-install:
	${INSTALL_SCRIPT} ${WRKDIR}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/${PORTNAME}
	${MKDIR} ${STAGEDIR}${DATADIR} && \
	cd ${WRKSRC} && \
	${INSTALL_DATA} *.pm ${STAGEDIR}${DATADIR} && \
	${INSTALL_SCRIPT} ${JSPACKER} ${STAGEDIR}${DATADIR}
.if !defined(NOPORTEXAMPLES)
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR} && \
	cd ${WRKSRC} && \
	${INSTALL_DATA} *.htm ${STAGEDIR}${EXAMPLESDIR}
.endif

.include <bsd.port.mk>
