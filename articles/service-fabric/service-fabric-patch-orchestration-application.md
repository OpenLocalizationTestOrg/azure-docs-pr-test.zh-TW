---
title: "aaaAzure Service Fabric 修補程式的協調流程的應用程式 |Microsoft 文件"
description: "應用程式 tooautomate 作業系統修補 Service Fabric 叢集上的系統。"
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a>修補程式 hello Service Fabric 叢集中的 Windows 作業系統

hello 修補程式的協調流程是 Azure Service Fabric 應用程式可自動化 azure Service Fabric 叢集，而不需要停機修補的作業系統。

hello 修補程式的協調流程的應用程式提供 hello 下列：

- **自動化的作業系統更新安裝**。 會自動下載並安裝作業系統更新。 會視需要重新啟動叢集節點，而不需要叢集停機。

- **叢集感知的修補和健康情況整合**。 同時套用更新，hello 修補程式的協調流程的應用程式會監視 hello hello 叢集節點健全狀況。 叢集節點一次只能升級一個節點，或一次升級一個網域。 如果因為 toohello 修補程序關閉 hello hello 叢集健全狀況，修補是停止的 tooprevent aggravating hello 問題。

## <a name="internal-details-of-hello-app"></a>內部的 hello 應用程式的詳細資料

hello 修補程式的協調流程的應用程式包含下列子元件的 hello:

- **協調器服務**︰是具狀態服務，負責：
    - Hello 整個叢集上協調 Windows Update 作業 hello。
    - 儲存已完成的 Windows 更新作業的 hello 結果。
- **節點代理程式服務**︰是無狀態服務，在所有 Service Fabric 叢集節點上執行。 hello 服務負責：
    - 啟動載入 hello 節點代理程式 NTService。
    - 監視 hello 節點代理程式 NTService。
- **節點代理程式 NTService**：在較高層級權限 (系統) 執行的 Windows NT 服務。 相反地，hello 節點代理程式服務，在 hello 協調器服務執行的較低層級權限 （網路服務）。 hello 服務負責執行下列所有 hello 叢集節點上的 Windows Update 作業 hello:
    - 停用自動 hello 節點上的 Windows Update。
    - 根據 toohello 原則 hello 使用者提供下載和安裝 Windows Update。
    - 重新啟動 hello 機器 post Windows Update 安裝。
    - 正在上傳 Windows 更新 toohello 協調器服務的 hello 的結果。
    - 萬一耗盡所有重試之後作業還是失敗，就報告健康情況報告。

> [!NOTE]
> hello 修補程式的協調流程的應用程式會使用 hello Service Fabric 修復管理員系統服務 toodisable 或啟用 hello 節點，執行健全狀況檢查。 hello 修補程式的協調流程應用程式追蹤 hello Windows Update 進行每個節點所建立的 hello 修復工作。

## <a name="prerequisites"></a>必要條件

### <a name="minimum-supported-service-fabric-runtime-version"></a>支援的最低 Service Fabric 執行階段版本

#### <a name="azure-clusters"></a>Azure 叢集
hello 修補程式的協調流程的應用程式必須具有 Service Fabric 執行階段版本 v5.5 的 Azure 叢集上執行或更新版本。

#### <a name="standalone-on-premises-clusters"></a>獨立的內部部署叢集
hello 修補程式的協調流程的應用程式必須具有 Service Fabric 執行階段版本 v5.6 獨立式叢集上執行或更新版本。

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a>啟用 hello 修復管理員服務 （如果它不已執行）

hello 修補程式的協調流程的應用程式需要 hello 修復管理員系統服務 toobe hello 叢集上啟用。

#### <a name="azure-clusters"></a>Azure 叢集

Hello 銀級持久性層中的 azure 叢集都有 hello 修復管理員服務預設會啟用。 Hello 金級持久性層中的 azure 叢集可能會或可能沒有啟用，根據這些叢集建立時的 hello 修復管理員服務。 在 hello 銅持久性層中，依預設，azure 的叢集沒有 hello 修復管理員服務已啟用。 如果已啟用 hello 服務，您可以看到在 hello Service Fabric 總管 hello 系統服務 區段中執行它。

##### <a name="azure-portal"></a>Azure 入口網站
您可以設定叢集的 hello 次啟用修復管理員從 Azure 入口網站。 選取`Include Repair Manager`選項在`Add on features`在叢集組態的 hello 階段。
![從 Azure 入口網站啟用修復管理員的映像](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Azure Resource Manager 範本
或者，您可以使用 hello [Azure Resource Manager 範本](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm)tooenable hello 修復管理員服務在新的和現有的 Service Fabric 叢集上。 您想 toodeploy hello 叢集取得 hello 範本。 您可以使用 hello 範例範本，或建立自訂的資源管理員範本。 

tooenable hello 修復管理員服務使用[Azure Resource Manager 範本](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. 先檢查該 hello`apiversion`設定得`2017-07-01-preview`hello`Microsoft.ServiceFabric/clusters`資源，如下列程式碼片段的 hello 中所示。 如果不同，則您需要 tooupdate hello `apiVersion` toohello 值`2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. 現在加入 hello 下列啟用 hello 修復管理員服務`addonFeatures`後面 hello 區段`fabricSettings`> 一節：

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. 您已更新您叢集的範本，這些變更之後，套用它們，並讓 hello 升級完成。 您現在可以看到您的叢集中執行 hello 修復管理員系統服務。 它會呼叫`fabric:/System/RepairManagerService`hello Service Fabric 總管在 hello 系統服務 區段中。 

### <a name="standalone-on-premises-clusters"></a>獨立的內部部署叢集

您可以使用 hello[獨立 Windows 叢集的組態設定](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest)tooenable hello 修復管理員服務在新的和現有的 Service Fabric 叢集上。

tooenable hello 修復管理員服務：

1. 先檢查該 hello`apiversion`中[一般的叢集設定](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations)設定得`04-2017`或更高版本：

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. 現在加入 hello 下列啟用修復管理員服務`addonFeaturres`後面 hello 區段`fabricSettings`區段如下所示：

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. 更新您的叢集資訊清單，這些變更，使用更新的 hello 叢集資訊清單[建立新的叢集](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server)或[升級 hello 叢集設定](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration)。 一旦 hello 叢集正在執行以更新的叢集資訊清單中，您現在可以看到執行中叢集，也就所謂的 hello 修復管理員系統服務`fabric:/System/RepairManagerService`下系統服務在 hello Service Fabric 總管 中的區段。

### <a name="disable-automatic-windows-update-on-all-nodes"></a>停用所有節點上的自動 Windows Update

Windows update 自動更新可能會導致 tooavailability 遺失，因為多個叢集節點可以重新啟動 hello 相同的時間。 hello 修補程式的協調流程的應用程式，根據預設，會嘗試 toodisable hello 自動的 Windows Update，每個叢集節點上。 不過，如果 hello 設定由系統管理員 」 或 「 群組原則管理，我們建議設定 hello 原則太"之前通知使用者下載 「 明確的 Windows Update。

### <a name="optional-enable-azure-diagnostics"></a>選擇性：啟用 Azure 診斷

執行 Service Fabric 執行階段版本 `5.6.220.9494` 和以上版本的叢集，會收集修補程式協調流程應用程式記錄作為 Service Fabric 記錄的一部分。
如果您的叢集是在 Service Fabric 執行階段 `5.6.220.9494` 版和以上版本執行，您可以略過此步驟。

叢集執行 Service Fabric 執行階段版本小於`5.6.220.9494`，記錄檔中的 hello 修補程式的協調流程的應用程式會在本機收集每個 hello 叢集節點上。
我們建議您設定 Azure 診斷 tooupload 記錄檔，從所有節點 tooa 中央位置。

如需啟用 Azure 診斷的詳細資訊，請參閱[使用 Azure 診斷收集記錄](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad)。

下列固定的提供者識別碼 hello 上產生記錄檔中的 hello 修補程式的協調流程的應用程式：

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

在資源管理員範本 goto`EtwEventSourceProviderConfiguration`區段`WadCfg`並加入下列項目 hello:

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> 如果您的 Service Fabric 叢集具有多個節點型別，則必須為所有 hello 新增 hello 上一節`WadCfg`區段。

## <a name="download-hello-app-package"></a>下載 hello 應用程式套件

下載 hello 應用程式從 hello[下載連結](https://go.microsoft.com/fwlink/P/?linkid=849590)。

## <a name="configure-hello-app"></a>Hello 應用程式設定

hello hello 修補程式的協調流程的應用程式的行為可以是您的需求設定的 toomeet。 在應用程式的建立或更新期間傳入 hello 應用程式參數來覆寫 hello 預設值。 可以藉由指定提供應用程式參數`ApplicationParameter`toohello`Start-ServiceFabricApplicationUpgrade`或`New-ServiceFabricApplication`cmdlet。

|**參數**        |**類型**                          | **詳細資料**|
|:-|-|-|
|MaxResultsToCache    |long                              | Windows Update 結果的最大數目，應加以快取。 <br>預設值為 3000，是基於以下假設： <br> - 節點數目 20。 <br> - 每個月在節點上發生的更新數目為 5。 <br> - 每個作業的結果數目可為 10。 <br> 要儲存結果的 hello 過去三個月。 |
|TaskApprovalPolicy   |例舉 <br> { NodeWise, UpgradeDomainWise }                          |TaskApprovalPolicy 指出是 toobe hello Service Fabric 叢集節點之間 hello 協調器服務 tooinstall Windows 更新所使用的 hello 原則。<br>                         允許的值包括： <br>                                                           <b>NodeWise</b>。 一次只會在一個節點上安裝 Windows Update。 <br>                                                           <b>UpgradeDomainWise</b>。 一次只會在一個升級網域上安裝 Windows Update。 （在最大的 hello，所有屬於 tooan 升級網域的 hello 節點可以移 Windows update）。
|LogsDiskQuotaInMB   |long  <br> (預設值︰1024)               |修補程式協調流程應用程式記錄的大小上限 (以 MB 為單位)，可在節點上本機保留。
| WUQuery               | 字串<br>(預設值："IsInstalled=0")                | 查詢 tooget Windows 更新。 如需詳細資訊，請參閱 [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)。
| InstallWindowsOSOnlyUpdates | Bool <br> (預設值︰True)                 | 這個旗標可讓 Windows 作業系統安裝的系統更新 toobe。            |
| WUOperationTimeOutInMinutes | int <br>(預設值︰90)                   | 指定 hello （搜尋或下載或安裝） 的任何 Windows Update 作業的逾時。 如果 hello 操作未完成內 hello 指定的逾時，它就會中止。       |
| WURescheduleCount     | int <br> (預設值︰5)                  | hello 最大次數 hello 服務會重新排定 hello Windows update，如果操作持續失敗的作業。          |
| WURescheduleTimeInMinutes | int <br>(預設值︰30) | hello 間隔在哪一個 hello 服務會重新排定 hello Windows update，如果失敗持續發生。 |
| WUFrequency           | 以逗號分隔的字串 (預設值︰"Weekly, Wednesday, 7:00:00")     | 安裝 Windows 更新的 hello 頻率。 hello 格式和可能的值如下： <br>-   Monthly, DD,HH:MM:SS，例如 Monthly, 5,12:22:32。 <br> -   Weekly, DAY,HH:MM:SS，例如 Weekly, Tuesday, 12:22:32。  <br> -   Daily, HH:MM:SS，例如 Daily, 12:22:32。  <br> -  None 表示不應該進行 Windows Update。  <br><br> 請注意，所有的 hello 時間-utc 時區。|
| AcceptWindowsUpdateEula | Bool <br>(預設值︰true) | 藉由設定這個旗標，hello 應用程式會接受 hello 使用者授權合約的 Windows Update 代表 hello 的 hello 機器的擁有者。              |

> [!TIP]
> 如果您想要 Windows Update toohappen 立即，設定`WUFrequency`相對 toohello 應用程式部署時間。 例如，假設您有五個節點測試叢集和計劃 toodeploy hello 應用程式，在大約 5:00 PM UTC。 如果您假設 hello 應用程式升級或部署會在 30 分鐘 hello 最大值、 設定 hello WUFrequency 為 「 每日、 17:30:00。 」

## <a name="deploy-hello-app"></a>部署 hello 應用程式

1. 完成所有 hello 先決條件步驟 tooprepare hello 叢集。
2. 部署 hello 修補程式的協調流程應用程式，例如其他 Service Fabric 應用程式。 您可以使用 PowerShell 來部署 hello 應用程式。 中的 hello 步驟[使用 PowerShell 部署和移除應用程式](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)。
3. tooconfigure hello 應用程式的部署，傳遞 hello hello 次`ApplicationParamater`toohello `New-ServiceFabricApplication` cmdlet。 為了方便起見，我們提供了 hello 指令碼 Deploy.ps1 以及 hello 應用程式。 toouse hello 指令碼：

    - 藉由連線 tooa Service Fabric 叢集`Connect-ServiceFabricCluster`。
    - 執行含有適當 hello hello PowerShell 指令碼 Deploy.ps1`ApplicationParameter`值。

> [!NOTE]
> Hello 中保留 hello 指令碼與 hello 應用程式資料夾 PatchOrchestrationApplication 相同的目錄。

## <a name="upgrade-hello-app"></a>升級 hello 應用程式

tooupgrade 現有修補程式的協調流程應用程式使用 PowerShell，請依照下列中的 hello 步驟[使用 PowerShell 的 Service Fabric 應用程式升級](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell)。

## <a name="remove-hello-app"></a>移除 hello 應用程式

tooremove hello 應用程式，在後續的 hello 步驟[使用 PowerShell 部署和移除應用程式](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications)。

為了方便起見，我們提供了 hello 指令碼 Undeploy.ps1 以及 hello 應用程式。 toouse hello 指令碼：

  - 藉由連線 tooa Service Fabric 叢集```Connect-ServiceFabricCluster```。

  - 執行 PowerShell 指令碼 Undeploy.ps1 hello。

> [!NOTE]
> Hello 中保留 hello 指令碼與 hello 應用程式資料夾 PatchOrchestrationApplication 相同的目錄。

## <a name="view-hello-windows-update-results"></a>檢視 hello Windows Update 結果

hello 修補程式的協調流程的應用程式會公開 REST Api toodisplay hello 歷程記錄結果 toohello 使用者。 Hello 結果 JSON 的範例：
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
如果沒有更新尚未排程，hello 結果 JSON 是空的。

登入 toohello 叢集 tooquery Windows Update 的結果。 找出 hello 主要的 hello 協調器服務的 hello 複本位址，然後叫用 hello 瀏覽器中的 hello URL: http://&lt;複本 IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 /GetWindowsUpdateResults。

hello hello 協調器服務的 REST 端點都有的動態連接埠。 toocheck hello 正確 URL，請參閱 toohello Service Fabric 總管。 比方說，hello 結果位於`http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`。

![REST 端點的圖片](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


如果 hello 反向 proxy 已啟用 hello 叢集上，您可以存取外部 hello 叢集中的 hello URL。
hello 端點需要 toobe 叫用次數是 http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults。

tooenable hello 反向 proxy hello 在叢集上，請依照下列中的 hello 步驟[反向 proxy，在 Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)。 

> 
> [!WARNING]
> Hello 反向 proxy 設定之後，所有微 hello 叢集中公開服務的 HTTP 端點都可以從 hello 叢集外定址。

## <a name="diagnosticshealth-events"></a>診斷/健康情況事件

### <a name="collect-patch-orchestration-app-logs"></a>收集修補程式協調流程應用程式記錄

收集修補程式協調流程應用程式的記錄，是執行階段版本 `5.6.220.9494` 及以上版本作為 Service Fabric 記錄的一部分。
叢集執行 Service Fabric 執行階段版本小於`5.6.220.9494`，可以使用其中一種 hello 遵循方法收集記錄檔。

#### <a name="locally-on-each-node"></a>本機的每個節點上

如果 Service Fabric 執行階段版本小於 `5.6.220.9494`，則只會在每個 Service Fabric 叢集節點的本機收集記錄。 hello 位置 tooaccess hello 記錄檔也\[Service Fabric\_安裝\_磁碟機\]:\\PatchOrchestrationApplication\\記錄檔。

例如，如果 Service Fabric 安裝磁碟機 D 上，hello 路徑是 d:\\PatchOrchestrationApplication\\記錄檔。

#### <a name="central-location"></a>中央位置

Azure 診斷設定先決條件步驟時，記錄檔中的 hello 修補程式的協調流程的應用程式可以使用 Azure 儲存體中。

### <a name="health-reports"></a>健康狀態報告

hello 修補程式的協調流程的應用程式也會將針對 hello 協調器服務或 hello 節點代理程式服務的健康情況報告發佈在下列情況下的 hello:

#### <a name="a-windows-update-operation-failed"></a>Windows Update 作業失敗

如果 Windows 更新作業失敗的節點上，健全狀況報表會產生針對 hello 節點代理程式服務。 Hello 健全狀況報表的詳細資料包含 hello 有問題的節點名稱。

修補 hello 有問題的節點上順利完成之後，就會自動清除 hello 報表。

#### <a name="hello-node-agent-ntservice-is-down"></a>hello 節點代理程式 NTService 已關閉

如果 hello 節點代理程式 NTService 已關閉節點上，警告層級的健全狀況報表會產生針對 hello 節點代理程式服務。

#### <a name="hello-repair-manager-service-is-not-enabled"></a>未啟用 hello 修復管理員服務

如果 hello 叢集上找不到 hello 修復管理員服務，hello 協調器服務會產生警告層級的健全狀況報表。

## <a name="frequently-asked-questions"></a>常見問題集

問： **為什麼 hello 修補程式的協調流程的應用程式執行時看到我的叢集處於錯誤狀態？**

A. 在 hello 安裝過程中，hello 修補程式的協調流程的應用程式會停用或重新啟動節點，這可能會暫時導致停機的 hello 叢集 hello 健全狀況。

根據 hello 應用程式的 hello 原則，可能是一個節點可以向下修補作業期間*或*可以同時向下整個升級網域。

Windows Update 安裝 hello hello 結束，重新啟動後的 hello 節點會重新啟用。

在下列範例的 hello，hello 叢集發生 tooan 錯誤狀態暫時因為兩個節點已關閉，而且 hello MaxPercentageUnhealthNodes 原則違反了。 hello 錯誤是暫時性的直到 hello 修補作業正在進行中。

![健康情況不良之叢集的圖片](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

如果 hello 問題持續發生，請參閱 toohello 疑難排解 > 一節。

問： **修補程式協調流程應用程式處於警告狀態**

A. 請檢查 toosee，如果公佈針對 hello 應用程式的健康情況報告 hello 根本原因。 通常，hello 警告包含 hello 問題的詳細的資料。 如果 hello 問題是暫時性的會在這個狀態中的預期的 tooauto 復原 hello 應用程式。

問： **如果我的叢集狀況不良，我需要 toodo 緊急作業系統更新，我可以做什麼？**

A. hello 修補程式的協調流程的應用程式不會安裝更新時 hello 叢集狀況不良。 請嘗試 toobring 您叢集 tooa 狀況良好狀態 toounblock hello 修補程式的協調流程的應用程式的工作流程。

問： **為什麼沒有修補在叢集中這麼久 toorun？**

A. hello hello 修補程式的協調流程的應用程式所需的時間主要是取決於下列因素的 hello:

- hello 原則 hello 協調器服務。 
  - hello 預設原則`NodeWise`，導致修補一次只有一個節點。 特別是在較大叢集的 hello 案例中，我們建議您使用 hello`UpgradeDomainWise`原則 tooachieve 更快的修補程式的多個叢集。
- hello 可供下載和安裝的更新數目。 
- hello toodownload 所需的平均時間，並安裝更新，不應超過幾個小時。
- hello hello VM 的效能和網路頻寬。

問： **為什麼看到某些更新 Windows Update 取得透過 REST api 的而非在 hello 機器上的 Windows Update 歷程記錄的結果中？**

A. 某些產品更新需要 toobe 簽入其各自的更新/修補歷程記錄。 例如：Windows Defender 更新不會顯示在 Windows Server 2016 上的 Windows Update 歷程記錄。

## <a name="disclaimers"></a>免責聲明

- hello 修補程式的協調流程的應用程式接受代表 hello 使用者 hello 使用者授權合約的 Windows Update。 （選擇性） hello 設定可以關閉 hello hello 應用程式組態中。

- hello 修補程式的協調流程的應用程式會收集遙測 tootrack 使用量和效能。 hello 應用程式的遙測遵循 hello 設定 hello Service Fabric 執行階段的遙測設定 （預設為開啟）。

## <a name="troubleshooting"></a>疑難排解

### <a name="a-node-is-not-coming-back-tooup-state"></a>節點不返回 tooup 狀態

**hello 節點可能會卡在停用狀態，因為**:

安全性檢查擱置。 tooremedy 這種情況下，確保足夠的節點，可在狀況良好的狀態。

**hello 節點可能會卡在停用狀態，因為**:

- hello 節點已手動停用。
- hello 節點已停用，因為 tooan 持續的 Azure 基礎結構工作。
- hello 節點已由 hello 修補程式的協調流程的應用程式 toopatch hello 節點暫時停用。

**hello 節點可能會卡在關閉的狀態因為**:

- hello 節點以手動方式放入關閉狀態。
- hello 節點正在進行重新啟動 （這可能會觸發 hello 修補程式的協調流程的應用程式）。
- hello 節點已關閉到期 tooa 故障 VM 或電腦或網路連線問題。

### <a name="updates-were-skipped-on-some-nodes"></a>已略過某些節點上的更新

hello 修補程式的協調流程的應用程式會嘗試 tooinstall Windows update 相應 toohello 方法是重新排定原則。 hello 服務嘗試 toorecover hello 節點，並略過 hello 更新相應 toohello 應用程式原則。

在這種情況下，會產生針對 hello 節點代理程式服務的警告層級的健全狀況報表。 Windows Update 的 hello 結果也會包含 hello 的 hello 失敗的可能原因。

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a>hello hello 叢集健全狀況 hello 更新安裝時，會 tooerror

錯誤的 Windows update 可以關閉應用程式或叢集上的特定節點或升級網域的 hello 健全狀況。 hello 修補程式的協調流程的應用程式會停止任何後續的 Windows 更新作業，直到 hello 叢集恢復狀況良好。

系統管理員必須介入，並判斷為什麼 hello 應用程式或叢集變成狀況不良的原因 tooWindows 更新。

## <a name="release-notes-"></a>版本資訊：

### <a name="version-110"></a>1.1.0 版
- 公開版本

### <a name="version-111"></a>1.1.1 版
- 修正 SetupEntryPoint of NodeAgentService 中的錯誤，該錯誤導致無法安裝 NodeAgentNTService。

### <a name="version-120-latest"></a>1.2.0 版 (最新)

- 關於系統重新啟動工作流程的錯誤修正。
- 如預期般，未發生 RM 工作因為 toowhich 健全狀況檢查期間準備修復工作建立的 bug 修正。
- 從 自動 toodelayed 自動的 windows 服務 POANodeSvc 變更的 hello 啟動模式。
