# Created by: Micha�l Gr�newald
# $FreeBSD$

PORTNAME=	classes
PORTVERSION=	4.00
CATEGORIES=	devel
MASTER_SITES=	http://wwwfun.kurims.kyoto-u.ac.jp/soft/olabl/dist/
PKGNAMEPREFIX=	ocaml-
DISTNAME=	ocaml-${PORTNAME}-${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Ocaml Object interface for ocaml's standard library modules

LICENSE=	LGPL21

BUILD_DEPENDS=	ocamlc:${PORTSDIR}/lang/ocaml
RUN_DEPENDS:=	${BUILD_DEPENDS}

MAKE_ENV=	INSTALL="${INSTALL_DATA}"

.include <bsd.port.mk>
