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
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="37321-103">使用 Azure 診斷收集記錄檔</span><span class="sxs-lookup"><span data-stu-id="37321-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37321-104">Windows</span><span class="sxs-lookup"><span data-stu-id="37321-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="37321-105">Linux</span><span class="sxs-lookup"><span data-stu-id="37321-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="37321-106">執行 Azure Service Fabric 叢集時，它是個不錯的主意 toocollect hello 記錄檔儲存在集中位置的所有 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="37321-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="37321-107">在中央位置擁有 hello 記錄檔可協助您分析和疑難排解問題在叢集中或在 hello 應用程式和服務在該叢集中執行的問題。</span><span class="sxs-lookup"><span data-stu-id="37321-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="37321-108">其中一種方式 tooupload 及收集記錄檔是 toouse hello Azure 診斷擴充功能，哪一個上傳記錄 tooAzure 儲存體、 Azure Application Insights 或 Azure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="37321-108">One way tooupload and collect logs is toouse hello Azure Diagnostics extension, which uploads logs tooAzure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="37321-109">無法直接在儲存體或事件中心中，那麼有用 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="37321-109">hello logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="37321-110">但是您可以使用外部處理序 tooread hello 事件從儲存體，例如將它們放在產品[記錄分析](../log-analytics/log-analytics-service-fabric.md)或另一個記錄檔剖析方案。</span><span class="sxs-lookup"><span data-stu-id="37321-110">But you can use an external process tooread hello events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="37321-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 隨附完整的記錄檔搜尋與分析服務內建功能。</span><span class="sxs-lookup"><span data-stu-id="37321-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37321-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="37321-112">Prerequisites</span></span>
<span data-ttu-id="37321-113">您可以使用這些工具 tooperform 一些在這份文件中的 hello 作業：</span><span class="sxs-lookup"><span data-stu-id="37321-113">You use these tools tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="37321-114">[Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)（相關 tooAzure 雲端服務但有良好的資訊和範例）</span><span class="sxs-lookup"><span data-stu-id="37321-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="37321-115">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="37321-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="37321-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="37321-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="37321-117">Azure Resource Manager 用戶端</span><span class="sxs-lookup"><span data-stu-id="37321-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="37321-118">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="37321-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a><span data-ttu-id="37321-119">您可能想 toocollect 的記錄檔來源</span><span class="sxs-lookup"><span data-stu-id="37321-119">Log sources that you might want toocollect</span></span>
* <span data-ttu-id="37321-120">**Service Fabric 記錄**: hello 平台 toostandard 事件追蹤的 Windows (ETW) 和 EventSource 通道所發出。</span><span class="sxs-lookup"><span data-stu-id="37321-120">**Service Fabric logs**: Emitted from hello platform toostandard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="37321-121">記錄檔可以是下列其中一種類型：</span><span class="sxs-lookup"><span data-stu-id="37321-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="37321-122">作業事件： hello Service Fabric 平台執行的作業記錄檔。</span><span class="sxs-lookup"><span data-stu-id="37321-122">Operational events: Logs for operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="37321-123">範例包括建立應用程式和服務、節點狀態變更和升級資訊。</span><span class="sxs-lookup"><span data-stu-id="37321-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="37321-124">Reliable Actors 程式設計模型事件</span><span class="sxs-lookup"><span data-stu-id="37321-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="37321-125">Reliable Services 程式設計模型事件</span><span class="sxs-lookup"><span data-stu-id="37321-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="37321-126">**應用程式事件**： 從您的服務程式碼發出，寫出使用 hello EventSource helper 類別中 hello Visual Studio 範本所提供的事件。</span><span class="sxs-lookup"><span data-stu-id="37321-126">**Application events**: Events emitted from your service's code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="37321-127">如需有關如何 toowrite 記錄從您的應用程式的詳細資訊，請參閱[監視及診斷服務在本機電腦的開發設定](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。</span><span class="sxs-lookup"><span data-stu-id="37321-127">For more information on how toowrite logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="37321-128">Hello 診斷延伸模組部署</span><span class="sxs-lookup"><span data-stu-id="37321-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="37321-129">hello 收集記錄檔中的第一個步驟是 toodeploy hello 診斷延伸模組，每個 hello Service Fabric 叢集中的 hello Vm 上。</span><span class="sxs-lookup"><span data-stu-id="37321-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="37321-130">hello 診斷延伸模組會收集每個 VM 上的記錄檔，並將其上傳 toohello 您指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="37321-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="37321-131">hello 步驟會稍有根據您使用 hello Azure 入口網站或 Azure 資源管理員而有所不同。</span><span class="sxs-lookup"><span data-stu-id="37321-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="37321-132">hello 步驟也隨著是否 hello 部署是建立叢集的一部分，或適用於叢集已經存在。</span><span class="sxs-lookup"><span data-stu-id="37321-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="37321-133">讓我們看看每個案例的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="37321-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a><span data-ttu-id="37321-134">Hello 叢集建立時，透過 hello 入口網站的診斷延伸模組部署</span><span class="sxs-lookup"><span data-stu-id="37321-134">Deploy hello Diagnostics extension as part of cluster creation through hello portal</span></span>
<span data-ttu-id="37321-135">toodeploy hello 診斷延伸模組 toohello Vm hello 叢集中建立叢集的一部分，您可以使用 hello 診斷設定面板 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="37321-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image.</span></span> <span data-ttu-id="37321-136">tooenable Reliable Actors 或可靠的服務事件的集合，請確定診斷設定得**上**(hello 預設設定)。</span><span class="sxs-lookup"><span data-stu-id="37321-136">tooenable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="37321-137">建立 hello 叢集之後，您無法使用 hello 入口網站來變更這些設定。</span><span class="sxs-lookup"><span data-stu-id="37321-137">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![在叢集建立的 hello 入口網站的 azure 診斷設定](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="37321-139">hello Azure 支援小組*需要*支援記錄 toohelp 解析您建立任何支援要求。</span><span class="sxs-lookup"><span data-stu-id="37321-139">hello Azure support team *requires* support logs toohelp resolve any support requests that you create.</span></span> <span data-ttu-id="37321-140">這些記錄檔會即時收集，且會儲存在其中一個 hello hello 資源群組中建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="37321-140">These logs are collected in real time and are stored in one of hello storage accounts created in hello resource group.</span></span> <span data-ttu-id="37321-141">hello 診斷設定會設定應用程式層級事件。</span><span class="sxs-lookup"><span data-stu-id="37321-141">hello Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="37321-142">這些事件包含[Reliable Actors](service-fabric-reliable-actors-diagnostics.md)事件，[可靠服務](service-fabric-reliable-services-diagnostics.md)事件，以及儲存在 Azure 儲存體中的某些系統層級 Service Fabric 事件 toobe。</span><span class="sxs-lookup"><span data-stu-id="37321-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events toobe stored in Azure Storage.</span></span>

<span data-ttu-id="37321-143">例如，產品[Elasticsearch](https://www.elastic.co/guide/index.html)或您自己的處理序可以取得 hello 事件從 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="37321-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get hello events from hello storage account.</span></span> <span data-ttu-id="37321-144">目前沒有任何方式 toofilter 或清理 hello 事件傳送 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="37321-144">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="37321-145">如果您不會實作 hello 資料表中的程序 tooremove 事件，hello 資料表會繼續 toogrow。</span><span class="sxs-lookup"><span data-stu-id="37321-145">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span>

<span data-ttu-id="37321-146">當您要使用 hello 入口網站來建立叢集時，我們強烈建議您下載 hello 範本**按一下 [確定] 之前**toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="37321-146">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="37321-147">如需詳細資訊，請參閱太[使用 Azure Resource Manager 範本設定 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="37321-147">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="37321-148">更新版本中，因為您無法使用 hello 入口網站進行一些變更，您將需要 hello toomake 變更 」 範本。</span><span class="sxs-lookup"><span data-stu-id="37321-148">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

<span data-ttu-id="37321-149">您可以使用下列步驟的 hello，從 hello 入口網站匯出範本。</span><span class="sxs-lookup"><span data-stu-id="37321-149">You can export templates from hello portal by using hello following steps.</span></span> <span data-ttu-id="37321-150">不過，這些範本可以是 toouse 更加困難，因為它們可能會遺失必要的資訊的 null 值。</span><span class="sxs-lookup"><span data-stu-id="37321-150">However, these templates can be more difficult toouse because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="37321-151">開啟您的資源群組。</span><span class="sxs-lookup"><span data-stu-id="37321-151">Open your resource group.</span></span>
2. <span data-ttu-id="37321-152">選取**設定**toodisplay hello 設定面板。</span><span class="sxs-lookup"><span data-stu-id="37321-152">Select **Settings** toodisplay hello settings panel.</span></span>
3. <span data-ttu-id="37321-153">選取**部署**toodisplay hello 部署歷程記錄面板。</span><span class="sxs-lookup"><span data-stu-id="37321-153">Select **Deployments** toodisplay hello deployment history panel.</span></span>
4. <span data-ttu-id="37321-154">選取 hello 部署的部署 toodisplay hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="37321-154">Select a deployment toodisplay hello details of hello deployment.</span></span>
5. <span data-ttu-id="37321-155">選取**匯出範本**toodisplay hello 範本面板。</span><span class="sxs-lookup"><span data-stu-id="37321-155">Select **Export Template** toodisplay hello template panel.</span></span>
6. <span data-ttu-id="37321-156">選取**儲存 toofile** tooexport 包含 hello 範本、 參數和 PowerShell 檔案的.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="37321-156">Select **Save toofile** tooexport a .zip file that contains hello template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="37321-157">匯出 hello 檔案之後，您會需要 toomake 所做的修改。</span><span class="sxs-lookup"><span data-stu-id="37321-157">After you export hello files, you need toomake a modification.</span></span> <span data-ttu-id="37321-158">編輯 hello parameters.json 檔案，並移除 hello **adminPassword**項目。</span><span class="sxs-lookup"><span data-stu-id="37321-158">Edit hello parameters.json file and remove hello **adminPassword** element.</span></span> <span data-ttu-id="37321-159">Hello 部署指令碼執行時，這會導致 hello 密碼的提示。</span><span class="sxs-lookup"><span data-stu-id="37321-159">This will cause a prompt for hello password when hello deployment script is run.</span></span> <span data-ttu-id="37321-160">如果您執行 hello 部署指令碼，您可能必須 toofix null 參數值。</span><span class="sxs-lookup"><span data-stu-id="37321-160">When you're running hello deployment script, you might have toofix null parameter values.</span></span>

<span data-ttu-id="37321-161">toouse hello 下載範本 tooupdate 設定：</span><span class="sxs-lookup"><span data-stu-id="37321-161">toouse hello downloaded template tooupdate a configuration:</span></span>

1. <span data-ttu-id="37321-162">擷取本機電腦上的 hello 內容 tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="37321-162">Extract hello contents tooa folder on your local computer.</span></span>
2. <span data-ttu-id="37321-163">修改 hello 內容 tooreflect hello 新組態。</span><span class="sxs-lookup"><span data-stu-id="37321-163">Modify hello contents tooreflect hello new configuration.</span></span>
3. <span data-ttu-id="37321-164">啟動 PowerShell 並變更 toohello 資料夾解壓縮 hello 內容的位置。</span><span class="sxs-lookup"><span data-stu-id="37321-164">Start PowerShell and change toohello folder where you extracted hello content.</span></span>
4. <span data-ttu-id="37321-165">執行**deploy.ps1**並填入 hello 訂用帳戶 ID，hello 資源群組名稱 (使用 hello 相同 tooupdate hello 組態的名稱)，以及獨特的部署名稱。</span><span class="sxs-lookup"><span data-stu-id="37321-165">Run **deploy.ps1** and fill in hello subscription ID, hello resource group name (use hello same name tooupdate hello configuration), and a unique deployment name.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="37321-166">使用 Azure Resource Manager 部署 hello 診斷延伸模組，建立叢集的一部分</span><span class="sxs-lookup"><span data-stu-id="37321-166">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="37321-167">toocreate 叢集中使用資源管理員，您需要 tooadd hello 診斷組態 JSON toohello 完整的叢集資源管理員範本，才能建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="37321-167">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="37321-168">我們提供診斷組態加入範例五個 VM 叢集資源管理員範本 tooit 我們的資源管理員範本範例的一部分。</span><span class="sxs-lookup"><span data-stu-id="37321-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="37321-169">您可以查看 hello Azure 範例庫中的此位置：[診斷資源管理員範本 」 範例使用五個節點叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)。</span><span class="sxs-lookup"><span data-stu-id="37321-169">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="37321-170">在 hello Resource Manager 範本、 開啟 hello azuredeploy.json 檔案，並搜尋 toosee hello 診斷設定**IaaSDiagnostics**。</span><span class="sxs-lookup"><span data-stu-id="37321-170">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="37321-171">使用此範本，選取 hello 叢集 toocreate**部署 tooAzure**按鈕位於 hello 前一個連結。</span><span class="sxs-lookup"><span data-stu-id="37321-171">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="37321-172">或者，下載 hello 資源管理員的範例，請變更 tooit 和 hello 修改的範本以建立叢集，利用 hello `New-AzureRmResourceGroupDeployment` Azure PowerShell 視窗中命令。</span><span class="sxs-lookup"><span data-stu-id="37321-172">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="37321-173">請參閱下列程式碼，您傳遞 toohello 命令中的 hello 參數 hello。</span><span class="sxs-lookup"><span data-stu-id="37321-173">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="37321-174">如需如何 toodeploy 資源群組使用 PowerShell 的詳細資訊，請參閱 hello 文章[部署的資源群組與 hello Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="37321-174">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="37321-175">部署 hello 診斷延伸模組 tooan 現有叢集</span><span class="sxs-lookup"><span data-stu-id="37321-175">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="37321-176">如果您有現有的叢集沒有診斷部署，或如果您想 toomodify 現有的組態，您可以新增或更新它。</span><span class="sxs-lookup"><span data-stu-id="37321-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="37321-177">修改是使用的 toocreate hello 現有叢集的 hello Resource Manager 範本，或從稍早所述的 hello 入口網站下載 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="37321-177">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="37321-178">執行下列工作的 hello 修改 hello template.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="37321-178">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="37321-179">加入 toohello 資源 > 一節，以將新的儲存體資源 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="37321-179">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="37321-180">接下來，加入 toohello 參數之間區段只在 hello 儲存體帳戶定義之後,`supportLogStorageAccountName`和`vmNodeType0Name`。</span><span class="sxs-lookup"><span data-stu-id="37321-180">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="37321-181">Hello 預留位置文字取代*此處為儲存體帳戶名稱*與 hello hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="37321-181">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

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
<span data-ttu-id="37321-182">接著，更新 hello `VirtualMachineProfile` hello template.json 檔案，加入下列程式碼 hello 擴充功能陣列中的 hello 區段。</span><span class="sxs-lookup"><span data-stu-id="37321-182">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="37321-183">是確定 tooadd 逗號 hello 開頭或 hello 結束時，根據插入的位置。</span><span class="sxs-lookup"><span data-stu-id="37321-183">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="37321-184">您修改所述的 hello template.json 檔案之後，重新發行 hello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="37321-184">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="37321-185">如果匯出的 hello 範本，執行 hello deploy.ps1 檔案再重新發行 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="37321-185">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="37321-186">部署之後，請確認 **ProvisioningState** 為 **Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="37321-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-toocollect-health-and-load-events"></a><span data-ttu-id="37321-187">更新的診斷 toocollect 健全狀況和負載事件</span><span class="sxs-lookup"><span data-stu-id="37321-187">Update diagnostics toocollect health and load events</span></span>

<span data-ttu-id="37321-188">從 Service Fabric 的 hello 5.4 版開始，健全狀況和負載度量事件可用於集合。</span><span class="sxs-lookup"><span data-stu-id="37321-188">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="37321-189">這些事件會反映使用 hello 健全狀況所 hello 系統或您的程式碼產生的事件或載入報表的應用程式開發介面，例如[ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx)或[ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx)。</span><span class="sxs-lookup"><span data-stu-id="37321-189">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="37321-190">這可讓您彙總及檢視一段時間的系統健康情況，以及根據健康情況或負載事件發出警示。</span><span class="sxs-lookup"><span data-stu-id="37321-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="37321-191">Visual Studio 的診斷事件檢視器中的這些事件新增的 tooview"Microsoft-ServiceFabric:4:0x4000000000000008"toohello ETW 提供者清單。</span><span class="sxs-lookup"><span data-stu-id="37321-191">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="37321-192">toocollect hello 事件，修改 hello 資源管理員範本 tooinclude</span><span class="sxs-lookup"><span data-stu-id="37321-192">toocollect hello events, modify hello resource manager template tooinclude</span></span>

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="37321-193">更新診斷 toocollect 並上傳新的 EventSource 通道的記錄檔</span><span class="sxs-lookup"><span data-stu-id="37321-193">Update Diagnostics toocollect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="37321-194">tooupdate 診斷 toocollect 記錄檔，從代表即將 toodeploy，新的應用程式的新 EventSource 通道執行相同步驟 hello 與 hello[上一節](#deploywadarm)現有的安裝程式的診斷資訊叢集。</span><span class="sxs-lookup"><span data-stu-id="37321-194">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as in hello [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="37321-195">更新 hello`EtwEventSourceProviderConfiguration`區段在 hello template.json 檔 tooadd 項目中針對使用 hello hello 新 EventSource 通道之前您要套用 hello 組態更新`New-AzureRmResourceGroupDeployment`PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="37321-195">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="37321-196">hello hello 事件來源名稱被定義為 hello Visual Studio 產生 ServiceEventSource.cs 檔案中的程式碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="37321-196">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="37321-197">例如，如果事件來源為我 Eventsource，加入 hello 我 Eventsource 中的下列程式碼 tooplace hello 事件，插入名為 MyDestinationTableName 資料表。</span><span class="sxs-lookup"><span data-stu-id="37321-197">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="37321-198">toocollect 效能計數器或事件記錄檔中，修改 hello Resource Manager 範本使用中提供的 hello 範例[使用監視和診斷的 Windows 虛擬機器建立使用 Azure Resource Manager 範本](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="37321-198">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="37321-199">然後，重新發行 hello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="37321-199">Then, republish hello Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37321-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37321-200">Next steps</span></span>
<span data-ttu-id="37321-201">更詳細的 toounderstand 時疑難排解問題，您應該尋找哪些事件請參閱 hello 診斷事件發出[Reliable Actors](service-fabric-reliable-actors-diagnostics.md)和[可靠服務](service-fabric-reliable-services-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="37321-201">toounderstand in more detail what events you should look for while troubleshooting issues, see hello diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="37321-202">相關文章</span><span class="sxs-lookup"><span data-stu-id="37321-202">Related articles</span></span>
* [<span data-ttu-id="37321-203">了解 toocollect 效能計數器或記錄檔使用 hello 診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="37321-203">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="37321-204">Log Analytics 中的 Service Fabric 解決方案</span><span class="sxs-lookup"><span data-stu-id="37321-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

