---
title: "aaaLinux HPC Pack 叢集中計算 Vm |Microsoft 文件"
description: "了解如何 toocreate 並使用 HPC Pack 叢集在 Azure 中的 Linux 高效能運算 (HPC) 工作負載"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>開始在 Azure 中的 HPC Pack 叢集使用 Linux 運算節點
在 Azure 中設定 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) 叢集，其中包含一個執行 Windows Server 的前端節點，以及數個執行支援之 Linux 散發套件的計算節點。 瀏覽選項 toomove 資料 hello Linux 節點與 hello Windows 叢集前端節點 hello 之間。 了解如何 toosubmit Linux HPC 作業 toohello 叢集。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

在高層級，hello 下列圖表顯示 hello HPC Pack 叢集您建立及使用。

![具有 Linux 節點的 HPC Pack 叢集][scenario]

針對其他選項 toorun Linux HPC 工作負載在 Azure 中，請參閱[技術資源，批次和高效能運算](../../../batch/big-compute-resources.md)。

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>部署具有 Linux 運算節點的 HPC Pack 叢集
本文將說明兩個選項 toodeploy HPC Pack 叢集在 Azure 中 Linux 計算節點。 這兩種方法使用 Marketplace 映像的 Windows Server 與 HPC Pack toocreate hello 前端節點。 

* **Azure Resource Manager 範本**-使用 hello Azure Marketplace 中的範本或快速入門中的範本 hello 社群，tooautomate 建立 hello Resource Manager 部署模型中的 hello 叢集。 例如，hello [Linux 工作負載的 HPC Pack 叢集](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)hello Azure Marketplace 中的範本會建立完整的 HPC Pack 叢集基礎結構的 Linux HPC 工作負載。
* **PowerShell 指令碼**-使用 hello [Microsoft HPC Pack IaaS 部署指令碼](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)(**New-hpciaascluster.ps1**) tooautomate hello 傳統部署模型中完整的叢集部署。 此 Azure PowerShell 指令碼使用 HPC Pack VM 映像 hello Azure Marketplace 中快速部署，並提供一組完整的組態參數 toodeploy Linux 計算節點。

如需有關在 Azure 中的 HPC Pack 叢集部署選項的詳細資訊，請參閱[選項 toocreate 及管理高效能運算 (HPC) 叢集，在 Azure 中使用 Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

### <a name="prerequisites"></a>必要條件
* **Azure 訂用帳戶**-您可以使用任一 hello Azure Global 或 Azure China 服務中的訂用帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/) 。
* **核心配額**-特別是當您選擇 toodeploy 具有多核心的 VM 大小的數個叢集節點，您可能需要的核心，tooincrease hello 配額。 tooincrease 配額限制時，會開啟免費線上客戶支援要求。
* **Linux 散發套件**-目前 HPC Pack 支援 hello 下列計算節點的 Linux 散發套件。 您可以使用這些發佈的 Marketplace 版本，或提供您自己的版本。
  
  * **CentOS 型**：6.5、6.6、6.7、7.0、7.1、7.2、6.5 HPC、7.1 HPC
  * **Red Hat Enterprise Linux**：6.7、6.8、7.2
  * **SUSE Linux Enterprise Server**：SLES 12、SLES 12 (Premium)、SLES 12 SP1、SLES 12 SP1 (Premium)、SLES 12 for HPC、SLES 12 for HPC (Premium)
  * **Ubuntu Server**：14.04 LTS、16.04 LTS
    
    > [!TIP]
    > toouse hello Azure RDMA 網路與 hello 具備 RDMA 功能的 VM 大小，其中指定從 hello Azure Marketplace 的 SUSE Linux Enterprise Server 12 HPC 或 CentOS 架構 HPC 映像。 如需詳細資訊，請參閱[高效能運算 VM 大小](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
    > 
    > 

使用 hello HPC Pack IaaS 部署指令碼的其他必要條件 toodeploy hello 叢集：

* **用戶端電腦**-您需要的 Windows 架構的用戶端電腦 toorun hello 叢集部署指令碼。
* **Azure PowerShell** - [安裝和設定 Azure PowerShell](/powershell/azure/overview) (0.8.10 版或更新版本)。
* **HPC Pack IaaS 部署指令碼**-下載及解壓縮 hello 最新版 hello 指令碼從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949)。 您可以執行檢查 hello hello 指令碼版本`.\New-HPCIaaSCluster.ps1 –Version`。 這篇文章根據 4.4.1 版本或更新版本的 hello 指令碼。

### <a name="deployment-option-1-use-a-resource-manager-template"></a>部署選項 1。 使用 Resource Manager 範本
1. 移 toohello [Linux 工作負載的 HPC Pack 叢集](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)hello Azure Marketplace 中的範本，然後按一下**部署**。
2. 在 hello Azure 入口網站，請檢閱 hello 資訊，然後按一下**建立**。
   
    ![建立入口網站][portal]
3. 在 hello**基本概念**刀鋒視窗中，輸入 hello 叢集，也會命名 hello 前端節點 VM 的名稱。 您可以選擇現有的資源群組，或可用 tooyou 的位置中建立 hello 部署群組。 hello 位置會影響特定 VM 大小和其他 Azure 服務的 hello 可用性 (請參閱[依地區可用的產品](https://azure.microsoft.com/regions/services/))。
4. 在 hello**前端節點設定**刀鋒視窗中，針對第一個部署，您通常可以接受 hello 預設設定。 
   
   > [!NOTE]
   > hello**後組態指令碼 URL**這選擇性設定 toospecify 公開可用 Windows PowerShell 指令碼之後, 您想要 toorun hello 前端節點 VM 上的執行。 
   > 
   > 
5. 在 hello**計算節點設定**刀鋒視窗中，選取的 hello 節點、 hello 數目和大小的 hello 節點的命名模式，然後 hello Linux 發佈 toodeploy。
6. 在 hello**基礎結構設定**刀鋒視窗中，輸入名稱 hello 虛擬網路和 Active Directory 網域、 網域和 VM 系統管理員認證和 hello 儲存體帳戶的命名模式。
   
   > [!NOTE]
   > HPC Pack 會使用 hello Active Directory 網域 tooauthenticate 叢集使用者。 
   > 
   > 
7. 以執行 hello 驗證測試，並檢閱 hello 使用條款之後，按**購買**。

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>部署選項 2。 使用 hello IaaS 部署指令碼
以下是使用 hello HPC Pack IaaS 部署指令碼的其他必要條件 toodeploy hello 叢集：

* **用戶端電腦**-您需要的 Windows 架構的用戶端電腦 toorun hello 叢集部署指令碼。
* **Azure PowerShell** - [安裝和設定 Azure PowerShell](/powershell/azure/overview) (0.8.10 版或更新版本)。
* **HPC Pack IaaS 部署指令碼**-下載及解壓縮 hello 最新版 hello 指令碼從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949)。 您可以執行檢查 hello hello 指令碼版本`.\New-HPCIaaSCluster.ps1 –Version`。 這篇文章根據 4.4.1 版本或更新版本的 hello 指令碼。

**XML 組態檔**

hello HPC Pack IaaS 部署指令碼會使用 XML 組態檔當做輸入的 toodescribe hello HPC 叢集。 hello 下列範例組態檔指定 HPC Pack 前端節點和兩個大小 A7 CentOS 7.0 Linux 運算節點組成的小叢集。 

視需要針對您的環境和所需的叢集組態中，修改 hello 檔案，並將它儲存例如 HPCDemoConfig.xml 的名稱。 例如，您需要 toosupply 訂用帳戶名稱和唯一的儲存體帳戶名稱和雲端服務名稱。 此外，您可能想 toochoose 不同 hello 計算節點支援 Linux 映像。 Hello hello 組態檔中的項目相關的詳細資訊，請參閱 hello 指令碼資料夾中的 hello Manual.rtf 檔案和[以 hello HPC Pack IaaS 部署指令碼建立 HPC 叢集](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**toorun hello HPC Pack IaaS 部署指令碼**

1. 系統管理員身分開啟 hello 用戶端電腦上的 Windows PowerShell。
2. 變更 hello 指令碼所在的目錄 toohello 資料夾安裝 (E:\IaaSClusterScript 在此範例中)。
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. 執行下列命令 toodeploy hello HPC Pack 叢集 hello。 這個範例假設 hello 設定檔位於 E:\HPCDemoConfig.xml
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    a. 因為 hello **AdminPassword**未指定 hello 上述命令，在中，您是使用者的提示的 tooenter hello 密碼*MyAdminName*。
   
    b. hello 指令碼，然後啟動 toovalidate hello 設定檔。 它可能會佔用 tooseveral 分鐘，取決於 hello 的網路連線。
   
    ![驗證][validate]
   
    c. 通過驗證之後，hello 指令碼會列出 hello 叢集資源 toocreate。 輸入*Y* toocontinue。
   
    ![資源][resources]
   
    d. hello 指令碼會啟動 toodeploy hello HPC Pack 叢集，並完成 hello 組態，而不需要進一步手動步驟。 hello 指令碼可以執行數分鐘。
   
    ![部署][deploy]
   
   > [!NOTE]
   > 在此範例中，hello 指令碼記錄檔會自動產生自 hello **-LogFile**未指定參數。 hello 記錄不即時寫入，但會收集在 hello 驗證和 hello 部署的 hello 結尾處。 如果 hello PowerShell 處理程序已停止執行 hello 指令碼時，某些記錄檔將會遺失。
   > 
   > 

## <a name="connect-toohello-head-node"></a>連接 toohello 前端節點
部署在 Azure 中的 hello HPC Pack 叢集之後[遠端桌面連線](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)toohello 前端節點 VM 使用 hello 部署 hello 叢集時所提供的網域認證 (例如， *hpc\\clusteradmin*)。 您可以管理 hello 叢集從 hello 前端節點。

Hello 前端節點上，啟動 hello HPC Pack 叢集的 HPC 叢集管理員 toocheck hello 狀態。 您可以管理和監視 Linux 計算節點 hello Windows 使用的相同方式計算節點。 例如，請參閱 hello Linux 節點中所列**資源管理**(這些節點會隨著 hello 部署**LinuxNode**範本)。

![節點管理][management]

另請參閱在 hello hello Linux 節點**熱度圖**檢視。

![熱圖][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>如何在 Linux 節點叢集中的 toomove 資料
您必須在 Linux 節點和 hello Windows 叢集前端節點 hello 之間的數個選項 toomove 資料。 以下是三種常見的方法，在 hello 下列各節中詳細說明：

* **Azure 檔案**-會公開受管理的 SMB 檔案共用 toostore 資料檔案，在 Azure 儲存體。 Windows 節點與 Linux 節點可以裝載為磁碟機或資料夾的 hello Azure 檔案共用相同的時間，即使它們部署在不同的虛擬網路。
* **前端節點 SMB 共用**-Linux 節點上裝載的 hello 前端節點的標準 Windows 共用的資料夾。
* **前端節點 NFS 伺服器** - 為混合式 Windows 與 Linux 環境提供檔案共用解決方案。

### <a name="azure-file-storage"></a>Azure 檔案儲存體
hello [Azure 檔案](https://azure.microsoft.com/services/storage/files/)服務會公開使用 hello 標準 SMB 2.1 通訊協定的檔案共用。 Azure Vm 和雲端服務可以透過掛接共用，應用程式元件之間共用檔案資料，並在內部部署應用程式可以透過 hello 檔案儲存體 API 存取檔案共用中的資料。 

如需詳細的步驟 toocreate Azure 檔案共用，並將其裝載 hello 前端節點上，請參閱[開始使用 Azure 檔案儲存在 Windows 上](../../../storage/files/storage-how-to-use-files-windows.md)。 toomount hello Azure 檔案共用 hello Linux 節點上，請參閱[如何 toouse Linux 的 Azure 檔案儲存體](../../../storage/files/storage-how-to-use-files-linux.md)。 tooset 持續連線，請參閱[Persisting 連線 tooMicrosoft Azure 檔案](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)。

下列範例的 hello，在 Azure 上建立檔案共用儲存體帳戶。 toomount hello 共用 hello 前端節點上，開啟命令提示字元，並輸入下列命令的 hello:

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

在此範例中，allvhdsje 是您的儲存體帳戶名稱、 storageaccountkey 是儲存體帳戶金鑰，而 rdma 是 hello Azure 檔案共用名稱。 hello Azure 檔案共用做為 z: hello 前端節點上裝載。

Linux 節點上，執行 toomount hello Azure 檔案共用**clusrun** hello 前端節點上的命令。 **[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** 是有用的 HPC Pack 工具 toocarry 多個節點上的系統管理工作。 (同時請參閱本文中的 [適用於 Linux 節點的 CLusrun](#Clusrun-for-Linux-nodes) )。

開啟 Windows PowerShell 視窗並輸入下列命令的 hello:

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

hello 第一個命令會建立名為 /rdma hello LinuxNodes 群組中的所有節點上的資料夾。 hello 第二個命令會掛接到目錄和檔案模式位元組 too777 hello /rdma 資料夾 hello Azure 檔案共用 allvhdsjw.file.core.windows.net/rdma。 在 hello 第二個命令中，allvhdsje 是您的儲存體帳戶名稱，且 storageaccountkey 儲存體帳戶金鑰。

> [!NOTE]
> hello"\`"hello 第二個命令中的符號是 PowerShell 的逸出符號。 「\`，」 表示該 hello"，"（逗號字元） 是 hello 命令的一部分。
> 
> 

### <a name="head-node-share"></a>前端節點共用
或者，在 Linux 節點上裝載共用的資料夾的 hello 前端節點。 共用提供最簡單方式 tooshare 檔案 hello，但在 hello，則必須部署 hello 前端節點和所有 Linux 節點相同的虛擬網路。 以下是 hello 步驟。

1. Hello 前端節點上建立資料夾，並共用它 tooEveryone 具有讀取/寫入權限。 例如，hello 與前端節點上的共用 D:\OpenFOAM \\CentOS7RDMA HN\OpenFOAM。 CentOS7RDMA HN 如下的 hello 前端節點的 hello 主機名稱。
   
    ![檔案共用權限][fileshareperms]
   
    ![檔案共用][filesharing]
2. 開啟 Windows PowerShell 視窗並執行下列命令的 hello:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

hello 第一個命令會建立名為 /openfoam hello LinuxNodes 群組中的所有節點上的資料夾。 hello 第二個命令會掛接到目錄和檔案模式位元組 too777 hello 資料夾 hello 共用資料夾 //CentOS7RDMA-HN/OpenFOAM。 hello 使用者名稱和密碼在 hello 命令應該 hello 使用者名稱和 hello 前端節點上的叢集使用者的密碼。 (請參閱 [Add or remove cluster users (新增或移除叢集使用者)](https://technet.microsoft.com/library/ff919330.aspx)。)

> [!NOTE]
> hello"\`"hello 第二個命令中的符號是 PowerShell 的逸出符號。 「\`，」 表示該 hello"，"（逗號字元） 是 hello 命令的一部分。
> 
> 

### <a name="nfs-server"></a>NFS 伺服器
hello NFS 服務可讓您 tooshare 和移轉執行使用 hello SMB 通訊協定的 hello Windows Server 2012 作業系統的電腦和 linux 電腦使用 hello NFS 通訊協定之間的檔案。 hello NFS 伺服器和所有其他節點已部署在 hello toobe 相同虛擬網路。 與 SMB 共用相比，它提供更好的 Linux 節點相容性。 例如，它支援檔案連結。

1. tooinstall 並設定 NFS 伺服器，請依照下列中的 hello 步驟[伺服器的網路檔案系統的第一個共用端對端](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx)。
   
    例如，建立名為下列屬性的 hello nfs 的 NFS 共用：
   
    ![NFS 授權][nfsauth]
   
    ![NFS 共用權限][nfsshare]
   
    ![NFS NTFS 權限][nfsperm]
   
    ![NFS 管理屬性][nfsmanage]
2. 開啟 Windows PowerShell 視窗並執行下列命令的 hello:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   hello 第一個命令會建立名為 /nfsshared hello LinuxNodes 群組中的所有節點上的資料夾。 hello 第二個命令掛接 hello NFS 共用 CentOS7RDMA HN: / nfs 到 hello 資料夾。 這裡 CentOS7RDMA HN: / nfs 的 NFS 共用的 hello 遠端路徑。

## <a name="how-toosubmit-jobs"></a>如何 toosubmit 工作
有數種方式 toosubmit 作業 toohello HPC Pack 叢集：

* HPC 叢集管理員或 HPC 工作管理員 GUI
* HPC Web 入口網站
* REST API

Azure HPC Pack GUI 工具和 hello HPC web 入口網站透過 toohello 叢集會將相同 hello 與 Windows 計算節點提交作業。 請參閱[HPC Pack 作業管理員](https://technet.microsoft.com/library/ff919691.aspx)和[toosubmit 從內部部署用戶端電腦的工作](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

透過 REST API hello toosubmit 作業，請參閱太[建立和提交工作使用 hello Microsoft HPC Pack 中的 REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx)。 toosubmit 工作，從 Linux 用戶端，也會參照 hello toohello Python 範例[HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756)。

## <a name="clusrun-for-linux-nodes"></a>適用於 Linux 節點的 CLusrun
hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx)工具都可以透過命令提示字元或 HPC 叢集管理員 Linux 節點上的使用的 tooexecute 命令。 以下有一些基本範例。

* Hello 叢集中所有節點上顯示目前的使用者名稱。
  
    ```command
    clusrun whoami
    ```
* 安裝 hello **gdb**偵錯工具與**yum** hello linuxnodes 群組，並在 10 分鐘後重新啟動 hello 節點中的所有節點上。
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* 建立顯示 hello 叢集中的每個數字 1 到 10 的每個 Linux 節點上一秒的殼層指令碼執行，然後立即顯示輸出來源 hello 節點。
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> 您可能需要 toouse 某些逸出字元**clusrun**命令。 此範例所示，使用 ^ 在命令提示字元 tooescape hello">"符號。
> 
> 

## <a name="next-steps"></a>後續步驟
* 請嘗試向上擴充 hello 叢集 tooa 較大節點數目，或在 hello 叢集上執行 Linux 的工作負載。 如需範例，請參閱 [在 Azure 中的 Linux 計算節點以 Microsoft HPC Pack 執行 NAMD](hpcpack-cluster-namd.md)。
* 再試一次與叢集[具備 RDMA 功能，需要大量計算 Vm](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI 工作負載。 如需範例，請參閱 [在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFOAM](hpcpack-cluster-openfoam.md)。
* 如果您有興趣使用 Linux 在內部部署 HPC Pack 叢集中的節點，請參閱 hello [TechNet 指引](https://technet.microsoft.com/library/mt595803.aspx)。

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
