---
title: "aaaAutoscale HPC Pack 叢集節點 |Microsoft 文件"
description: "自動擴增和縮減 HPC Pack 叢集計算節點，在 Azure 中的 hello 數目"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>自動擴增和縮減 Azure 根據 toohello 叢集工作負載中的 hello HPC Pack 叢集資源
如果您在 HPC Pack 叢集中部署 Azure 「 高載 」 節點，或您建立 Azure Vm 中的 HPC Pack 叢集，您可以自動成長或壓縮 hello 叢集資源，例如節點或核心根據 hello hello 叢集上的工作負載的方式。 以這種方式調整 hello 叢集資源可讓您 toouse 您的 Azure 資源更有效率地並控制其成本。

本文將說明 HPC Pack 提供 tooautoscale 計算資源的兩種方式：

* hello HPC Pack 叢集屬性**AutoGrowShrink**

* hello **AzureAutoGrowShrink.ps1** HPC PowerShell 指令碼

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

目前您只能自動擴增和縮減正在執行 Windows Server 作業系統的 HPC Pack 計算節點。


## <a name="set-hello-autogrowshrink-cluster-property"></a>設定 hello AutoGrowShrink 叢集屬性
### <a name="prerequisites"></a>必要條件

* **HPC Pack 2012 R2 更新 2 或更新版本的叢集**-hello 叢集前端節點可以是部署在內部或 Azure VM 中。 請參閱[設定混合式叢集使用 HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget 啟動內部部署前端節點與 Azure 「 高載 」 節點。 請參閱 hello [HPC Pack IaaS 部署指令碼](hpcpack-cluster-powershell-script.md)tooquickly HPC Pack 叢集部署在 Azure Vm。

* **針對在 Azure (Resource Manager 部署模型) 中具有前端節點的叢集** - 從 HPC Pack 2016 開始，Azure Active Directory 應用程式中的憑證驗證會用於自動增加或縮減利用 Azure Resource Manager 部署的叢集 VM。 設定憑證，如下所示︰

  1. 叢集部署之後，連線的遠端桌面 tooone 前端節點。

  2. 上傳 hello 憑證 （具有私密金鑰的 PFX 格式） tooeach 前端節點，並安裝 tooCert:\LocalMachine\My 和 Cert: \LocalMachine\Root。

  3. 系統管理員身分啟動 Azure PowerShell，然後執行下列命令，其中一個前端節點上的 hello:

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    如果您的帳戶是在多個 Azure Active Directory 租用戶或 Azure 訂用帳戶，您可以執行下列 hello 命令 tooselect hello 正確租用戶和訂用帳戶：
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    執行下列命令 tooview hello hello 目前已選取租用戶和訂用帳戶：
    
    ```powershell
        Get-AzureRMContext
    ```

  4. 執行下列指令碼的 hello

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    其中

    **DisplayName** - Azure Active 應用程式顯示名稱。 如果 hello 應用程式不存在，它會建立 Azure Active Directory 中。

    **首頁**-hello hello 應用程式的首頁。 您可以設定空的 URL，如 hello 前面範例所示。

    **IdentifierUri** -hello 應用程式識別項。 您可以設定空的 URL，如 hello 前面範例所示。

    **CertificateThumbprint** -您在步驟 1 中的 hello 前端節點安裝的 hello 憑證的指紋。

    **TenantId** - Azure Active Directory 的租用戶識別碼。 您可以從 hello Azure Active Directory 入口網站取得租用戶識別碼 hello**屬性**頁面。

    如需 **ConfigARMAutoGrowShrinkCert.ps1** 的詳細資訊，請執行 `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`。


* **針對在 Azure （傳統部署模型） 中的前端節點的叢集**-如果您使用 hello HPC Pack IaaS 部署指令碼 toocreate hello 叢集在 hello 傳統部署模型中，啟用 hello **AutoGrowShrink**叢集藉由設定 hello 叢集組態檔中的 hello AutoGrowShrink 選項屬性。 如需詳細資訊，請參閱伴隨的 hello 的 hello 文件[指令碼下載](https://www.microsoft.com/download/details.aspx?id=44949)。

    或者，啟用 hello **AutoGrowShrink**叢集內容之後使用 HPC PowerShell 部署 hello 叢集命令 hello 之後 > 一節中所述。 這個 tooprepare，第一個完成的 hello 下列步驟：

  1. Hello 前端節點上，並在 hello Azure 訂用帳戶中設定 Azure 管理憑證。 針對測試部署，您可以使用 hello Microsoft 預設 HPC Azure 自我簽署的憑證，在 hello 前端節點上安裝 HPC Pack，並再上傳該憑證 tooyour Azure 訂用帳戶。 選項和步驟，請參閱 hello [TechNet 文件庫指引](https://technet.microsoft.com/library/gg481759.aspx)。

  2. 執行**regedit** hello 前端節點上，請移 tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo，並加入的字串值。 設定 hello 值名稱太 「 指紋 」，以及在步驟 1 中的 hello 憑證的值資料 toohello 指紋。

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>HPC PowerShell 命令 tooset hello AutoGrowShrink 屬性
以下是範例 HPC PowerShell 命令 tooset **AutoGrowShrink**和 tootune 其行為與其他參數。 請參閱[AutoGrowShrink 參數](#AutoGrowShrink-parameters)本文稍後的 hello 設定的完整清單。

toorun 這些命令時，系統管理員身分啟動 HPC PowerShell hello 叢集前端節點上。

**tooenable hello AutoGrowShrink 屬性**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**toodisable hello AutoGrowShrink 屬性**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**toochange hello 成長以分鐘為單位的間隔**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**toochange hello 壓縮以分鐘為單位的間隔**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**tooview hello 目前組態 AutoGrowShrink**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**從 AutoGrowShrink tooexclude 節點群組**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> 從 HPC Pack 2016 開始支援這個參數
>

### <a name="autogrowshrink-parameters"></a>AutoGrowShrink 參數
hello 如下 AutoGrowShrink 參數，您可以修改使用 hello**組 HpcClusterProperty**命令。

* **EnableGrowShrink** -切換 tooenable 或停用 hello **AutoGrowShrink**屬性。
* **ParamSweepTasksPerCore** -參數式整理數目工作 toogrow 一個核心。 hello 預設值為 toogrow 每項工作的其中一個核心。

  > [!NOTE]
  > HPC Pack QFE KB3134307 變更**ParamSweepTasksPerCore**太**TasksPerResourceUnit**。 它根據 hello 作業資源類型，而且可以是節點，通訊端或核心。
  >
  >
* **GrowThreshold** -佇列的工作 tootrigger 自動成長的臨界值。 hello 預設值為 1，這表示，如果有 1 或更多的工作，在 [hello 排入佇列的狀態、 自動成長] 節點。
* **GrowInterval** -分鐘 tootrigger 自動成長的時間間隔。 hello 預設間隔是 5 分鐘。
* **ShrinkInterval** -間隔分鐘 tootrigger 自動壓縮。 hello 預設間隔是 5 分鐘。 |
* **ShrinkIdleTimes** -連續檢查 tooshrink tooindicate hello 節點數目會處於閒置狀態。 hello 預設值為 3 次。 例如，如果 hello **ShrinkInterval**為 5 分鐘，HPC Pack 檢查 hello 節點是否為閒置每隔 5 分鐘。 如果 hello 節點在 hello 閒置狀態 3 連續檢查 （15 分鐘） 之後，HPC Pack 會縮小該節點。
* **ExtraNodesGrowRatio** -其他節點 toogrow 訊息傳遞介面 (MPI) 工作的百分比。 hello 預設值為 1，表示 HPC Pack 成長節點 MPI 工作的 1%。
* **GrowByMin** -切換 tooindicate 是否 hello 自動成長原則根據 hello hello 工作所需的最小資源。 hello 預設值為 false，這表示 HPC Pack 成長作業 hello hello 作業所需的最大資源為基礎的節點。
* **SoaJobGrowThreshold** -臨界值的連入 SOA 要求 tootrigger hello 自動成長的程序。 hello 預設值是 50000。

  > [!NOTE]
  > 從 HPC Pack 2012 R2 Update 3 開始支援這個參數。
  >
  >
* **SoaRequestsPerCore** -要求 toogrow 一個核心的連入 SOA 的數目。 hello 預設值為 20000。

  > [!NOTE]
  > 從 HPC Pack 2012 R2 Update 3 開始支援這個參數。
  >
* **ExcludeNodeGroups** – hello 中的節點指定節點群組不會自動擴增和縮減。
  
  > [!NOTE]
  > 從 HPC Pack 2016 開始支援這個參數。
  >

### <a name="mpi-example"></a>MPI 範例
根據預設 HPC Pack 成長 1%的 MPI 工作的額外節點 (**ExtraNodesGrowRatio**設定 too1)。 hello 的原因是 MPI 可能需要多個節點，而且當準備所有節點只能執行 hello 作業。 當 Azure 啟動節點時，有時一個節點可能需要更多時間 toostart 比其他造成閒置時等候該節點 tooget 準備其他節點 toobe。 藉由增加額外的節點，HPC Pack 會減少此資源的等候時間，並可能節省成本。 tooincrease hello 百分比的 MPI 工作 （例如，too10%） 的額外節點執行類似的命令

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>SOA 範例
根據預設， **SoaJobGrowThreshold**設定 too50000 和**SoaRequestsPerCore** too200000 設定。 如果您送出一個包含 70000 個要求的 SOA 作業，則會有一個排入佇列工作，且傳入要求為 70000。 在此情況下 HPC Pack 成長 1 個核心的 hello 排入佇列的工作，與針對內送要求，成長 (70000-50000) / 20000 = 1 核心，因此在總計成長 2 核心，此 SOA 工作。

## <a name="run-hello-azureautogrowshrinkps1-script"></a>執行 hello AzureAutoGrowShrink.ps1 指令碼
### <a name="prerequisites"></a>必要條件

* **HPC Pack 2012 R2 更新 1 或更新版本的叢集**-hello **AzureAutoGrowShrink.ps1** hello %ccp_home%bin 資料夾中安裝指令碼。 hello 叢集前端節點可以是部署在內部或 Azure VM 中。 請參閱[設定混合式叢集使用 HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget 啟動內部部署前端節點與 Azure 「 高載 」 節點。 請參閱 hello [HPC Pack IaaS 部署指令碼](hpcpack-cluster-powershell-script.md)tooquickly HPC Pack 叢集部署在 Azure Vm，或使用[Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/)。
* **Azure PowerShell 1.4.0** -hello 指令碼目前取決於這個特定版本的 Azure PowerShell。
* **針對 Azure 的叢集高載節點**-HPC Pack 已安裝用戶端電腦上或 hello 前端節點上執行 hello 指令碼。 如果用戶端電腦上執行，請確定您設定 hello 變數 $env: CCP_SCHEDULER toopoint toohello 前端節點。 hello Azure 「 高載 」 節點必須加入 toohello 叢集中，但它們也可能處於 hello 未部署 」 狀態。
* **叢集部署在 Azure Vm （Resource Manager 部署模型） 中的**-針對 Azure Vm 部署在 hello Resource Manager 部署模型中的叢集，hello 指令碼支援兩種方法進行 Azure 驗證： 登入 tooyour Azure 帳戶toorun hello 指令碼每次 (藉由執行`Login-AzureRmAccount`，或使用憑證設定服務主體的 tooauthenticate。 HPC Pack 提供 hello 指令碼**ConfigARMAutoGrowShrinkCert.ps** toocreate 憑證的服務主體。 hello 指令碼會建立 Azure Active Directory (Azure AD) 應用程式和服務主體，並指派 hello 參與者角色 toohello 服務主體。 toorun hello 指令碼，以系統管理員身分啟動 Azure PowerShell，然後執行下列命令的 hello:

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    如需 **ConfigARMAutoGrowShrinkCert.ps1** 的詳細資訊，請執行 `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`。

* **叢集部署 Azure 虛擬機器 （傳統部署模型） 中的**-hello 前端節點 VM 上執行 hello 指令碼，因為它相依於 hello **Start-hpciaasnode.ps1**和**Stop-hpciaasnode.ps1**所安裝的指令碼。 這些指令碼額外需要 Azure 管理憑證或發佈設定檔 (請參閱 [在 Azure 中的 HPC Pack 叢集管理計算節點](hpcpack-cluster-node-manage.md))。 請確定所有 hello 計算節點 Vm，您必須已加入 toohello 叢集。 它們也可能處於 hello 已停止 」 狀態。



### <a name="syntax"></a>語法
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>參數
* **NodeTemplates** -hello hello 節點 toogrow 範圍和壓縮的 hello 節點範本 toodefine 名稱。 如果未指定 (hello 預設值是 @ （)），hello 中的所有節點**AzureNodes**節點群組都會納入範圍時**NodeType** hello 中的值為 AzureNodes，以及所有節點**ComputeNodes**節點群組都會納入範圍時**NodeType**的值為 ComputeNodes。
* **Jobtemplate** -名稱 hello 作業 hello 節點 toogrow 範本 toodefine hello 範圍。
* **NodeType** -hello toogrow 節點的類型，並壓縮。 支援的值包括：

  * **AzureNodes** - 針對內部部署或 Azure IaaS 叢集中的 Azure PaaS (高載) 節點。
  * **ComputeNodes** - 針對只在 Azure IaaS 叢集的計算節點 VM。

* **NumOfQueuedJobsPerNodeToGrow** -所需的佇列工作數目 toogrow 一個節點。
* **NumOfQueuedJobsToGrowThreshold** -hello 臨界值數目的佇列的工作 toostart hello 成長程序。
* **NumOfActiveQueuedTasksPerNodeToGrow** -hello 作用中佇列工作數目所需 toogrow 一個節點。 如果 **NumOfQueuedJobsPerNodeToGrow** 指定了大於 0 的值，則會忽略這個參數。
* **NumOfActiveQueuedTasksToGrowThreshold** -hello 臨界值數目的作用中佇列的工作 toostart hello 成長程序。
* **NumOfInitialNodesToGrow** -hello 初始節點 toogrow 的最小數目，如果所有範圍中的 hello 節點**未部署**或**已停止 （取消配置）**。
* **GrowCheckIntervalMins** -hello 以分鐘為單位的間隔檢查 toogrow。
* **ShrinkCheckIntervalMins** -hello 以分鐘為單位的間隔檢查 tooshrink。
* **ShrinkCheckIdleTimes** -hello 數連續壓縮檢查 (隔開**ShrinkCheckIntervalMins**) tooindicate hello 節點處於閒置狀態。
* **UseLastConfigurations** -hello 先前 hello 引數檔案中儲存的組態。
* **ArgFile**-hello hello 引數使用的檔案 toosave 的名稱，並更新 hello 組態 toorun hello 指令碼。
* **LogFilePrefix** -hello hello 記錄檔的前置詞名稱。 您可以指定路徑。 根據預設 hello 記錄檔是寫入的 toohello 目前工作目錄。

### <a name="example-1"></a>範例 1
hello 下列範例會設定的 hello Azure 高載節點使用預設 AzureNode 範本 toogrow 部署和自動壓縮。 如果所有節點一開始都會處於 hello**未部署**狀態時，至少 3 個節點都都已啟動。 Hello 指令碼如果 hello 佇列工作數目超過 8 個，啟動節點，直到其數目超過佇列工作與 hello 比例**NumOfQueuedJobsPerNodeToGrow**。 如果發現節點 toobe 閒置 3 連續的閒置時間，會將它停止。

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>範例 2
hello 下列範例會設定的 hello Azure 計算節點 Vm 部署的 hello 預設 ComputeNode 範本 toogrow 和自動壓縮。
hello 預設工作範本所設定的 hello 作業定義的工作負載 hello 範圍 hello 叢集上。 如果一開始會停止所有 hello 節點，會啟動最少 5 個節點。 Hello 指令碼如果 hello 作用中佇列工作數目超過 15，啟動節點，直到其數目超過作用中佇列工作的 hello 比率太**NumOfActiveQueuedTasksPerNodeToGrow**。 如果發現節點 toobe 閒置 10 個連續的閒置時間，會將它停止。

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
