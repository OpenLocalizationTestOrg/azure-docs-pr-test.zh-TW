---
title: "aaaUse 需要大量計算的 Azure Vm 與批次 |Microsoft 文件"
description: "具備 RDMA 功能，或按一下 啟用 GPU 的 VM tootake 利用 Azure Batch 集區中的調整大小"
services: batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: danlep
ms.openlocfilehash: 6a462a5f2a44ddcec8bf4e5c200d444cac8fafe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-rdma-capable-or-gpu-enabled-instances-in-batch-pools"></a>在 Batch 集區中使用具備 RDMA 功能或已啟用 GPU 功能的執行個體

toorun 特定批次作業，您可能會想針對大規模的計算的 Azure VM 大小的 tootake 優點。 例如，toorun 多重執行個體[MPI 工作負載](batch-mpi.md)、 您可以選擇 A8、 A9、 或 H 序列的大小會有網路介面的遠端直接記憶體存取 (RDMA)。 這些大小連接 tooan InfiniBand 網路節點間的通訊，可加速 MPI 應用程式。 如果是 CUDA 應用程式，則可以選擇 N 系列大小，因為這些大小包含 NVIDIA Tesla 圖形處理器 (GPU) 顯示卡。

本文提供指引和範例 toouse 一些 Azure 的特定大小，請在批次集區。 若要了解規格及背景，請參閱：

* 高效能計算 VM 大小 ([Linux](../virtual-machines/linux/sizes-hpc.md)、[Windows](../virtual-machines/windows/sizes-hpc.md)) 

* 已啟用 GPU 功能的 VM 大小 ([Linux](../virtual-machines/linux/sizes-gpu.md)、[Windows](../virtual-machines/windows/sizes-gpu.md)) 


## <a name="subscription-and-account-limits"></a>訂用帳戶與帳戶限制

* **配額**-hello 數目或類型，可能會限制一個或多個 Azure 配額的節點中，您可以加入 tooa 批次集區。 您會更有可能 toobe 限制，當您選擇具備 RDMA 功能，啟用 GPU 或其他多核心的 VM 大小。 根據您所建立的批次帳戶 hello 類型，toohello 帳戶本身或 tooyour 訂用帳戶，無法套用 hello 配額。

    * 如果您建立您的 Batch 帳戶在 hello**批次服務**組態都受到 hello[每個批次帳戶的專用的核心配額](batch-quota-limit.md#resource-quotas)。 根據預設，這個配額為 20 個核心。 個別配額套用太[低優先權 Vm](batch-low-pri-vms.md)，如果您使用它們。 

    * 如果您建立 hello 帳戶在 hello**使用者訂用帳戶**組態，您的訂用帳戶限制每個區域的 VM 核心的 hello 數目。 請參閱 [Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)。 您的訂用帳戶也會套用地區配額 toocertain VM 大小，包括 HPC 和 GPU 的執行個體。 在 hello 使用者訂用帳戶設定中，沒有其他配額套用 toohello Batch 帳戶。 

  在批次中使用特製化的 VM 大小時您可能需要指定 tooincrease 一或多個配額。 toorequest 增加配額，開啟[線上客戶支援要求](../azure-supportability/how-to-create-azure-support-request.md)不收費。

* **區域可用性**-需要大量計算 Vm 可能無法使用您用來建立批次帳戶的 hello 區域中。 toocheck 的大小是可用，請參閱[依地區可用的產品](https://azure.microsoft.com/regions/services/)。


## <a name="dependencies"></a>相依項目

只能在某些作業系統支援 hello RDMA 和 GPU 功能需要大量計算的大小。 根據您的作業系統，您可能需要 tooinstall，或設定額外的驅動程式或其他軟體。 hello 下表摘要說明這些相依性。 如需詳細資訊，請參閱連結的文章。 選項 tooconfigure 批次集區，請參閱本文稍後。


### <a name="linux-pools---virtual-machine-configuration"></a>Linux 集區 - 虛擬機器組態

| 大小 | 功能 | 作業系統 | 必要的軟體 | 集區設定 |
| -------- | -------- | ----- |  -------- | ----- |
| [H16r、H16mr、A8、A9](../virtual-machines/linux/sizes-hpc.md#rdma-capable-instances) | RDMA | SUSE Linux Enterprise Server 12 HPC 或<br/>CentOS 型 HPC<br/>(Azure Marketplace) | Intel MPI 5 | 啟用節點間通訊、停用並行工作執行 |
| [NC 系列*](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms) | NVIDIA Tesla K80 GPU | Ubuntu 16.04 LTS。<br/>Red Hat Enterprise Linux 7.3，或<br/>CentOS 型 7.3<br/>(Azure Marketplace) | NVIDIA CUDA Toolkit 8.0 驅動程式 | N/A | 
| [NV 系列](../virtual-machines/linux/n-series-driver-setup.md#install-grid-drivers-for-nv-vms) | NVIDIA Tesla M60 GPU | Ubuntu 16.04 LTS<br/>Red Hat Enterprise Linux 7.3<br/>CentOS 型 7.3<br/>(Azure Marketplace) | NVIDIA GRID 4.3 驅動程式 | N/A |

*具有 Intel MPI 的 CentOS 型 7.3 HPC 可支援在 NC24r VM 上進行 RDMA 連線。



### <a name="windows-pools---virtual-machine-configuration"></a>Windows 集區 - 虛擬機器組態

| 大小 | 功能 | 作業系統 | 必要的軟體 | 集區設定 |
| -------- | ------ | -------- | -------- | ----- |
| [H16r、H16mr、A8、A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2 或<br/>Windows Server 2012 (Azure Marketplace) | Microsoft MPI 2012 R2 或更新版本，或<br/> Intel MPI 5<br/><br/>HpcVMDrivers Azure VM 擴充功能 | 啟用節點間通訊、停用並行工作執行 |
| [NC 系列*](../virtual-machines/windows/n-series-driver-setup.md) | NVIDIA Tesla K80 GPU | Windows Server 2016 或 <br/>Windows Server 2012 R2 (Azure Marketplace) | NVIDIA Tesla 驅動程式或 CUDA Toolkit 8.0 驅動程式| N/A | 
| [NV 系列](../virtual-machines/windows/n-series-driver-setup.md) | NVIDIA Tesla M60 GPU | Windows Server 2016 或<br/>Windows Server 2012 R2 (Azure Marketplace) | NVIDIA GRID 4.3 驅動程式 | N/A |

*具有 HpcVMDrivers 擴充功能和 Microsoft MPI 或 Intel MPI 的 Windows Server 2012 R2 可支援在 NC24r VM 上進行 RDMA 連線。

### <a name="windows-pools---cloud-services-configuration"></a>Windows 集區 - 雲端服務組態

> [!NOTE]
> 批次集區與 hello 雲端服務組態中不支援 N 序列的大小。
>

| 大小 | 功能 | 作業系統 | 必要的軟體 | 集區設定 |
| -------- | ------- | -------- | -------- | ----- |
| [H16r、H16mr、A8、A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2、<br/>Windows Server 2012 或<br/>Windows Server 2008 R2 (Guest OS 系列) | Microsoft MPI 2012 R2 或更新版本，或<br/>Intel MPI 5<br/><br/>HpcVMDrivers Azure VM 擴充功能 | 啟用節點間通訊、<br/> 停用並行工作執行 |





## <a name="pool-configuration-options"></a>集區組態選項

tooconfigure 特製化的 VM 大小，批次集區、 hello 批次應用程式開發介面和工具會提供數個選項所需的 tooinstall 軟體或驅動程式，包括：

* [啟動工作](batch-api-basics.md#start-task)-以資源檔案 tooan hello 中的 Azure 儲存體帳戶上傳的安裝套件與 hello 批次帳戶相同的區域。 Hello 集區啟動時，請以無訊息方式建立開始工作命令列 tooinstall hello 資源檔案。 如需詳細資訊，請參閱 hello [REST API 文件](/rest/api/batchservice/add-a-pool-to-an-account#bk_starttask)。

  > [!NOTE] 
  > hello 啟動工作必須執行以提升權限 （系統管理員） 權限，以及必須等候成功。
  >

* [應用程式封裝](batch-application-packages.md)-zip 壓縮的安裝封裝 tooyour 批次帳戶中加入和設定封裝參考 hello 集區。 這個設定會將上傳，並會 hello hello 集區中的所有節點上的封裝。 如果 hello 封裝是安裝程式，建立啟動工作命令列 toosilently 安裝 hello 應用程式集區的所有節點上。 排程的 toorun 節點上工作時，選擇性地安裝 hello 封裝。

* [自訂的集區映像](batch-api-basics.md#pool)-建立自訂的 Windows 或 Linux VM 映像，其中包含驅動程式、 軟體或其他設定所需的 hello VM 大小。 如果您建立您的 Batch 帳戶在 hello 使用者訂用帳戶設定中，指定 hello 批次集區的自訂映像。 （自訂映像不支援在 hello 批次服務組態中的帳戶）。自訂映像只可以搭配 hello 虛擬機器組態中的集區。

  > [!IMPORTANT]
  > 在 Batch 集區中，您目前無法使用以受控磁碟或進階儲存體建立的自訂映像。
  >



* [批次造船廠](https://github.com/Azure/batch-shipyard)hello GPU 和 rdma 來說 toowork 以透明的方式會以自動設定 Azure 批次的容器化工作負載。 Batch Shipyard 完全是透過組態檔來驅動。 有許多範例配方設定可啟用 GPU 和 rdma 來說工作負載，例如 hello [CNTK GPU 配方](https://github.com/Azure/batch-shipyard/tree/master/recipes/CNTK-GPU-OpenMPI)的預先設定了 N 系列 Vm 的 GPU 驅動程式，並載入 Microsoft 認知工具組做為 Docker 映像的軟體。


## <a name="example-microsoft-mpi-on-an-a8-vm-pool"></a>範例：A8 VM 集區上的 Microsoft MPI

toorun Windows MPI 應用程式集區的 Azure A8 節點上，您需要 tooinstall 支援的 MPI 實作。 以下是範例步驟 tooinstall [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) Windows 在集區使用的批次應用程式套件。

1. 下載 hello[安裝套件](http://go.microsoft.com/FWLink/p/?LinkID=389556)(MSMpiSetup.exe) 的 Microsoft MPI hello 最新版本。
2. 建立 hello 封裝 zip 檔案。
3. 上傳 hello 封裝 tooyour Batch 帳戶。 如需步驟，請參閱 hello[應用程式封裝](batch-application-packages.md)指引。 指定應用程式識別碼 (例如 MSMPI) 和版本 (例如 8.1)。 
4. 使用 hello 批次 Api 或 Azure 入口網站，建立具有所需的 hello 節點和小數位數數目的 hello 雲端服務組態中的集區。 hello 下表顯示範例設定 tooset MPI 註冊以使用啟動工作的自動安裝模式：

| 設定 | 值 |
| ---- | ----- | 
| **映像類型** | 雲端服務 |
| **作業系統系列** | Windows Server 2012 R2 (作業系統系列 4) |
| **節點大小** | A8 標準 |
| **已啟用節點間通訊** | True |
| **每個節點的工作數上限** | 1 |
| **應用程式套件參考** | MSMPI |
| **已啟用啟動工作** | True<br>**命令列** - `"cmd /c %AZ_BATCH_APP_PACKAGE_MSMPI#8.1%\\MSMpiSetup.exe -unattend -force"`<br/>**使用者身分識別** - 集區的自動使用者、系統管理員<br/>**等待成功** - True

## <a name="example-nvidia-tesla-drivers-on-nc-vm-pool"></a>範例：NC VM 集區上的 NVIDIA Tesla 驅動程式

toorun CUDA 應用程式集區的 NC Linux 節點上，您需要 tooinstall CUDA Toolkit 8.0 hello 節點上。 hello Toolkit 安裝 hello 必要 NVIDIA Tesla GPU 驅動程式。 以下是範例步驟 toodeploy hello GPU 驅動程式的自訂 Ubuntu 16.04 LTS 映像：

1. 部署執行 Ubuntu 16.04 LTS 的 Azure NC6 VM。 例如，在 hello 美國中南部地區建立 hello VM。 請確定您有標準的儲存區，建立 hello VM 和*沒有*管理的磁碟。
2. 請遵循 hello 步驟 tooconnect toohello VM 和[安裝 CUDA 驅動程式](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms)。
3. 取消佈建 hello Linux 代理程式，然後擷取 Linux VM 映像使用 hello Azure CLI 1.0 命令。 如需相關步驟，請參閱[擷取在 Azure 上執行的 Linux 虛擬機器](../virtual-machines/linux/capture-image-nodejs.md)。 記下 hello 影像 URI。
  > [!IMPORTANT]
  > 請勿針對 Azure 批次使用 Azure CLI 2.0 命令 toocapture hello 映像。 目前 hello CLI 2.0 命令只會擷取使用受管理的磁碟建立的 Vm。
  >
4. 建立批次帳戶，使用 hello 使用者訂用帳戶設定，支援 NC Vm 所在的地區。
5. 使用 hello 批次 Api 或 Azure 入口網站使用 hello 自訂映像來建立資料庫，並以 hello 所需的節點和小數位數數目。 hello 下表顯示 hello 映像的範例集區設定：

| 設定 | 值 |
| ---- | ---- |
| **映像類型** | 自訂映像 |
| **自訂映像** | 影像 hello 表單的 URI`https://yourstorageaccountdisks.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd` |
| **節點代理程式 SKU** | batch.node.ubuntu 16.04 |
| **節點大小** | NC6 標準 |



## <a name="next-steps"></a>後續步驟

* Azure Batch 集區上的 toorun MPI 工作，請參閱 「 hello [Windows](batch-mpi.md)或[Linux](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/)範例。

* 例如批次中的 GPU 工作負載的詳細資訊，請參閱 hello[批次造船廠](https://github.com/Azure/batch-shipyard/)的訣竅。
