AUTOMAKE_OPTIONS = check-news
ACLOCAL_AMFLAGS = -I local_m4

MNI_AUTOREG := mni_autoreg
MODEL_BASE := icbm_avg_152
PRIM_MODAL := t1_tal_lin
MODALS := $(PRIM_MODAL) \
	t2_tal_lin \
	pd_tal_lin

# mess with the data install directory
pkgdatadir = $(prefix)/share/$(MNI_AUTOREG)

# package data
dist_pkgdata_DATA := \
	$(MODEL_BASE)_$(MODALS).mnc.gz \
	$(MODEL_BASE)_$(PRIM_MODAL)_mask.mnc.gz \
	$(MODEL_BASE)_$(PRIM_MODAL)_headmask.mnc.gz

# installed data data
pkgdata_DATA := $(dist_pkgdata_DATA:.gz=) \
	$(MODEL_BASE)_$(MODALS)_16_blur.mnc \
	$(MODEL_BASE)_$(MODALS)_16_mask.mnc \
	$(MODEL_BASE)_$(MODALS)_2_blur.mnc \
	$(MODEL_BASE)_$(MODALS)_2_dxyz.mnc \
	$(MODEL_BASE)_$(MODALS)_2_mask.mnc \
	$(MODEL_BASE)_$(MODALS)_4_blur.mnc \
	$(MODEL_BASE)_$(MODALS)_4_dxyz.mnc \
	$(MODEL_BASE)_$(MODALS)_4_mask.mnc \
	$(MODEL_BASE)_$(MODALS)_8_blur.mnc \
	$(MODEL_BASE)_$(MODALS)_8_dxyz.mnc \
	$(MODEL_BASE)_$(MODALS)_8_mask.mnc

EXTRA_DIST = $(m4_files) \
	epm-header.in

m4_files = local_m4/ac_prog_gzip.m4 \
	local_m4/ac_prog_make_model.m4

# gunzip rule
%: %.gz
	$(gzip) -d -c $< > $@

# make_model rule
$(MODEL_BASE)_$(MODALS)_16_blur.mnc: $(dist_pkgdata_DATA)
	$(make_model) $(MODEL_BASE)_$(MODALS)
