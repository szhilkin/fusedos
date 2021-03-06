# ================================================================
#
# Licensed Materials - Property of IBM
#
# Blue Gene/Q
#
# (C) Copyright IBM Corp.  2010, 2012
#
# US Government Users Restricted Rights -
# Use, duplication or disclosure restricted
# by GSA ADP Schedule Contract with IBM Corp.
#
# This software is available to you under either the GNU General
# Public License (GPL) version 2 or the Eclipse Public License
# (EPL) at your discretion.
#
# ================================================================
#
# Comment/uncomment the following line to disable/enable debugging
DEBUG = y

# Add your debugging flag (or not) to CFLAGS
ifeq ($(DEBUG),y)
	DEBFLAGS = -O -g # "-O" is needed to expand inlines
else
	DEBFLAGS = -O2
endif

ifneq ($(KERNELRELEASE),)

# Call from kernel build system
obj-m := fusedosfs.o
fusedosfs-y := inode.o
ccflags-y := -I$(src)/../include -D__FUSEDOS__ -D__FUSEDOSFS__ $(DEBFLAGS)
else

# Make.rules from repository top-level
include ../Make.rules

KERNELDIR ?= $(LINUX_DIR)/$(LINUX_VERS)/
#KERNELDIR ?= $(LINUX_DIR)/$(LINUX_VERS)/
PWD := $(shell pwd)

default:
	$(MAKE) -C $(KERNELDIR) M=$(PWD) modules
	objdump -dlS fusedosfs.ko > fusedosfs.objdump

endif

clean:
	rm -rf *.o *~ core .depend .*.cmd *.ko *.mod.c .tmp_versions *.objdump modules.order Module.symvers

depend .depend dep:
	$(CC) $(CFLAGS) -M *.c > .depend

ifeq (.depend,$(wildcard .depend))
include .depend
endif
