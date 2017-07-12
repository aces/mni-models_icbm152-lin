AUTOMAKE_OPTIONS = check-news
ACLOCAL_AMFLAGS = -I local_m4

MODEL_DIR := mni-models

# mess with the data install directory
pkgdatadir = $(prefix)/share/$(MODEL_DIR)

MODEL_BASE := icbm_avg_152
PRIM_MODAL := t1_tal_lin
MODELS := $(MODEL_BASE)_$(PRIM_MODAL) \
	$(MODEL_BASE)_t2_tal_lin \
	$(MODEL_BASE)_pd_tal_lin

# datestamp
DATE_STAMP := `date +%D-%T`

# package data
noinst_DATA := \
	$(MODELS:=.mnc.gz) \
	$(MODEL_BASE)_$(PRIM_MODAL)_mask.mnc.gz \
	$(MODEL_BASE)_$(PRIM_MODAL)_headmask.mnc.gz

# installed data data
pkgdata_DATA := \
	$(MODELS:=.mnc) \
	$(MODELS:=_mask.mnc) \
	$(MODELS:=_headmask.mnc)

EXTRA_DIST = $(noinst_DATA) $(m4_files) \
	epm-header.in

m4_files = local_m4/ac_prog_gzip.m4

# be tidy
CLEANFILES = $(pkgdata_DATA)

# gunzip rule
%: %.gz
	$(gzip) -d -c $< > $@

all: $(noinst_DATA:.gz=) $(DATE)
	for i in $(MODELS); \
	do \
		echo "Doing $$i"; \
		for m in mask headmask; \
		do \
			echo "Checking for $$i\_$$m.mnc"; \
			if [ ! -e $$i\_$$m.mnc ]; \
			then \
				ln -s $(MODEL_BASE)_$(PRIM_MODAL)_$$m.mnc $$i\_$$m.mnc; \
			fi \
		done; \
	done
	echo "USER: $$USER"
	for i in $(pkgdata_DATA); \
   do \
      echo "Adding mni-model header to $$i"; \
      minc_modify_header \
			-sinsert mni-model:package=$(PACKAGE) \
			-sinsert mni-model:version=$(VERSION) \
			-sinsert mni-model:compile-date=$(DATE_STAMP) \
			-sinsert mni-model:compile-user=$$USER \
			$$i; \
   done
