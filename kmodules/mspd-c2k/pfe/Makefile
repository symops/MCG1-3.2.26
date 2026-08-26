# Mindspeed-C2K PFE Makefile

## Depends: KERNELDIR as environment variable from outside
## Modify TOOLCHAIN_DIR & CROSS_COMPILE for a different toolchain
## E.g. make KERNELDIR=<path to compiled kernel> TOOLCHAIN_DIR=<path to toolchain root> CROSS_COMPILE=<toolchain>

TOOLCHAIN_DIR ?= /xtools/3rdPartyCompilers/arm-linux-gnueabihf
CROSS_COMPILE ?= arm-linux-gnueabihf-
ARCH ?= arm

export PATH := $(TOOLCHAIN_DIR)/bin:$(PATH)

all: module

pre:
	$(CROSS_COMPILE)gcc -v

module: pre
	$(MAKE) -C ./pfe_ctrl CROSS_COMPILE=$(CROSS_COMPILE) ARCH=$(ARCH) KERNELDIR=$(KERNELDIR) WIFI_ENABLE=y INT_COAL=y all
	$(CROSS_COMPILE)strip --strip-debug -o pfe.ko ./pfe_ctrl/pfe.ko

clean:
	pfe_files="`find pfe -name '*.o*'; find pfe_ctrl -name '*.*o*'; find pfe_ctrl -name '*.*o.*'`"; rm -rf $$pfe_files
	rm -f pfe.ko

