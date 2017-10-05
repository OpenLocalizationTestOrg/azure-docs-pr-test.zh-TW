---
title: "Azure Service Fabric 容器監視與診斷 | Microsoft Docs"
description: "了解如何使用 OMS 的容器解決方案監視與診斷在 Microsoft Azure Service Fabric 上協調的容器。"
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
ms.openlocfilehash: 874c1a5c4b399ff2254072b7282f05d83a005cc3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a><span data-ttu-id="c92ca-103">使用 OMS 監視 Windows Server 容器</span><span class="sxs-lookup"><span data-stu-id="c92ca-103">Monitoring Windows Server containers with OMS</span></span>

## <a name="oms-containers-solution"></a><span data-ttu-id="c92ca-104">OMS 容器解決方案</span><span class="sxs-lookup"><span data-stu-id="c92ca-104">OMS Containers Solution</span></span>

<span data-ttu-id="c92ca-105">Operations Management Suite (OMS) 小組發行了容器解決方案，用於診斷與監視容器。</span><span class="sxs-lookup"><span data-stu-id="c92ca-105">The Operations Management Suite (OMS) team has published a Containers solution for diagnostics and monitoring for containers.</span></span> <span data-ttu-id="c92ca-106">此解決方案加上其 Service Fabric 解決方案是很棒的工具，可監視在 Service Fabric 上協調的容器部署。</span><span class="sxs-lookup"><span data-stu-id="c92ca-106">Alongside their Service Fabric solution, this solution is a great tool to monitor container deployments orchestrated on Service Fabric.</span></span> <span data-ttu-id="c92ca-107">以下是解決方案中儀表板外觀的簡單範例︰</span><span class="sxs-lookup"><span data-stu-id="c92ca-107">Here's a simple example of what the dashboard in the solution looks like:</span></span>

![基本 OMS 儀表板](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

<span data-ttu-id="c92ca-109">它也會收集各種可使用 OMS Log Analytics 工具查詢的記錄，並可用於視覺化任何正在產生的計量或事件。</span><span class="sxs-lookup"><span data-stu-id="c92ca-109">It also collects different kinds of logs that can be queried in the OMS Log Analytics tool, and can be used to visualize any metrics or events being generated.</span></span> <span data-ttu-id="c92ca-110">所收集的記錄類型有：</span><span class="sxs-lookup"><span data-stu-id="c92ca-110">The log types that are collected are:</span></span>

1. <span data-ttu-id="c92ca-111">ContainerInventory︰顯示容器位置、名稱和映像的相關資訊</span><span class="sxs-lookup"><span data-stu-id="c92ca-111">ContainerInventory: shows information about container location, name, and images</span></span>
2. <span data-ttu-id="c92ca-112">ContainerImageInventory︰已部署映像相關資訊，包括 ID 或大小</span><span class="sxs-lookup"><span data-stu-id="c92ca-112">ContainerImageInventory: information about deployed images, including IDs or sizes</span></span>
3. <span data-ttu-id="c92ca-113">ContainerLog︰特定的錯誤記錄檔、 docker 記錄檔 (stdout 等) 及其他項目</span><span class="sxs-lookup"><span data-stu-id="c92ca-113">ContainerLog: specific error logs, docker logs (stdout, etc.), and other entries</span></span>
4. <span data-ttu-id="c92ca-114">ContainerServiceLog：已執行的 docker 精露命令</span><span class="sxs-lookup"><span data-stu-id="c92ca-114">ContainerServiceLog: docker daemon commands that have been run</span></span>
5. <span data-ttu-id="c92ca-115">效能︰包括容器 CPU、記憶體、網路流量、磁碟 I/O，以及主機電腦的自訂計量</span><span class="sxs-lookup"><span data-stu-id="c92ca-115">Perf: performance counters including container cpu, memory, network traffic, disk i/o, and custom metrics from the host machines</span></span>

<span data-ttu-id="c92ca-116">本文章涵蓋為您的叢集設定容器監視所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="c92ca-116">This article covers the steps required to set up container monitoring for your cluster.</span></span> <span data-ttu-id="c92ca-117">若要深入了解 OMS 的容器解決方案，請參閱其[文件](../log-analytics/log-analytics-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="c92ca-117">To learn more about OMS's Containers solution, check out their [documentation](../log-analytics/log-analytics-containers.md).</span></span>

## <a name="1-set-up-a-service-fabric-cluster"></a><span data-ttu-id="c92ca-118">1.設定 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="c92ca-118">1. Set up a Service Fabric cluster</span></span>

<span data-ttu-id="c92ca-119">使用[此處](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample)的 Azure Resource Manager 範本建立叢集。</span><span class="sxs-lookup"><span data-stu-id="c92ca-119">Create a cluster using the Azure Resource Manager template found [here](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample).</span></span> <span data-ttu-id="c92ca-120">務必新增唯一的 OMS 工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="c92ca-120">Make sure to add a unique OMS workspace name.</span></span> <span data-ttu-id="c92ca-121">此範本也預設為將叢集部署在 Service Fabric (v255.255) 的預覽組建中，這表示它無法用於生產中，且無法升級為不同的 Service Fabric 版本。</span><span class="sxs-lookup"><span data-stu-id="c92ca-121">This template also defaults to deploying a cluster in the preview build of Service Fabric (v255.255), which means that it cannot be used in production, and cannot be upgraded to a different Service Fabric version.</span></span> <span data-ttu-id="c92ca-122">如果您決定要長期使用此範本或用於生產，請將版本變更為穩定的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="c92ca-122">If you decide to use this template for long-term or production use, change the version to a stable version number.</span></span>

<span data-ttu-id="c92ca-123">叢集設定完畢後，確認您已安裝適當的憑證，並確定您可以連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="c92ca-123">Once the cluster is set up, confirm that you have installed the appropriate certificate, and make sure you are able to connect to the cluster.</span></span>

<span data-ttu-id="c92ca-124">前往 [Azure 入口網站](https://portal.azure.com/)並尋找部署，以確認您的資源群組設定正確。</span><span class="sxs-lookup"><span data-stu-id="c92ca-124">Confirm that your Resource Group is set up correctly by heading to the [Azure portal](https://portal.azure.com/) and finding the deployment.</span></span> <span data-ttu-id="c92ca-125">資源群組應該包含所有 Service Fabric 資源，亦擁有 Log Analytics 解決方案及 Service Fabric 解決方案。</span><span class="sxs-lookup"><span data-stu-id="c92ca-125">The resource group should contain all the Service Fabric resources, and also have a Log Analytics solution as well as a Service Fabric solution.</span></span>

<span data-ttu-id="c92ca-126">如需修改現有的 Service Fabric 叢集：</span><span class="sxs-lookup"><span data-stu-id="c92ca-126">For modifying an existing Service Fabric cluster:</span></span>
* <span data-ttu-id="c92ca-127">確認已啟用診斷功能 (如果沒有，請透過[更新虛擬機器擴展集](/rest/api/virtualmachinescalesets/create-or-update-a-set)啟用)</span><span class="sxs-lookup"><span data-stu-id="c92ca-127">Confirm that Diagnostics is enabled (if not, enable it via [updating the virtual machine scale set](/rest/api/virtualmachinescalesets/create-or-update-a-set))</span></span>
* <span data-ttu-id="c92ca-128">透過 Azure Marketplace 建立「Service Fabric 分析」解決方案來新增 OMS 工作區</span><span class="sxs-lookup"><span data-stu-id="c92ca-128">Add an OMS Workspace by creating a "Service Fabric Analytics" solution via the Azure Marketplace</span></span>
* <span data-ttu-id="c92ca-129">編輯 Service Fabric 解決方案的資料來源，藉此在叢集所在的資源群組中，從適當的 Azure 儲存體資料表 (由 WAD 設定) 中挑選資料</span><span class="sxs-lookup"><span data-stu-id="c92ca-129">Edit the data sources of the Service Fabric solution to pick up data from the appropriate Azure Storage tables (set up by WAD) in the Resource Group that the cluster is in</span></span>
* <span data-ttu-id="c92ca-130">透過 PowerShell 或藉由更新虛擬機器擴展集，以新增代理程式做為[虛擬機器擴展集的延伸模組](/powershell/module/azurerm.compute/add-azurermvmssextension) (與上述相同的連結，可修改 Resource Manager 範本)</span><span class="sxs-lookup"><span data-stu-id="c92ca-130">Add the agent as an [extension to the virtual machine scale set](/powershell/module/azurerm.compute/add-azurermvmssextension) via PowerShell or through updating the virtual machine scale set (same link as above, to modify the Resource Manager template)</span></span>

## <a name="2-deploy-a-container"></a><span data-ttu-id="c92ca-131">2.部署容器</span><span class="sxs-lookup"><span data-stu-id="c92ca-131">2. Deploy a container</span></span>

<span data-ttu-id="c92ca-132">一旦叢集已就緒且您已確認可以存取叢集，請將容器部署至叢集。</span><span class="sxs-lookup"><span data-stu-id="c92ca-132">Once the cluster is ready and you have confirmed that you can access it, deploy a container to it.</span></span> <span data-ttu-id="c92ca-133">如果您選擇使用該範本所設定的預覽版本，您也可以探索 Service Fabric 的新 Docker Compose 功能。</span><span class="sxs-lookup"><span data-stu-id="c92ca-133">If you chose to use the preview version as set by the template, you can also explore Service Fabric's new docker compose functionality.</span></span> <span data-ttu-id="c92ca-134">請記住，第一次將容器映像部署至叢集時，須花費數分鐘時間下載影像，視其大小而定。</span><span class="sxs-lookup"><span data-stu-id="c92ca-134">Bear in mind that the first time a container image is deployed to a cluster, it takes several minutes to download the image depending on its size.</span></span>

## <a name="3-add-the-containers-solution"></a><span data-ttu-id="c92ca-135">3.新增容器解決方案</span><span class="sxs-lookup"><span data-stu-id="c92ca-135">3. Add the Containers solution</span></span>

<span data-ttu-id="c92ca-136">在 Azure 入口網站中，透過 Azure Marketplace 建立容器資源 (在 [監視 + 管理] 類別下)。</span><span class="sxs-lookup"><span data-stu-id="c92ca-136">In the Azure portal, create a Containers resource (under the Monitoring + Management category) through Azure Marketplace.</span></span> 

![新增容器解決方案](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

<span data-ttu-id="c92ca-138">在建立步驟中，它會要求 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="c92ca-138">In the creation step, it requests an OMS workspace.</span></span> <span data-ttu-id="c92ca-139">選取以上述部署建立的工作區。</span><span class="sxs-lookup"><span data-stu-id="c92ca-139">Select the one that was created with the deployment above.</span></span> <span data-ttu-id="c92ca-140">此步驟會在您的 OMS 工作區中建立容器解決方案，且由範本所建立的 OMS 代理程式會自動偵測。</span><span class="sxs-lookup"><span data-stu-id="c92ca-140">This step adds a Containers solution within your OMS workspace, and is automatically detected by the OMS agent deployed by the template.</span></span> <span data-ttu-id="c92ca-141">代理程式會開始收集叢集中容器處理序的資料，並在約 10-15 分鐘內開始，您應看見解決方案因資料而增色，如上方儀表板圖所示。</span><span class="sxs-lookup"><span data-stu-id="c92ca-141">The agent will start gathering data on the containers processes in the cluster, and in about 10-15 minutes, you should see the solution light up with data as in the image of the dashboard above.</span></span>

## <a name="4-next-steps"></a><span data-ttu-id="c92ca-142">4.後續步驟</span><span class="sxs-lookup"><span data-stu-id="c92ca-142">4. Next steps</span></span>

<span data-ttu-id="c92ca-143">OMS 在工作區中提供各種工具，讓工作區對您更有幫助。</span><span class="sxs-lookup"><span data-stu-id="c92ca-143">OMS offers various tools in the workspace to make if more useful for you.</span></span> <span data-ttu-id="c92ca-144">瀏覽以下選項，以依照您的需求自訂解決方案：</span><span class="sxs-lookup"><span data-stu-id="c92ca-144">Explore the following options to customize the solution to your needs:</span></span>
- <span data-ttu-id="c92ca-145">熟悉 Log Analytics 的[記錄搜尋和查詢](../log-analytics/log-analytics-log-searches.md)功能</span><span class="sxs-lookup"><span data-stu-id="c92ca-145">Get familiarized with the [log search and querying](../log-analytics/log-analytics-log-searches.md) features offered as part of Log Analytics</span></span>
- <span data-ttu-id="c92ca-146">設定 OMS 代理程式以挑選特定的效能計數器 (移至工作區 [首頁] > [設定] > [資料] > [Windows 效能計數器])</span><span class="sxs-lookup"><span data-stu-id="c92ca-146">Configure the OMS agent to pick up specific performance counters (go to the workspace Home > Settings > Data > Windows Performance Counters)</span></span>
- <span data-ttu-id="c92ca-147">設定 OMS 以設定[自動化警示](../log-analytics/log-analytics-alerts.md)規則，來協助偵測與診斷</span><span class="sxs-lookup"><span data-stu-id="c92ca-147">Configure OMS to set up [automated alerting](../log-analytics/log-analytics-alerts.md) rules to aid in detecting and diagnostics</span></span>