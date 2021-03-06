# Created by: Nicole Reid <root@cooltrainer.org>
# $FreeBSD$

PORTNAME=	visualboyadvance-m
PORTVERSION=	1.8.0r${SVN_REV}
CATEGORIES=	emulators
MASTER_SITES=	https://cooltrainer.org/freebsd-ports/visualboyadvance-m/

MAINTAINER=	root@cooltrainer.org
COMMENT=	Game Boy Advance emulator with GTK frontend

LICENSE=	GPLv2

LIB_DEPENDS=	libpng15.so:${PORTSDIR}/graphics/png \
		libsfml-system.so:${PORTSDIR}/devel/sfml

OPTIONS_DEFINE=	NLS FFMPEG LINK LIRC DEBUGGER
OPTIONS_MULTI=	INTERFACE
OPTIONS_MULTI_INTERFACE=	GVBAM SDL
OPTIONS_DEFINE_i386=	ASMCORE	ASMSCALERS
OPTIONS_DEFAULT=	DEBUGGER SDL
OPTIONS_SUB=	yes

GVBAM_DESC=	Enable GTK interface
SDL_DESC=	Enable SDL interface
FFMPEG_DESC=	Enable FFmpeg A/V recording
LINK_DESC=	Enable GBA linking functionality
LIRC_DESC=	Enable LIRC infrared support
DEBUGGER_DESC=	Enable the debugger
ASMCORE_DESC=	Enable x86 ASM CPU cores (i386 only)
ASMSCALERS_DESC=	Enable x86 ASM graphic filters (i386 only)

NLS_USES=	gettext
WANT_GNOME=	yes
DOS2UNIX_REGEX=	.*\.(c|cpp|h|ypp)
USE_XORG=	x11 xext
USE_GL=		gl glu
USE_SDL=	sdl
USES=		cmake dos2unix pkgconfig tar:bzip2
INSTALLS_ICONS=	yes
SVN_REV=	1231
CMAKE_ARGS+=	-DVERSION:STRING="${PORTVERSION}" \
		-DSYSCONFDIR:STRING="${PREFIX}/etc"  \
		-DENABLE_WX:BOOL=no

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MASMCORE} || ${PORT_OPTIONS:MASMSCALERS}
BUILD_DEPENDS+=	as:${PORTSDIR}/devel/binutils
.if ${PORT_OPTIONS:MASMCORE}
CMAKE_ARGS+=	-DENABLE_ASM_CORE:BOOL=yes
.else
CMAKE_ARGS+=	-DENABLE_ASM_CORE:BOOL=no
.endif
.if ${PORT_OPTIONS:MASMSCALERS}
CMAKE_ARGS+=	-DENABLE_ASM_SCALERS:BOOL=yes
.else
CMAKE_ARGS+=	-DENABLE_ASM_SCALERS:BOOL=no
.endif
.endif

.if ${PORT_OPTIONS:MGVBAM}
USE_GNOME=	gtk20
LIB_DEPENDS+=	libgtkmm-2.4.so:${PORTSDIR}/x11-toolkits/gtkmm24 \
		libglibmm-2.4.so:${PORTSDIR}/devel/glibmm \
		libgiomm-2.4.so:${PORTSDIR}/devel/glibmm \
		libcairomm-1.0.so:${PORTSDIR}/graphics/cairomm \
		libglademm-2.4.so:${PORTSDIR}/devel/libglademm24 \
		libgdkglextmm-x11-1.2.so:${PORTSDIR}/x11-toolkits/gtkglextmm
CMAKE_ARGS+=	-DENABLE_GTK:BOOL=yes
USES+=	desktop-file-utils
.else
CMAKE_ARGS+=	-DENABLE_GTK:BOOL=no
.endif

.if ${PORT_OPTIONS:MSDL}
.if !${PORT_OPTIONS:MDEBUGGER}
BROKEN=	SDL requires DEBUGGER
.endif
CMAKE_ARGS+=	-DENABLE_SDL:BOOL=yes
.else
CMAKE_ARGS+=	-DENABLE_SDL:BOOL=no
.endif

.if ${PORT_OPTIONS:MDEBUGGER}
CMAKE_ARGS+=	-DENABLE_DEBUGGER:BOOL=yes
.else
CMAKE_ARGS+=	-DENABLE_DEBUGGER:BOOL=no
.endif

.if ${PORT_OPTIONS:MFFMPEG}
LIB_DEPENDS+=	libavcodec.so:${PORTSDIR}/multimedia/ffmpeg
CMAKE_ARGS+=	-DENABLE_FFMPEG:BOOL=yes
.else
CMAKE_ARGS+=	-DENABLE_FFMPEG:BOOL=no
.endif

.if ${PORT_OPTIONS:MNLS}
CMAKE_ARGS+=	-DENABLE_NLS:BOOL=yes
.else
CMAKE_ARGS+=	-DENABLE_NLS:BOOL=no
.endif

.if ${PORT_OPTIONS:MLINK}
CMAKE_ARGS+=	-DENABLE_LINK:BOOL=yes
.else
CMAKE_ARGS+=	-DENABLE_LINK:BOOL=no
.endif

.if ${PORT_OPTIONS:MLIRC}
LIB_DEPENDS+=	liblirc_client.so:${PORTSDIR}/comms/lirc
RUN_DEPENDS+=	lircd:${PORTSDIR}/comms/lirc
CMAKE_ARGS+=	-DENABLE_LIRC:BOOL=yes
.else
CMAKE_ARGS+=	-DENABLE_LIRC:BOOL=no
.endif

post-patch:
	@${REINPLACE_CMD} -e 's|/usr/local|${LOCALBASE}|g' ${WRKSRC}/CMakeScripts/FindSFML.cmake

maint-gen-distfile:
	@if [ -f ${DISTDIR}/${DISTNAME}${EXTRACT_SUFX} ]; then \
		${ECHO_CMD} "ERROR: the distfile already exists."; \
		${FALSE}; \
	fi
	svn export -r${SVN_REV} \
		 https://svn.code.sf.net/p/vbam/code/trunk/ ${DISTNAME}
	${TAR} jcf ${DISTDIR}/${DISTNAME}${EXTRACT_SUFX} ${DISTNAME}
	${RM} -rf ${DISTNAME}

.include <bsd.port.mk>
