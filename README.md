# Xilinx DMA IP 参考驱动

## Xilinx QDMA

Xilinx PCI Express Multi Queue DMA (QDMA) IP 提供了高性能PCIE DMA. 本PCIe QDMA 可以应用于 UltraScale+ 设备。

Both the linux kernel driver and the DPDK driver can be run on a PCI Express root port host PC to interact with the QDMA endpoint IP via PCI Express.

### 起步文档

* [QDMA 参考驱动详细文档](https://Xilinx.github.io/dma_ip_drivers/)

## Xilinx-VSEC (XVSEC)

Xilinx-VSEC (XVSEC) are Xilinx supported VSECs. The XVSEC Driver helps creating and deploying designs that may include the Xilinx VSEC PCIe Features.

VSEC (Vendor Specific Extended Capability) is a feature of PCIe.

The VSEC itself is implemented in the PCIe extended capability register in the FPGA hardware (as either soft or hard IP). The drivers and SW are created to interface with and use this hardware implemented feature.

The XVSEC driver currently include the MCAP VSEC, but will be expanded to include the XVC VSEC and NULL VSEC. Over time it will also include the Xilinx Versal implementation of the MCAP VSEC.

### 起步文档

* [XVSEC Linux Kernel Reference Driver User Guide](XVSEC/linux-kernel/docs/ug04-2000-0142_xvsec.pdf)
