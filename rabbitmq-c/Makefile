# New ports collection makefile for:	rabbitmq-c
# Date created:				31 March 2010
# Whom:					Geoff Garside
#
# $FreeBSD$
#

PORTNAME=	rabbitmq-c
PORTVERSION=	0.0.1
#PORTREVISION=	0
DISTVERSION=	55d472107b53
CODEVERSION=	821f5ee7b040
CATEGORIES=	net
MASTER_SITES=	http://hg.rabbitmq.com/rabbitmq-c/archive/:c \
		http://hg.rabbitmq.com/rabbitmq-codegen/archive/:codegen
DISTNAME=	${PORTNAME}-${DISTVERSION}
DISTFILES=	${DISTVERSION}.tar.bz2:c \
		${CODEVERSION}.tar.bz2:codegen
DIST_SUBDIR=	rabbitmq

MAINTAINER=	freebsd@geoffgarside.co.uk
COMMENT=	RabbitMQ C AMQP client library

BUILD_DEPENDS=  ${PYTHON_PKGNAMEPREFIX}simplejson>=2.0:${PORTSDIR}/devel/py-simplejson

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
CONFIGURE_ARGS+=	--enable-64-bit
.endif

.if defined(WITH_POPT)
LIB_DEPENDS+=		popt.0:${PORTSDIR}/devel/popt
CONFIGURE_ARGS+=	--with-popt
.else
CONFIGURE_ARGS+=	--without-popt
.endif

post-install:
	${STRIP_CMD} ${PREFIX}/lib/librabbitmq.so.0

post-extract:
	@${REINPLACE_CMD} -e 's|rabbitmq-codegen|rabbitmq-codegen-${CODEVERSION}|g' ${WRKSRC}/configure.ac

pre-configure:
	@(cd ${CONFIGURE_WRKSRC} && ${SETENV} ${AUTOTOOLS_ENV} ${LIBTOOLIZE})

.include <bsd.port.mk>
