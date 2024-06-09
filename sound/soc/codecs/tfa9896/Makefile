
# Copyright (C) 2014-2020 NXP Semiconductors, All Rights Reserved.
# Copyright 2020 GOODIX 
#
#This program is free software; you can redistribute it and/or modify
#it under the terms of the GNU General Public License version 2 as
#published by the Free Software Foundation.

# make sure that the environment variables ARCH and CROSS_COMPILE
# are set for your architecture and cross compiler.
# And that KDIR points to the kernel to build against.
#
# e.g.:
# export ARCH=arm
# export CROSS_COMPILE=arm-linux-gnueabihf-
# export KDIR=../linux

ifneq ($(KERNELRELEASE),)

# add version number derived from Git
ifeq ($(KDIR),)
PLMA_TFA_AUDIO_DRV_DIR=$(realpath -f $(srctree)/$(src))
else
PLMA_TFA_AUDIO_DRV_DIR=$(realpath -f $(src))
endif
GIT_VERSION=$(shell cd $(PLMA_TFA_AUDIO_DRV_DIR); git describe --tags --dirty --match "v[0-9]*.[0-9]*.[0-9]*")
EXTRA_CFLAGS += -DTFA98XX_GIT_VERSIONS=\"$(GIT_VERSION)\"

EXTRA_CFLAGS += -I$(src)/inc
EXTRA_CFLAGS += -Werror

obj-$(CONFIG_SND_SOC_TFA9896) := snd-soc-tfa98xx.o

snd-soc-tfa98xx-objs += tfa98xx.o
snd-soc-tfa98xx-objs += tfa_container.o
snd-soc-tfa98xx-objs += tfa_dsp.o
snd-soc-tfa98xx-objs += tfa_init.o


else

MAKEARCH := $(MAKE) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE)

all:
	$(MAKEARCH) -C $(KDIR) M=$(PWD) modules

clean:
	$(MAKEARCH) -C $(KDIR) M=$(PWD) clean
	rm -f $(snd-soc-tfa98xx-objs)

endif
