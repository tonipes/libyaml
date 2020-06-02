## Run `./bootstrap` to generate the "Makefile.in" files in this directory and
## the "$SUBDIRS" subdirectories.

SUBDIRS = include src . tests

EXTRA_DIST = Changes ReadMe.md License CMakeLists.txt doc/doxygen.cfg

export LIBYAML_ROOT := $(PWD)

LIBYAML_TEST_REPO ?= https://github.com/yaml/libyaml-test
LIBYAML_TEST_COMMIT ?= 1f1b00ab6763647d05e44200b63fa62f1d2269a3

# XXX
LIBYAML_TEST_REPO := https://github.com/yaml/libyaml-test
LIBYAML_TEST_COMMIT := origin/master

# NOTE: Uncomment to use a local copy of libyaml-test
#   LIBYAML_TEST_REPO := ../libyaml-test/.git
#   LIBYAML_TEST_COMMIT := master

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = yaml-0.1.pc

maintainer-clean-local:
	rm -f aclocal.m4 config.h.in configure config/*
	-find ${builddir} -name Makefile.in -exec rm -f '{}' ';'

distclean-local:
	rm -fr libyaml-test packaging
	-git worktree prune

.PHONY: bootstrap libyaml-test
bootstrap: maintainer-clean
	./bootstrap
	./configure
	make

test-all: test test-suite

test: all
	make -C tests check-TESTS

test-suite: libyaml-test all
	make -C $< $@

libyaml-test:
	-git clone $(LIBYAML_TEST_REPO) $@
	( cd $@ && git reset --hard $(LIBYAML_TEST_COMMIT) )

docker-dist: packaging
	make -C $</docker libyaml-dist

docker-test-pyyaml: packaging
	make -C $</docker test-pyyaml

packaging:
	-git branch --track $@ origin/$@
	git worktree add --force $@ $@
