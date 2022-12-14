#
# Copyright (c) 2000-2002 Silicon Graphics, Inc.  All Rights Reserved.
#

TOPDIR = ..
include $(TOPDIR)/include/builddefs

COMMINCL = \
	arch_xlate.h \
	cldmgr.h \
	content.h \
	content_inode.h \
	dlog.h \
	drive.h \
	exit.h \
	fs.h \
        getdents.h \
	global.h \
	hsmapi.h \
	lock.h \
	media.h \
	mlog.h \
	openutil.h \
	path.h \
	qlock.h \
	rec_hdr.h \
	ring.h \
	stream.h \
	timeutil.h \
	ts_mtio.h \
	types.h \
	util.h

INVINCL = \
	inventory.h \
	inv_priv.h

INVCOMMON = \
	inv_api.c \
	inv_core.c \
	inv_files.c \
	inv_fstab.c \
	inv_idx.c \
	inv_mgr.c \
	inv_stobj.c

COMMON = \
	arch_xlate.c \
	cldmgr.c \
	dlog.c \
	drive.c \
	drive_scsitape.c \
	drive_simple.c \
	drive_minrmt.c \
	fs.c \
        getdents.c \
	global.c \
	hsmapi.c \
	lock.c \
	main.c \
	mlog.c \
	openutil.c \
	path.c \
	qlock.c \
	ring.c \
	stream.c \
	timeutil.c \
	util.c

LOCALS = \
	bag.c \
	content.c \
	dirattr.c \
	inomap.c \
	mmap.c \
	namreg.c \
	node.c \
	tree.c \
	win.c

LOCALINCL = \
	bag.h \
	dirattr.h \
	getopt.h \
	inomap.h \
	mmap.h \
	namreg.h \
	node.h \
	tree.h \
	win.h

LTCOMMAND = xfsrestore

CFILES = $(LOCALS)
LCFILES = $(COMMON) $(INVCOMMON)
HFILES = $(LOCALINCL)
LHFILES = $(COMMINCL) $(INVINCL)
LINKS = $(COMMINCL) $(COMMON) $(INVINCL) $(INVCOMMON)
LDIRT = $(LINKS)
LLDLIBS = $(LIBUUID) $(LIBHANDLE) $(LIBATTR) $(LIBRMT) $(LIBPTHREAD)
LTDEPENDENCIES = $(LIBRMT)

LCFLAGS = -DRESTORE

ifeq ($(HAVE_FALLOCATE),yes)
LCFLAGS += -DHAVE_FALLOCATE
endif

default: depend $(LTCOMMAND)

include $(BUILDRULES)

install: default
	$(INSTALL) -m 755 -d $(PKG_ROOT_SBIN_DIR)
	$(LTINSTALL) -m 755 $(LTCOMMAND) $(PKG_ROOT_SBIN_DIR)
	$(INSTALL) -m 755 -d $(PKG_SBIN_DIR)
	# skip symlink when /sbin is alread symlinked to /usr/sbin, like on Fedora
install-dev:

.dep: $(COMMINCL) $(COMMON) $(INVINCL) $(INVCOMMON)

$(COMMINCL) $(COMMON):
	@echo "    [LN]     $@"
	$(Q)$(RM) $@; $(LN_S) ../common/$@ $@

$(INVINCL) $(INVCOMMON):
	@echo "    [LN]     $@"
	$(Q)$(RM) $@; $(LN_S) ../inventory/$@ $@

-include .dep
