---
title: "aaaAzure 服務網狀架構容器監視和診斷 |Microsoft 文件"
description: "深入了解如何 toomonitor 並診斷在 Microsoft Azure Service Fabric 協調與 OMS 的容器解決方案的容器。"
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
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a><span data-ttu-id="070fe-103">使用 OMS 監視 Windows Server 容器</span><span class="sxs-lookup"><span data-stu-id="070fe-103">Monitoring Windows Server containers with OMS</span></span>

## <a name="oms-containers-solution"></a><span data-ttu-id="070fe-104">OMS 容器解決方案</span><span class="sxs-lookup"><span data-stu-id="070fe-104">OMS Containers Solution</span></span>

<span data-ttu-id="070fe-105">hello Operations Management Suite (OMS) 小組已發行容器解決方案，以診斷和監視的容器。</span><span class="sxs-lookup"><span data-stu-id="070fe-105">hello Operations Management Suite (OMS) team has published a Containers solution for diagnostics and monitoring for containers.</span></span> <span data-ttu-id="070fe-106">Service Fabric 方案，連同此方案處於協調服務網狀架構上很棒的工具 toomonitor 容器部署。</span><span class="sxs-lookup"><span data-stu-id="070fe-106">Alongside their Service Fabric solution, this solution is a great tool toomonitor container deployments orchestrated on Service Fabric.</span></span> <span data-ttu-id="070fe-107">以下是 hello 方案中的哪些 hello 儀表板看起來像的簡單範例：</span><span class="sxs-lookup"><span data-stu-id="070fe-107">Here's a simple example of what hello dashboard in hello solution looks like:</span></span>

![基本 OMS 儀表板](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

<span data-ttu-id="070fe-109">它也會收集不同類型的記錄檔所能查詢在 hello OMS 記錄分析工具中，而且可以使用的 toovisualize 任何度量或正在產生的事件。</span><span class="sxs-lookup"><span data-stu-id="070fe-109">It also collects different kinds of logs that can be queried in hello OMS Log Analytics tool, and can be used toovisualize any metrics or events being generated.</span></span> <span data-ttu-id="070fe-110">hello 所收集的記錄類型包括：</span><span class="sxs-lookup"><span data-stu-id="070fe-110">hello log types that are collected are:</span></span>

1. <span data-ttu-id="070fe-111">ContainerInventory︰顯示容器位置、名稱和映像的相關資訊</span><span class="sxs-lookup"><span data-stu-id="070fe-111">ContainerInventory: shows information about container location, name, and images</span></span>
2. <span data-ttu-id="070fe-112">ContainerImageInventory︰已部署映像相關資訊，包括 ID 或大小</span><span class="sxs-lookup"><span data-stu-id="070fe-112">ContainerImageInventory: information about deployed images, including IDs or sizes</span></span>
3. <span data-ttu-id="070fe-113">ContainerLog︰特定的錯誤記錄檔、 docker 記錄檔 (stdout 等) 及其他項目</span><span class="sxs-lookup"><span data-stu-id="070fe-113">ContainerLog: specific error logs, docker logs (stdout, etc.), and other entries</span></span>
4. <span data-ttu-id="070fe-114">ContainerServiceLog：已執行的 docker 精露命令</span><span class="sxs-lookup"><span data-stu-id="070fe-114">ContainerServiceLog: docker daemon commands that have been run</span></span>
5. <span data-ttu-id="070fe-115">效能： 包括容器效能計數器 cpu、 記憶體、 網路流量、 磁碟 i/o 和自訂度量以從 hello 裝載機器</span><span class="sxs-lookup"><span data-stu-id="070fe-115">Perf: performance counters including container cpu, memory, network traffic, disk i/o, and custom metrics from hello host machines</span></span>

<span data-ttu-id="070fe-116">本文涵蓋 hello 步驟需要的 tooset 容器監視您的叢集設定。</span><span class="sxs-lookup"><span data-stu-id="070fe-116">This article covers hello steps required tooset up container monitoring for your cluster.</span></span> <span data-ttu-id="070fe-117">toolearn 更多關於 OMS 的容器解決方案，請參閱其[文件](../log-analytics/log-analytics-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="070fe-117">toolearn more about OMS's Containers solution, check out their [documentation](../log-analytics/log-analytics-containers.md).</span></span>

## <a name="1-set-up-a-service-fabric-cluster"></a><span data-ttu-id="070fe-118">1.設定 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="070fe-118">1. Set up a Service Fabric cluster</span></span>

<span data-ttu-id="070fe-119">使用找到的 hello Azure Resource Manager 範本建立叢集[這裡](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample)。</span><span class="sxs-lookup"><span data-stu-id="070fe-119">Create a cluster using hello Azure Resource Manager template found [here](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample).</span></span> <span data-ttu-id="070fe-120">請確定 tooadd 唯一的 OMS 工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="070fe-120">Make sure tooadd a unique OMS workspace name.</span></span> <span data-ttu-id="070fe-121">此範本也預設的 toodeploying hello 預覽中的叢集建立的 Service Fabric (v255.255)，也就是說，它不能用在生產環境中，並不能升級 tooa Service Fabric 版本不同。</span><span class="sxs-lookup"><span data-stu-id="070fe-121">This template also defaults toodeploying a cluster in hello preview build of Service Fabric (v255.255), which means that it cannot be used in production, and cannot be upgraded tooa different Service Fabric version.</span></span> <span data-ttu-id="070fe-122">如果您決定 toouse 這個範本的長期或生產環境使用，請變更 hello 版本 tooa 穩定版本號碼。</span><span class="sxs-lookup"><span data-stu-id="070fe-122">If you decide toouse this template for long-term or production use, change hello version tooa stable version number.</span></span>

<span data-ttu-id="070fe-123">一旦設定 hello 叢集之後，請確認您已安裝 hello 適當的憑證，並確定您能夠 tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="070fe-123">Once hello cluster is set up, confirm that you have installed hello appropriate certificate, and make sure you are able tooconnect toohello cluster.</span></span>

<span data-ttu-id="070fe-124">確認您的資源群組已正確設定，時的標題 toohello [Azure 入口網站](https://portal.azure.com/)和尋找 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="070fe-124">Confirm that your Resource Group is set up correctly by heading toohello [Azure portal](https://portal.azure.com/) and finding hello deployment.</span></span> <span data-ttu-id="070fe-125">hello 資源群組應該包含所有的 hello 服務網狀架構資源，而且也有 記錄分析解決方案，以及服務網狀架構方案。</span><span class="sxs-lookup"><span data-stu-id="070fe-125">hello resource group should contain all hello Service Fabric resources, and also have a Log Analytics solution as well as a Service Fabric solution.</span></span>

<span data-ttu-id="070fe-126">如需修改現有的 Service Fabric 叢集：</span><span class="sxs-lookup"><span data-stu-id="070fe-126">For modifying an existing Service Fabric cluster:</span></span>
* <span data-ttu-id="070fe-127">確認已啟用診斷 (如果沒有，請啟用它透過[更新 hello 虛擬機器規模集](/rest/api/virtualmachinescalesets/create-or-update-a-set))</span><span class="sxs-lookup"><span data-stu-id="070fe-127">Confirm that Diagnostics is enabled (if not, enable it via [updating hello virtual machine scale set](/rest/api/virtualmachinescalesets/create-or-update-a-set))</span></span>
* <span data-ttu-id="070fe-128">建立透過 hello Azure Marketplace 以 「 服務網狀架構分析 」 解決方案加入 OMS 工作區</span><span class="sxs-lookup"><span data-stu-id="070fe-128">Add an OMS Workspace by creating a "Service Fabric Analytics" solution via hello Azure Marketplace</span></span>
* <span data-ttu-id="070fe-129">在 hello hello 叢集的資源群組處於中編輯 hello hello Service Fabric 方案 toopick hello （設定 wad） 適當 Azure 儲存體資料表中資料的資料來源</span><span class="sxs-lookup"><span data-stu-id="070fe-129">Edit hello data sources of hello Service Fabric solution toopick up data from hello appropriate Azure Storage tables (set up by WAD) in hello Resource Group that hello cluster is in</span></span>
* <span data-ttu-id="070fe-130">加入 hello 代理程式做為[延伸 toohello 虛擬機器規模集](/powershell/module/azurerm.compute/add-azurermvmssextension)透過 PowerShell 或透過更新 hello 的虛擬機器規模集 （上述的相同連結、 toomodify hello Resource Manager 範本）</span><span class="sxs-lookup"><span data-stu-id="070fe-130">Add hello agent as an [extension toohello virtual machine scale set](/powershell/module/azurerm.compute/add-azurermvmssextension) via PowerShell or through updating hello virtual machine scale set (same link as above, toomodify hello Resource Manager template)</span></span>

## <a name="2-deploy-a-container"></a><span data-ttu-id="070fe-131">2.部署容器</span><span class="sxs-lookup"><span data-stu-id="070fe-131">2. Deploy a container</span></span>

<span data-ttu-id="070fe-132">Hello 叢集已就緒，而且在您確認您可以存取它，一旦部署容器 tooit。</span><span class="sxs-lookup"><span data-stu-id="070fe-132">Once hello cluster is ready and you have confirmed that you can access it, deploy a container tooit.</span></span> <span data-ttu-id="070fe-133">如果您選擇 toouse hello 預覽版本所設定的 hello 範本，您也可以探索 Service Fabric 新 docker 撰寫功能。</span><span class="sxs-lookup"><span data-stu-id="070fe-133">If you chose toouse hello preview version as set by hello template, you can also explore Service Fabric's new docker compose functionality.</span></span> <span data-ttu-id="070fe-134">要記住 hello 第一次的容器映像部署的 tooa 叢集，花幾分鐘的時間 toodownload hello 映像依據其大小。</span><span class="sxs-lookup"><span data-stu-id="070fe-134">Bear in mind that hello first time a container image is deployed tooa cluster, it takes several minutes toodownload hello image depending on its size.</span></span>

## <a name="3-add-hello-containers-solution"></a><span data-ttu-id="070fe-135">3.新增 hello 容器解決方案</span><span class="sxs-lookup"><span data-stu-id="070fe-135">3. Add hello Containers solution</span></span>

<span data-ttu-id="070fe-136">在 hello Azure 入口網站中建立容器的資源 (在 hello 監視 + 管理類別目錄) 透過 Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="070fe-136">In hello Azure portal, create a Containers resource (under hello Monitoring + Management category) through Azure Marketplace.</span></span> 

![新增容器解決方案](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

<span data-ttu-id="070fe-138">在 hello 建立步驟中，它會要求 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="070fe-138">In hello creation step, it requests an OMS workspace.</span></span> <span data-ttu-id="070fe-139">選取 hello 與 hello 部署上面所建立。</span><span class="sxs-lookup"><span data-stu-id="070fe-139">Select hello one that was created with hello deployment above.</span></span> <span data-ttu-id="070fe-140">此步驟新增您的 OMS 工作區中的容器解決方案，並會自動偵測 hello 範本所部署的 hello OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="070fe-140">This step adds a Containers solution within your OMS workspace, and is automatically detected by hello OMS agent deployed by hello template.</span></span> <span data-ttu-id="070fe-141">hello 代理程式會開始收集資料 hello hello 叢集中的容器處理程序，並在 10-15 分鐘內，您應該會看到 hello 方案亮燈如 hello 映像的 hello 儀表板上面所示的資料。</span><span class="sxs-lookup"><span data-stu-id="070fe-141">hello agent will start gathering data on hello containers processes in hello cluster, and in about 10-15 minutes, you should see hello solution light up with data as in hello image of hello dashboard above.</span></span>

## <a name="4-next-steps"></a><span data-ttu-id="070fe-142">4.後續步驟</span><span class="sxs-lookup"><span data-stu-id="070fe-142">4. Next steps</span></span>

<span data-ttu-id="070fe-143">OMS 提供各種工具，在 [hello] 工作區 toomake 如果更有用了。</span><span class="sxs-lookup"><span data-stu-id="070fe-143">OMS offers various tools in hello workspace toomake if more useful for you.</span></span> <span data-ttu-id="070fe-144">瀏覽下列選項 toocustomize hello 方案 tooyour 需求 hello:</span><span class="sxs-lookup"><span data-stu-id="070fe-144">Explore hello following options toocustomize hello solution tooyour needs:</span></span>
- <span data-ttu-id="070fe-145">取得以 hello 請[記錄搜尋和查詢](../log-analytics/log-analytics-log-searches.md)做為記錄分析的一部分提供的功能</span><span class="sxs-lookup"><span data-stu-id="070fe-145">Get familiarized with hello [log search and querying](../log-analytics/log-analytics-log-searches.md) features offered as part of Log Analytics</span></span>
- <span data-ttu-id="070fe-146">設定特定的效能計數器向上 hello OMS 代理程式 toopick (移 toohello 工作區首頁 > 設定 > 資料 > Windows 效能計數器)</span><span class="sxs-lookup"><span data-stu-id="070fe-146">Configure hello OMS agent toopick up specific performance counters (go toohello workspace Home > Settings > Data > Windows Performance Counters)</span></span>
- <span data-ttu-id="070fe-147">設定 OMS tooset[自動化警示](../log-analytics/log-analytics-alerts.md)規則 tooaid 中偵測及診斷</span><span class="sxs-lookup"><span data-stu-id="070fe-147">Configure OMS tooset up [automated alerting](../log-analytics/log-analytics-alerts.md) rules tooaid in detecting and diagnostics</span></span>
