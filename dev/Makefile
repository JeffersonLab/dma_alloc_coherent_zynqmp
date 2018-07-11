obj-m	:= memalloc.o

KERNELDIR ?= /lib/modules/$(shell uname -r)/build
PWD       := $(shell pwd)

all: modules

install: modules_install udev_install

modules:
	@echo
	@echo "Building kernel module"
	$(MAKE) -C $(KERNELDIR) M=$(PWD)

modules_install: modules
	@echo
	@echo "Installing kernel module"
	$(MAKE) -C $(KERNELDIR) M=$(PWD) modules_install

udev_install: modules
	@echo
	@echo "Installing rules"
	@/bin/install -v -b 99-tipcie.rules /etc/udev/rules.d/
	@echo
	@echo "Reboot, or restart udev, to complete udev rule installation"

clean:
	@rm -rf *.o *~ core .depend .*.cmd *.ko *.mod.c .tmp_versions
