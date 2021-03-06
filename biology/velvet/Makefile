# Created by: Motomichi Matsuzaki <mzaki@m.u-tokyo.ac.jp>
# $FreeBSD$

PORTNAME=	velvet
PORTVERSION=	1.2.10
CATEGORIES=	biology
MASTER_SITES=	http://www.ebi.ac.uk/~zerbino/velvet/
DISTNAME=	${PORTNAME}_${PORTVERSION}
EXTRACT_SUFX=	.tgz

MAINTAINER=	mzaki@m.u-tokyo.ac.jp
COMMENT=	Sequence assembler for very short reads

ALL_TARGET=	default

MAXKMERLENGTH?=	31
VELVET_CATEGORIES?=	2
MAKE_ENV+=	MAXKMERLENGTH=${MAXKMERLENGTH} CATEGORIES=${VELVET_CATEGORIES}

USES=		perl5 gmake
USE_PERL5=	run

BINARIES=	velvetg velveth
SCRIPTS=	contrib/shuffleSequences_fasta/shuffleSequences_fasta.pl \
		contrib/shuffleSequences_fasta/shuffleSequences_fastq.pl \
		contrib/VelvetOptimiser-2.2.4/VelvetOptimiser.pl \
		contrib/afg_handling/asmbly_splitter.pl \
		contrib/afg_handling/snp_view.pl \
		contrib/columbus_scripts/enlarge_exons.pl \
		contrib/columbus_scripts/gff2fasta.pl \
		contrib/columbus_scripts/merge_gtf_exons.pl \
		contrib/estimate-exp_cov/velvet-estimate-exp_cov.pl \
		contrib/extractContigReads/extractContigReads.pl \
		contrib/fasta2agp/fasta2agp.pl \
		contrib/observed-insert-length.pl/observed-insert-length.pl \
		contrib/read_prepare/pe_read_prepare.0.1.pl \
		contrib/select_paired/select_paired.pl \
		contrib/show_repeats/show_repeats.pl
PERLMOD_DIRS=	contrib/VelvetOptimiser-2.2.4/VelvetOpt
PERLMOD_FILES=	contrib/VelvetOptimiser-2.2.4/VelvetOpt/Assembly.pm \
		contrib/VelvetOptimiser-2.2.4/VelvetOpt/Utils.pm \
		contrib/VelvetOptimiser-2.2.4/VelvetOpt/gwrap.pm \
		contrib/VelvetOptimiser-2.2.4/VelvetOpt/hwrap.pm

.if !defined(WITHOUT_PYTHON)
USE_PYTHON=	yes
SCRIPTS+=	contrib/AssemblyAssembler1.3/AssemblyAssembler1.3.py
.endif

.for f in ${BINARIES} ${SCRIPTS}
PLIST_FILES+=	bin/${f:T}
.endfor
.for d in ${PERLMOD_DIRS}
PLIST_DIRS+=	%%SITE_PERL%%/${d:T}
.endfor
.for f in ${PERLMOD_FILES}
PLIST_FILES+=	%%SITE_PERL%%/${f:H:T}/${f:T}
.endfor

PORTDOCS=	ChangeLog Manual.pdf Columbus_manual.pdf

OPTIONS_DEFINE=	DOCS

.include <bsd.port.options.mk>

post-patch:
.for f in ${SCRIPTS}
	${REINPLACE_CMD} -e s,#!/usr/bin/perl,${PERL}, ${WRKSRC}/${f}
.endfor
.if !defined(WITHOUT_PYTHON)
	${REINPLACE_CMD} -e s,#!/usr/bin/python,${PYTHON_CMD}, ${WRKSRC}/contrib/AssemblyAssembler1.3/AssemblyAssembler1.3.py
.endif

do-install:
.for f in ${BINARIES}
	${INSTALL_PROGRAM} ${WRKSRC}/${f} ${STAGEDIR}${PREFIX}/bin
.endfor
.for f in ${SCRIPTS}
	${INSTALL_SCRIPT} ${WRKSRC}/${f} ${STAGEDIR}${PREFIX}/bin/${f:T}
.endfor
.for d in ${PERLMOD_DIRS}
	${MKDIR} ${STAGEDIR}${PREFIX}/${SITE_PERL_REL}/${d:T}
.endfor
.for f in ${PERLMOD_FILES}
	${INSTALL_DATA} ${WRKSRC}/${f} ${STAGEDIR}${PREFIX}/${SITE_PERL_REL}/${f:H:T}/${f:T}
.endfor
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_MAN} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
