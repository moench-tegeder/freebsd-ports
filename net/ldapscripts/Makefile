# Created by: Ganael LAPLANCHE <ganael.laplanche@martymac.org>
# $FreeBSD$

PORTNAME=	ldapscripts
PORTVERSION=	2.0.5
PORTREVISION=	1
CATEGORIES=	net
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/${PORTNAME}-${PORTVERSION} \
		http://contribs.martymac.org/ldapscripts/
EXTRACT_SUFX=	.tgz

MAINTAINER=	martymac@FreeBSD.org
COMMENT=	Scripts to manage posix accounts in an OpenLDAP directory

LICENSE=	GPLv2

RUN_DEPENDS=	ldapadd:${PORTSDIR}/net/openldap${OPENLDAP_VER}-client \
		ldapsearch:${PORTSDIR}/net/openldap${OPENLDAP_VER}-client \
		ldapdelete:${PORTSDIR}/net/openldap${OPENLDAP_VER}-client \
		ldapmodify:${PORTSDIR}/net/openldap${OPENLDAP_VER}-client \
		ldapmodrdn:${PORTSDIR}/net/openldap${OPENLDAP_VER}-client \
		ldappasswd:${PORTSDIR}/net/openldap${OPENLDAP_VER}-client

USE_OPENLDAP=	yes
USES=		iconv
LIBDIR=	${PREFIX}/lib/${PORTNAME}
MAKE_ENV+=	MANDIR=${MANPREFIX}/man \
		ETCDIR=${ETCDIR}

SUB_FILES=	pkg-message

PORTDOCS=	README CHANGELOG VERSION TODO

# Unset 'all' target set by default to 'help'
# and set paths to OpenLDAP binaries
post-patch:
	${REINPLACE_CMD} "s|^all:.*|all:|g" ${WRKSRC}/Makefile
	${REINPLACE_CMD} "s|^PREFIX = .*|PREFIX = ${PREFIX}|g" ${WRKSRC}/Makefile
	${REINPLACE_CMD} \
	-e "s|^LDAPSEARCHBIN=.*|LDAPSEARCHBIN=\"${LOCALBASE}/bin/ldapsearch\"|g" \
	-e "s|^LDAPADDBIN=.*|LDAPADDBIN=\"${LOCALBASE}/bin/ldapadd\"|g" \
	-e "s|^LDAPDELETEBIN=.*|LDAPDELETEBIN=\"${LOCALBASE}/bin/ldapdelete\"|g" \
	-e "s|^LDAPMODIFYBIN=.*|LDAPMODIFYBIN=\"${LOCALBASE}/bin/ldapmodify\"|g" \
	-e "s|^LDAPMODRDNBIN=.*|LDAPMODRDNBIN=\"${LOCALBASE}/bin/ldapmodrdn\"|g" \
	-e "s|^LDAPPASSWDBIN=.*|LDAPPASSWDBIN=\"${LOCALBASE}/bin/ldappasswd\"|g" \
	-e "s|^ICONVBIN=.*|ICONVBIN=\"${LOCALBASE}/bin/iconv\"|g" \
	${WRKSRC}/etc/ldapscripts.conf

# Install remaining stuff
post-install:
	@${RM} ${STAGEDIR}${ETCDIR}/ldapscripts.conf \
		${STAGEDIR}${ETCDIR}/ldapscripts.passwd
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
