# Created by: Miklos Niedermayer <mico@bsd.hu>
# $FreeBSD$

PORTNAME=	mysql++
PORTVERSION=	1.7.40
PORTREVISION=	2
CATEGORIES=	databases devel
MASTER_SITES=	http://tangentsoft.net/mysql++/releases/
PKGNAMESUFFIX=	1-mysql${MYSQL_VER}

MAINTAINER=	sergey@network-asp.biz
COMMENT=	Complex C++ API for MySQL${MYSQL_VER}

USE_MYSQL=	yes
USE_AUTOTOOLS=	libtool
CONFIGURE_ARGS=	--with-mysql=${LOCALBASE} \
		--includedir=${PREFIX}/include/mysql++ \
		--disable-examples
USE_LDCONFIG=	yes

CONFLICTS=	${PORTNAME}*-2.*

post-install:
.if !defined(NOPORTDOCS)
	@${MKDIR} ${STAGEDIR}${DOCSDIR}/userman/html ${STAGEDIR}${DOCSDIR}/refman/html
	@${INSTALL_DATA} ${WRKSRC}/doc/userman/html/* ${STAGEDIR}${DOCSDIR}/userman/html
	@${INSTALL_DATA} ${WRKSRC}/doc/refman/html/* ${STAGEDIR}${DOCSDIR}/refman/html
	@${INSTALL_DATA} ${WRKSRC}/doc/*.pdf ${STAGEDIR}${DOCSDIR}
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	@${INSTALL_DATA} ${WRKSRC}/examples/*.cpp ${STAGEDIR}${EXAMPLESDIR}
	@${INSTALL_DATA} ${WRKSRC}/examples/*.h ${STAGEDIR}${EXAMPLESDIR}
	@${INSTALL_DATA} ${WRKSRC}/examples/README ${STAGEDIR}${EXAMPLESDIR}
	@${INSTALL_DATA} ${WRKSRC}/examples/Makefile.simple ${STAGEDIR}${EXAMPLESDIR}/Makefile.temp
	@${SED} -e "s|/usr/include/mysql++|${PREFIX}/include/mysql++|" < ${STAGEDIR}${EXAMPLESDIR}/Makefile.temp | \
		${SED} -e "s|/usr/include/mysql|${LOCALBASE}/include/mysql|" | \
		${SED} -e "s|-lmysqlpp|-L${PREFIX}/lib -L${LOCALBASE}/lib/mysql -lmysqlpp|" \
		> ${STAGEDIR}${EXAMPLESDIR}/Makefile
	@${RM} -f ${STAGEDIR}${EXAMPLESDIR}/Makefile.temp
.endif

.include <bsd.port.mk>
