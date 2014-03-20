ACLOCAL_AMFLAGS = -I m4


SUBDIRS=src
if MANUAL_CONFD
SUBDIRS+=conf.d
endif

RPMDIR = RPMBUILD

dist-hook:
	find "$(distdir)" -name .gitignore -exec rm {} \;

if MAKE_RPMS

RPMFILENAME=$(PACKAGE_NAME)-$(VERSION)
.PHONY: rpm
rpm:
	rm -rf "$(RPMDIR)/SOURCES/$(RPMFILENAME)"
	mkdir -p $(RPMDIR)/BUILD/ $(RPMDIR)/SRPMS/ $(RPMDIR)/RPMS/ $(RPMDIR)/SOURCES
	make ${AM_MAKEFLAGS} distdir='$(RPMDIR)/SOURCES/$(RPMFILENAME)' distdir
	cp apache/src/mod_netconf.conf "$(RPMDIR)/SOURCES/$(RPMFILENAME)"
	find "$(RPMDIR)" -name '*.back' -exec rm -f {} \;
	( cd "$(RPMDIR)/SOURCES/"; tar -z -c -f $(RPMFILENAME)-$(RELEASE).tar.gz $(RPMFILENAME); rm -rf $(RPMFILENAME); )
	$(RPMBUILD) -ba $(PACKAGE_NAME).spec --define "_topdir `pwd`/$(RPMDIR)";

rpm-clean:
	rm -rf $(RPMDIR)
else
endif