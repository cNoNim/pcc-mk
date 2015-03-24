#	$Id$
#
# Makefile.in for top-level of pcc.
#



ALL_SUBDIRS=	cc cpp ccom cxxcom driver

all install clean:
	@for subdir in $(ALL_SUBDIRS); do \
		_nextdir_=$${_thisdir_+$$_thisdir_/}$$subdir; \
		echo "===> $$_nextdir_"; \
		(_thisdir_=$$_nextdir_; export _thisdir_; cd $$subdir && \
		    exec $(MAKE) $(MFLAGS) $@) || exit $$?; \
		echo "<=== $$_nextdir_"; \
	done
