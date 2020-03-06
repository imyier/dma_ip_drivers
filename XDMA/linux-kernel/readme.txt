此目录中的文件提供了 Xilinx PCIe DMA 驱动、示例软件,用于测试IP的示例测试脚本。

本软件可以直接用来创建Xilinx FPGA硬件设计的驱动与软件。

目录和文件描述:
= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
- xdma/:此目录包含Xilinx PCIe DMA内核模块驱动程序文件。
- libxdma/:这个目录包含内核驱动程序模块的支持文件，接口对应XDMA IP。
- include/:此目录包含编译驱动程序所需的所有包含文件。
- tests/:这个目录提供内核模块驱动程序和Xilinx PCIe DMA IP示例应用程序软件。这个目录还包含以下脚本和目录。
- load_driver.sh:
这个脚本加载内核模块并创建软件使用内核节点必要的模块。设备节点创建在/dev/xdma*下。其他设备节点创建在/dev/xdma/card*下。
- run_test.sh:
此脚本在Xilinx PCIe DMA目标上运行示例测试返回一个pass(0)或fail(1)结果。
此脚本用于PCIe DMA示例设计。
- perform_hwcount.sh:
这个脚本测试XDMA的硬件性能包括主机到卡(H2C)和卡到主机(C2H)模式。结果被复制到“hw_log_h2c.txt和hw_log_c2h.txt文本文件。
对于每种模式，性能脚本从64字节开始翻倍到4mb。
您可以在这两个文件上grep 'data rate'来查看数据率值。
数据速率值以最大吞吐量的百分比表示。
x8Gen3的最大数据速率是8Gbytes/s，因此对于x8Gen3 0.81数据速率的设计值为0.81*8 = 6.48Gbytes/s。
x16Gen3的最大数据速率是16gb /s，因此对于x16Gen3 0.78数据率的设计值为0.78*16 = 12.48Gbytes/s。
该程序可以运行在axim - mm实例设计上。axis - st设计为环回设计，包括H2C和C2H 。运行在axis - st示例设计上则不会生成正确的数字。
如果axis-st设计独立于H2C和C2H，可以生成性能数字。
-data/:
此目录包含用于将DMA数据传输到Xilinx FPGA PCIe终端设备的二进制数据文件。

用法:
-将目录更改为驱动程序目录。
cd xdma
-编译和安装内核模块驱动程序。
make install
-将目录更改为工具目录。
cd tools
-编译提供的示例测试工具。
make
-加载内核模块驱动程序:
a:modprobe xdma
b:使用提供的脚本。
cd tests
./load_driver.sh
-运行提供的测试脚本，以生成基本的DMA流。
./ run_test.sh
-检查驱动程序版本号
modinfo xdma(或)
modinfo ../ xdma/xdma.ko
更新和向后兼容:
-以下功能已添加到PCIe DMA IP和驱动程序的Vivado 2016.1。如果是PCIe DMA IP，更早的版本则不能使用这些特性。
-轮询模式:早期版本的Vivado只支持中断模式，是驱动程序的默认行为。
-源/目标地址:Vivado PCIe DMA IP的早期版本要求源地址和目标地址的低阶位相同。截至2011年1月，这一限制已被取消，源和目标地址可以是任何有效的任意地址。

常见问题:
问:如何卸载内核模块驱动程序?
答:使用以下命令卸载驱动程序卸载内核模块。
rmmod -s xdma
问:如何修改内核模块驱动程序识别的PCIe设备id ?
答:xdma/xdma_mod.c文件维护pci_device_id结构标志。PCIe设备的id是由驱动程序以下面格式识别:
{PCI_DEVICE(0x10ee, 0x8038)，}，
根据需要在这个结构中添加、删除或修改PCIe设备id。然后卸载现有的xdma内核模块，再次编译驱动程序，然后使用load_driver.sh脚本重新安装驱动程序。
问:在默认情况下，当DMA传输时，驱动程序使用中断来发送信号完成。我如何修改驱动程序使用轮询而不是中断来确定DMA事务何时完成?
答:驱动程序可以从中断驱动(默认)改为在插入内核模块时轮询驱动(轮询模式)。要做到这一点修改load_driver.sh文件如下:
修改:insmod xdma / xdma.ko
为:insmod xdma / xdma。ko poll_mode = 1
注意:中断vs轮询模式将适用于所有的DMA通道。如果需要的驱动程序可以修改，这样一些通道是中断驱动的同时其他的则是轮询驱动的。请参阅PG195的轮询模式部分查询关于在轮询模式中使用PCIe DMA IP的更多信息。


