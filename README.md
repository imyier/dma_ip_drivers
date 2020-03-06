# Xilinx DMA IP 参考驱动

## Xilinx QDMA

Xilinx PCI Express Multi Queue DMA (QDMA) IP 提供了高性能PCIE DMA. 本PCIe QDMA 可以应用于 UltraScale+ 设备。

Linux 驱动与 DPDK 驱动都可以运行在有 PCI Express root port 的PC主机上通过PCI Express 与 QDMA 终端 IP 设备交互。

### 起步文档

* [QDMA 参考驱动详细文档](https://Xilinx.github.io/dma_ip_drivers/)

## Xilinx-VSEC (XVSEC)

Xilinx-VSEC (XVSEC) 是 Xilinx 支持的 VSECs。 XVSEC 驱动为创建与部署带 Xilinx VSEC PCIe 特性的设计提供帮助。

VSEC (Vendor Specific Extended Capability) 是一种 PCIe 特性.

VSEC 本身在FPGA硬件的PCIe扩展功能寄存器中实现 (可能是软IP或硬IP). 此驱动与软件用于使用硬件实现特性与交互。

XVSEC 驱动目前包含 MCAP VSEC, 但是将扩展包含 XVC VSEC 与 NULL VSEC. 之后也将包含 MCAP VSEC 的 Xilinx Versal实现.

### 起步文档

* [XVSEC Linux 内核参考驱动用户指南](XVSEC/linux-kernel/docs/ug04-2000-0142_xvsec.pdf)
