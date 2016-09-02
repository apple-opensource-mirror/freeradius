#
# Makefile
#
# Version:	$Id: Makefile,v 1.22.2.1.2.4 2006/07/06 19:16:41 aland Exp $
#

include ../../Make.inc

WHAT_TO_MAKE	= all

all:
	@$(MAKE) $(MFLAGS) WHAT_TO_MAKE=$@ common

install:
	$(INSTALL) -d -m 755 $(R)$(libdir)
	@$(MAKE) $(MFLAGS) WHAT_TO_MAKE=$@ common

clean:
	@$(MAKE) $(MFLAGS) WHAT_TO_MAKE=$@ common
	@rm -f *~ lib/rlm_* lib/*.o lib/smbencrypt

distclean:
	@$(MAKE) $(MFLAGS) WHAT_TO_MAKE=$@ common

#
#  Do NOT use "common", because some modules may not be built,
#  and therefore their makefiles may be empty or non-existent.
#
reconfig:
	@[ "x$(AUTOCONF)" != "x" ] || exit 0
	@[ "x$(AUTOHEADER)" != "x" ] || exit 0
	@for x in `find . -name "configure.in" -print`; do \
		( \
		 cd `dirname $$x` || exit $$?; \
		 if [ -f configure.in ]; then \
			$(AUTOCONF) -I $(top_builddir); \
		 fi; \
		 if grep AC_CONFIG_HEADERS configure.in >/dev/null; then\
			$(AUTOHEADER); \
		 fi; \
		) || exit $$?; \
	done

common:
	@[ -d lib/ ] || mkdir lib
	@for mod in $(MODULES); do \
		if [ -d $$mod ] && [ -f $$mod/Makefile ]; then \
			echo "Making $(WHAT_TO_MAKE) in $$mod..."; \
			$(MAKE) $(MFLAGS) -C $$mod $(WHAT_TO_MAKE) || exit $$?; \
		fi; \
	done