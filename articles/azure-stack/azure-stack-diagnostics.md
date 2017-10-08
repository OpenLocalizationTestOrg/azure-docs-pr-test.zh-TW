---
title: "在 Azure 堆疊 aaaDiagnostics |Microsoft 文件"
description: "Toocollect 記錄檔以 Azure 堆疊中的診斷資訊的方式"
services: azure-stack
documentationcenter: 
author: adshar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: adshar
ms.openlocfilehash: a4a5ddf29e75df710e9fae366d6ac16e6fb36d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-diagnostics-tools"></a>Azure Stack 診斷工具
 
Azure Stack 是元件共同作業並與彼此互動的大型集合。 所有這些元件都將會產生自己的唯一記錄，這表示診斷問題將很快就成為極富挑戰性的工作，尤其是針對來自多個互動的 Azure Stack 元件的錯誤。 

我們的診斷工具協助確定 hello 記錄機制進行簡單而有效。 hello 圖說明如何記錄收集工具在 Azure 堆疊工作：

![記錄收集工具](media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a>追蹤收集器
 
預設會啟用 hello 追蹤收集器。 它持續 hello 背景中執行 Azure 堆疊上，從 元件服務收集所有事件追蹤的 Windows (ETW) 記錄檔並將它們儲存在一般的本機共用上。 

hello 下面是有關 hello 追蹤收集器的重要事項 tooknow:
 
* hello 追蹤收集器會持續執行預設的大小限制。 hello 預設允許的大小上限 (200 MB) 的每個檔案是**不**截止大小。 大小檢查會定期發生 （目前每隔 10 分鐘），而且如果 hello 目前的檔案是 > = 200 MB 時，它會儲存並產生新的檔案。 Hello 檔案大小總計產生每個事件工作階段上也沒有為 8 GB （設定） 的限制。 一旦達到此限制時，建立新的時，會刪除 hello 最舊的檔案。
* Hello 記錄檔沒有 5 天的天數。 此限制也可設定。 
* 每個元件會定義 hello 追蹤組態屬性，透過 JSON 檔案。 hello JSON 檔案儲存在`C:\TraceCollector\Configuration`。 如果有需要，這些檔案都可以編輯 toochange hello 存在時間和大小限制的 hello 收集記錄檔。 變更 toothese 檔案需要重新啟動 hello *Microsoft Azure 堆疊追蹤收集器*hello 的服務變更 tootake 效果。
* hello 下列範例是追蹤組態 JSON 檔 FabricRingServices 作業從 hello XRP VM: 

```
{
    "LogFile": 
    {
        "SessionName": "FabricRingServicesOperationsLogSession",
        "FileName": "\\\\SU1FileServer\\SU1_ManagementLibrary_1\\Diagnostics\\FabricRingServices\\Operations\\AzureStack.Common.Infrastructure.Operations.etl",
        "RollTimeStamp": "00:00:00",
        "MaxDaysOfFiles": "5",
        "MaxSizeInMB": "200",
        "TotalSizeInMB": "5120"
    },
    "EventSources":
    [
        {"Name": "Microsoft-AzureStack-Common-Infrastructure-ResourceManager" },
        {"Name": "Microsoft-OperationManager-EventSource" },
        {"Name": "Microsoft-Operation-EventSource" }
    ]
}
```

* **MaxDaysOfFiles**

    此參數控制 hello 檔案 tookeep 存留期。 較舊的記錄檔將會受到刪除。
* **MaxSizeInMB**

    此參數控制 hello 大小閾值，單一檔案。 如果達到 hello 大小，則會建立新的.etl 檔案。
* **TotalSizeInMB**

    此參數控制 hello 從事件工作階段產生的 hello.etl 檔案的大小總計。 如果 hello 檔案總大小大於此參數值，則會刪除較舊的檔案。
  
## <a name="log-collection-tool"></a>記錄收集工具
 
hello PowerShell 命令`Get-AzureStackLog`可以是從所有 Azure 堆疊環境中的 hello 元件使用的 toocollect 記錄檔。 其會將它們以 ZIP 檔案儲存在使用者定義的位置。 如果我們的技術支援小組需要記錄檔 toohelp 疑難排解問題，可能會要求 toorun 這項工具。

> [!CAUTION]
> 這些記錄檔可能包含個人識別資訊 (PII)。 在您公開公佈任何記錄檔之前，請先將這點納入考量。
 
目前，我們會收集下列記錄類型的 hello:
*   **Azure Stack 部署記錄**
*   **Windows 事件記錄**
*   **Panther 記錄**

     tootroubleshoot VM 建立問題。
*   **叢集記錄**
*   **儲存體診斷記錄**
*   **ETW 記錄**

    這些是 hello 追蹤收集器所收集而且儲存在共用從哪裡`Get-AzureStackLog`擷取它們。
 
tooidentify 所有 hello 取得從所有的 hello 元件收集的記錄檔，請參閱 toohello`<Logs>`位於 hello 客戶設定檔中的標記`C:\EceStore\<Guid>\<GuidWithMaxFileSize>`。
 
### <a name="toorun-get-azurestacklog"></a>toorun Get AzureStackLog
1.  以登入 AzureStack\AzureStackAdmin hello 主機上。
2.  以系統管理員身分開啟 PowerShell 視窗。
3.  執行 `Get-AzureStackLog`。  

    **範例**

    - 為所有角色收集所有記錄：

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs`

    - 從 VirtualMachines 與 BareMetal 角色收集記錄：

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - 收集記錄檔篩選記錄檔以取得 hello 過去 8 小時的日期與 VirtualMachines 和 BareMetal 角色：

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

如果 hello`FromDate`和`ToDate`如果未指定參數、 記錄檔預設會收集 hello 過去 4 小時。

目前，您可以使用 hello`FilterByRole`參數 toofilter 記錄檔集合，由下列角色的 hello:

|   |   |   |
| - | - | - |
| `ACSMigrationService`     | `ACSMonitoringService`   | `ACSSettingsService` |
| `ACS`                     | `ACSFabric`              | `ACSFrontEnd`        |
| `ACSTableMaster`          | `ACSTableServer`         | `ACSWac`             |
| `ADFS`                    | `ASAppGateway`           | `BareMetal`          |
| `BRP`                     | `CA`                     | `CPI`                |
| `CRP`                     | `DeploymentMachine`      | `DHCP`               |
|`Domain`                   | `ECE`                    | `ECESeedRing`        |        
| `FabricRing`              | `FabricRingServices`     | `FRP`                |
|` Gateway`                 | `HealthMonitoring`       | `HRP`                |               
| `IBC`                     | `InfraServiceController` | `KeyVaultAdminResourceProvider`|
| `KeyVaultControlPlane`    | `KeyVaultDataPlane`      | `NC`                 |            
| `NonPrivilegedAppGateway` | `NRP`                    | `SeedRing`           |
| `SeedRingServices`        | `SLB`                    | `SQL`                |     
| `SRP`                     | `Storage`                | `StorageController`  |
| `URP`                     | `UsageBridge`            | `VirtualMachines`    |  
| `WAS`                     | `WASPUBLIC`              | `WDS`                |


幾件事 toonote:

* 此命令將會需要一些時間來收集記錄，視乎將收集哪些角色記錄。 促成因素包括 hello 指定記錄檔集合與 hello hello Azure 堆疊環境中的節點數目的持續時間。
* 記錄檔收集完成之後，請檢查 hello hello 中建立的新資料夾`-OutputPath`hello 命令中指定的參數。
* 呼叫檔案`Get-AzureStackLog_Output.log`hello 包含 hello zip 檔案的資料夾中建立並包含 hello 命令輸出中，可以用於疑難排解記錄檔集合中的任何失敗。
* 每個角色在個別 ZIP 檔案皆有其記錄。 
* tooinvestigate 特定錯誤，記錄檔可能需要從多個元件。
    -   系統和基礎結構的所有 vm 的事件記錄檔會收集在 hello *VirtualMachines*角色。
    -   系統和所有主機的事件記錄檔會收集在 hello *BareMetal*角色。
    -   容錯移轉叢集和 HYPER-V 事件記錄檔會收集在 hello*儲存體*角色。
    -   ACS 的記錄檔會收集在 hello*儲存體*和*ACS*角色。
* 如需詳細資訊，您可以參考 toohello 客戶設定檔。 調查 hello `<Logs>` hello 不同角色的標記。

> [!NOTE]
> 我們會強制執行大小和存在時間限制，所以您確定不會取得大量湧入記錄檔的儲存體空間 toomake 基本 tooensure 有效率地利用所收集的 toohello 記錄檔。 強調的是，當診斷的問題，您通常需要記錄檔，可能不存在 toothese 限制強制執行到期。 因此，**強烈建議**您卸載記錄 tooan 外部儲存空間 （在公用 Azure 儲存體帳戶、 內部額外存放裝置等等） 來 too12 每 8 小時，讓它們那里取決於 1-3 個月您的需求。


## <a name="next-steps"></a>後續步驟
[Microsoft Azure Stack 疑難排解](azure-stack-troubleshooting.md)
