# Created by: Edson Brandi <ebrandi@fugspbr.org>
# $FreeBSD$

PORTNAME=	dar
PORTVERSION=	2.4.14
CATEGORIES=	sysutils archivers
MASTER_SITES=	SF

MAINTAINER=	5u623l20@gmail.com
COMMENT=	Command-line backup tool, aimed for disks

LICENSE=	GPLv2 # (or later)

USES=		libtool shebangfix
SHEBANG_FILES=	doc/samples/dar_backup doc/samples/*.bash doc/samples/*.sh
USE_GCC=	any
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--datadir=${DATADIR} --disable-build-html \
		--disable-upx \
		--disable-ea-support --disable-nodump-flag \
		--disable-gnugetopt --disable-dar-static \
		--with-pkgconfigdir=${PREFIX}/libdata/pkgconfig
INSTALL_TARGET=	install-strip
USE_LDCONFIG=	yes

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

OPTIONS_DEFINE=		DOCS GCRYPT LZO NLS
OPTIONS_SUB=		yes

GCRYPT_CONFIGURE_ENABLE=libgcrypt-linking
GCRYPT_LIB_DEPENDS=	libgcrypt.so:${PORTSDIR}/security/libgcrypt
LZO_DESC=		Support lzo compression via liblzo2
LZO_LIB_DEPENDS=	liblzo2.so:${PORTSDIR}/archivers/lzo2
LZO_CONFIGURE_ENABLE=	liblzo2-linking
NLS_USES=		gettext
NLS_CONFIGURE_ENABLE=	nls

.include <bsd.port.options.mk>

.if ${OSVERSION} < 1000052
LIB_DEPENDS+=	libexecinfo.so:${PORTSDIR}/devel/libexecinfo
.endif

post-patch:
	@${REINPLACE_CMD} -e \
		's|(char \*\*) \(\&inptr,\)|\1| ; \
		 /LIBS/s|-lpthread|-pthread|' ${WRKSRC}/configure
	@${FIND} ${WRKSRC}/doc -name "Makefile.in" | ${XARGS} \
		${REINPLACE_CMD} -e \
		's|$$(pkgdatadir)|$$(docdir)|g'

.include <bsd.port.mk>
