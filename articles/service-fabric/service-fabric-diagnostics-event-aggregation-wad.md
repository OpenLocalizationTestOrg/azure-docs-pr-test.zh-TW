---
title: "使用 Windows Azure 診斷的 Azure Service Fabric 事件彙總 | Microsoft Docs"
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
ms.openlocfilehash: 5773361fdec4cb8ee54fa2856f6aa969d5dac4e9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="4a3c0-103">使用 Windows Azure 診斷的事件彙總和收集</span><span class="sxs-lookup"><span data-stu-id="4a3c0-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a3c0-104">Windows</span><span class="sxs-lookup"><span data-stu-id="4a3c0-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="4a3c0-105">Linux</span><span class="sxs-lookup"><span data-stu-id="4a3c0-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="4a3c0-106">當您執行 Azure Service Fabric 叢集時，最好從中央位置的所有節點收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="4a3c0-107">將記錄檔集中在中央位置，可協助您分析並針對叢集或該叢集中執行之應用程式與服務的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="4a3c0-108">上傳和收集記錄的其中一種方式就是使用「Windows Azure 診斷 (WAD)」延伸模組，此延伸模組可將記錄上傳到「Azure 儲存體」，也可以選擇將記錄傳送至 Azure Application Insights 或「事件中樞」。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-108">One way to upload and collect logs is to use the Windows Azure Diagnostics (WAD) extension, which uploads logs to Azure Storage, and also has the option to send logs to Azure Application Insights or Event Hubs.</span></span> <span data-ttu-id="4a3c0-109">您也可以使用外部程序來讀取儲存體中的事件，然後將它們放在 [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) 這類的分析平台產品或其他記錄剖析解決方案中。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-109">You can also use an external process to read the events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a3c0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4a3c0-110">Prerequisites</span></span>
<span data-ttu-id="4a3c0-111">這些工具是用來執行這份文件中的某些作業：</span><span class="sxs-lookup"><span data-stu-id="4a3c0-111">These tools are used to perform some of the operations in this document:</span></span>

* <span data-ttu-id="4a3c0-112">[Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md) (與 Azure 雲端服務相關，但具備有用的資訊和範例)</span><span class="sxs-lookup"><span data-stu-id="4a3c0-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="4a3c0-113">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4a3c0-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="4a3c0-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a3c0-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="4a3c0-115">Azure Resource Manager 用戶端</span><span class="sxs-lookup"><span data-stu-id="4a3c0-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="4a3c0-116">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="4a3c0-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="4a3c0-117">記錄和事件來源</span><span class="sxs-lookup"><span data-stu-id="4a3c0-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="4a3c0-118">Service Fabric 平台事件</span><span class="sxs-lookup"><span data-stu-id="4a3c0-118">Service Fabric platform events</span></span>
<span data-ttu-id="4a3c0-119">如[本文](service-fabric-diagnostics-event-generation-infra.md)所述，Service Fabric 會設定一些現成的記錄通道；其中，使用 WAD 可以輕鬆地設定下列通道，將監視和診斷資料傳送至儲存體資料表或其他位置：</span><span class="sxs-lookup"><span data-stu-id="4a3c0-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which the following channels are easily configured with WAD to send monitoring and diagnostics data to a storage table or elsewhere:</span></span>
  * <span data-ttu-id="4a3c0-120">操作事件：Service Fabric 平台所執行之較高層級的作業。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-120">Operational events: higher-level operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="4a3c0-121">範例包括建立應用程式和服務、節點狀態變更和升級資訊。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="4a3c0-122">這些是以 Windows 事件追蹤 (ETW) 記錄的形式發出。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="4a3c0-123">Reliable Actors 程式設計模型事件</span><span class="sxs-lookup"><span data-stu-id="4a3c0-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="4a3c0-124">Reliable Services 程式設計模型事件</span><span class="sxs-lookup"><span data-stu-id="4a3c0-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="4a3c0-125">應用程式事件</span><span class="sxs-lookup"><span data-stu-id="4a3c0-125">Application events</span></span>
 <span data-ttu-id="4a3c0-126">從您的應用程式和服務程式碼發出，且使用 Visual Studio 範本中所提供的 EventSource 協助程式類別所寫出的事件。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-126">Events emitted from your applications' and services' code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="4a3c0-127">如需如何從應用程式寫入 EventSource 記錄的詳細資訊，請參閱[監視和診斷本機開發設定中的服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-127">For more information on how to write EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="4a3c0-128">部署診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="4a3c0-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="4a3c0-129">收集記錄檔的第一個步驟是將診斷擴充功能部署在 Service Fabric 叢集的每個 WM 上。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="4a3c0-130">診斷擴充功能會收集每個 VM 上的記錄檔，並將它們上傳至您指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="4a3c0-131">步驟視您使用 Azure 入口網站或 Azure Resource Manager 而稍微有所不同。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="4a3c0-132">步驟也會視部署為叢集建立的一部分，或是針對現有的叢集而有所不同。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="4a3c0-133">讓我們看看每個案例的步驟。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="4a3c0-134">透過 Azure 入口網站建立叢集時部署診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="4a3c0-134">Deploy the Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="4a3c0-135">為了在建立叢集時將診斷延伸模組部署至叢集中的 WM，您會使用下圖所示的 [診斷設定] 面板。請確定 [診斷] 設定為 [開啟] \(預設設定\) 。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image - ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="4a3c0-136">建立叢集之後，您就無法使用入口網站變更這些設定。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-136">After you create the cluster, you can't change these settings by using the portal.</span></span>

![入口網站中用於建立叢集的 Azure 診斷設定](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="4a3c0-138">當您使用入口網站來建立叢集時，強烈建議您**在按一下 [確定] 來建立叢集之前**，先下載範本。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-138">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="4a3c0-139">如需詳細資訊，請參閱[使用 Azure Resource Manager 範本來設定 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-139">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="4a3c0-140">您需要範本以在稍後進行變更，因為您無法使用入口網站進行某些變更。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-140">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="4a3c0-141">使用 Azure Resource Manager 在建立叢集時部署診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="4a3c0-141">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="4a3c0-142">若要使用 Resource Manager 建立叢集，您需要在建立叢集之前，將診斷組態 JSON 加入至完整的叢集 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-142">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="4a3c0-143">我們在 Resource Manager 範本範例中提供一個五 VM 叢集 Resource Manager 範本，且已在其中加入診斷設定。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="4a3c0-144">您可以在 Azure 資源庫中的這個位置看到它： [具有診斷 Resource Manager 範本範例的五節點叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad)。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-144">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="4a3c0-145">若要查看 Resource Manager 範本中的 [診斷] 設定，請開啟 azuredeploy.json 檔案，並搜尋 **IaaSDiagnostics**。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-145">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="4a3c0-146">若要使用這個範本建立叢集，請選取上一個連結所提供的 [部署到 Azure] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-146">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="4a3c0-147">或者，您也可以下載資源管理員範例，對它進行變更，然後在 Azure PowerShell 視窗中使用 `New-AzureRmResourceGroupDeployment` 命令來使用修改過的範本建立叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-147">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="4a3c0-148">針對您傳遞給命令的參數，請參閱以下程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-148">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="4a3c0-149">如需如何使用 PowerShell 部署資源群組的詳細資訊，請參閱[使用 Azure Resource Manager 範本部署資源群組](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-149">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="4a3c0-150">將診斷擴充功能部署到現有的叢集</span><span class="sxs-lookup"><span data-stu-id="4a3c0-150">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="4a3c0-151">如果您具有未部署診斷的現有叢集，或是想要修改現有的組態，您可以使用下列步驟來新增或更新它。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="4a3c0-152">修改用來建立現有叢集的 Resource Manager 範本，或是以上述方式從入口網站下載範本。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-152">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="4a3c0-153">執行下列工作來修改 template.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-153">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="4a3c0-154">藉由新增儲存體資源到資源區段，以將其新增至範本。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-154">Add a new storage resource to the template by adding to the resources section.</span></span>

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

 <span data-ttu-id="4a3c0-155">接下來，新增至參數區段中儲存體帳戶定義之後的位置，位於 `supportLogStorageAccountName` 和 `vmNodeType0Name` 之間。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-155">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="4a3c0-156">以儲存體帳戶的名稱取代預留位置文字 *storage account name goes here*。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-156">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
<span data-ttu-id="4a3c0-157">然後，透過在擴充功能陣列內新增下列內容，更新 template.json 檔案的 `VirtualMachineProfile` 區段。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-157">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="4a3c0-158">請務必在開頭或結尾 (取決於其插入的位置) 加入逗點。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-158">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="4a3c0-159">如所述修改 template.json 檔案之後，將 Resource Manager 範本重新發佈。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-159">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="4a3c0-160">如果已匯出範本，執行 deploy.ps1 檔案將會重新發佈範本。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-160">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="4a3c0-161">部署之後，請確認 **ProvisioningState** 為 **Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="4a3c0-162">收集健康情況和負載事件</span><span class="sxs-lookup"><span data-stu-id="4a3c0-162">Collect health and load events</span></span>

<span data-ttu-id="4a3c0-163">從 Service Fabric 5.4 版開始，健康情況和負載計量事件均可供收集。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-163">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="4a3c0-164">這些事件可藉由使用健康情況或負載報告 API (例如 [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) 或 [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx))，反映系統或程式碼所產生的事件。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-164">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="4a3c0-165">這可讓您彙總及檢視一段時間的系統健康情況，以及根據健康情況或負載事件發出警示。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="4a3c0-166">若要在 Visual Studio 的「診斷事件檢視器」中檢視這些事件，請將 "Microsoft-ServiceFabric:4:0x4000000000000008" 新增到 ETW 提供者清單中。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-166">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="4a3c0-167">若要收集事件，請修改 Resource Manager 範本，使其包含</span><span class="sxs-lookup"><span data-stu-id="4a3c0-167">To collect the events, modify the Resource Manager template to include</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="4a3c0-168">收集反向 proxy 事件</span><span class="sxs-lookup"><span data-stu-id="4a3c0-168">Collect reverse proxy events</span></span>

<span data-ttu-id="4a3c0-169">從 Service Fabric 5.7 版開始，[反向 proxy](service-fabric-reverseproxy.md) 事件可供收集。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-169">Starting with the 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="4a3c0-170">反向 proxy 會將事件發至兩個通道，其中一個包含可反映要求處理失敗的錯誤事件，而另一個包含在反向 proxy 處理之所有要求的詳細資訊事件。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and the other one containing verbose events about all the requests processed at the reverse proxy.</span></span> 

1. <span data-ttu-id="4a3c0-171">收集錯誤事件︰若要在 Visual Studio 的「診斷事件檢視器」中檢視這些事件，請將 "Microsoft-ServiceFabric:4:0x4000000000000010" 新增到 ETW 提供者清單中。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-171">Collect error events: To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" to the list of ETW providers.</span></span>
<span data-ttu-id="4a3c0-172">若要從 Azure 叢集收集事件，請修改 Resource Manager 範本，使其包含</span><span class="sxs-lookup"><span data-stu-id="4a3c0-172">To collect the events from Azure clusters, modify the Resource Manager template to include</span></span>

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

2. <span data-ttu-id="4a3c0-173">收集所有要求處理事件：在 Visual Studio 的診斷事件檢視器中，將 ETW 提供者清單中的 Microsoft-ServiceFabric 項目更新為 "Microsoft-ServiceFabric:4:0x4000000000000020"。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update the Microsoft-ServiceFabric entry in the ETW provider list to "Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="4a3c0-174">對於 Azure Service Fabric 叢集，修改資源管理員範本，使其包含</span><span class="sxs-lookup"><span data-stu-id="4a3c0-174">For Azure Service Fabric clusters, modify the resource manager template to include</span></span>

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
> <span data-ttu-id="4a3c0-175">建議審慎地允許從此通道收集事件，因為這可透過反向 proxy 收集所有流量並可快速地取用儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-175">It is recommended to judiciously enable collecting events from this channel as this collects all traffic through the reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="4a3c0-176">對於 Azure Service Fabric 叢集，所有節點的事件都會收集在 SystemEventTable 中並且彙總。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-176">For Azure Service Fabric clusters, the events from all the nodes are collected and aggregated in the SystemEventTable.</span></span>
<span data-ttu-id="4a3c0-177">如需反向 proxy 事件的詳細疑難排解，請參閱[反向 proxy 診斷指南](service-fabric-reverse-proxy-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-177">For detailed troubleshooting of the reverse proxy events, refer the [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="4a3c0-178">從新的 EventSource 通道收集</span><span class="sxs-lookup"><span data-stu-id="4a3c0-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="4a3c0-179">若要更新診斷以從新的 EventSource 通道 (代表您將要部署的新應用程式) 收集記錄，請執行先前所述的相同步驟，以針對現有叢集設定診斷。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-179">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as previously described for the setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="4a3c0-180">在您使用 `New-AzureRmResourceGroupDeployment` PowerShell 命令套用組態更新之前，請先更新 template.json 檔案中的 `EtwEventSourceProviderConfiguration` 區段，以新增 EventSource 通道的項目。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-180">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="4a3c0-181">在 Visual Studio 產生的 ServiceEventSource.cs 檔案中，事件來源的名稱定義為程式碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-181">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="4a3c0-182">例如，如果您的事件資源名稱是 My-Eventsource，新增下列程式碼以將來自 My-Eventsource 的事件置於名稱為 MyDestinationTableName 的資料表中。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-182">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="4a3c0-183">若要收集效能計數器或事件記錄檔，請以[使用 Azure Resource Manager 範本建立具有監視和診斷的 Windows 虛擬機器](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中提供的範例來修改 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-183">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="4a3c0-184">然後請重新發佈 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-184">Then, republish the Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="4a3c0-185">收集效能計數器</span><span class="sxs-lookup"><span data-stu-id="4a3c0-185">Collect Performance Counters</span></span>

<span data-ttu-id="4a3c0-186">若要收集叢集中的效能計量，請在叢集的 Resource Manager 範本中將效能計數器新增至 "WadCfg > DiagnosticMonitorConfiguration"。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-186">To collect performance metrics from your cluster, add the performance counters to your "WadCfg > DiagnosticMonitorConfiguration" in the Resource Manager template for your cluster.</span></span> <span data-ttu-id="4a3c0-187">如需我們建議收集的效能計數器，請參閱 [Service Fabric 效能計數器](service-fabric-diagnostics-event-generation-perf.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="4a3c0-188">例如，我們在這裡設定一個效能計數器，其每 15 秒取樣一次 (此值可以變更，並遵循格式 "PT\<時間>\<單位>"，例如，PT3M 會以三分鐘的間隔取樣一次)，且每分鐘傳送到適當的儲存體資料表一次。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows the format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred to the appropriate storage table every one minute.</span></span>

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
  
<span data-ttu-id="4a3c0-189">如果您要使用 Application Insights 接收 (如下節所述)，而且想要將這些計量顯示在 Application Insights 中，則請確定在 "sinks" 區段中新增接收名稱 (如上所示)。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-189">If you are using an Application Insights sink, as described in the section below, and want these metrics to show up in Application Insights, then make sure to add the sink name in the "sinks" section as shown above.</span></span> <span data-ttu-id="4a3c0-190">此外，請考慮建立個別的資料表以傳送效能計數器，讓它們不會塞滿來自其他已啟用之記錄通道的資料。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-190">Additionally, consider creating a separate table to send your Performance Counters to, so they don't crowd out the data coming from the other logging channels you have enabled.</span></span>


## <a name="send-logs-to-application-insights"></a><span data-ttu-id="4a3c0-191">將記錄傳送至 Application Insights</span><span class="sxs-lookup"><span data-stu-id="4a3c0-191">Send logs to Application Insights</span></span>

<span data-ttu-id="4a3c0-192">將監視和診斷資料傳送至 Application Insights (AI) 的作業，可以在設定 WAD 時進行。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-192">Sending monitoring and diagnostics data to Application Insights (AI) can be done as part of the WAD configuration.</span></span> <span data-ttu-id="4a3c0-193">如果您決定使用 AI 進行事件分析和視覺效果，請閱讀[使用 Application Insights 進行事件分析和視覺效果](service-fabric-diagnostics-event-analysis-appinsights.md)，以在 "WadCfg" 時設定「AI 接收」。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-193">If you decide to use AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) to set up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a3c0-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a3c0-194">Next steps</span></span>

<span data-ttu-id="4a3c0-195">正確設定 Azure 診斷之後，您會從 ETW 和 EventSource 記錄中看到「儲存體」資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from the ETW and EventSource logs.</span></span> <span data-ttu-id="4a3c0-196">如果您選擇使用 OMS、Kibana 或未直接設定於 Resource Manager 範本的任何其他資料分析和視覺效果平台，請務必設定您要用來讀取這些儲存體資料表資料的平台。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-196">If you choose to use OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in the Resource Manager template, make sure to set up the platform of your choice to read in the data from these storage tables.</span></span> <span data-ttu-id="4a3c0-197">對 OMS 而言，這是非常一般的作業，且會在[透過 OMS 的事件和記錄分析](service-fabric-diagnostics-event-analysis-oms.md)中進行。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="4a3c0-198">也就是說，Application Insights 是特殊案例，因為它可以在設定診斷延伸模組時設定；因此，如果您選擇使用 AI，則請參閱[適當的文章](service-fabric-diagnostics-event-analysis-appinsights.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of the Diagnostics extension configuration, so refer to the [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose to use AI.</span></span>

>[!NOTE]
><span data-ttu-id="4a3c0-199">目前沒有任何方法可以篩選或清理已傳送至資料表的事件。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-199">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="4a3c0-200">如果不實作從資料表移除事件的處理序，資料表將會繼續成長。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-200">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span> <span data-ttu-id="4a3c0-201">目前，我們可以提供具有 [Watchdog 範例](https://github.com/Azure-Samples/service-fabric-watchdog-service)中所執行資料清理服務的範例，除非您必須儲存超過 30 或 90 天時間範圍的記錄，否則建議您自行撰寫資料清理服務。</span><span class="sxs-lookup"><span data-stu-id="4a3c0-201">Currently, there is an example of a data grooming service running in the [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you to store logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="4a3c0-202">了解如何使用診斷擴充功能收集效能計數器或記錄檔</span><span class="sxs-lookup"><span data-stu-id="4a3c0-202">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4a3c0-203">使用 Application Insights 進行事件分析和視覺效果</span><span class="sxs-lookup"><span data-stu-id="4a3c0-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="4a3c0-204">使用 OMS 進行事件分析和視覺效果</span><span class="sxs-lookup"><span data-stu-id="4a3c0-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)