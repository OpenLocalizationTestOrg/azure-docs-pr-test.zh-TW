---
title: "針對 Azure 虛擬網路閘道和連線進行疑難排解 - PowerShell | Microsoft Docs"
description: "此頁面說明如何使用 Azure 網路監看員來針對 PowerShell Cmdlet 進行疑難排解"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: e135e719d8f267f6a189d0f8a903a49980a5a035
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="dcb0b-103">使用 Azure 網路監看員 PowerShell 來針對虛擬網路閘道和連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="dcb0b-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="dcb0b-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="dcb0b-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="dcb0b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcb0b-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="dcb0b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="dcb0b-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="dcb0b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dcb0b-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="dcb0b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="dcb0b-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="dcb0b-109">網路監看員提供了許多功能，因為它的作用就是為了讓您了解您在 Azure 中的網路資源。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="dcb0b-110">這些功能的其中之一便是資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="dcb0b-111">您可以透過入口網站、PowerShell、CLI 或 REST API 呼叫資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="dcb0b-112">一經呼叫，網路監看員就會檢查虛擬網路閘道或連線的健全狀況，並傳回其調查結果。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dcb0b-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="dcb0b-113">Before you begin</span></span>

<span data-ttu-id="dcb0b-114">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="dcb0b-115">如需支援的閘道類型清單，請瀏覽[支援的閘道類型](network-watcher-troubleshoot-overview.md#supported-gateway-types)。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="dcb0b-116">概觀</span><span class="sxs-lookup"><span data-stu-id="dcb0b-116">Overview</span></span>

<span data-ttu-id="dcb0b-117">資源疑難排解可讓您針對虛擬網路閘道和連線所發生的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="dcb0b-118">在要求進行資源疑難排解後，便會查詢並檢查記錄。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="dcb0b-119">檢查完成時，就會傳回結果。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="dcb0b-120">資源疑難排解要求是執行時間很長的要求，可能需要幾分鐘的時間才會傳回結果。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="dcb0b-121">疑難排解記錄會儲存在指定儲存體帳戶的容器中。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="dcb0b-122">針對閘道或連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="dcb0b-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="dcb0b-123">瀏覽至 [Azure 入口網站](https://portal.azure.com)然後按一下 [網路] > [網路監看員] > [VPN 診斷]</span><span class="sxs-lookup"><span data-stu-id="dcb0b-123">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="dcb0b-124">選取 [訂用帳戶]、[資源群組] 和 [位置]。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="dcb0b-125">資源疑難排解會傳回有關資源健康情況的資料。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-125">Resource troubleshooting returns data about the health of the resource.</span></span> <span data-ttu-id="dcb0b-126">它也會將相關的記錄儲存至儲存體帳戶以供檢閱。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-126">It also saves relevant logs to a storage account to be reviewed.</span></span> <span data-ttu-id="dcb0b-127">按一下 [儲存體帳戶] 以選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-127">Click **Storage Account** to select a storage account.</span></span>
4. <span data-ttu-id="dcb0b-128">在 [儲存體帳戶] 刀鋒視窗上，選取現有的儲存體帳戶，或按一下 [+ 儲存體帳戶] 來建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-128">On the **Storage accounts** blade, select an existing storage account or click **+ Storage account** to create a new one.</span></span>
5. <span data-ttu-id="dcb0b-129">在 [容器] 刀鋒視窗上，選擇現有的容器，或按一下 [+ 容器] 來建立新的容器。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-129">On the **Containers** blade, choose an existing container or click **+ Container** to create a new container.</span></span> <span data-ttu-id="dcb0b-130">完成時，按一下 [選取]</span><span class="sxs-lookup"><span data-stu-id="dcb0b-130">When complete click **Select**</span></span>
6. <span data-ttu-id="dcb0b-131">選取要進行疑難排解的閘道和連線資源，並按一下 [開始疑難排解]</span><span class="sxs-lookup"><span data-stu-id="dcb0b-131">Select the Gateway and Connection resources to troubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="dcb0b-132">如果選取多個資源，系統會在這些閘道資源上同時執行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="dcb0b-133">它無法同時在連線及與其相關聯的閘道上執行。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-133">It can not run on a connection and it's associated gateway at the same time.</span></span> <span data-ttu-id="dcb0b-134">建議先針對閘道進行疑難排解，因為對連線進行疑難排解的程序會花上較久的時間。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-134">It is recommended to troubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="dcb0b-135">當 VPN 診斷在資源上執行時，[疑難排解狀態] 欄位會顯示 [正在執行] 的狀態</span><span class="sxs-lookup"><span data-stu-id="dcb0b-135">While VPN Diagnostics is running on a resource the **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="dcb0b-136">完成時，狀態欄位會變更為 [狀況良好] 或 [狀況不良]。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-136">When complete, the status column changes to **Healthy** or **Unhealthy**.</span></span>

![疑難排解完成][2]

## <a name="understanding-the-results"></a><span data-ttu-id="dcb0b-138">了解結果</span><span class="sxs-lookup"><span data-stu-id="dcb0b-138">Understanding the results</span></span>

<span data-ttu-id="dcb0b-139">在視窗的 [詳細資料] 區段中，[狀態] 索引標籤會針對所選的資源，顯示上次執行的疑難排解狀態。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-139">In the **Details** section of the window, the **Status** tab shows the status of the last troubleshooting run on the selected resource.</span></span> <span data-ttu-id="dcb0b-140">最新的診斷結果會顯示自上次執行後已經過 xx 分鐘。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-140">Results of the latest diagnostic are shown xx minutes after the last run.</span></span>

|<span data-ttu-id="dcb0b-141">屬性</span><span class="sxs-lookup"><span data-stu-id="dcb0b-141">Property</span></span>  |<span data-ttu-id="dcb0b-142">說明</span><span class="sxs-lookup"><span data-stu-id="dcb0b-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="dcb0b-143">資源</span><span class="sxs-lookup"><span data-stu-id="dcb0b-143">Resource</span></span>     | <span data-ttu-id="dcb0b-144">資源的連結。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-144">A link to the resource.</span></span>        |
|<span data-ttu-id="dcb0b-145">儲存體路徑</span><span class="sxs-lookup"><span data-stu-id="dcb0b-145">Storage path</span></span>     |  <span data-ttu-id="dcb0b-146">包含記錄檔的儲存體帳戶及容器的路徑 (若在執行期間有產生的話)。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-146">Path to the storage account and container that contain the logs (if any were produced during the run).</span></span> <span data-ttu-id="dcb0b-147">在您離開入口網站之後，此設定將不會保存。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-147">This setting does not persist after you leave the portal.</span></span>        |
|<span data-ttu-id="dcb0b-148">摘要</span><span class="sxs-lookup"><span data-stu-id="dcb0b-148">Summary</span></span>     | <span data-ttu-id="dcb0b-149">資源健康狀態的摘要。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-149">Summary of the resource health.</span></span>        |
|<span data-ttu-id="dcb0b-150">詳細資料</span><span class="sxs-lookup"><span data-stu-id="dcb0b-150">Detail</span></span>     | <span data-ttu-id="dcb0b-151">資源健康狀態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-151">Detailed information on the resource health.</span></span>        |
|<span data-ttu-id="dcb0b-152">上次執行</span><span class="sxs-lookup"><span data-stu-id="dcb0b-152">Last run</span></span>     | <span data-ttu-id="dcb0b-153">上次執行疑難排解的時間。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-153">The time the last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="dcb0b-154">[動作] 索引標籤會提供如何解決問題的一般指引。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-154">The **Action** tab provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="dcb0b-155">如果問題有可行動作，則會提供附有其他指引的連結。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-155">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="dcb0b-156">如果沒有其他指引，回應中會提供 URL 以供您開啟支援案例。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-156">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="dcb0b-157">如需回應屬性和所含內容的詳細資訊，請瀏覽[網路監看員疑難排解概觀](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="dcb0b-157">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="dcb0b-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dcb0b-158">Next steps</span></span>

<span data-ttu-id="dcb0b-159">如果設定已變更而停止了 VPN 連線，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)以追蹤可能有問題的網路安全性群組和安全性規則。</span><span class="sxs-lookup"><span data-stu-id="dcb0b-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
