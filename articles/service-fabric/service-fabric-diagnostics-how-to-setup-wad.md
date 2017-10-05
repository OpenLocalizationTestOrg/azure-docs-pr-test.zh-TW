---
title: "使用 Azure 診斷收集記錄檔 | Microsoft Docs"
description: "本文將說明如何設定 Azure 診斷從 Azure 中執行的 Service Fabric 叢集收集記錄檔"
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
ms.openlocfilehash: 190a8a393f2e7d74a792db4efa81f94a18b02221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="626d8-103">使用 Azure 診斷收集記錄檔</span><span class="sxs-lookup"><span data-stu-id="626d8-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="626d8-104">Windows</span><span class="sxs-lookup"><span data-stu-id="626d8-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="626d8-105">Linux</span><span class="sxs-lookup"><span data-stu-id="626d8-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="626d8-106">當您執行 Azure Service Fabric 叢集時，最好從中央位置的所有節點收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="626d8-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="626d8-107">將記錄檔集中在中央位置，可協助您分析並針對叢集或該叢集中執行之應用程式與服務的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="626d8-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="626d8-108">上傳和收集記錄檔的其中一種方式就是使用「Azure 診斷」擴充功能，此擴充功能可將記錄檔上傳到「Azure 儲存體」、Azure Application Insights 或「Azure 事件中樞」。</span><span class="sxs-lookup"><span data-stu-id="626d8-108">One way to upload and collect logs is to use the Azure Diagnostics extension, which uploads logs to Azure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="626d8-109">這些記錄檔在儲存體或「事件中樞」中並不直接那麼有用。</span><span class="sxs-lookup"><span data-stu-id="626d8-109">The logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="626d8-110">但是您可以使用外部處理程序從儲存體讀取事件，然後將它們放在 [Log Analytics](../log-analytics/log-analytics-service-fabric.md) 之類的產品或其他記錄檔剖析解決方案中。</span><span class="sxs-lookup"><span data-stu-id="626d8-110">But you can use an external process to read the events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="626d8-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 隨附完整的記錄檔搜尋與分析服務內建功能。</span><span class="sxs-lookup"><span data-stu-id="626d8-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="626d8-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="626d8-112">Prerequisites</span></span>
<span data-ttu-id="626d8-113">您將使用這些工具來執行這份文件中的某些作業：</span><span class="sxs-lookup"><span data-stu-id="626d8-113">You use these tools to perform some of the operations in this document:</span></span>

* <span data-ttu-id="626d8-114">[Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md) (與 Azure 雲端服務相關，但具備有用的資訊和範例)</span><span class="sxs-lookup"><span data-stu-id="626d8-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="626d8-115">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="626d8-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="626d8-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="626d8-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="626d8-117">Azure Resource Manager 用戶端</span><span class="sxs-lookup"><span data-stu-id="626d8-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="626d8-118">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="626d8-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-to-collect"></a><span data-ttu-id="626d8-119">您可能想要收集的記錄來源</span><span class="sxs-lookup"><span data-stu-id="626d8-119">Log sources that you might want to collect</span></span>
* <span data-ttu-id="626d8-120">**Service Fabric 記錄檔**：由平台發出到標準 Windows 事件追蹤 (ETW) 和 EventSource 通道。</span><span class="sxs-lookup"><span data-stu-id="626d8-120">**Service Fabric logs**: Emitted from the platform to standard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="626d8-121">記錄檔可以是下列其中一種類型：</span><span class="sxs-lookup"><span data-stu-id="626d8-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="626d8-122">操作事件：Service Fabric 平台所執行之作業的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="626d8-122">Operational events: Logs for operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="626d8-123">範例包括建立應用程式和服務、節點狀態變更和升級資訊。</span><span class="sxs-lookup"><span data-stu-id="626d8-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="626d8-124">Reliable Actors 程式設計模型事件</span><span class="sxs-lookup"><span data-stu-id="626d8-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="626d8-125">Reliable Services 程式設計模型事件</span><span class="sxs-lookup"><span data-stu-id="626d8-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="626d8-126">**應用程式事件**：從您的服務程式碼發出且使用 Visual Studio 範本所提供的 EventSource 協助程式類別所寫出的事件。</span><span class="sxs-lookup"><span data-stu-id="626d8-126">**Application events**: Events emitted from your service's code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="626d8-127">如需有關如何從應用程式寫入記錄檔的詳細資訊，請參閱[監視和診斷本機開發設定中的服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。</span><span class="sxs-lookup"><span data-stu-id="626d8-127">For more information on how to write logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="626d8-128">部署診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="626d8-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="626d8-129">收集記錄檔的第一個步驟是將診斷擴充功能部署在 Service Fabric 叢集的每個 WM 上。</span><span class="sxs-lookup"><span data-stu-id="626d8-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="626d8-130">診斷擴充功能會收集每個 VM 上的記錄檔，並將它們上傳至您指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="626d8-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="626d8-131">步驟視您使用 Azure 入口網站或 Azure Resource Manager 而稍微有所不同。</span><span class="sxs-lookup"><span data-stu-id="626d8-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="626d8-132">步驟也會視部署為叢集建立的一部分，或是針對現有的叢集而有所不同。</span><span class="sxs-lookup"><span data-stu-id="626d8-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="626d8-133">讓我們看看每個案例的步驟。</span><span class="sxs-lookup"><span data-stu-id="626d8-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-the-portal"></a><span data-ttu-id="626d8-134">透過入口網站建立叢集時部署診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="626d8-134">Deploy the Diagnostics extension as part of cluster creation through the portal</span></span>
<span data-ttu-id="626d8-135">為了在建立叢集時將診斷擴充功能部署至叢集中的 WM，您會使用下圖所示的診斷設定面板。</span><span class="sxs-lookup"><span data-stu-id="626d8-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image.</span></span> <span data-ttu-id="626d8-136">若要收集 Reliable Actors 或 Reliable Services 事件，請確定已將 [診斷] 設定為 [開啟] \(這是預設設定)。</span><span class="sxs-lookup"><span data-stu-id="626d8-136">To enable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="626d8-137">建立叢集之後，您就無法使用入口網站變更這些設定。</span><span class="sxs-lookup"><span data-stu-id="626d8-137">After you create the cluster, you can't change these settings by using the portal.</span></span>

![入口網站中用於建立叢集的 Azure 診斷設定](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="626d8-139">Azure 支援團隊「需要」支援記錄檔，才能盡心處理您所建立的任何支援要求。</span><span class="sxs-lookup"><span data-stu-id="626d8-139">The Azure support team *requires* support logs to help resolve any support requests that you create.</span></span> <span data-ttu-id="626d8-140">這些記錄檔會即時收集，並儲存在建立於資源群組中的其中一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="626d8-140">These logs are collected in real time and are stored in one of the storage accounts created in the resource group.</span></span> <span data-ttu-id="626d8-141">[診斷] 設定可設定應用程式層級的事件。</span><span class="sxs-lookup"><span data-stu-id="626d8-141">The Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="626d8-142">這些事件包括會儲存在 Azure 儲存體的 [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) 事件、[Reliable Services](service-fabric-reliable-services-diagnostics.md) 事件，以及部分系統層級 Service Fabric 事件。</span><span class="sxs-lookup"><span data-stu-id="626d8-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events to be stored in Azure Storage.</span></span>

<span data-ttu-id="626d8-143">[Elasticsearch](https://www.elastic.co/guide/index.html) 之類的產品或您自己的處理程序可以從儲存體帳戶中取得事件。</span><span class="sxs-lookup"><span data-stu-id="626d8-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get the events from the storage account.</span></span> <span data-ttu-id="626d8-144">目前沒有任何方法可以篩選或清理已傳送至資料表的事件。</span><span class="sxs-lookup"><span data-stu-id="626d8-144">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="626d8-145">如果不實作從資料表移除事件的處理序，資料表將會繼續成長。</span><span class="sxs-lookup"><span data-stu-id="626d8-145">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span>

<span data-ttu-id="626d8-146">當您使用入口網站來建立叢集時，強烈建議您**在按一下 [確定] 來建立叢集之前**，先下載範本。</span><span class="sxs-lookup"><span data-stu-id="626d8-146">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="626d8-147">如需詳細資訊，請參閱[使用 Azure Resource Manager 範本來設定 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="626d8-147">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="626d8-148">您需要範本以在稍後進行變更，因為您無法使用入口網站進行某些變更。</span><span class="sxs-lookup"><span data-stu-id="626d8-148">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

<span data-ttu-id="626d8-149">您可以使用下列步驟從入口網站匯出範本。</span><span class="sxs-lookup"><span data-stu-id="626d8-149">You can export templates from the portal by using the following steps.</span></span> <span data-ttu-id="626d8-150">不過，這些範本的使用方式可能會比較困難，因為它們可能包含缺少必要資訊的 null 值。</span><span class="sxs-lookup"><span data-stu-id="626d8-150">However, these templates can be more difficult to use because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="626d8-151">開啟您的資源群組。</span><span class="sxs-lookup"><span data-stu-id="626d8-151">Open your resource group.</span></span>
2. <span data-ttu-id="626d8-152">選取 [設定] 以顯示設定面板。</span><span class="sxs-lookup"><span data-stu-id="626d8-152">Select **Settings** to display the settings panel.</span></span>
3. <span data-ttu-id="626d8-153">選取 [部署] 以顯示部署歷程記錄面板。</span><span class="sxs-lookup"><span data-stu-id="626d8-153">Select **Deployments** to display the deployment history panel.</span></span>
4. <span data-ttu-id="626d8-154">選取一個部署以顯示該部署的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="626d8-154">Select a deployment to display the details of the deployment.</span></span>
5. <span data-ttu-id="626d8-155">選取 [匯出範本] 以顯示範本面板。</span><span class="sxs-lookup"><span data-stu-id="626d8-155">Select **Export Template** to display the template panel.</span></span>
6. <span data-ttu-id="626d8-156">選取 [儲存至檔案] 以匯出包含範本、參數和 PowerShell 檔案的 .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="626d8-156">Select **Save to file** to export a .zip file that contains the template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="626d8-157">匯出檔案之後，您需要進行修改。</span><span class="sxs-lookup"><span data-stu-id="626d8-157">After you export the files, you need to make a modification.</span></span> <span data-ttu-id="626d8-158">編輯 parameters.json 檔案，並移除 **adminPassword** 元素。</span><span class="sxs-lookup"><span data-stu-id="626d8-158">Edit the parameters.json file and remove the **adminPassword** element.</span></span> <span data-ttu-id="626d8-159">執行部署指令碼時，這樣會導致密碼的提示。</span><span class="sxs-lookup"><span data-stu-id="626d8-159">This will cause a prompt for the password when the deployment script is run.</span></span> <span data-ttu-id="626d8-160">在執行部署指令碼時，您可能必須修正 null 參數值。</span><span class="sxs-lookup"><span data-stu-id="626d8-160">When you're running the deployment script, you might have to fix null parameter values.</span></span>

<span data-ttu-id="626d8-161">使用下載的範本來更新組態：</span><span class="sxs-lookup"><span data-stu-id="626d8-161">To use the downloaded template to update a configuration:</span></span>

1. <span data-ttu-id="626d8-162">將內容解壓縮到本機電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="626d8-162">Extract the contents to a folder on your local computer.</span></span>
2. <span data-ttu-id="626d8-163">修改內容以反映新的組態。</span><span class="sxs-lookup"><span data-stu-id="626d8-163">Modify the contents to reflect the new configuration.</span></span>
3. <span data-ttu-id="626d8-164">啟動 PowerShell 並變更到您要解壓縮內容的資料夾。</span><span class="sxs-lookup"><span data-stu-id="626d8-164">Start PowerShell and change to the folder where you extracted the content.</span></span>
4. <span data-ttu-id="626d8-165">執行 **deploy.ps1** 並填入訂用帳戶識別碼、資源群組名稱 (使用相同的名稱來更新組態) 和唯一的部署名稱。</span><span class="sxs-lookup"><span data-stu-id="626d8-165">Run **deploy.ps1** and fill in the subscription ID, the resource group name (use the same name to update the configuration), and a unique deployment name.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="626d8-166">使用 Azure Resource Manager 在建立叢集時部署診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="626d8-166">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="626d8-167">若要使用 Resource Manager 建立叢集，您需要在建立叢集之前，將診斷組態 JSON 加入至完整的叢集 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="626d8-167">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="626d8-168">我們在 Resource Manager 範本範例中提供一個五 VM 叢集 Resource Manager 範本，且已在其中加入診斷設定。</span><span class="sxs-lookup"><span data-stu-id="626d8-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="626d8-169">您可以在 Azure 資源庫中的這個位置看到它： [具有診斷 Resource Manager 範本範例的五節點叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)。</span><span class="sxs-lookup"><span data-stu-id="626d8-169">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="626d8-170">若要查看 Resource Manager 範本中的 [診斷] 設定，請開啟 azuredeploy.json 檔案，並搜尋 **IaaSDiagnostics**。</span><span class="sxs-lookup"><span data-stu-id="626d8-170">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="626d8-171">若要使用這個範本建立叢集，請選取上一個連結所提供的 [部署到 Azure] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="626d8-171">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="626d8-172">或者，您也可以下載資源管理員範例，對它進行變更，然後在 Azure PowerShell 視窗中使用 `New-AzureRmResourceGroupDeployment` 命令來使用修改過的範本建立叢集。</span><span class="sxs-lookup"><span data-stu-id="626d8-172">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="626d8-173">針對您傳遞給命令的參數，請參閱以下程式碼。</span><span class="sxs-lookup"><span data-stu-id="626d8-173">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="626d8-174">如需如何使用 PowerShell 部署資源群組的詳細資訊，請參閱[使用 Azure Resource Manager 範本部署資源群組](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="626d8-174">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="626d8-175">將診斷擴充功能部署到現有的叢集</span><span class="sxs-lookup"><span data-stu-id="626d8-175">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="626d8-176">如果您具有未部署診斷的現有叢集，或是想要修改現有的組態，您可以使用下列步驟來新增或更新它。</span><span class="sxs-lookup"><span data-stu-id="626d8-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="626d8-177">修改用來建立現有叢集的 Resource Manager 範本，或是以上述方式從入口網站下載範本。</span><span class="sxs-lookup"><span data-stu-id="626d8-177">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="626d8-178">執行下列工作來修改 template.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="626d8-178">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="626d8-179">藉由新增儲存體資源到資源區段，以將其新增至範本。</span><span class="sxs-lookup"><span data-stu-id="626d8-179">Add a new storage resource to the template by adding to the resources section.</span></span>

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

 <span data-ttu-id="626d8-180">接下來，新增至參數區段中儲存體帳戶定義之後的位置，位於 `supportLogStorageAccountName` 和 `vmNodeType0Name` 之間。</span><span class="sxs-lookup"><span data-stu-id="626d8-180">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="626d8-181">以儲存體帳戶的名稱取代預留位置文字 *storage account name goes here*。</span><span class="sxs-lookup"><span data-stu-id="626d8-181">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

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
<span data-ttu-id="626d8-182">然後，透過在擴充功能陣列內新增下列內容，更新 template.json 檔案的 `VirtualMachineProfile` 區段。</span><span class="sxs-lookup"><span data-stu-id="626d8-182">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="626d8-183">請務必在開頭或結尾 (取決於其插入的位置) 加入逗點。</span><span class="sxs-lookup"><span data-stu-id="626d8-183">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="626d8-184">如所述修改 template.json 檔案之後，將 Resource Manager 範本重新發佈。</span><span class="sxs-lookup"><span data-stu-id="626d8-184">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="626d8-185">如果已匯出範本，執行 deploy.ps1 檔案將會重新發佈範本。</span><span class="sxs-lookup"><span data-stu-id="626d8-185">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="626d8-186">部署之後，請確認 **ProvisioningState** 為 **Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="626d8-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-to-collect-health-and-load-events"></a><span data-ttu-id="626d8-187">更新診斷以收集健康情況和負載事件</span><span class="sxs-lookup"><span data-stu-id="626d8-187">Update diagnostics to collect health and load events</span></span>

<span data-ttu-id="626d8-188">從 Service Fabric 5.4 版開始，健康情況和負載計量事件均可供收集。</span><span class="sxs-lookup"><span data-stu-id="626d8-188">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="626d8-189">這些事件可藉由使用健康情況或負載報告 API (例如 [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) 或 [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx))，反映系統或程式碼所產生的事件。</span><span class="sxs-lookup"><span data-stu-id="626d8-189">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="626d8-190">這可讓您彙總及檢視一段時間的系統健康情況，以及根據健康情況或負載事件發出警示。</span><span class="sxs-lookup"><span data-stu-id="626d8-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="626d8-191">若要在 Visual Studio 的「診斷事件檢視器」中檢視這些事件，請將 "Microsoft-ServiceFabric:4:0x4000000000000008" 新增到 ETW 提供者清單中。</span><span class="sxs-lookup"><span data-stu-id="626d8-191">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="626d8-192">若要收集事件，請修改 Resource Manager 範本，使其包含</span><span class="sxs-lookup"><span data-stu-id="626d8-192">To collect the events, modify the resource manager template to include</span></span>

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

## <a name="update-diagnostics-to-collect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="626d8-193">更新診斷從新的 EventSource 通道收集並上傳記錄檔</span><span class="sxs-lookup"><span data-stu-id="626d8-193">Update Diagnostics to collect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="626d8-194">若要更新診斷以從新的 EventSource 通道 (代表您將要部署的新應用程式) 收集記錄檔，請執行[上一節](#deploywadarm)中相同的步驟，以針對現有叢集設定診斷。</span><span class="sxs-lookup"><span data-stu-id="626d8-194">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as in the [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="626d8-195">在您使用 `New-AzureRmResourceGroupDeployment` PowerShell 命令套用組態更新之前，請先更新 template.json 檔案中的 `EtwEventSourceProviderConfiguration` 區段，以新增 EventSource 通道的項目。</span><span class="sxs-lookup"><span data-stu-id="626d8-195">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="626d8-196">在 Visual Studio 產生的 ServiceEventSource.cs 檔案中，事件來源的名稱定義為程式碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="626d8-196">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="626d8-197">例如，如果您的事件資源名稱是 My-Eventsource，新增下列程式碼以將來自 My-Eventsource 的事件置於名稱為 MyDestinationTableName 的資料表中。</span><span class="sxs-lookup"><span data-stu-id="626d8-197">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="626d8-198">若要收集效能計數器或事件記錄檔，請以[使用 Azure Resource Manager 範本建立具有監視和診斷的 Windows 虛擬機器](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中提供的範例來修改 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="626d8-198">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="626d8-199">然後請重新發佈 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="626d8-199">Then, republish the Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="626d8-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="626d8-200">Next steps</span></span>
<span data-ttu-id="626d8-201">若要更詳細了解進行問題移難排解時應該注意的事件，請查看針對 [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) 和 [Reliable Services](service-fabric-reliable-services-diagnostics.md) 所發出的診斷事件。</span><span class="sxs-lookup"><span data-stu-id="626d8-201">To understand in more detail what events you should look for while troubleshooting issues, see the diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="626d8-202">相關文章</span><span class="sxs-lookup"><span data-stu-id="626d8-202">Related articles</span></span>
* [<span data-ttu-id="626d8-203">了解如何使用診斷擴充功能收集效能計數器或記錄檔</span><span class="sxs-lookup"><span data-stu-id="626d8-203">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="626d8-204">Log Analytics 中的 Service Fabric 解決方案</span><span class="sxs-lookup"><span data-stu-id="626d8-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

