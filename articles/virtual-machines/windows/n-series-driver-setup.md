---
title: "適用於 Windows 的 aaaAzure N 序列驅動程式安裝 |Microsoft 文件"
description: "如何 tooset 向上 N 系列 Vm 在 Azure 中執行 Windows 的 NVIDIA GPU 驅動程式"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>為執行 Windows Server 的 N 系列 VM 設定 GPU 驅動程式
tootake 利用 hello GPU 功能的 Azure N 系列 Vm 執行 Windows Server 2016 或 Windows Server 2012 R2，安裝支援 NVIDIA 圖形驅動程式。 本文提供您在部署 N 系列 VM 後的驅動程式安裝步驟。 驅動程式設定資訊也適用於 [ VM](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

如需基本規格、儲存體容量與磁碟的詳細資料，請參閱 [GPU Windows VM 大小](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>驅動程式安裝

1. 遠端桌面 tooeach N 系列 VM 的連線。

2. 下載、 擷取，並安裝 Windows 作業系統的支援 hello 驅動程式。

在 Azure NV VM 上，安裝驅動程式之後必須重新啟動。 在 NC VM 上，則不需要重新啟動。

## <a name="verify-driver-installation"></a>確認驅動程式安裝

您可以在 [裝置管理員] 中確認驅動程式安裝。 hello 下列範例顯示成功之組態 hello Tesla K80 卡 NC Azure VM 上。

![GPU 驅動程式屬性](./media/n-series-driver-setup/GPU_driver_properties.png)

tooquery hello GPU 裝置狀態、 執行 hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface)與 hello 驅動程式一起安裝的命令列公用程式。

1. 開啟命令提示字元並變更 toohello **C:\Program Files\NVIDIA Corporation\NVSMI**目錄。

2. 執行 **nvidia-smi**。 如果安裝 hello 驅動程式會輸出類似 toobelow。 請注意， **GPU Util**顯示**0%**除非 hello VM 上目前正在 GPU 工作負載。

![NVIDIA 裝置狀態](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>適用於 NC24r VM 的 RDMA 網路

可以部署在 hello 的 NC24r Vm 上啟用 RDMA 網路連線相同可用性設定組。 hello HpcVmDrivers 延伸模組必須先新增 tooinstall Windows 網路裝置驅動程式，啟用 RDMA 連接。 tooadd hello VM 延伸模組 tooan NC24r VM 使用[Azure PowerShell](/powershell/azure/overview) Azure 資源管理員的 cmdlet。

> [!NOTE]
> 目前，只有 Windows Server 2012 R2 支援 hello RDMA 網路 NC24r Vm 上。
> 

tooinstall hello 最新版本 1.1 HpcVMDrivers 延伸模組現有具備 RDMA 功能的 VM 上名為 myVM hello 美國西部區域中：
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  如需詳細資訊，請參閱[適用於 Windows 的虛擬機器擴充功能和功能](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

hello RDMA 網路以執行應用程式支援訊息傳遞介面 (MPI) 流量[Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx)或 Intel MPI 5.x。 


## <a name="next-steps"></a>後續步驟

* 在 hello N 系列 Vm 上 hello NVIDIA Gpu 的相關資訊，請參閱：
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (適用於 Azure NC VM)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (適用於 Azure NV VM)

* 建置 hello NVIDIA Tesla Gpu 的 GPU 加速應用程式的開發人員同時下載及安裝 hello CUDA Toolkit 8 的[Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe)或[Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe)。 如需詳細資訊，請參閱 hello [CUDA 安裝指南](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi)。


