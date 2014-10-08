# root Makefile.am

ACLOCAL_AMFLAGS = -I aclocal

SUBDIRS = include
EXTRA_DIST = bootstrap

# Uncrustify the source
uncrustify: uncrustify.cfg
	@for dir in $(SUBDIRS) $(DEVDIRS); do \
		find "$(top_srcdir)/$$dir" -type f -name '*.[ch]' -print0 | xargs -0r uncrustify -c $(top_srcd
ir)/uncrustify.cfg --replace --no-backup; \
	done


