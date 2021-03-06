
# Makefile for the linux kernel.
#

include $(srctree)/drivers/misc/mediatek/Makefile.custom

ccflags-y += -I$(srctree)/

ifeq ($(CONFIG_MTK_INTERNAL), y)
ifeq ($(MTK_USE_RESERVED_EXT_MEM), y)
KBUILD_CFLAGS += -DMTK_USE_RESERVED_EXT_MEM
endif
endif

ifeq ($(MTK_TB_WIFI_3G_MODE), WIFI_ONLY)
KBUILD_CFLAGS += -DMTK_TB_WIFI_3G_MODE_WIFI_ONLY
endif

obj-y := core.o timer.o mt_dbg.o
obj-y += mt_devs.o mt_gpt.o board.o 
obj-y += ca7_timer.o
#obj-y += mt_dma.o
obj-y += mt_reg_dump.o
obj-y += mt_pm_init.o
ifeq ($(CONFIG_SMP),y)
ccflags-y += -I$(srctree)
obj-y += mt-smp.o hotplug.o mt-headsmp.o mt_hotplug.o mt_hotplug_mechanism.o
endif
# TO-FIX add # for do early porting in JB migration
obj-y += eint.o mt_freqhopping.o
obj-$(CONFIG_MT65XX_TRACER) += pmu_v7.o mon_interface.o mt_mon.o mt_emi_bm.o
obj-y += camera_isp.o
obj-y += camera_sysram.o 
obj-y += camera_pipe_mgr.o
#obj-y += camera_eis.o
#obj-y += camera_fdvt.o
obj-y += mt_pm_ldo.o
obj-y += innercache.o mt_l2c.o

obj-y += mt_spm.o mt_spm_sleep.o mt_spm_idle.o mt_spm_mtcmos.o
obj-y += mt_sleep.o
#obj-y += mt_cpufreq.o mt_gpufreq.o mt_cpu_ss.o
obj-y += mt_cpufreq.o mt_cpu_ss.o
obj-y += mt_emifreq.o
obj-y += mt_dormant.o cpu_dormant.o
obj-y += mt_dcm.o mt_idle.o
obj-y += mt_clkmgr_common.o
obj-y += mt_clkmgr.o
obj-y += sbchk_base.o
obj-y += mtk_ccci_helper.o
obj-y += mtk_eemcs_helper.o

ifneq ($(CONFIG_MTK_CCCI_DEVICES),y)
ccflags-y  += -D__USING_DUMMY_CCCI_API__
endif

ifeq ($(CONFIG_MTK_EEMCS_DRIVER),y)
ccflags-y  += -D__EEMCS_DRV_EN__
endif

obj-y += mt_ptp.o
obj-y += mssv.o

# Hibernation
#AFLAGS_swsusp.o	:= -DTEXT_OFFSET=$(TEXT_OFFSET)
obj-$(CONFIG_HIBERNATION)	+= cpu_hibernate.o swsusp.o

KBUILD_AFLAGS	:=$(KBUILD_AFLAGS:-msoft-float=-Wa,-mfpu=neon)

# Module project related part
obj-y += $(ARCH_MTK_PROJECT)/

obj-y += mako_hotplug.o
