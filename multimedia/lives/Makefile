# Created by: Andrew Pantyukhin <infofarmer@FreeBSD.org>
# $FreeBSD$

PORTNAME=	lives
PORTVERSION=	2.2.4
PORTREVISION=	1
CATEGORIES=	multimedia
MASTER_SITES=	http://salsaman.home.xs4all.nl/lives/current/
DISTNAME=	LiVES-${PORTVERSION}

MAINTAINER=	pawel@FreeBSD.org
COMMENT=	Video editing system

LICENSE=	GPLv3

BUILD_DEPENDS=	${LOCALBASE}/include/linux/input.h:${PORTSDIR}/multimedia/v4l_compat \
		${LOCALBASE}/bin/analyseplugin:${PORTSDIR}/audio/ladspa
LIB_DEPENDS=	libasound.so:${PORTSDIR}/audio/alsa-lib \
		libjack.so:${PORTSDIR}/audio/jack \
		libpulse.so:${PORTSDIR}/audio/pulseaudio \
		liboil-0.3.so:${PORTSDIR}/devel/liboil \
		libvisual-0.4.so:${PORTSDIR}/graphics/libvisual04 \
		libopencv_calib3d.so:${PORTSDIR}/graphics/opencv \
		libfftw3.so:${PORTSDIR}/math/fftw3 \
		libfftw3f.so:${PORTSDIR}/math/fftw3-float \
		libavcodec.so:${PORTSDIR}/multimedia/ffmpeg \
		libdv.so:${PORTSDIR}/multimedia/libdv \
		libmjpegutils.so:${PORTSDIR}/multimedia/mjpegtools \
		libschroedinger-1.0.so:${PORTSDIR}/multimedia/schroedinger
RUN_DEPENDS=	${LOCALBASE}/bin/analyseplugin:${PORTSDIR}/audio/ladspa \
		mpg123:${PORTSDIR}/audio/mpg123 \
		sox:${PORTSDIR}/audio/sox \
		ogg123:${PORTSDIR}/audio/vorbis-tools \
		convert:${PORTSDIR}/graphics/ImageMagick \
		sswf:${PORTSDIR}/graphics/sswf \
		mencoder:${PORTSDIR}/multimedia/mencoder \
		mplayer:${PORTSDIR}/multimedia/mplayer \
		ogmmerge:${PORTSDIR}/multimedia/ogmtools \
		transcode:${PORTSDIR}/multimedia/transcode \
		x264:${PORTSDIR}/multimedia/x264 \
		cdrecord:${PORTSDIR}/sysutils/cdrtools

WRKSRC=		${WRKDIR}/${DISTNAME:tl}

USES=		libtool pathfix perl5 pkgconfig shebangfix tar:bzip2 
SHEBANG_FILES=	build-lives-rfx-plugin build-lives-rfx-plugin-multi \
		smogrify tools/autolives.pl
GNU_CONFIGURE=	yes
USE_CSTD=	gnu89
USE_PYTHON=	yes
USE_GHOSTSCRIPT_RUN=	yes
USE_GNOME=	gtk20
USE_LDCONFIG=	yes

CONFIGURE_ARGS=	--disable-ldvgrab --disable-gtk3
INSTALL_TARGET=	install-strip

CPPFLAGS+=	-I${LOCALBASE}/include -fPIC
LDFLAGS+=	-L${LOCALBASE}/lib -pthread

DOC_FILES=	AUTHORS BUGS ChangeLog FEATURES GETTING.STARTED README \
		OMC/lives-OMC.txt RFX/LiVES-Perl.odt RFX/rfxbuilder.odt \
		RFX/RFX.spec docs/clip_format.txt \
		lives-plugins/marcos-encoders/README.multi_encoder \
		weed-docs/weedspec.txt weed-docs/weedevents.txt

PORT_VERBS=	lives LiVES _encoder.py midistart midistop smogrify sendOSC

OPTIONS_DEFINE=	DOCS DOXYGEN FREI0R MATROSKA NLS
OPTIONS_SUB=	yes

DOXYGEN_BUILD_DEPENDS=	doxygen:${PORTSDIR}/devel/doxygen
DOXYGEN_CONFIGURE_OFF=	--disable-doxygen
FREI0R_BUILD_DEPENDS=	frei0r>0:${PORTSDIR}/graphics/frei0r
FREI0R_RUN_DEPENDS=	frei0r>0:${PORTSDIR}/graphics/frei0r
MATROSKA_RUN_DEPENDS=	mkvmerge:${PORTSDIR}/multimedia/mkvtoolnix
NLS_USES=		gettext
NLS_CONFIGURE_OFF=	--disable-nls

.include <bsd.port.options.mk>

.if ! ${PORT_OPTIONS:MFREI0R}
CONFIGURE_ENV+=	ac_cv_header_frei0r_h=no
.endif

post-patch:
	@${REINPLACE_CMD} -e 's| install-docDATA||g; s|-$$(VERSION)||g' \
		${WRKSRC}/Makefile.in
	@${REINPLACE_CMD} -e 's|: install-data-local |: |g; s|-ldl||' \
		${WRKSRC}/lives-plugins/weed-plugins/gdk/Makefile.in \
		${WRKSRC}/lives-plugins/weed-plugins/Makefile.in
	@${REINPLACE_CMD} -e 's|off64_t|off_t|g ; s|lseek64|lseek|g' \
		${WRKSRC}/src/audio.c \
		${WRKSRC}/lives-plugins/plugins/decoders/dv_decoder.c \
		${WRKSRC}/lives-plugins/plugins/decoders/ogg_decoder.h
	@${REINPLACE_CMD} -e 's|/usr/local/lib/|${LOCALBASE}/lib/|g' \
		${WRKSRC}/lives-plugins/weed-plugins/frei0r.c
	@${REINPLACE_CMD} 's|/bin/touch|/usr/bin/touch|g' \
		${WRKSRC}/src/callbacks.c \
		${WRKSRC}/src/saveplay.c \
		${WRKSRC}/src/utils.c
	@${REINPLACE_CMD} '/cp -rf/ s|data/|data|g; /cp -rf/ s|icons/|icons|g' \
		${WRKSRC}/lives-plugins/weed-plugins/cairo/Makefile.in \
		${WRKSRC}/lives-plugins/weed-plugins/Makefile.in

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${DOC_FILES:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}
	cd ${STAGEDIR}${PREFIX}/bin && ${RM} lives && ${LN} -s lives-exe lives

.if ${PORT_OPTIONS:MDOXYGEN}
	@cd ${STAGEDIR}${PREFIX} && \
	${FIND} ${DOCSDIR:S|${PREFIX}/||}/html ! -type d >> ${TMPPLIST} && \
	${FIND} ${DOCSDIR:S|${PREFIX}/||} -type d | ${SORT} -r | \
	${SED} 's|^|@dirrm |' >> ${TMPPLIST}
.endif

.include <bsd.port.mk>
