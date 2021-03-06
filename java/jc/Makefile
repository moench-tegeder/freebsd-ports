# Created by: Archie Cobbs <archie@FreeBSD.org>
# $FreeBSD$

PORTNAME=	jc
PORTVERSION=	1.4.7
PORTREVISION=	7
CATEGORIES=	java
MASTER_SITES=	SF/${PORTNAME}vm/JC%20source%20distribution/Release%20${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	JVM that converts class files to C source and compiles them with GCC

BROKEN=		Fails to build

BUILD_DEPENDS=	${LOCALBASE}/share/classpath/glibj.zip:${PORTSDIR}/java/classpath
LIB_DEPENDS=	popt.0:${PORTSDIR}/devel/popt

NO_PACKAGE=	Takes too many resources to build

MAN1=		jc.1

USES=		gmake
USE_JAVA=	yes
JAVA_BUILD=	jre
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-classpath=${LOCALBASE}
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
INFO=		jc
ONLY_FOR_ARCHS=	i386

NO_STAGE=	yes
.include <bsd.port.pre.mk>

post-install:
.for dir in ${PREFIX}/include/jc ${PREFIX}/lib/jc ${PREFIX}/share/jc
	@${FIND} ${dir} ! -type d | \
		${SED} 's,^${PREFIX}/,,' >> ${TMPPLIST}
	@${FIND} ${dir} -type d | ${SORT} -r | \
		${SED} 's,^${PREFIX}/,@dirrm ,' >> ${TMPPLIST}
	@if [ -f ${PREFIX}/lib/libjc.a ]; then \
		${ECHO} lib/libjc.a >> ${TMPPLIST}; \
	fi
.endfor

.include <bsd.port.post.mk>
