#	$Id$
#
# Makefile.in for the cc part of pcc.
#
VPATH=../../../pcc/cc/cc
srcdir=../../../pcc/cc/cc
top_srcdir=../../../pcc
top_builddir=../..
prefix = /usr/local
exec_prefix = ${prefix}
bindir = ${exec_prefix}/bin
libdir = ${exec_prefix}/lib
libexecdir = ${exec_prefix}/libexec
includedir = ${prefix}/include
datarootdir = ${prefix}/share
mandir = ${datarootdir}/man
CC = gcc
EXEEXT = .exe
TARGOS = win32
TARGOSVER = 0
TARGMACH = i386
TARGET = i686-pc-mingw32
VERSION = 1.2.0.DEVEL
PCCLIBDIR = $(libdir)/pcc/$(TARGET)/$(VERSION)/lib
PCCINCDIR = $(libdir)/pcc/$(TARGET)/$(VERSION)/include
CFLAGS = -g -O2  -Wall -Wmissing-prototypes -Wshadow -Wsign-compare
CPPFLAGS =  -DLIBEXECDIR=\"$(libexecdir)/\" \
	 -DGCC_COMPAT -DPCC_DEBUG -DINCLUDEDIR=\"$(includedir)/\" \
	-DPCCINCDIR=\"$(PCCINCDIR)/\" -DPCCLIBDIR=\"$(PCCLIBDIR)/\" \
	-Dos_$(TARGOS) -Dmach_$(TARGMACH) -DTARGOSVER=$(TARGOSVER) \
	-DCPPROGNAME=\"$(CPPDEST)\" -I$(top_srcdir)/cc/driver \
	-I$(top_builddir) -I$(top_srcdir)/os/$(TARGOS) -I$(MIPDIR) -I$(MDIR)
LIBS =
LDFLAGS =
INSTALL = /bin/install -c
INSTALL_PROGRAM = ${INSTALL} -s
INSTALL_DATA = ${INSTALL} -m 644

MIPDIR=$(top_srcdir)/mip
MDIR=$(top_srcdir)/arch/$(TARGMACH)

DEST=cc$(EXEEXT)
DRIVERS=pcc pcpp p++

all: $(DEST)

OBJS=	cc.o compat.o strlist.o xalloc.o

cc.o:	$(srcdir)/cc.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -c -o $@ $(srcdir)/cc.c

compat.o: $(MIPDIR)/compat.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -c -o $@ $(MIPDIR)/compat.c

strlist.o: $(top_srcdir)/cc/driver/strlist.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -c -o $@ $(top_srcdir)/cc/driver/strlist.c

xalloc.o: $(top_srcdir)/cc/driver/xalloc.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -c -o $@ $(top_srcdir)/cc/driver/xalloc.c

$(DEST): $(OBJS)
	$(CC) $(LDFLAGS) $(OBJS) -o $@ $(LIBS)

install:
	test -z "$(DESTDIR)$(bindir)" || mkdir -p "$(DESTDIR)$(bindir)"
	test -z "$(DESTDIR)$(mandir)/man1" || mkdir -p "$(DESTDIR)$(mandir)/man1"
	@for driver in $(DRIVERS); do \
		$(INSTALL_PROGRAM) $(DEST) $(DESTDIR)$(bindir)/$$driver$(EXEEXT); \
		$(INSTALL_DATA) $(srcdir)/cc.1 $(DESTDIR)$(mandir)/man1/$$driver.1; \
	done
	test -z "$(DESTDIR)$(PCCINCDIR)" || mkdir -p "$(DESTDIR)$(PCCINCDIR)"
	test -z "$(DESTDIR)$(PCCLIBDIR)" || mkdir -p "$(DESTDIR)$(PCCLIBDIR)"

clean:
	rm -f  $(OBJS) $(CPPDEST) $(DEST)
