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
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="ba202-103">使用 Windows Azure 診斷的事件彙總和收集</span><span class="sxs-lookup"><span data-stu-id="ba202-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba202-104">Windows</span><span class="sxs-lookup"><span data-stu-id="ba202-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="ba202-105">Linux</span><span class="sxs-lookup"><span data-stu-id="ba202-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="ba202-106">執行 Azure Service Fabric 叢集時，它是個不錯的主意 toocollect hello 記錄檔儲存在集中位置的所有 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="ba202-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="ba202-107">在中央位置擁有 hello 記錄檔可協助您分析和疑難排解問題在叢集中或在 hello 應用程式和服務在該叢集中執行的問題。</span><span class="sxs-lookup"><span data-stu-id="ba202-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="ba202-108">其中一種方式 tooupload 及收集記錄檔是 toouse hello Windows Azure 診斷 (WAD) 延伸，其中上傳記錄檔 tooAzure 存放裝置，而且也 hello 選項 toosend 記錄 tooAzure Application Insights 或事件中心。</span><span class="sxs-lookup"><span data-stu-id="ba202-108">One way tooupload and collect logs is toouse hello Windows Azure Diagnostics (WAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="ba202-109">您也可以使用外部處理序 tooread hello 事件從儲存體，並放在中，已分析的平台產品，例如[OMS 記錄分析](../log-analytics/log-analytics-service-fabric.md)或另一個記錄檔剖析方案。</span><span class="sxs-lookup"><span data-stu-id="ba202-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba202-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ba202-110">Prerequisites</span></span>
<span data-ttu-id="ba202-111">這些工具會使用的 tooperform 一些在這份文件中的 hello 作業：</span><span class="sxs-lookup"><span data-stu-id="ba202-111">These tools are used tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="ba202-112">[Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)（相關 tooAzure 雲端服務但有良好的資訊和範例）</span><span class="sxs-lookup"><span data-stu-id="ba202-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="ba202-113">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba202-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="ba202-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba202-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="ba202-115">Azure Resource Manager 用戶端</span><span class="sxs-lookup"><span data-stu-id="ba202-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="ba202-116">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="ba202-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="ba202-117">記錄和事件來源</span><span class="sxs-lookup"><span data-stu-id="ba202-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="ba202-118">Service Fabric 平台事件</span><span class="sxs-lookup"><span data-stu-id="ba202-118">Service Fabric platform events</span></span>
<span data-ttu-id="ba202-119">中所述[本文](service-fabric-diagnostics-event-generation-infra.md)Service Fabric 設定您具有少數的方塊外的記錄通道，其中 hello 通道會輕鬆地設定 WAD toosend 監視和診斷資料 tooa 儲存資料表或其他地方：</span><span class="sxs-lookup"><span data-stu-id="ba202-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which hello following channels are easily configured with WAD toosend monitoring and diagnostics data tooa storage table or elsewhere:</span></span>
  * <span data-ttu-id="ba202-120">作業事件： 較高層級 hello Service Fabric 平台執行的作業。</span><span class="sxs-lookup"><span data-stu-id="ba202-120">Operational events: higher-level operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="ba202-121">範例包括建立應用程式和服務、節點狀態變更和升級資訊。</span><span class="sxs-lookup"><span data-stu-id="ba202-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="ba202-122">這些是以 Windows 事件追蹤 (ETW) 記錄的形式發出。</span><span class="sxs-lookup"><span data-stu-id="ba202-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="ba202-123">Reliable Actors 程式設計模型事件</span><span class="sxs-lookup"><span data-stu-id="ba202-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="ba202-124">Reliable Services 程式設計模型事件</span><span class="sxs-lookup"><span data-stu-id="ba202-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="ba202-125">應用程式事件</span><span class="sxs-lookup"><span data-stu-id="ba202-125">Application events</span></span>
 <span data-ttu-id="ba202-126">事件發出從您的應用程式及服務的程式碼，並使用 hello EventSource helper 類別寫入 hello 提供 Visual Studio 範本。</span><span class="sxs-lookup"><span data-stu-id="ba202-126">Events emitted from your applications' and services' code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="ba202-127">如需有關如何 toowrite EventSource 記錄從您的應用程式的詳細資訊，請參閱[監視及診斷服務在本機電腦的開發設定](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。</span><span class="sxs-lookup"><span data-stu-id="ba202-127">For more information on how toowrite EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="ba202-128">Hello 診斷延伸模組部署</span><span class="sxs-lookup"><span data-stu-id="ba202-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="ba202-129">hello 收集記錄檔中的第一個步驟是 toodeploy hello 診斷延伸模組，每個 hello Service Fabric 叢集中的 hello Vm 上。</span><span class="sxs-lookup"><span data-stu-id="ba202-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="ba202-130">hello 診斷延伸模組會收集每個 VM 上的記錄檔，並將其上傳 toohello 您指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ba202-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="ba202-131">hello 步驟會稍有根據您使用 hello Azure 入口網站或 Azure 資源管理員而有所不同。</span><span class="sxs-lookup"><span data-stu-id="ba202-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="ba202-132">hello 步驟也隨著是否 hello 部署是建立叢集的一部分，或適用於叢集已經存在。</span><span class="sxs-lookup"><span data-stu-id="ba202-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="ba202-133">讓我們看看每個案例的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ba202-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="ba202-134">Hello 叢集建立時，透過 Azure 入口網站的診斷延伸模組部署</span><span class="sxs-lookup"><span data-stu-id="ba202-134">Deploy hello Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="ba202-135">toodeploy hello 診斷延伸模組 toohello Vm hello 叢集中，叢集建立時，使用 hello hello 下列所示的診斷設定面板影像-請確定診斷設定太**上**(hello 預設設定).</span><span class="sxs-lookup"><span data-stu-id="ba202-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image - ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="ba202-136">建立 hello 叢集之後，您無法使用 hello 入口網站來變更這些設定。</span><span class="sxs-lookup"><span data-stu-id="ba202-136">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![在叢集建立的 hello 入口網站的 azure 診斷設定](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="ba202-138">當您要使用 hello 入口網站來建立叢集時，我們強烈建議您下載 hello 範本**按一下 [確定] 之前**toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="ba202-138">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="ba202-139">如需詳細資訊，請參閱太[使用 Azure Resource Manager 範本設定 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="ba202-139">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="ba202-140">更新版本中，因為您無法使用 hello 入口網站進行一些變更，您將需要 hello toomake 變更 」 範本。</span><span class="sxs-lookup"><span data-stu-id="ba202-140">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="ba202-141">使用 Azure Resource Manager 部署 hello 診斷延伸模組，建立叢集的一部分</span><span class="sxs-lookup"><span data-stu-id="ba202-141">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="ba202-142">toocreate 叢集中使用資源管理員，您需要 tooadd hello 診斷組態 JSON toohello 完整的叢集資源管理員範本，才能建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="ba202-142">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="ba202-143">我們提供診斷組態加入範例五個 VM 叢集資源管理員範本 tooit 我們的資源管理員範本範例的一部分。</span><span class="sxs-lookup"><span data-stu-id="ba202-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="ba202-144">您可以查看 hello Azure 範例庫中的此位置：[診斷資源管理員範本 」 範例使用五個節點叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad)。</span><span class="sxs-lookup"><span data-stu-id="ba202-144">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="ba202-145">在 hello Resource Manager 範本、 開啟 hello azuredeploy.json 檔案，並搜尋 toosee hello 診斷設定**IaaSDiagnostics**。</span><span class="sxs-lookup"><span data-stu-id="ba202-145">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="ba202-146">使用此範本，選取 hello 叢集 toocreate**部署 tooAzure**按鈕位於 hello 前一個連結。</span><span class="sxs-lookup"><span data-stu-id="ba202-146">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="ba202-147">或者，下載 hello 資源管理員的範例，請變更 tooit 和 hello 修改的範本以建立叢集，利用 hello `New-AzureRmResourceGroupDeployment` Azure PowerShell 視窗中命令。</span><span class="sxs-lookup"><span data-stu-id="ba202-147">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="ba202-148">請參閱下列程式碼，您傳遞 toohello 命令中的 hello 參數 hello。</span><span class="sxs-lookup"><span data-stu-id="ba202-148">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="ba202-149">如需如何 toodeploy 資源群組使用 PowerShell 的詳細資訊，請參閱 hello 文章[部署的資源群組與 hello Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="ba202-149">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="ba202-150">部署 hello 診斷延伸模組 tooan 現有叢集</span><span class="sxs-lookup"><span data-stu-id="ba202-150">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="ba202-151">如果您有現有的叢集沒有診斷部署，或如果您想 toomodify 現有的組態，您可以新增或更新它。</span><span class="sxs-lookup"><span data-stu-id="ba202-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="ba202-152">修改是使用的 toocreate hello 現有叢集的 hello Resource Manager 範本，或從稍早所述的 hello 入口網站下載 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="ba202-152">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="ba202-153">執行下列工作的 hello 修改 hello template.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="ba202-153">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="ba202-154">加入 toohello 資源 > 一節，以將新的儲存體資源 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="ba202-154">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="ba202-155">接下來，加入 toohello 參數之間區段只在 hello 儲存體帳戶定義之後,`supportLogStorageAccountName`和`vmNodeType0Name`。</span><span class="sxs-lookup"><span data-stu-id="ba202-155">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="ba202-156">Hello 預留位置文字取代*此處為儲存體帳戶名稱*與 hello hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="ba202-156">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

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
<span data-ttu-id="ba202-157">接著，更新 hello `VirtualMachineProfile` hello template.json 檔案，加入下列程式碼 hello 擴充功能陣列中的 hello 區段。</span><span class="sxs-lookup"><span data-stu-id="ba202-157">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="ba202-158">是確定 tooadd 逗號 hello 開頭或 hello 結束時，根據插入的位置。</span><span class="sxs-lookup"><span data-stu-id="ba202-158">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="ba202-159">您修改所述的 hello template.json 檔案之後，重新發行 hello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="ba202-159">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="ba202-160">如果匯出的 hello 範本，執行 hello deploy.ps1 檔案再重新發行 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="ba202-160">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="ba202-161">部署之後，請確認 **ProvisioningState** 為 **Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="ba202-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="ba202-162">收集健康情況和負載事件</span><span class="sxs-lookup"><span data-stu-id="ba202-162">Collect health and load events</span></span>

<span data-ttu-id="ba202-163">從 Service Fabric 的 hello 5.4 版開始，健全狀況和負載度量事件可用於集合。</span><span class="sxs-lookup"><span data-stu-id="ba202-163">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="ba202-164">這些事件會反映使用 hello 健全狀況所 hello 系統或您的程式碼產生的事件或載入報表的應用程式開發介面，例如[ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx)或[ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba202-164">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="ba202-165">這可讓您彙總及檢視一段時間的系統健康情況，以及根據健康情況或負載事件發出警示。</span><span class="sxs-lookup"><span data-stu-id="ba202-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="ba202-166">Visual Studio 的診斷事件檢視器中的這些事件新增的 tooview"Microsoft-ServiceFabric:4:0x4000000000000008"toohello ETW 提供者清單。</span><span class="sxs-lookup"><span data-stu-id="ba202-166">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="ba202-167">toocollect hello 事件，修改 hello 資源管理員範本 tooinclude</span><span class="sxs-lookup"><span data-stu-id="ba202-167">toocollect hello events, modify hello Resource Manager template tooinclude</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="ba202-168">收集反向 proxy 事件</span><span class="sxs-lookup"><span data-stu-id="ba202-168">Collect reverse proxy events</span></span>

<span data-ttu-id="ba202-169">從 Service Fabric 的 hello 5.7 版開始[反向 proxy](service-fabric-reverseproxy.md)事件可用於集合。</span><span class="sxs-lookup"><span data-stu-id="ba202-169">Starting with hello 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="ba202-170">反向 proxy 發出到兩個通道，一個包含錯誤的事件事件反映要求處理失敗並 hello 另一個包含所有在 hello 反向 proxy 處理的 hello 要求的相關詳細資料事件。</span><span class="sxs-lookup"><span data-stu-id="ba202-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and hello other one containing verbose events about all hello requests processed at hello reverse proxy.</span></span> 

1. <span data-ttu-id="ba202-171">收集錯誤事件： tooview 這些事件，Visual Studio 的診斷事件檢視器中加入 「 Microsoft-ServiceFabric:4:0x4000000000000010"toohello ETW 提供者清單。</span><span class="sxs-lookup"><span data-stu-id="ba202-171">Collect error events: tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" toohello list of ETW providers.</span></span>
<span data-ttu-id="ba202-172">從 Azure 的叢集，toocollect hello 事件修改 hello 資源管理員範本 tooinclude</span><span class="sxs-lookup"><span data-stu-id="ba202-172">toocollect hello events from Azure clusters, modify hello Resource Manager template tooinclude</span></span>

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

2. <span data-ttu-id="ba202-173">收集所有事件處理的要求： 在 Visual Studio 中的診斷事件檢視器 中的更新 hello Microsoft ServiceFabric 項目太 hello ETW 提供者清單 」 Microsoft-ServiceFabric:4:0x4000000000000020"。</span><span class="sxs-lookup"><span data-stu-id="ba202-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update hello Microsoft-ServiceFabric entry in hello ETW provider list too"Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="ba202-174">Azure Service Fabric 叢集，並修改 hello 資源管理員範本 tooinclude</span><span class="sxs-lookup"><span data-stu-id="ba202-174">For Azure Service Fabric clusters, modify hello resource manager template tooinclude</span></span>

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
> <span data-ttu-id="ba202-175">建議是從這個通道 toojudiciously 啟用收集事件因為這會收集所有流量通過 hello 反向 proxy，並可以快速地使用儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="ba202-175">It is recommended toojudiciously enable collecting events from this channel as this collects all traffic through hello reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="ba202-176">Azure Service Fabric 叢集的所有 hello 節點中的 hello 事件會收集並彙總顯示在 hello SystemEventTable。</span><span class="sxs-lookup"><span data-stu-id="ba202-176">For Azure Service Fabric clusters, hello events from all hello nodes are collected and aggregated in hello SystemEventTable.</span></span>
<span data-ttu-id="ba202-177">如需詳細的 hello 反向 proxy 事件進行疑難排解，請參閱 hello[反向 proxy 診斷指南](service-fabric-reverse-proxy-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="ba202-177">For detailed troubleshooting of hello reverse proxy events, refer hello [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="ba202-178">從新的 EventSource 通道收集</span><span class="sxs-lookup"><span data-stu-id="ba202-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="ba202-179">tooupdate 診斷 toocollect 記錄檔，從代表即將 toodeploy，新的應用程式的新 EventSource 通道執行相同的步驟如先前所述的 hello hello 安裝程式的診斷資訊的現有叢集。</span><span class="sxs-lookup"><span data-stu-id="ba202-179">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as previously described for hello setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="ba202-180">更新 hello`EtwEventSourceProviderConfiguration`區段在 hello template.json 檔 tooadd 項目中針對使用 hello hello 新 EventSource 通道之前您要套用 hello 組態更新`New-AzureRmResourceGroupDeployment`PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="ba202-180">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="ba202-181">hello hello 事件來源名稱被定義為 hello Visual Studio 產生 ServiceEventSource.cs 檔案中的程式碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="ba202-181">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="ba202-182">例如，如果事件來源為我 Eventsource，加入 hello 我 Eventsource 中的下列程式碼 tooplace hello 事件，插入名為 MyDestinationTableName 資料表。</span><span class="sxs-lookup"><span data-stu-id="ba202-182">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="ba202-183">toocollect 效能計數器或事件記錄檔中，修改 hello Resource Manager 範本使用中提供的 hello 範例[使用監視和診斷的 Windows 虛擬機器建立使用 Azure Resource Manager 範本](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba202-183">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ba202-184">然後，重新發行 hello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="ba202-184">Then, republish hello Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="ba202-185">收集效能計數器</span><span class="sxs-lookup"><span data-stu-id="ba202-185">Collect Performance Counters</span></span>

<span data-ttu-id="ba202-186">toocollect 效能度量資訊，從您的叢集，叢集中的 hello Resource Manager 範本中加入 hello 效能計數器 tooyour"WadCfg > DiagnosticMonitorConfiguration"。</span><span class="sxs-lookup"><span data-stu-id="ba202-186">toocollect performance metrics from your cluster, add hello performance counters tooyour "WadCfg > DiagnosticMonitorConfiguration" in hello Resource Manager template for your cluster.</span></span> <span data-ttu-id="ba202-187">如需我們建議收集的效能計數器，請參閱 [Service Fabric 效能計數器](service-fabric-diagnostics-event-generation-perf.md)。</span><span class="sxs-lookup"><span data-stu-id="ba202-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="ba202-188">這裡比方說，我們會設定在不同的效能計數器取樣每 15 秒 (此項可能變更，如下所示 hello 的格式"PT\<時間 >\<單元 >"，PT3M 會每隔三分鐘的範例，例如)，以及傳送 toohello適當的儲存體資料表每隔一分鐘。</span><span class="sxs-lookup"><span data-stu-id="ba202-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows hello format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred toohello appropriate storage table every one minute.</span></span>

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
  
<span data-ttu-id="ba202-189">如果您使用 Application Insights 接收器 hello 節 < 中所述，且想這些度量 tooshow Application Insights 中，則請確定 tooadd hello 接收名稱如上所示的 hello 「 接收 」 區段中。</span><span class="sxs-lookup"><span data-stu-id="ba202-189">If you are using an Application Insights sink, as described in hello section below, and want these metrics tooshow up in Application Insights, then make sure tooadd hello sink name in hello "sinks" section as shown above.</span></span> <span data-ttu-id="ba202-190">此外，請考慮建立個別的資料表 toosend 效能計數器，因此它們不塞滿出 hello 來自 hello 其他您已啟用的記錄通道。</span><span class="sxs-lookup"><span data-stu-id="ba202-190">Additionally, consider creating a separate table toosend your Performance Counters to, so they don't crowd out hello data coming from hello other logging channels you have enabled.</span></span>


## <a name="send-logs-tooapplication-insights"></a><span data-ttu-id="ba202-191">傳送記錄 tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="ba202-191">Send logs tooApplication Insights</span></span>

<span data-ttu-id="ba202-192">傳送監視和診斷資料 tooApplication Insights (AI) 即可 hello WAD 組態的一部分。</span><span class="sxs-lookup"><span data-stu-id="ba202-192">Sending monitoring and diagnostics data tooApplication Insights (AI) can be done as part of hello WAD configuration.</span></span> <span data-ttu-id="ba202-193">如果您決定 toouse AI 事件分析和視覺效果，請參閱[事件分析和視覺效果使用 Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset 向上 AI 接收，您 「 WadCfg 」 的一部分。</span><span class="sxs-lookup"><span data-stu-id="ba202-193">If you decide toouse AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba202-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba202-194">Next steps</span></span>

<span data-ttu-id="ba202-195">一旦您已正確設定 Azure 診斷，您會看到從 hello ETW 和 EventSource 記錄檔儲存體資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="ba202-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from hello ETW and EventSource logs.</span></span> <span data-ttu-id="ba202-196">如果您選擇 toouse OMS，Kibana 或任何其他資料分析和視覺效果平台不直接設定在 hello 資源管理員範本中，在選擇 tooread hello 平台上的確定 tooset hello 這些儲存體資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="ba202-196">If you choose toouse OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in hello Resource Manager template, make sure tooset up hello platform of your choice tooread in hello data from these storage tables.</span></span> <span data-ttu-id="ba202-197">對 OMS 而言，這是非常一般的作業，且會在[透過 OMS 的事件和記錄分析](service-fabric-diagnostics-event-analysis-oms.md)中進行。</span><span class="sxs-lookup"><span data-stu-id="ba202-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="ba202-198">Application Insights 是位元的特殊案例中就這個意義而言，因為它可以設定為 hello 診斷延伸模組組態的一部分，因此請參閱 toohello[相關的文件](service-fabric-diagnostics-event-analysis-appinsights.md)如果您選擇 toouse AI。</span><span class="sxs-lookup"><span data-stu-id="ba202-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of hello Diagnostics extension configuration, so refer toohello [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose toouse AI.</span></span>

>[!NOTE]
><span data-ttu-id="ba202-199">目前沒有任何方式 toofilter 或清理 hello 事件傳送 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="ba202-199">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="ba202-200">如果您不會實作 hello 資料表中的程序 tooremove 事件，hello 資料表會繼續 toogrow。</span><span class="sxs-lookup"><span data-stu-id="ba202-200">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span> <span data-ttu-id="ba202-201">目前沒有在 hello 中執行資料清理服務的範例[監視範例](https://github.com/Azure-Samples/service-fabric-watchdog-service)，並建議您將資料寫入您自己的其中一個，除非有很好的理由，為您 toostore 超過 30 個或 90 天的時間範圍內的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ba202-201">Currently, there is an example of a data grooming service running in hello [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you toostore logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="ba202-202">了解 toocollect 效能計數器或記錄檔使用 hello 診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="ba202-202">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ba202-203">使用 Application Insights 進行事件分析和視覺效果</span><span class="sxs-lookup"><span data-stu-id="ba202-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="ba202-204">使用 OMS 進行事件分析和視覺效果</span><span class="sxs-lookup"><span data-stu-id="ba202-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)