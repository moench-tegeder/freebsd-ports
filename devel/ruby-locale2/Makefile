# Created by: stas
# $FreeBSD$

PORTNAME=	locale2
PORTVERSION=	2.0.5
CATEGORIES=	devel ruby
MASTER_SITES=	RF
MASTER_SITE_SUBDIR=	locale
PKGNAMEPREFIX=	${RUBY_PKGNAMEPREFIX}
DISTNAME=	ruby-locale-${PORTVERSION}
DIST_SUBDIR=	ruby

MAINTAINER=	ruby@FreeBSD.org
COMMENT=	Pure ruby library which provides basic APIs for localization

CONFLICTS=	${PKGNAMEPREFIX}locale-[0-9]*

USE_RUBY=	yes
USE_RUBY_SETUP=	yes

post-install:
	${MKDIR} ${STAGEDIR}${RUBY_MODDOCDIR}/
	${INSTALL_DATA} ${WRKSRC}/README.rdoc ${STAGEDIR}${RUBY_MODDOCDIR}/
	${MKDIR} ${STAGEDIR}${RUBY_MODEXAMPLESDIR}/
	@(cd ${WRKSRC}/samples/ && ${COPYTREE_SHARE} \* ${STAGEDIR}${RUBY_MODEXAMPLESDIR}/)

.include <bsd.port.mk>
