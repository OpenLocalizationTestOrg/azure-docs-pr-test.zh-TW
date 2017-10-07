---
title: "服務網狀架構事件彙總與 Windows Azure 診斷 aaaAzure |Microsoft 文件"
description: "了解如何使用 WAD 彙總及收集事件，來監視和診斷 Azure Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>使用 Windows Azure 診斷的事件彙總和收集
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

執行 Azure Service Fabric 叢集時，它是個不錯的主意 toocollect hello 記錄檔儲存在集中位置的所有 hello 節點。 在中央位置擁有 hello 記錄檔可協助您分析和疑難排解問題在叢集中或在 hello 應用程式和服務在該叢集中執行的問題。

其中一種方式 tooupload 及收集記錄檔是 toouse hello Windows Azure 診斷 (WAD) 延伸，其中上傳記錄檔 tooAzure 存放裝置，而且也 hello 選項 toosend 記錄 tooAzure Application Insights 或事件中心。 您也可以使用外部處理序 tooread hello 事件從儲存體，並放在中，已分析的平台產品，例如[OMS 記錄分析](../log-analytics/log-analytics-service-fabric.md)或另一個記錄檔剖析方案。

## <a name="prerequisites"></a>必要條件
這些工具會使用的 tooperform 一些在這份文件中的 hello 作業：

* [Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)（相關 tooAzure 雲端服務但有良好的資訊和範例）
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Resource Manager 用戶端](https://github.com/projectkudu/ARMClient)
* [Azure Resource Manager 範本](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>記錄和事件來源

### <a name="service-fabric-platform-events"></a>Service Fabric 平台事件
中所述[本文](service-fabric-diagnostics-event-generation-infra.md)Service Fabric 設定您具有少數的方塊外的記錄通道，其中 hello 通道會輕鬆地設定 WAD toosend 監視和診斷資料 tooa 儲存資料表或其他地方：
  * 作業事件： 較高層級 hello Service Fabric 平台執行的作業。 範例包括建立應用程式和服務、節點狀態變更和升級資訊。 這些是以 Windows 事件追蹤 (ETW) 記錄的形式發出。
  * [Reliable Actors 程式設計模型事件](service-fabric-reliable-actors-diagnostics.md)
  * [Reliable Services 程式設計模型事件](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a>應用程式事件
 事件發出從您的應用程式及服務的程式碼，並使用 hello EventSource helper 類別寫入 hello 提供 Visual Studio 範本。 如需有關如何 toowrite EventSource 記錄從您的應用程式的詳細資訊，請參閱[監視及診斷服務在本機電腦的開發設定](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。

## <a name="deploy-hello-diagnostics-extension"></a>Hello 診斷延伸模組部署
hello 收集記錄檔中的第一個步驟是 toodeploy hello 診斷延伸模組，每個 hello Service Fabric 叢集中的 hello Vm 上。 hello 診斷延伸模組會收集每個 VM 上的記錄檔，並將其上傳 toohello 您指定的儲存體帳戶。 hello 步驟會稍有根據您使用 hello Azure 入口網站或 Azure 資源管理員而有所不同。 hello 步驟也隨著是否 hello 部署是建立叢集的一部分，或適用於叢集已經存在。 讓我們看看每個案例的 hello 步驟。

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Hello 叢集建立時，透過 Azure 入口網站的診斷延伸模組部署
toodeploy hello 診斷延伸模組 toohello Vm hello 叢集中，叢集建立時，使用 hello hello 下列所示的診斷設定面板影像-請確定診斷設定太**上**(hello 預設設定). 建立 hello 叢集之後，您無法使用 hello 入口網站來變更這些設定。

![在叢集建立的 hello 入口網站的 azure 診斷設定](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

當您要使用 hello 入口網站來建立叢集時，我們強烈建議您下載 hello 範本**按一下 [確定] 之前**toocreate hello 叢集。 如需詳細資訊，請參閱太[使用 Azure Resource Manager 範本設定 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。 更新版本中，因為您無法使用 hello 入口網站進行一些變更，您將需要 hello toomake 變更 」 範本。

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>使用 Azure Resource Manager 部署 hello 診斷延伸模組，建立叢集的一部分
toocreate 叢集中使用資源管理員，您需要 tooadd hello 診斷組態 JSON toohello 完整的叢集資源管理員範本，才能建立 hello 叢集。 我們提供診斷組態加入範例五個 VM 叢集資源管理員範本 tooit 我們的資源管理員範本範例的一部分。 您可以查看 hello Azure 範例庫中的此位置：[診斷資源管理員範本 」 範例使用五個節點叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad)。

在 hello Resource Manager 範本、 開啟 hello azuredeploy.json 檔案，並搜尋 toosee hello 診斷設定**IaaSDiagnostics**。 使用此範本，選取 hello 叢集 toocreate**部署 tooAzure**按鈕位於 hello 前一個連結。

或者，下載 hello 資源管理員的範例，請變更 tooit 和 hello 修改的範本以建立叢集，利用 hello `New-AzureRmResourceGroupDeployment` Azure PowerShell 視窗中命令。 請參閱下列程式碼，您傳遞 toohello 命令中的 hello 參數 hello。 如需如何 toodeploy 資源群組使用 PowerShell 的詳細資訊，請參閱 hello 文章[部署的資源群組與 hello Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)。

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a>部署 hello 診斷延伸模組 tooan 現有叢集
如果您有現有的叢集沒有診斷部署，或如果您想 toomodify 現有的組態，您可以新增或更新它。 修改是使用的 toocreate hello 現有叢集的 hello Resource Manager 範本，或從稍早所述的 hello 入口網站下載 hello 範本。 執行下列工作的 hello 修改 hello template.json 檔案。

加入 toohello 資源 > 一節，以將新的儲存體資源 toohello 範本。

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 接下來，加入 toohello 參數之間區段只在 hello 儲存體帳戶定義之後,`supportLogStorageAccountName`和`vmNodeType0Name`。 Hello 預留位置文字取代*此處為儲存體帳戶名稱*與 hello hello 儲存體帳戶名稱。

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
接著，更新 hello `VirtualMachineProfile` hello template.json 檔案，加入下列程式碼 hello 擴充功能陣列中的 hello 區段。 是確定 tooadd 逗號 hello 開頭或 hello 結束時，根據插入的位置。

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

您修改所述的 hello template.json 檔案之後，重新發行 hello Resource Manager 範本。 如果匯出的 hello 範本，執行 hello deploy.ps1 檔案再重新發行 hello 範本。 部署之後，請確認 **ProvisioningState** 為 **Succeeded**。

## <a name="collect-health-and-load-events"></a>收集健康情況和負載事件

從 Service Fabric 的 hello 5.4 版開始，健全狀況和負載度量事件可用於集合。 這些事件會反映使用 hello 健全狀況所 hello 系統或您的程式碼產生的事件或載入報表的應用程式開發介面，例如[ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx)或[ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx)。 這可讓您彙總及檢視一段時間的系統健康情況，以及根據健康情況或負載事件發出警示。 Visual Studio 的診斷事件檢視器中的這些事件新增的 tooview"Microsoft-ServiceFabric:4:0x4000000000000008"toohello ETW 提供者清單。

toocollect hello 事件，修改 hello 資源管理員範本 tooinclude

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a>收集反向 proxy 事件

從 Service Fabric 的 hello 5.7 版開始[反向 proxy](service-fabric-reverseproxy.md)事件可用於集合。
反向 proxy 發出到兩個通道，一個包含錯誤的事件事件反映要求處理失敗並 hello 另一個包含所有在 hello 反向 proxy 處理的 hello 要求的相關詳細資料事件。 

1. 收集錯誤事件： tooview 這些事件，Visual Studio 的診斷事件檢視器中加入 「 Microsoft-ServiceFabric:4:0x4000000000000010"toohello ETW 提供者清單。
從 Azure 的叢集，toocollect hello 事件修改 hello 資源管理員範本 tooinclude

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. 收集所有事件處理的要求： 在 Visual Studio 中的診斷事件檢視器 中的更新 hello Microsoft ServiceFabric 項目太 hello ETW 提供者清單 」 Microsoft-ServiceFabric:4:0x4000000000000020"。
Azure Service Fabric 叢集，並修改 hello 資源管理員範本 tooinclude

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> 建議是從這個通道 toojudiciously 啟用收集事件因為這會收集所有流量通過 hello 反向 proxy，並可以快速地使用儲存體容量。

Azure Service Fabric 叢集的所有 hello 節點中的 hello 事件會收集並彙總顯示在 hello SystemEventTable。
如需詳細的 hello 反向 proxy 事件進行疑難排解，請參閱 hello[反向 proxy 診斷指南](service-fabric-reverse-proxy-diagnostics.md)。

## <a name="collect-from-new-eventsource-channels"></a>從新的 EventSource 通道收集

tooupdate 診斷 toocollect 記錄檔，從代表即將 toodeploy，新的應用程式的新 EventSource 通道執行相同的步驟如先前所述的 hello hello 安裝程式的診斷資訊的現有叢集。

更新 hello`EtwEventSourceProviderConfiguration`區段在 hello template.json 檔 tooadd 項目中針對使用 hello hello 新 EventSource 通道之前您要套用 hello 組態更新`New-AzureRmResourceGroupDeployment`PowerShell 命令。 hello hello 事件來源名稱被定義為 hello Visual Studio 產生 ServiceEventSource.cs 檔案中的程式碼的一部分。

例如，如果事件來源為我 Eventsource，加入 hello 我 Eventsource 中的下列程式碼 tooplace hello 事件，插入名為 MyDestinationTableName 資料表。

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

toocollect 效能計數器或事件記錄檔中，修改 hello Resource Manager 範本使用中提供的 hello 範例[使用監視和診斷的 Windows 虛擬機器建立使用 Azure Resource Manager 範本](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 然後，重新發行 hello Resource Manager 範本。

## <a name="collect-performance-counters"></a>收集效能計數器

toocollect 效能度量資訊，從您的叢集，叢集中的 hello Resource Manager 範本中加入 hello 效能計數器 tooyour"WadCfg > DiagnosticMonitorConfiguration"。 如需我們建議收集的效能計數器，請參閱 [Service Fabric 效能計數器](service-fabric-diagnostics-event-generation-perf.md)。

這裡比方說，我們會設定在不同的效能計數器取樣每 15 秒 (此項可能變更，如下所示 hello 的格式"PT\<時間 >\<單元 >"，PT3M 會每隔三分鐘的範例，例如)，以及傳送 toohello適當的儲存體資料表每隔一分鐘。

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
如果您使用 Application Insights 接收器 hello 節 < 中所述，且想這些度量 tooshow Application Insights 中，則請確定 tooadd hello 接收名稱如上所示的 hello 「 接收 」 區段中。 此外，請考慮建立個別的資料表 toosend 效能計數器，因此它們不塞滿出 hello 來自 hello 其他您已啟用的記錄通道。


## <a name="send-logs-tooapplication-insights"></a>傳送記錄 tooApplication Insights

傳送監視和診斷資料 tooApplication Insights (AI) 即可 hello WAD 組態的一部分。 如果您決定 toouse AI 事件分析和視覺效果，請參閱[事件分析和視覺效果使用 Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset 向上 AI 接收，您 「 WadCfg 」 的一部分。

## <a name="next-steps"></a>後續步驟

一旦您已正確設定 Azure 診斷，您會看到從 hello ETW 和 EventSource 記錄檔儲存體資料表中的資料。 如果您選擇 toouse OMS，Kibana 或任何其他資料分析和視覺效果平台不直接設定在 hello 資源管理員範本中，在選擇 tooread hello 平台上的確定 tooset hello 這些儲存體資料表的資料。 對 OMS 而言，這是非常一般的作業，且會在[透過 OMS 的事件和記錄分析](service-fabric-diagnostics-event-analysis-oms.md)中進行。 Application Insights 是位元的特殊案例中就這個意義而言，因為它可以設定為 hello 診斷延伸模組組態的一部分，因此請參閱 toohello[相關的文件](service-fabric-diagnostics-event-analysis-appinsights.md)如果您選擇 toouse AI。

>[!NOTE]
>目前沒有任何方式 toofilter 或清理 hello 事件傳送 toohello 資料表。 如果您不會實作 hello 資料表中的程序 tooremove 事件，hello 資料表會繼續 toogrow。 目前沒有在 hello 中執行資料清理服務的範例[監視範例](https://github.com/Azure-Samples/service-fabric-watchdog-service)，並建議您將資料寫入您自己的其中一個，除非有很好的理由，為您 toostore 超過 30 個或 90 天的時間範圍內的記錄檔。

* [了解 toocollect 效能計數器或記錄檔使用 hello 診斷延伸模組](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [使用 Application Insights 進行事件分析和視覺效果](service-fabric-diagnostics-event-analysis-appinsights.md)
* [使用 OMS 進行事件分析和視覺效果](service-fabric-diagnostics-event-analysis-oms.md)