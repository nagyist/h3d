
# ifeq (3.81,$(lastword $(sort $(MAKE_VERSION) 3.81))) # https://lists.gnu.org/archive/html/help-make/2006-04/msg00067.html
# $(error Version of make too old! ($(MAKE_VERSION) <= 3.81))
# endif

SUBDIR?=../../submodules/

SHELL:= /bin/bash
GVmake=$(MAKE) #any line with $(MAKE) gets exectued even with -n, GVmake should merely be used for makefile-visualization to avoid its execution with -n

## run IM tools without setting cration and modification date (or -strip) to avoid changes in PNGs that are not visual: http://stackoverflow.com/questions/13577280/getting-imagemagick-convert-to-not-write-out-extra-info
## some bug now needs even more default options: http://unix.stackexchange.com/questions/255252/create-the-same-png-with-imagemagick-2-times-binaries-differ#255256
convertIM:= convert -define png:exclude-chunks=date,time +set date:create +set date:modify
mogrifyIM:= mogrify -define png:exclude-chunks=date,time +set date:create +set date:modify

SPACE := $(eval) $(eval)
base_ = $(subst $(SPACE),_,$(filter-out $(lastword $(subst _, ,$1)),$(subst _, ,$1)))
base. = $(subst $(SPACE),.,$(filter-out $(lastword $(subst ., ,$1)),$(subst ., ,$1)))

BN:= h3d
BNseg:= $(BN)_seg_B+a


include gmsl


center:= 1353 1970 0418
#center:= 1271 1646 0656
#center:= 1271 1646 0700
extent:=  300  300  300
#extent:=  400  400  400
1D_EXT:= 220 145 60 1
halfex:= $(call map,halve,$(extent))
origin:= $(call pairmap,subtract,$(center),$(halfex))

slices:= $(call pairmap,addprefix,x@ y@ z@,$(halfex))
fig_luBounds_BG_PNGs:= $(slices:%=$(BN)_ROI_%.png)
fig_luBounds_LS_PNGs:= $(slices:%=$(BNseg)_lu+1_low_ROI_%_LUT.png)
fig_luBounds_MS_PNGs:= $(slices:%=$(BNseg)_lu+1_mid_ROI_%_LUT.png)
fig_luBounds_US_PNGs:= $(slices:%=$(BNseg)_lu+1_upp_ROI_%_LUT.png)

fig_luBounds_x_PNGs:= $(BN)_ROI_$(word 1,$(slices)).png
fig_luBounds_x_PNGs+= $(BNseg)_lu+1_low_ROI_$(word 1,$(slices))_LUT.png
fig_luBounds_x_PNGs+= $(BNseg)_lu+1_mid_ROI_$(word 1,$(slices))_LUT.png
fig_luBounds_x_PNGs+= $(BNseg)_lu+1_upp_ROI_$(word 1,$(slices))_LUT.png
fig_luBounds_x_PNGs+= fig_luBounds_x_RGB.png

fig_luBounds_y_PNGs:= $(BN)_ROI_$(word 2,$(slices)).png
fig_luBounds_y_PNGs+= $(BNseg)_lu+1_low_ROI_$(word 2,$(slices))_LUT.png
fig_luBounds_y_PNGs+= $(BNseg)_lu+1_mid_ROI_$(word 2,$(slices))_LUT.png
fig_luBounds_y_PNGs+= $(BNseg)_lu+1_upp_ROI_$(word 2,$(slices))_LUT.png
fig_luBounds_y_PNGs+= fig_luBounds_y_RGB.png

fig_luBounds_z_PNGs:= $(BN)_ROI_$(word 3,$(slices)).png
fig_luBounds_z_PNGs+= $(BNseg)_lu+1_low_ROI_$(word 3,$(slices))_LUT.png
fig_luBounds_z_PNGs+= $(BNseg)_lu+1_mid_ROI_$(word 3,$(slices))_LUT.png
fig_luBounds_z_PNGs+= $(BNseg)_lu+1_upp_ROI_$(word 3,$(slices))_LUT.png
fig_luBounds_z_PNGs+= fig_luBounds_z_RGB.png

fig_luBounds_z_SVGs:= $(fig_luBounds_z_PNGs:%.png=fig_luBounds_z/%.svg)
fig_luBounds_z_SVGs+= fig_luBounds_z/fig_luBounds_z_RGB.svg


.PHONY: all clean clean_all


all : luBounds.csv
all : line-plot.svg fig_luBounds_z_RGB_1D-1p.png
all : $(fig_luBounds_z_SVGs) $(addprefix fig_luBounds_z/,$(fig_luBounds_z_PNGs)) $(addprefix fig_luBounds_y/,$(fig_luBounds_y_PNGs)) $(addprefix fig_luBounds_x/,$(fig_luBounds_x_PNGs))

clean :
	@-rm -v $(BNseg)_lu+1_???_* 
	@-rm -v $(BNseg)_lu+1_???.ana* 
	@-rm -v $(BN)_* 
	@-rm -v mask.mha
	@-rm -v luBounds.*
	@-rm -rv fig_luBounds*
	@-rm -v all.*
	@-rm -v LUT.png
	@-rm -v line-plot.svg
#	@-rmdir -v 

clean_all : clean
	@-rm -v $(BN).mha $(BNseg)* # uncomment for production 


% :: %.gz # try decompress-first rule https://www.gnu.org/software/make/manual/html_node/Match_002dAnything-Rules.html#Match_002dAnything-Rules  https://www.gnu.org/software/make/manual/html_node/Double_002dColon.html#Double_002dColon
	unpigz -v -k -- $<

%.gz : %
	pigz -v -- $< 


$(BN).mha : ../$(BN).mha
	ln -sf $< $@

$(BNseg).mha : ../$(BN)_seg_B+a.mha mask.mha # crop to mask to avoid WS wells outside mask
	mask $^ $@ 0

mask.mha : ../h3d_hull_02-seg.mha # lu+1 does not necessary reach upto $(BN)_seg_T+B+a@1.mha => use h3d_hull_02-seg
	ln -sf $< $@

%_lu+1_low.mha %_lu+1_mid.mha %_lu+1_upp.mha : $(BN).mha %.mha
	touch $@.stime
	label_uncertainty_float $^ $*_lu+1  0 1 0 # ~210GB of RAM

%.ana : %.mha
	touch $@.stime
	analyse_labels $< 1 > $@

%_ROI.mha : %.mha
	touch $@.stime
	subimage_extract  $< $@ 0 $(origin) $(extent)

# %_dc.mha : %.mha
# 	touch $@.stime
# 	file_converter $< $@ 0

%_add+1.mha : %.mha
	touch $@.stime
	add_const  $< $@ 0 +1

%_T-mask.mha : %_add+1.mha mask.mha
	touch $@.stime
	mask $^ $@ 0

%.anaJS : %.mha # %_dc.mha # if label_uncertainty_float saves compressed
	touch $@.stime
	octave  $(SUBDIR)/octave/scripts/jointSurf3D.m  $<  > $@ # each needs about 40GB of RAM (~5h) => can run in parallel

%.anaJJ : %.ana %.anaJS # need difference 
	paste $^ | awk '{if($$27==0){print $$25 - $$29}}' | sed '1i\\S' > $@

luBounds.csv : $(BNseg)_lu+1_low_T-mask.ana $(BNseg)_lu+1_low_T-mask.anaJJ $(BNseg)_lu+1_mid_T-mask.ana $(BNseg)_lu+1_mid_T-mask.anaJJ $(BNseg)_lu+1_upp_T-mask.ana $(BNseg)_lu+1_upp_T-mask.anaJJ
	paste \
	<(echo -ne '# ANAs combined by paste\nT\nB\nA') \
	<(awk '{print $$24}' $(word 1,$^)) \
	$(word 2,$^) \
	<(awk '{print $$24}' $(word 3,$^)) \
	$(word 4,$^) \
	<(awk '{print $$24}' $(word 5,$^)) \
	$(word 6,$^) \
	| sed '2i\\tVl\tSl\tVm\tSm\tVu\tSu' > $@ # process substitution;-) http://superuser.com/questions/317819/passing-two-arguments-to-a-command-using-pipes#317855  http://tldp.org/LDP/abs/html/process-sub.html


LUT.png :
	$(convertIM) xc:#000 xc:#f00 xc:#0f0 xc:#00f -append -transparent black $@

%_LUT.png : %.png LUT.png
#	$(eval options= -transparent black)
	$(convertIM) $<  LUT.png  -fx "v.p{0,u.p*2^`$(convertIM) $< -format '%z' info:`}" $(options) $@ # p in [0;1], QuantumRange==IM's max bit depth (see Qxx in convert -version), u.depth should work but does not and is very slow


### BEGIN line-plot_1D-img

%_1D.png : %.png
	subimage_extract $< $@ 0 $(1D_EXT)

%-1p.png : %.png
	$(convertIM) $< -gravity East -chop 1x0 $@ # remove 1 pixel on the right to fit gnuplot filledsteps

%.ppm.raw : %.png
#	convert $< -compress none $@ # arbitrary multi-column output 
	convert $< -compress none PPM:- | sed '1,3d;s/\([0-9]* [0-9]* [0-9]*\) /\1\n/g' | sed '/^$$/d' | sed '1ilow mid upp' > $@ # RGB-column reformatted output: http://www.imagemagick.org/Usage/formats/#pbmplus

%.pgm.raw : %.png
	convert $< -negate -compress none PGM:- | sed '1,3d' | tr -s ' ' '\n' > $@ # single-column inverted output

line-plot.svg : h3d_ROI_z@150_1D.pgm.raw fig_luBounds_z_RGB_1D.ppm.raw
	VAL=` gnuplot -e "datafiles='$^';outfile='$@'" $(SUBDIR)/gnuplot/line-plot_1D-img.gp ` ; \
	sed -i "s|viewBox=.*\$$|$${VAL}|" $@ # adjust SVG viewbox for typesetting with latex ;-)

define BASE_SVG
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg width="$(word 1, $(extent))" height="$(word 2, $(extent))" viewBox="0 0 $(word 1, $(extent)) $(word 2, $(extent))"
     xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink" >
  <image x="0" y="0"
     xlink:href="file:///myURL/$(BNseg)_lu+1_upp_ROI_XYZ@150_LUT.png"
     style="image-rendering:optimizeSpeed" /><!-- no smoothing -->
  <rect x="$(word 1,$(1D_EXT))" y="$(word 2,$(1D_EXT))" width="$(word 3,$(1D_EXT))" height="$(word 4,$(1D_EXT))" fill="rgb(0,0,0)" fill-opacity=".5" />
</svg>
endef
export BASE_SVG

fig_base.svg :
	echo "$$BASE_SVG" > $@ # no heredoc possible, but: http://stackoverflow.com/questions/649246/is-it-possible-to-create-a-multi-line-string-variable-in-a-makefile#649462


%.svg : %.png fig_base.svg
	sed 's$$xlink:href="file:///myURL/.*\.png$$xlink:href="$(notdir $<)$$g' < fig_base.svg > $@

fig_luBounds_%/ :
	mkdir -p $@

fig_luBounds_x/% : % | fig_luBounds_x/ ; cp $< $@
fig_luBounds_y/% : % | fig_luBounds_y/ ; cp $< $@
fig_luBounds_z/% : % | fig_luBounds_z/ ; cp $< $@

### END line-plot_1D-img


## below a rule with "make", a very special case for NOT using $(MAKE) or +make
### lines that contain "$(MAKE)" even in a comment get exectued even with -n|--dry-run !!!
%.gv : % Makefile $(MAKEFILES) # put % to get executed after target has been made to avoid make2graph error due to missing files; http://www.gnu.org/software/make/manual/make.html#MAKEFILES-Variable
	$(GVmake) -Bnd $* | make2graph | sed 's/label=".*_\([^_\.]\+\)\.[^\.]*"/label="\1"/g' > $@ # DO NOT PUT a comment with make-var here

#prevent removal of any intermediate files http://stackoverflow.com/questions/5426934/why-this-makefile-removes-my-goal https://www.gnu.org/software/make/manual/html_node/Chained-Rules.html
#.SECONDARY: 

.SERIAL: $(BNseg)_lu+1_low.mha $(BNseg)_lu+1_mid.mha $(BNseg)_lu+1_upp.mha # $(BNseg)_lu+1_low_T-mask.anaJS $(BNseg)_lu+1_mid_T-mask.anaJS $(BNseg)_lu+1_upp_T-mask.anaJS

.PRECIOUS: %.anaJS

.SECONDEXPANSION: # https://www.gnu.org/software/make/manual/html_node/Secondary-Expansion.html

%.png : $$(call base_,%).mha # even though functions are expanded immediately, this needs to be in SECONDEXPANSION for % to be expanded: http://stackoverflow.com/questions/9526295/how-to-call-functions-within-order-only-prerequisites#9533980
	@echo "process $+ to $*"
	$(eval pos= $(subst $(basename $+),,$*))
	$(eval pos= $(subst _,,$(pos)))

	$(eval sep= $(subst @, ,$(pos)))
	$(eval normal= $(word 1, $(sep)))
	$(eval sliceN= $(word 2, $(sep)))

	touch $@.stime
	slice $+ $@ 0 $(normal) $(sliceN)
	$(mogrifyIM) $@

fig_luBounds_%_RGB.png : $$(wordlist 2,4,$$(fig_luBounds_$$*_PNGs))
	$(convertIM) $^ -threshold 1 -channel RGB -combine $@

%.Make.svg : $$(call base.,%).gv # rule should be more specific than %.svg!
	$(eval pos= $(subst $(basename $+),,$*))
	$(eval pos= $(subst .,,$(pos)))

	$(pos) -Tpng -o $@ $<




