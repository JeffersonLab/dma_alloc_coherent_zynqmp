# dma_memalloc

Device drivers that use dma_alloc_coherent (contiguous memory allocation) are relatively easy to be implemented on Xilinx Zynq-7000 boards (ARM Cortex-A9, 32bit), but they are not on Xinlinx ZynqMP boards (ARM Cortex-A53, 64bit). This example will showcase how to write a device driver for both the architectures. The work is on-going. Currently, `dma_alloc_coherent` returns `NULL` on the ARM 64bit CPU.

Thanks to Massimiliano Giacometti (max.giacometti@gmail.com) for an initial version of this code, and Giuseppe Di Guglielmo for the original git repo.

## How To

These are the steps to test the device driver on Xilinx Zynq-7000 boards, i.e. ARM Cortex-A9, 32bit architecture. 

```
$ source <...> Xilinx/SDK/2016.2/settings64.sh
$ make ARCH=arm CROSS_COMPILE=arm-xilinx-linux-gnueabi KERNELDIR=<KERNEL BUILD DIRECTORY>
```



Now you can copy (`scp`) both the device driver (`*.ko`) and the test program on Linux that runs on the Xilinx Zynq-7000 board.

```
# insmod memalloc.ko
# ./memalloc_test
```

To increase the maximum amount of DMA memory that can be allocated,
set the "cma= " kernel commandline option (from kernel-parameters.txt):

```
	cma=nn[MG]@[start[MG][-end[MG]]]
			[ARM,X86,KNL]
			Sets the size of kernel global memory area for
			contiguous memory allocations and optionally the
			placement constraint by the physical address range of
			memory allocations. A value of 0 disables CMA
			altogether. For more information, see
			include/linux/dma-contiguous.h

```
