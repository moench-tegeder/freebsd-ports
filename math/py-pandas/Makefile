# $FreeBSD$

PORTNAME=	pandas
PORTVERSION=	0.14.0
CATEGORIES=	math devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	john@saltant.com
COMMENT=	Flexible, high-performance data analysis in Python

LICENSE=	BSD3CLAUSE

BUILD_DEPENDS=	${PYNUMPY}
RUN_DEPENDS:=	${BUILD_DEPENDS} \
		${PYTHON_PKGNAMEPREFIX}dateutil>0:${PORTSDIR}/devel/py-dateutil \
		${PYTHON_PKGNAMEPREFIX}pytz>0:${PORTSDIR}/devel/py-pytz \
		${PYTHON_PKGNAMEPREFIX}sqlite3>0:${PORTSDIR}/databases/py-sqlite3
TEST_DEPENDS:=	${RUN_DEPENDS} \
		nosetests:${PORTSDIR}/devel/py-nose \
		cython:${PORTSDIR}/lang/cython \
		${PYTHON_PKGNAMEPREFIX}boto>0:${PORTSDIR}/devel/py-boto \
		${PYTHON_PKGNAMEPREFIX}lxml>0:${PORTSDIR}/devel/py-lxml \
		${PYTHON_PKGNAMEPREFIX}tables>0:${PORTSDIR}/devel/py-tables \
		${PYTHON_PKGNAMEPREFIX}bottleneck>0:${PORTSDIR}/math/py-bottleneck \
		${PYTHON_PKGNAMEPREFIX}matplotlib>0:${PORTSDIR}/math/py-matplotlib \
		${PYTHON_PKGNAMEPREFIX}numexpr>0:${PORTSDIR}/math/py-numexpr \
		${PYTHON_PKGNAMEPREFIX}scipy>0:${PORTSDIR}/science/py-scipy \
		${PYTHON_PKGNAMEPREFIX}openpyxl1<2.0.0:${PORTSDIR}/textproc/py-openpyxl1 \
		${PYTHON_PKGNAMEPREFIX}xlrd>0:${PORTSDIR}/textproc/py-xlrd \
		${PYTHON_PKGNAMEPREFIX}xlwt>0:${PORTSDIR}/textproc/py-xlwt \
		${PYTHON_PKGNAMEPREFIX}beautifulsoup>0:${PORTSDIR}/www/py-beautifulsoup \
		${PYTHON_PKGNAMEPREFIX}html5lib>0:${PORTSDIR}/www/py-html5lib
# Note: we cannot include math/py-statsmodels in TEST_DEPENDS because it
# depends upon us for BUILD and RUN.

OPTIONS_DEFINE=		MPL SCIPY
OPTIONS_GROUP=		ACCEL STORAGE HTML EXCEL
OPTIONS_GROUP_ACCEL=	BTLNCK NUMEXPR
OPTIONS_GROUP_STORAGE=	BOTO TABLES
OPTIONS_GROUP_HTML=	LXML HTML5LIB
OPTIONS_GROUP_EXCEL=	OPENPYXL XLRD XLWT

MPL_DESC=	Support graphical plotting output via math/py-matplotlib
SCIPY_DESC=	Support various statistical functions via science/py-scipy
BTLNCK_DESC=	Accelerate certain NaN evals via math/py-bottleneck
NUMEXPR_DESC=	Accelerate certain numerical ops via math/py-numexpr
BOTO_DESC=	Support Amazon S3 storage via devel/py-boto
TABLES_DESC=	Support HDF5-based storage via devel/py-tables
LXML_DESC=	Parse HTML with devel/py-lxml and www/py-beautifulsoup
HTML5LIB_DESC=	Parse HTML with www/py-html5lib and www/py-beautifulsoup
OPENPYXL_DESC=	Read/write MS Excel 2007+ with textproc/py-openpyxl1
XLRD_DESC=	Read MS Excel with textproc/py-xlrd
XLWT_DESC=	Write MS Excel with textproc/py-xlwt
ACCEL_DESC=	Computation Acceleration Add-ons
STORAGE_DESC=	Data Storage Add-ons
HTML_DESC=	HTML Parsing Add-ons
EXCEL_DESC=	MS Excel I/O Add-ons

MPL_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}matplotlib>0:${PORTSDIR}/math/py-matplotlib
SCIPY_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}scipy>0:${PORTSDIR}/science/py-scipy
BTLNCK_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}bottleneck>0:${PORTSDIR}/math/py-bottleneck
NUMEXPR_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}numexpr>0:${PORTSDIR}/math/py-numexpr
BOTO_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}boto>0:${PORTSDIR}/devel/py-boto
TABLES_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}tables>0:${PORTSDIR}/devel/py-tables
LXML_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}lxml>0:${PORTSDIR}/devel/py-lxml
HTML5LIB_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}html5lib>0:${PORTSDIR}/www/py-html5lib
OPENPYXL_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}openpyxl1<2.0.0:${PORTSDIR}/textproc/py-openpyxl1
XLRD_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}xlrd>0:${PORTSDIR}/textproc/py-xlrd
XLWT_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}xlwt>0:${PORTSDIR}/textproc/py-xlwt

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MLXML} || ${PORT_OPTIONS:MHTML5LIB}
RUN_DEPENDS+=	${PYTHON_PKGNAMEPREFIX}beautifulsoup>0:${PORTSDIR}/www/py-beautifulsoup
.endif

SUB_FILES=	pkg-message

USE_PYTHON=		yes
USE_PYDISTUTILS=	yes
PYDISTUTILS_AUTOPLIST=	yes

# Uncomment the following line to enable regression-test
# on a headless (X11-less) host (eg: RedPorts)
#USES=		display:regression-test

XUNITFILE=	${WRKDIR}/nosetests.xml
NOSE_ENV=	http_proxy=${HTTP_PROXY}
NOSE_ARGS=	${PORTNAME} --exe --with-xunit --xunit-file=${XUNITFILE}

regression-test: build
	@(cd ${WRKSRC} && \
		${PYTHON_CMD} ${PYSETUP} build_ext --inplace && \
		${PYTHON_CMD} -c 'import pandas.util.print_versions as pv; pv.show_versions()' && \
		( ${SETENV} ${NOSE_ENV} nosetests ${NOSE_ARGS} || ${TRUE} ) && \
		${PYTHON_CMD} ${SCRIPTDIR}/print_skipped.py ${XUNITFILE} \
	)

.include <bsd.port.mk>
