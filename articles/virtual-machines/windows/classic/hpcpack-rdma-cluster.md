---
title: "讓 Windows RDMA 叢集 toorun MPI 應用程式的 aaaSet |Microsoft 文件"
description: "了解如何 toocreate Windows HPC Pack 叢集大小 H16r 的 H16mr、 A8、 A9 Vm toouse 與 hello Azure RDMA 網路 toorun MPI 應用程式。"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 7d9f5bc8-012f-48dd-b290-db81c7592215
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 23bc8740dbd05a7c7ab3f998489a41d0df4520a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-rdma-cluster-with-hpc-pack-toorun-mpi-applications"></a>設定 Windows RDMA 叢集與 HPC Pack toorun MPI 應用程式
設定在 Azure 中的 Windows RDMA 叢集[Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029)和[高效能計算 VM 大小](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)toorun 平行訊息傳遞介面 (MPI) 應用程式。 當您在 HPC Pack 叢集中設定了支援 RDMA 的 Windows Server 型節點時，MPI 應用程式會在 Azure 中透過以遠端直接記憶體存取 (RDMA) 技術為基礎的低延遲、高輸送量網路，有效率地進行通訊。

如果您想 toorun Linux Vm 存取 hello Azure RDMA 網路的 MPI 工作負載，請參閱[Linux RDMA 叢集 toorun MPI 應用程式設定](../../linux/classic/rdma-cluster.md)。

## <a name="hpc-pack-cluster-deployment-options"></a>HPC Pack 叢集部署選項
Microsoft HPC Pack 是一種工具，提供任何額外的成本 toocreate 在 HPC 叢集，在內部部署或 Azure toorun Windows 或 Linux HPC 應用程式中。 HPC Pack 包含 hello 的 hello 訊息傳遞介面 for Windows (MS-MPI) 的 Microsoft 實作的執行階段環境。 執行支援的 Windows Server 作業系統具備 RDMA 功能的執行個體搭配使用時，HPC Pack 提供有效率的方法 toorun Windows MPI 應用程式存取 hello Azure RDMA 網路。 

這篇文章導入了兩個案例，以及連結使用 Microsoft HPC Pack Windows RDMA 叢集 toodetailed 指引 tooset。 

* 案例 1. 部署計算密集型背景工作角色執行個體 (PaaS)
* 案例 2. 在大量運算 VM 中部署運算節點 (IaaS)

一般先決條件與 Windows 的 toouse 需要大量計算執行個體，請參閱[高效能計算 VM 大小](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="scenario-1-deploy-compute-intensive-worker-role-instances-paas"></a>案例 1︰部署計算密集型背景工作角色執行個體 (PaaS)
從現有的 HPC Pack 叢集，在執行於雲端服務 (PaaS) 的 Azure 背景工作角色執行個體 (Azure 節點) 中新增額外的運算資源。 這項功能，也稱為 「 高載 tooAzure 」 從 HPC Pack 支援許多大小 hello 背景工作角色執行個體。 當加入 hello Azure 節點時，指定其中一個 hello 具備 RDMA 功能的大小。

以下是考量和步驟 tooburst tooRDMA 能夠 Azure 執行個體從現有 （通常是內部） 叢集。 使用類似程序 tooadd 背景工作角色執行個體 tooan HPC Pack 前端節點部署 Azure VM 中。

> [!NOTE]
> 使用 HPC Pack 教學課程 tooburst tooAzure，請參閱[設定混合式叢集使用 HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)。 請注意 hello 套用特別 tooRDMA 能力的 Azure 節點的步驟中的 hello 考量。
> 
> 

![高載 tooAzure][burst]

### <a name="steps"></a>步驟
1. **部署及設定 HPC Pack 2012 R2 前端節點**
   
    Hello 從下載最新 HPC Pack 安裝套件 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922)。 如需 Azure 高載部署的需求和指示 tooprepare，請參閱[tooAzure 背景工作執行個體，使用 Microsoft HPC Pack 高載](https://technet.microsoft.com/library/gg481749.aspx)。
2. **在 hello Azure 訂用帳戶中設定管理憑證**
   
    設定憑證 toosecure hello hello 前端節點與 Azure 之間連線。 選項和程序，請參閱[案例 tooConfigure hello Azure 管理憑證，為 HPC Pack](http://technet.microsoft.com/library/gg481759.aspx)。 測試部署 HPC Pack 安裝預設 Microsoft HPC Azure 管理憑證可以快速上傳 tooyour Azure 訂用帳戶。
3. **建立新的雲端服務和儲存體帳戶**
   
    Hello 具備 RDMA 功能的執行個體可用的區域中的 hello 部署的雲端服務和儲存體帳戶使用 Azure 入口網站 toocreate hello。
4. **建立 Azure 節點範本**
   
    使用 HPC 叢集管理員中的 hello 建立節點範本精靈。 如需步驟，請參閱[建立 Azure 節點範本](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Templ)中 「 步驟 tooDeploy Azure 節點使用 Microsoft HPC Pack"。
   
    為初始測試，我們建議在 hello 範本中設定手動可用性原則。
5. **新增節點 toohello 叢集**
   
    使用 HPC 叢集管理員中的 hello 新增節點精靈。 如需詳細資訊，請參閱[新增 Azure 節點 toohello Windows HPC 叢集](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Add)。
   
    指定的 hello 節點 hello 大小，請選取其中一個 hello 具備 RDMA 功能的執行個體大小。
   
   > [!NOTE]
   > 每個 tooAzure 部署高載 hello 需要大量計算執行個體中的 HPC Pack 會自動部署至少兩個具備 RDMA 功能的執行個體 （如 A8) 做為 proxy 節點，此外 toohello Azure 背景工作角色執行個體指定。 hello proxy 節點使用的核心配置 toohello 訂用帳戶，而且會產生任何費用以及 hello Azure 背景工作角色執行個體。
   > 
   > 
6. **啟動 （佈建） hello 節點，並使其線上 toorun 工作**
   
    選取 hello 節點，然後使用 hello**啟動**HPC 叢集管理員中的動作。 佈建完成時，請選取 hello 節點，然後使用 hello**上線**HPC 叢集管理員中的動作。 hello 節點而準備的 toorun 作業。
7. **提交工作 toohello 叢集**
   
   使用 HPC Pack 工作提交工具 toorun 叢集作業。 請參閱 [Microsoft HPC Pack：工作管理](http://technet.microsoft.com/library/jj899585.aspx)。
8. **停止 （解除佈建） hello 節點**
   
   當您完成執行的作業時，使 hello 節點離線，並使用 hello**停止**HPC 叢集管理員中的動作。

## <a name="scenario-2-deploy-compute-nodes-in-compute-intensive-vms-iaas"></a>案例 2︰在大量計算 VM 中部署計算節點 (IaaS)
在此案例中，您可以部署 hello HPC Pack 前端節點和叢集計算節點 Vm 上的 Azure 虛擬網路。 HPC Pack 提供一些 [Azure VM 中的部署選項](../../linux/hpcpack-cluster-options.md)，包括自動部署指令碼和 Azure 快速入門範本。 例如，hello 下列考量和步驟會引導您 toouse hello [HPC Pack IaaS 部署指令碼](hpcpack-cluster-powershell-script.md)來自動化 hello 部署在 Azure 中部署 HPC Pack 2012 R2 叢集。

![Azure VM 中的叢集][iaas]

### <a name="steps"></a>步驟
1. **建立叢集前端節點和計算節點 Vm 上的用戶端電腦執行 hello HPC Pack IaaS 部署指令碼**
   
    從 hello 下載 hello HPC Pack IaaS 部署指令碼封裝[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922)。
   
    tooprepare hello 用戶端電腦，建立 hello 指令碼組態檔，並執行的 hello 指令碼，請參閱[以 hello HPC Pack IaaS 部署指令碼建立 HPC 叢集](hpcpack-cluster-powershell-script.md)。 
   
    toodeploy 具備 RDMA 功能的計算節點，請注意 hello 下列其他考量：
   
   * **虛擬網路**： 指定新的虛擬網路中的 hello 具備 RDMA 功能的執行個體大小的區域在您想 toouse 為止。
   * **Windows Server 作業系統**: toosupport RDMA 連接，指定在 Windows Server 2012 R2 或 Windows Server 2012 作業系統的 hello 運算節點 Vm。
   * **雲端服務**：建議您將前端節點部署在一個雲端服務中，而將計算節點部署在另一個雲端服務中。
   * **前端節點大小**： 對於此案例中，請考慮的大小至少 A4 （超大型） hello 前端節點。
   * **HpcVmDrivers 延伸模組**: hello 部署指令碼 hello Azure VM 代理程式 」 和 「 hello HpcVmDrivers 延伸模組會自動安裝時部署具有 Windows Server 作業系統的大小 A8 或 A9 計算節點。 HpcVmDrivers hello 運算節點 Vm 上安裝驅動程式，以便 toohello RDMA 網路連線。 在具備 RDMA 功能的 H 系列 Vm，您必須手動安裝 hello HpcVmDrivers 延伸模組。 請參閱[高效能運算 VM 大小](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
   * **叢集網路組態**: hello 部署指令碼會自動設定拓撲 5 （hello 企業網路上的所有節點） 中的 hello HPC Pack 叢集。 VM 中的所有 HPC Pack 叢集部署都需要此拓撲。 稍後請勿變更 hello 叢集網路拓撲。
2. **將 hello 計算節點線上 toorun 工作**
   
    選取 hello 節點，然後使用 hello**上線**HPC 叢集管理員中的動作。 hello 節點而準備的 toorun 作業。
3. **提交工作 toohello 叢集**
   
    連接 toosubmit toohello 前端節點的作業，或這設定在內部部署電腦 toodo。 如需資訊，請參閱[提交作業 tooan HPC 叢集在 Azure 中](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
4. **Take hello 節點離線，並會停止 （取消配置） 它們**
   
    當您完成執行的作業，採取 hello 節點離線 HPC 叢集管理員中。 然後，使用 Azure 管理工具 tooshut 它們關閉。

## <a name="run-mpi-applications-on-hello-cluster"></a>Hello 叢集上執行 MPI 應用程式
### <a name="example-run-mpipingpong-on-an-hpc-pack-cluster"></a>範例：在 HPC Pack 叢集上執行 mpipingpong
tooverify hello 具備 RDMA 功能的執行個體，執行的 HPC Pack 部署 hello HPC Pack **mpipingpong** hello 叢集上的命令。 **mpipingpong**傳送配對的節點之間的資料封包重複 toocalculate 延遲和輸送量的測量和統計資料的 hello RDMA 功能的應用程式網路。 此範例示範執行 MPI 工作的一般模式 (在此情況下， **mpipingpong**) 使用 hello 叢集**mpiexec**命令。

這個範例假設您在 「 高載 tooAzure 」 組態中加入 Azure 節點 ([案例 1](#scenario-1.-deploy-compute-intensive-worker-role-instances-\(PaaS\) in this article)。 如果您部署 HPC Pack 叢集上的 Azure Vm，您將需要 toomodify hello 命令語法 toospecify 不同節點群組，並設定其他環境變數 toodirect 網路流量 toohello RDMA 網路。

toorun mpipingpong hello 叢集上：

1. Hello 前端節點上，或已正確設定的用戶端電腦上，開啟 命令提示字元。
2. tooestimate 成對 Azure 高載部署的四個節點，下列命令 toosubmit 具有小型封包和反覆項目多作業 toorun mpipingpong 類型 hello 中的節點之間的延遲：
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 1:100000 -op -s nul
    ```
   
    hello 命令傳回 hello 作業已送出 hello 識別碼。
   
    如果您部署 Azure Vm 上部署的 hello HPC Pack 叢集時，指定包含的節點群組計算節點 Vm 部署在單一雲端服務中，並修改 hello **mpiexec**命令，如下所示：
   
    ```Command
    job submit /nodegroup:vmcomputenodes /numnodes:4 mpiexec -c 1 -affinity -env MSMPI_DISABLE_SOCK 1 -env MSMPI_PRECONNECT all -env MPICH_NETMASK 172.16.0.0/255.255.0.0 mpipingpong -p 1:100000 -op -s nul
    ```
3. Hello 作業完成時，tooview hello 輸出 （在此案例中的 hello 工作 task 1 的 hello 輸出），下列類型 hello
   
    ```Command
    task view <JobID>.1
    ```
   
    其中&lt; *JobID* &gt; hello 送出 hello 作業識別碼。
   
    hello 輸出包括延遲結果類似 toohello 下列。
   
    ![Ping pong 延遲][pingpong1]
4. tooestimate 輸送量之間成對的 Azure 高載節點、 輸入 hello 下列命令 toosubmit 作業 toorun **mpipingpong**具有大型封包和幾個反覆項目：
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 4000000:1000 -op -s nul
    ```
   
    hello 命令傳回 hello 作業已送出 hello 識別碼。
   
    在 HPC Pack 叢集上部署在 Azure Vm 上，修改 hello 命令，如步驟 2 中所述。
5. Hello 作業完成時，tooview hello 輸出 （在此案例中的 hello 工作 task 1 的 hello 輸出），下列類型 hello:
   
    ```Command
    task view <JobID>.1
    ```
   
   hello 輸出包括輸送量結果類似 toohello 下列。
   
   ![Ping pong 輸送量][pingpong2]

### <a name="mpi-application-considerations"></a>MPI 應用程式考量
以下是在 Azure 中使用 HPC Pack 執行 MPI 應用程式時的考量。 部分適用於僅 toodeployments 的 Azure 節點 （背景工作角色執行個體在 「 高載 tooAzure 」 組態中加入）。

* Azure 會定期重新佈建雲端服務中的背景工作角色執行個體，不另行通知 (例如為了維護系統，或是因為執行個體失敗)。 如果執行 MPI 工作時，會重新佈建執行個體，hello 執行個體就會失去其資料，並傳回 toohello 狀態，第一次部署時，這可能導致 hello MPI 工作 toofail。 hello 更多的節點，用單一 MPI 工作，以及 hello 再 hello 執行作業時，更有可能，其中一個 hello 執行個體重新佈建作業執行時的 hello。 也請考慮下列事項如果您將 hello 部署中的單一節點指定為檔案伺服器。
* 在 Azure 中的 toorun MPI 工作，您不需要 toouse hello 具備 RDMA 功能的執行個體。 您可以使用 HPC Pack 支援的任何執行個體大小。 不過，建議使用 hello 具備 RDMA 功能的執行個體執行相當大型的 MPI 工作機密 toohello 延遲且 hello hello hello 節點連接的網路頻寬。 如果您使用其他大小 toorun 延遲和頻寬敏感的 MPI 工作時，建議您執行單一工作只在少數節點執行的小型作業。
* 主旨 toohello 授權條款 hello 應用程式相關聯的應用程式部署 tooAzure 執行個體。 請 hello 廠商授權的任何商業應用程式或 hello 雲端中執行的其他限制。 並非所有廠商都提供隨用隨付授權。
* Tooaccess 在內部部署節點、 共用和授權伺服器，需要進一步設定 azure 執行個體。 例如，tooenable hello Azure 節點 tooaccess-內部部署授權伺服器，您可以設定站對站 Azure 虛擬網路。
* Azure 的執行個體上的 toorun MPI 應用程式註冊每個 MPI 應用程式的 Windows 防火牆 hello 執行個體上執行 hello **hpcfwutil**命令。 這可讓 MPI 通訊 tootake 放在 hello 防火牆動態指派連接埠。
  
  > [!NOTE]
  > 針對高載 tooAzure 部署，您也可以設定防火牆例外狀況命令 toorun 自動加入 tooyour 叢集的所有新 Azure 節點上。 執行 hello 之後**hpcfwutil**命令，並驗證您的應用程式運作方式，加入 hello 命令 tooa 啟動指令碼針對您的 Azure 節點。 如需詳細資訊，請參閱 [Use a Startup Script for Azure Nodes (使用 Azure 節點的啟動指令碼)](https://technet.microsoft.com/library/jj899632.aspx)。
  > 
  > 
* HPC Pack 的 MPI 通訊使用 hello CCP_MPI_NETMASK 叢集環境變數 toospecify 可接受的位址範圍。 從 HPC Pack 2012 R2 開始，hello CCP_MPI_NETMASK 叢集環境變數只會影響加入網域的叢集計算節點之間的 MPI 通訊 (內部或在 Azure Vm 中)。 高載 tooAzure 組態中加入的節點，會忽略 hello 變數。
* MPI 工作無法跨部署在不同的雲端服務 （例如，在不同節點範本或部署在多個雲端服務的 Azure VM 運算節點的高載 tooAzure 部署） 的 Azure 執行個體執行。 如果您有多個使用不同節點範本啟動的 Azure 節點部署，hello MPI 工作必須執行一組 Azure 節點上。
* 當您新增 Azure 節點 tooyour 叢集並使其上線，hello HPC 工作排程器服務立即嘗試 toostart hello 節點上的作業。 如果只有部分工作負載可以在 Azure 上執行，請確定您已更新或建立工作範本 toodefine 類型可以在 Azure 執行哪一項作業。 例如，提交工作範本只能在 Azure 節點上執行的工作新增 hello 節點群組屬性 toohello 工作範本，並選取 AzureNodes 為 hello tooensure 必要值。 您的 Azure 節點的 toocreate 自訂群組使用 hello Add-hpcgroup HPC PowerShell 指令程式。

## <a name="next-steps"></a>後續步驟
* 做為替代 toousing HPC Pack，開發與 hello Azure Batch 服務 toorun MPI 應用程式上的運算節點，在 Azure 中的受管理集區。 請參閱[使用多個執行個體工作 toorun Azure 批次中的訊息傳遞介面 (MPI) 應用程式](../../../batch/batch-mpi.md)。
* 如果您想 toorun Linux MPI 應用程式存取 hello Azure RDMA 網路，請參閱[Linux RDMA 叢集 toorun MPI 應用程式設定](../../linux/classic/rdma-cluster.md)。

<!--Image references-->
[burst]:media/hpcpack-rdma-cluster/burst.png
[iaas]:media/hpcpack-rdma-cluster/iaas.png
[pingpong1]:media/hpcpack-rdma-cluster/pingpong1.png
[pingpong2]:media/hpcpack-rdma-cluster/pingpong2.png
