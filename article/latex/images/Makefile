

SHELL:= /bin/bash
GVmake=$(MAKE) #any line with $(MAKE) gets exectued even with -n, GVmake should merely be used for makefile-visualization to avoid its execution with -n



Fig_slideOV= MR3006g_OT2_b+64.svg MR3006g_OT2_b+64.png MR3006g_OT2_s088_RGB_b+10.png MR3006g_OT2_s088_tra_b+10.png h3d_OT2_s088_b+03.png
Fig_slideOV:= $(addprefix ../../../processing/slides2stack/,$(Fig_slideOV))

Fig_histo_3D-sliced+seg= 3D-OV.png  BG_x@0838.png  BG_y@1624.png  BG_z@0688_sb.png  OV1_LUT_x@0838.png  OV1_LUT_y@1624.png  OV1_LUT_z@0688.png
Fig_histo_3D-sliced+seg:= $(addprefix ../../../manual/slices/fig_histo_3D-sliced+seg/,$(Fig_histo_3D-sliced+seg))

Fig_line-plot= line-plot.svg fig_luBounds_z_RGB_1D-1p.png
Fig_line-plot:= $(addprefix ../../../processing/low_upp-bounds/,$(Fig_line-plot))

Fig_v-render= fig_v-render_01_trim.png fig_v-render_02_trim.svg fig_v-render_02_trim.png fig_v-render_02_oao_trim.png fig_v-render_03_LE_trim.png fig_v-render_03_RE_trim.png
Fig_v-render:= $(addprefix ../../../manual/VR/,$(Fig_v-render))

Fig_ov01= fig_ov01_1.png fig_ov01_2.png fig_ov01_3.png fig_ov01_4.png
Fig_ov01:= $(addprefix ../../../manual/VE/fig_ov01/,$(Fig_ov01))

Fig_luBounds=  fig_luBounds_z/h3d_ROI_z@150.png fig_luBounds_y/h3d_ROI_y@150.png fig_luBounds_x/h3d_ROI_x@150.png
Fig_luBounds+= fig_luBounds_z/h3d_seg_B+a_lu+1_low_ROI_z@150_LUT.png fig_luBounds_y/h3d_seg_B+a_lu+1_low_ROI_y@150_LUT.png fig_luBounds_x/h3d_seg_B+a_lu+1_low_ROI_x@150_LUT.png
Fig_luBounds+= fig_luBounds_z/h3d_seg_B+a_lu+1_upp_ROI_z@150_LUT.png fig_luBounds_y/h3d_seg_B+a_lu+1_upp_ROI_y@150_LUT.png fig_luBounds_x/h3d_seg_B+a_lu+1_upp_ROI_x@150_LUT.png
Fig_luBounds+= fig_luBounds_z/fig_luBounds_z_RGB.png fig_luBounds_y/fig_luBounds_y_RGB.png fig_luBounds_x/fig_luBounds_x_RGB.png
Fig_luBounds+= fig_luBounds_z/h3d_ROI_z@150.svg fig_luBounds_z/h3d_seg_B+a_lu+1_low_ROI_z@150_LUT.svg fig_luBounds_z/h3d_seg_B+a_lu+1_upp_ROI_z@150_LUT.svg fig_luBounds_z/fig_luBounds_z_RGB.svg
# Fig_luBounds:= $(addprefix ../../../processing/low_upp-bounds/,$(Fig_luBounds))

Fig_A2V= fig_A2V_1.png fig_A2V_2.png fig_A2V_3.png fig_A2V_4.png fig_A2V_5.png fig_A2V_6.png
Fig_A2V:= $(addprefix ../../../manual/VE/fig_A2V/,$(Fig_A2V))

Fig_srv-curved= fig_SRV-curved_0.png fig_SRV-curved_2.png fig_SRV-curved_3.png fig_SRV-curved_4.png fig_SRV-curved_4.png
Fig_srv-curved:= $(addprefix ../../../manual/SRV/fig_SRV-curved/,$(Fig_srv-curved))

Fig_SRV2D=   h3d_srv+500+500+0.331662+2_x@0250.png h3d_srv+500+500+0.331662+2_y@0250.png
Fig_SRV2D+=  plane-A_x@0250.png plane-A_y@0250.png
Fig_SRV2D+=  plane-B_x@0250.png plane-B_y@0250.png
Fig_SRV2D+=  h3d_srv+500+500+0.331662+2_z@0129.png h3d_srv+500+500+0.331662+2_z@0640.png h3d_srv+500+500+0.331662+2_z@1131.png h3d_srv+500+500+0.331662+2_z@1533.png h3d_srv+500+500+0.331662+2_z@1601.png h3d_srv+500+500+0.331662+2_z@1773.png h3d_srv+500+500+0.331662+2_z@2156.png h3d_srv+500+500+0.331662+2_z@2190.png h3d_srv+500+500+0.331662+2_z@2389.png h3d_srv+500+500+0.331662+2_z@2497.png h3d_srv+500+500+0.331662+2_z@2578.png h3d_srv+500+500+0.331662+2_z@2692.png h3d_srv+500+500+0.331662+2_z@2945.png h3d_srv+500+500+0.331662+2_z@3041.png h3d_srv+500+500+0.331662+2_z@3250.png h3d_srv+500+500+0.331662+2_z@4046.png
Fig_SRV2D+=  plane-A_z@0129.png plane-A_z@0640.png plane-A_z@1131.png plane-A_z@1533.png plane-A_z@1601.png plane-A_z@1773.png plane-A_z@2156.png plane-A_z@2190.png plane-A_z@2389.png plane-A_z@2497.png plane-A_z@2578.png plane-A_z@2692.png plane-A_z@2945.png plane-A_z@3041.png plane-A_z@3250.png plane-A_z@4046.png
Fig_SRV2D+=  plane-B_z@0129.png plane-B_z@0640.png plane-B_z@1131.png plane-B_z@1533.png plane-B_z@1601.png plane-B_z@1773.png plane-B_z@2156.png plane-B_z@2190.png plane-B_z@2389.png plane-B_z@2497.png plane-B_z@2578.png plane-B_z@2692.png plane-B_z@2945.png plane-B_z@3041.png plane-B_z@3250.png plane-B_z@4046.png
Fig_SRV2D:= $(addprefix ../../../manual/SRV/SRV2D/,$(Fig_SRV2D))


.PHONY: all clean
#.PHONY: FIG_slideOV FIG_histo_3D-sliced+seg FIG_line-plot FIG_v-render FIG_ov01 FIG_luBounds FIG_A2V FIG_srv-curved FIG_srv # FIG_histo_colored 



all: FIG_slideOV FIG_histo_3D-sliced+seg FIG_line-plot FIG_v-render FIG_ov01 FIG_luBounds FIG_A2V FIG_srv-curved FIG_srv # FIG_histo_colored 


fig_histo_3D-sliced+seg/ \
fig_ov01/ \
fig_luBounds_z/ fig_luBounds_y/ fig_luBounds_x/ \
fig_A2V/ \
fig_SRV-curved/ \
fig_SRV-curvedPV/ \
fig_SRV-straightenedPV/ \
SRV2D/ :
	mkdir -p $@


# fig_histo_colored : MR3006g_OT1_RGB_point-sel_00_comb.png MR3006g_OT1_118_bi8.png kap-net_histo_reg_8bit_z118.png kap-net_histo_reg_8bit_rep_smROISBS_masked_m+3+3_z118.png

FIG_slideOV : $(Fig_slideOV)
	cp -v $^ .
	touch $@

FIG_histo_3D-sliced+seg : fig_histo_3D-sliced+seg.svg 
	touch $@

fig_histo_3D-sliced+seg.svg : ../../../manual/slices/fig_histo_3D-sliced+seg.svg $(Fig_histo_3D-sliced+seg) | fig_histo_3D-sliced+seg/
	cp -v $^ fig_histo_3D-sliced+seg/
	mv fig_histo_3D-sliced+seg/$@ $@

FIG_line-plot : $(Fig_line-plot)
	cp -v $^ .
	touch $@

FIG_v-render : $(Fig_v-render)
	cp -v $^ .
	touch $@

FIG_ov01 : $(Fig_ov01) | fig_ov01/
	cp -v $^ fig_ov01/
	touch $@

FIG_A2V : $(Fig_A2V) | fig_A2V/
	cp -v $^ fig_A2V/
	touch $@

FIG_srv-curved : $(Fig_srv-curved) | fig_SRV-curved/
	cp -v $^ fig_SRV-curved/
	mv fig_SRV-curved/fig_SRV-curved_0.png fig_SRV-curved/fig_SRV-curved_1.png
	touch $@

FIG_srv : fig_SRV-curvedPV.svg fig_SRV-straightenedPV.svg fig_SRV2D.svg
	touch $@

fig_SRV-curvedPV.svg : ../../../manual/SRV/fig_SRV-curvedPV.svg ../../../manual/SRV/fig_SRV-curvedPV/vis_SRV-curved_ori-axes.png ../../../manual/SRV/fig_SRV-curvedPV/vis_SRV-curved.png | fig_SRV-curvedPV/
	cp -v $^ fig_SRV-curvedPV/
	mv fig_SRV-curvedPV/$@ $@

fig_SRV-straightenedPV.svg : ../../../manual/SRV/fig_SRV-straightenedPV.svg ../../../manual/SRV/fig_SRV-straightenedPV/vis_SRV-straightened_ori-axes.png  ../../../manual/SRV/fig_SRV-straightenedPV/vis_SRV-straightened.png | fig_SRV-straightenedPV/
	cp -v $^ fig_SRV-straightenedPV/
	mv fig_SRV-straightenedPV/$@ $@

fig_SRV2D.svg : ../../../manual/SRV/fig_SRV2D.svg $(Fig_SRV2D) | SRV2D/
	cp -v $^ SRV2D/
	mv SRV2D/$@ $@


FIG_luBounds : $(Fig_luBounds)
	touch $@

fig_luBounds_x/%.png : ../../../processing/low_upp-bounds/fig_luBounds_x/%.png | fig_luBounds_x/ ; cp -v $^ $@
fig_luBounds_y/%.png : ../../../processing/low_upp-bounds/fig_luBounds_y/%.png | fig_luBounds_y/ ; cp -v $^ $@
fig_luBounds_z/%.png : ../../../processing/low_upp-bounds/fig_luBounds_z/%.png | fig_luBounds_z/ ; cp -v $^ $@
fig_luBounds_z/%.svg : ../../../processing/low_upp-bounds/fig_luBounds_z/%.svg | fig_luBounds_z/ ; cp -v $^ $@



# fig_v-render_02_trim.svg : fig_v-render_02_trim.png fig_v-render_02_oao_trim.png


