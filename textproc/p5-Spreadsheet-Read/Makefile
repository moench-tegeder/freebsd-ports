# Created by: Steve Wills <steve@mouf.net>
# $FreeBSD$

PORTNAME=	Spreadsheet-Read
PORTVERSION=	0.54
CATEGORIES=	textproc perl5
MASTER_SITES=	CPAN
MASTER_SITE_SUBDIR=	CPAN:HMBRAND
PKGNAMEPREFIX=	p5-
EXTRACT_SUFX=	.tgz

MAINTAINER=	swills@FreeBSD.org
COMMENT=	Read the data from a spreadsheet

LICENSE=	ART10 GPLv1
LICENSE_COMB=	dual

BUILD_DEPENDS=	p5-IO-stringy>0:${PORTSDIR}/devel/p5-IO-stringy \
		p5-Text-CSV_XS>0:${PORTSDIR}/textproc/p5-Text-CSV_XS \
		p5-Text-CSV>0:${PORTSDIR}/textproc/p5-Text-CSV \
		p5-Spreadsheet-ReadSXC>0:${PORTSDIR}/textproc/p5-Spreadsheet-ReadSXC \
		p5-Spreadsheet-ParseExcel>0:${PORTSDIR}/textproc/p5-Spreadsheet-ParseExcel
RUN_DEPENDS:=	${BUILD_DEPENDS}
TEST_DEPENDS=	p5-Test-NoWarnings>0:${PORTSDIR}/devel/p5-Test-NoWarnings

USES=		perl5
USE_PERL5=	configure

.include <bsd.port.mk>
