# Created by: Hajimu UMEMOTO <ume@FreeBSD.org>
# $FreeBSD$

PORTNAME=	gkrellmvolume
PORTVERSION=	0.8
PORTREVISION=	8
CATEGORIES=	audio
MASTER_SITES=	http://gkrellm.luon.net/files/
DISTNAME=	volume-${PORTVERSION}

MAINTAINER=	ume@FreeBSD.org
COMMENT=	GKrellM volume plugin

DEPRECATED=	GKrellM 1.X is no longer being developed, consider using 2.X.
EXPIRATION_DATE=2014-06-30

BUILD_DEPENDS=	${LOCALBASE}/include/gkrellm/gkrellm.h:${PORTSDIR}/sysutils/gkrellm
RUN_DEPENDS=	gkrellm:${PORTSDIR}/sysutils/gkrellm

WRKSRC=		${WRKDIR}/volume

PLIST_FILES=	libexec/gkrellm/plugins/volume.so
USE_GNOME=	imlib
NO_STAGE=	yes

.include <bsd.port.mk>
