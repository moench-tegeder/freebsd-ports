# Created by: Max Khon
# $FreeBSD$

PORTNAME=	sqpack
PORTVERSION=	1.2.4
PORTREVISION=	2
CATEGORIES=	news mail
MASTER_SITES=	SF/husky/${PORTNAME}/1.2-release
DISTNAME=	${PORTNAME}-${PORTVERSION}-src

MAINTAINER=	fjoe@FreeBSD.org
COMMENT=	Message base packer

LIB_DEPENDS=	fidoconfig.0:${PORTSDIR}/news/husky-fidoconf

MAN1=		sqpack.1
MANCOMPRESSED=	yes
PLIST_FILES=	bin/sqpack

NO_STAGE=	yes
post-patch:
	@${REINPLACE_CMD} -e 's^/etc/fido/config^${PREFIX}/etc/fido/config^' \
		${WRKSRC}/sqpack.1

.include "${.CURDIR}/../husky-base/Makefile.inc"
.include <bsd.port.mk>
