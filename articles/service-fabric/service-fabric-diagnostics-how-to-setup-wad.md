---
title: "使用 Azure 診斷程式 aaaCollect 記錄檔 |Microsoft 文件"
description: "本文說明如何設定 Azure 診斷 toocollect tooset 記錄從 Service Fabric 叢集在 Azure 中執行。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>使用 Azure 診斷收集記錄檔
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

執行 Azure Service Fabric 叢集時，它是個不錯的主意 toocollect hello 記錄檔儲存在集中位置的所有 hello 節點。 在中央位置擁有 hello 記錄檔可協助您分析和疑難排解問題在叢集中或在 hello 應用程式和服務在該叢集中執行的問題。

其中一種方式 tooupload 及收集記錄檔是 toouse hello Azure 診斷擴充功能，哪一個上傳記錄 tooAzure 儲存體、 Azure Application Insights 或 Azure 事件中心。 無法直接在儲存體或事件中心中，那麼有用 hello 記錄檔。 但是您可以使用外部處理序 tooread hello 事件從儲存體，例如將它們放在產品[記錄分析](../log-analytics/log-analytics-service-fabric.md)或另一個記錄檔剖析方案。 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 隨附完整的記錄檔搜尋與分析服務內建功能。

## <a name="prerequisites"></a>必要條件
您可以使用這些工具 tooperform 一些在這份文件中的 hello 作業：

* [Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)（相關 tooAzure 雲端服務但有良好的資訊和範例）
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Resource Manager 用戶端](https://github.com/projectkudu/ARMClient)
* [Azure Resource Manager 範本](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a>您可能想 toocollect 的記錄檔來源
* **Service Fabric 記錄**: hello 平台 toostandard 事件追蹤的 Windows (ETW) 和 EventSource 通道所發出。 記錄檔可以是下列其中一種類型：
  * 作業事件： hello Service Fabric 平台執行的作業記錄檔。 範例包括建立應用程式和服務、節點狀態變更和升級資訊。
  * [Reliable Actors 程式設計模型事件](service-fabric-reliable-actors-diagnostics.md)
  * [Reliable Services 程式設計模型事件](service-fabric-reliable-services-diagnostics.md)
* **應用程式事件**： 從您的服務程式碼發出，寫出使用 hello EventSource helper 類別中 hello Visual Studio 範本所提供的事件。 如需有關如何 toowrite 記錄從您的應用程式的詳細資訊，請參閱[監視及診斷服務在本機電腦的開發設定](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。

## <a name="deploy-hello-diagnostics-extension"></a>Hello 診斷延伸模組部署
hello 收集記錄檔中的第一個步驟是 toodeploy hello 診斷延伸模組，每個 hello Service Fabric 叢集中的 hello Vm 上。 hello 診斷延伸模組會收集每個 VM 上的記錄檔，並將其上傳 toohello 您指定的儲存體帳戶。 hello 步驟會稍有根據您使用 hello Azure 入口網站或 Azure 資源管理員而有所不同。 hello 步驟也隨著是否 hello 部署是建立叢集的一部分，或適用於叢集已經存在。 讓我們看看每個案例的 hello 步驟。

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a>Hello 叢集建立時，透過 hello 入口網站的診斷延伸模組部署
toodeploy hello 診斷延伸模組 toohello Vm hello 叢集中建立叢集的一部分，您可以使用 hello 診斷設定面板 hello 下列影像所示。 tooenable Reliable Actors 或可靠的服務事件的集合，請確定診斷設定得**上**(hello 預設設定)。 建立 hello 叢集之後，您無法使用 hello 入口網站來變更這些設定。

![在叢集建立的 hello 入口網站的 azure 診斷設定](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

hello Azure 支援小組*需要*支援記錄 toohelp 解析您建立任何支援要求。 這些記錄檔會即時收集，且會儲存在其中一個 hello hello 資源群組中建立的儲存體帳戶。 hello 診斷設定會設定應用程式層級事件。 這些事件包含[Reliable Actors](service-fabric-reliable-actors-diagnostics.md)事件，[可靠服務](service-fabric-reliable-services-diagnostics.md)事件，以及儲存在 Azure 儲存體中的某些系統層級 Service Fabric 事件 toobe。

例如，產品[Elasticsearch](https://www.elastic.co/guide/index.html)或您自己的處理序可以取得 hello 事件從 hello 儲存體帳戶。 目前沒有任何方式 toofilter 或清理 hello 事件傳送 toohello 資料表。 如果您不會實作 hello 資料表中的程序 tooremove 事件，hello 資料表會繼續 toogrow。

當您要使用 hello 入口網站來建立叢集時，我們強烈建議您下載 hello 範本**按一下 [確定] 之前**toocreate hello 叢集。 如需詳細資訊，請參閱太[使用 Azure Resource Manager 範本設定 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。 更新版本中，因為您無法使用 hello 入口網站進行一些變更，您將需要 hello toomake 變更 」 範本。

您可以使用下列步驟的 hello，從 hello 入口網站匯出範本。 不過，這些範本可以是 toouse 更加困難，因為它們可能會遺失必要的資訊的 null 值。

1. 開啟您的資源群組。
2. 選取**設定**toodisplay hello 設定面板。
3. 選取**部署**toodisplay hello 部署歷程記錄面板。
4. 選取 hello 部署的部署 toodisplay hello 詳細資料。
5. 選取**匯出範本**toodisplay hello 範本面板。
6. 選取**儲存 toofile** tooexport 包含 hello 範本、 參數和 PowerShell 檔案的.zip 檔案。

匯出 hello 檔案之後，您會需要 toomake 所做的修改。 編輯 hello parameters.json 檔案，並移除 hello **adminPassword**項目。 Hello 部署指令碼執行時，這會導致 hello 密碼的提示。 如果您執行 hello 部署指令碼，您可能必須 toofix null 參數值。

toouse hello 下載範本 tooupdate 設定：

1. 擷取本機電腦上的 hello 內容 tooa 資料夾。
2. 修改 hello 內容 tooreflect hello 新組態。
3. 啟動 PowerShell 並變更 toohello 資料夾解壓縮 hello 內容的位置。
4. 執行**deploy.ps1**並填入 hello 訂用帳戶 ID，hello 資源群組名稱 (使用 hello 相同 tooupdate hello 組態的名稱)，以及獨特的部署名稱。

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>使用 Azure Resource Manager 部署 hello 診斷延伸模組，建立叢集的一部分
toocreate 叢集中使用資源管理員，您需要 tooadd hello 診斷組態 JSON toohello 完整的叢集資源管理員範本，才能建立 hello 叢集。 我們提供診斷組態加入範例五個 VM 叢集資源管理員範本 tooit 我們的資源管理員範本範例的一部分。 您可以查看 hello Azure 範例庫中的此位置：[診斷資源管理員範本 」 範例使用五個節點叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)。

在 hello Resource Manager 範本、 開啟 hello azuredeploy.json 檔案，並搜尋 toosee hello 診斷設定**IaaSDiagnostics**。 使用此範本，選取 hello 叢集 toocreate**部署 tooAzure**按鈕位於 hello 前一個連結。

或者，下載 hello 資源管理員的範例，請變更 tooit 和 hello 修改的範本以建立叢集，利用 hello `New-AzureRmResourceGroupDeployment` Azure PowerShell 視窗中命令。 請參閱下列程式碼，您傳遞 toohello 命令中的 hello 參數 hello。 如需如何 toodeploy 資源群組使用 PowerShell 的詳細資訊，請參閱 hello 文章[部署的資源群組與 hello Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)。

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

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

## <a name="update-diagnostics-toocollect-health-and-load-events"></a>更新的診斷 toocollect 健全狀況和負載事件

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a>更新診斷 toocollect 並上傳新的 EventSource 通道的記錄檔
tooupdate 診斷 toocollect 記錄檔，從代表即將 toodeploy，新的應用程式的新 EventSource 通道執行相同步驟 hello 與 hello[上一節](#deploywadarm)現有的安裝程式的診斷資訊叢集。

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

## <a name="next-steps"></a>後續步驟
更詳細的 toounderstand 時疑難排解問題，您應該尋找哪些事件請參閱 hello 診斷事件發出[Reliable Actors](service-fabric-reliable-actors-diagnostics.md)和[可靠服務](service-fabric-reliable-services-diagnostics.md)。

## <a name="related-articles"></a>相關文章
* [了解 toocollect 效能計數器或記錄檔使用 hello 診斷延伸模組](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Log Analytics 中的 Service Fabric 解決方案](../log-analytics/log-analytics-service-fabric.md)

