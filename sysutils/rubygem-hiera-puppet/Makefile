# Created by: Greg Larkin <glarkin@FreeBSD.org>
# $FreeBSD$

PORTNAME=	hiera-puppet
PORTVERSION=	1.0.0
PORTREVISION=	1
CATEGORIES=	sysutils rubygems
MASTER_SITES=	RG

MAINTAINER=	mat@FreeBSD.org
COMMENT=	A data backend for Hiera that queries the Puppet scope for data

RUN_DEPENDS=	puppet27>=0:${PORTSDIR}/sysutils/puppet27 \
		rubygem-hiera>=1.0:${PORTSDIR}/sysutils/rubygem-hiera

CONFLICTS=	puppet-3.*

USE_RUBY=	yes
USE_RUBYGEMS=	yes
RUBYGEM_AUTOPLIST=	yes
PLIST_FILES=	bin/extlookup2hiera

.include <bsd.port.mk>
