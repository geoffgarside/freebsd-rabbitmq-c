# New ports collection makefile for:	rabbitmq-c
# Date created:				31 March 2010
# Whom:					Geoff Garside
#
# $FreeBSD$
#

PORTNAME=	rabbitmq-c
PORTVERSION=	0.0.1
CATEGORIES=	net
MASTER_SITES=	http://hg.rabbitmq.com/rabbitmq-c/archive/:c \
		http://hg.rabbitmq.com/rabbitmq-codegen/archive/:codegen
DISTNAME=	${PORTNAME}-4e789c776a45
DISTFILES=	4e789c776a45.tar.bz2:c \
		821f5ee7b040.tar.bz2:codegen
DIST_SUBDIR=	rabbitmq

MAINTAINER=	rabbitmq@geoffgarside.co.uk
COMMENT=	RabbitMQ C AMQP client library

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}simplejson>=2.0:${PORTSDIR}/devel/py-simplejson

CONFLICTS=	rabbitmq-c-devel-[0-9]*

USE_BZIP2=	YES
USE_GMAKE=	YES
USE_PYTHON=	YES
USE_LDCONFIG=	YES
GNU_CONFIGURE=	YES
USE_AUTOTOOLS=	aclocal:110 autoconf:262 automake:110 autoheader:262 libtool:22
AUTOMAKE_ARGS=	-i --add-missing
ACLOCAL_ARGS=	-I . -I ${LOCALBASE}/share/aclocal

OPTIONS=	64BIT "Produce 64-bit library" Off \
		POPT  "Popt support in tools" Off

.include <bsd.port.options.mk>

.if defined(WITH_64BIT)
ONLY_FOR_ARCHS=	amd64 sparc64 powerpc
ONLY_FOR_ARCHS_REASON=	WITH_64BIT is set
CONFIGURE_ARGS+=	--enable-64-bit
.endif

.if defined(WITH_POPT)
LIB_DEPENDS+=	popt.0:${PORTSDIR}/devel/popt
CONFIGURE_ENV+=	CFLAGS="${CFLAGS} -I${LOCALBASE}/include" \
		LDFLAGS="${LDFLAGS} -L${LOCALBASE}/lib"

CONFIGURE_ARGS+=	--with-popt
.else
CONFIGURE_ARGS+=	--without-popt
.endif

post-install:
	${STRIP_CMD} ${PREFIX}/lib/librabbitmq.so.0

post-extract:
	@${REINPLACE_CMD} -e 's|rabbitmq-codegen|rabbitmq-codegen-821f5ee7b040|g' ${WRKSRC}/configure.ac

pre-configure:
	@(cd ${CONFIGURE_WRKSRC} && ${SETENV} ${AUTOTOOLS_ENV} ${LIBTOOLIZE})

.include <bsd.port.mk>
