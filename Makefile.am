AUTOMAKE_OPTIONS = check-news
ACLOCAL_AMFLAGS = -I local_m4

MNI_AUTOREG := mni_autoreg
MODEL_BASE := average_305

# mess with the data install directory
pkgdatadir = $(prefix)/share/$(MNI_AUTOREG)

# package data
dist_pkgdata_DATA := \
	$(MODEL_BASE).mnc.gz \
	$(MODEL_BASE)_mask.mnc.gz \
	$(MODEL_BASE)_headmask.mnc.gz

# installed data data
pkgdata_DATA := $(dist_pkgdata_DATA:.gz=) \
	$(MODEL_BASE)_16_blur.mnc \
	$(MODEL_BASE)_16_mask.mnc \
	$(MODEL_BASE)_2_blur.mnc \
	$(MODEL_BASE)_2_dxyz.mnc \
	$(MODEL_BASE)_2_mask.mnc \
	$(MODEL_BASE)_4_blur.mnc \
	$(MODEL_BASE)_4_dxyz.mnc \
	$(MODEL_BASE)_4_mask.mnc \
	$(MODEL_BASE)_8_blur.mnc \
	$(MODEL_BASE)_8_dxyz.mnc \
	$(MODEL_BASE)_8_mask.mnc

EXTRA_DIST = $(m4_files) \
	epm-header.in

m4_files = local_m4/ac_prog_gzip.m4 \
	local_m4/ac_prog_make_model.m4

# gunzip rule
%: %.gz
	$(gzip) -d -c $< > $@

# make_model rule
$(MODEL_BASE)_16_blur.mnc: $(dist_pkgdata_DATA)
	$(make_model) $(MODEL_BASE)
