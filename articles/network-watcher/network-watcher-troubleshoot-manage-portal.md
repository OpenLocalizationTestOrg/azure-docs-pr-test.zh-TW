---
title: "aaaTroubleshoot Azure 虛擬網路閘道與連線-PowerShell |Microsoft 文件"
description: "此頁面說明 toouse hello Azure 網路監看員如何疑難排解 PowerShell cmdlet"
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
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="85e82-103">使用 Azure 網路監看員 PowerShell 來針對虛擬網路閘道和連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="85e82-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="85e82-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="85e82-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="85e82-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85e82-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="85e82-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="85e82-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="85e82-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="85e82-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="85e82-108">REST API</span><span class="sxs-lookup"><span data-stu-id="85e82-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="85e82-109">網路監看員會提供許多功能與 toounderstanding 您在 Azure 中的網路資源。</span><span class="sxs-lookup"><span data-stu-id="85e82-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="85e82-110">這些功能的其中之一便是資源疑難排解。</span><span class="sxs-lookup"><span data-stu-id="85e82-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="85e82-111">疑難排解資源可以透過 hello 入口網站、 PowerShell、 CLI 或 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="85e82-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="85e82-112">呼叫時，網路監看員會檢查 hello 的虛擬網路閘道或連線的健全狀況，並傳回其發現。</span><span class="sxs-lookup"><span data-stu-id="85e82-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="85e82-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="85e82-113">Before you begin</span></span>

<span data-ttu-id="85e82-114">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="85e82-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="85e82-115">如需支援的閘道類型清單，請瀏覽[支援的閘道類型](network-watcher-troubleshoot-overview.md#supported-gateway-types)。</span><span class="sxs-lookup"><span data-stu-id="85e82-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="85e82-116">概觀</span><span class="sxs-lookup"><span data-stu-id="85e82-116">Overview</span></span>

<span data-ttu-id="85e82-117">疑難排解資源提供 hello 功能的虛擬網路閘道與連線發生問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="85e82-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="85e82-118">當提出要求時 tooresource 疑難排解記錄檔正在檢查和查詢。</span><span class="sxs-lookup"><span data-stu-id="85e82-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="85e82-119">檢查完成時，會傳回 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="85e82-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="85e82-120">疑難排解要求是長時間執行的資源要求，但這可能需要多個分鐘 tooreturn 結果。</span><span class="sxs-lookup"><span data-stu-id="85e82-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="85e82-121">hello 疑難排解記錄檔會儲存在指定的儲存體帳戶的容器。</span><span class="sxs-lookup"><span data-stu-id="85e82-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="85e82-122">針對閘道或連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="85e82-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="85e82-123">瀏覽 toohello [Azure 入口網站](https://portal.azure.com)按一下**網路** > **網路監看員** > **VPN 診斷**</span><span class="sxs-lookup"><span data-stu-id="85e82-123">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="85e82-124">選取 [訂用帳戶]、[資源群組] 和 [位置]。</span><span class="sxs-lookup"><span data-stu-id="85e82-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="85e82-125">疑難排解資源傳回 hello hello 資源健全狀況的相關資料。</span><span class="sxs-lookup"><span data-stu-id="85e82-125">Resource troubleshooting returns data about hello health of hello resource.</span></span> <span data-ttu-id="85e82-126">它也會儲存 toobe 檢閱相關的記錄檔 tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="85e82-126">It also saves relevant logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="85e82-127">按一下**儲存體帳戶**tooselect 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="85e82-127">Click **Storage Account** tooselect a storage account.</span></span>
4. <span data-ttu-id="85e82-128">在 hello**儲存體帳戶**刀鋒視窗中，選取現有的儲存體帳戶，或按一下**+ 儲存體帳戶**toocreate 新建一個。</span><span class="sxs-lookup"><span data-stu-id="85e82-128">On hello **Storage accounts** blade, select an existing storage account or click **+ Storage account** toocreate a new one.</span></span>
5. <span data-ttu-id="85e82-129">在 hello**容器**刀鋒視窗中，選擇現有的容器，或按一下**+ 容器**toocreate 新的容器。</span><span class="sxs-lookup"><span data-stu-id="85e82-129">On hello **Containers** blade, choose an existing container or click **+ Container** toocreate a new container.</span></span> <span data-ttu-id="85e82-130">完成時，按一下 [選取]</span><span class="sxs-lookup"><span data-stu-id="85e82-130">When complete click **Select**</span></span>
6. <span data-ttu-id="85e82-131">選取 hello 資源 tootroubleshoot 閘道與連線，然後按一下**啟動疑難排解**</span><span class="sxs-lookup"><span data-stu-id="85e82-131">Select hello Gateway and Connection resources tootroubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="85e82-132">如果選取多個資源，系統會在這些閘道資源上同時執行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="85e82-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="85e82-133">它不可以在連接上執行，以及它有相關聯的 hello 位於閘道相同的時間。</span><span class="sxs-lookup"><span data-stu-id="85e82-133">It can not run on a connection and it's associated gateway at hello same time.</span></span> <span data-ttu-id="85e82-134">建議 tootroubleshoot 閘道第一次為連接疑難排解是較長的程序。</span><span class="sxs-lookup"><span data-stu-id="85e82-134">It is recommended tootroubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="85e82-135">資源 hello 執行 VPN 診斷時**疑難排解狀態**資料行將會顯示狀態為**執行**</span><span class="sxs-lookup"><span data-stu-id="85e82-135">While VPN Diagnostics is running on a resource hello **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="85e82-136">完成時，hello 狀態資料行變更太**狀況良好**或**狀況不良**。</span><span class="sxs-lookup"><span data-stu-id="85e82-136">When complete, hello status column changes too**Healthy** or **Unhealthy**.</span></span>

![疑難排解完成][2]

## <a name="understanding-hello-results"></a><span data-ttu-id="85e82-138">了解 hello 結果</span><span class="sxs-lookup"><span data-stu-id="85e82-138">Understanding hello results</span></span>

<span data-ttu-id="85e82-139">在 hello**詳細資料**區段 hello 視窗的 hello**狀態**索引標籤會顯示 hello 狀態 hello 最後疑難排解執行選取的 hello 資源上。</span><span class="sxs-lookup"><span data-stu-id="85e82-139">In hello **Details** section of hello window, hello **Status** tab shows hello status of hello last troubleshooting run on hello selected resource.</span></span> <span data-ttu-id="85e82-140">Hello 最新診斷的結果會顯示的 xx 分鐘 hello 上次執行之後。</span><span class="sxs-lookup"><span data-stu-id="85e82-140">Results of hello latest diagnostic are shown xx minutes after hello last run.</span></span>

|<span data-ttu-id="85e82-141">屬性</span><span class="sxs-lookup"><span data-stu-id="85e82-141">Property</span></span>  |<span data-ttu-id="85e82-142">說明</span><span class="sxs-lookup"><span data-stu-id="85e82-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="85e82-143">資源</span><span class="sxs-lookup"><span data-stu-id="85e82-143">Resource</span></span>     | <span data-ttu-id="85e82-144">連結 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="85e82-144">A link toohello resource.</span></span>        |
|<span data-ttu-id="85e82-145">儲存體路徑</span><span class="sxs-lookup"><span data-stu-id="85e82-145">Storage path</span></span>     |  <span data-ttu-id="85e82-146">路徑 toohello 儲存體帳戶和容器，包含 hello 的記錄檔 （如果有任何已 hello 執行期間所產生）。</span><span class="sxs-lookup"><span data-stu-id="85e82-146">Path toohello storage account and container that contain hello logs (if any were produced during hello run).</span></span> <span data-ttu-id="85e82-147">此設定不會保存，當您離開 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="85e82-147">This setting does not persist after you leave hello portal.</span></span>        |
|<span data-ttu-id="85e82-148">摘要</span><span class="sxs-lookup"><span data-stu-id="85e82-148">Summary</span></span>     | <span data-ttu-id="85e82-149">Hello 資源健全狀況的摘要。</span><span class="sxs-lookup"><span data-stu-id="85e82-149">Summary of hello resource health.</span></span>        |
|<span data-ttu-id="85e82-150">詳細資料</span><span class="sxs-lookup"><span data-stu-id="85e82-150">Detail</span></span>     | <span data-ttu-id="85e82-151">Hello 資源健全狀況的詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="85e82-151">Detailed information on hello resource health.</span></span>        |
|<span data-ttu-id="85e82-152">上次執行</span><span class="sxs-lookup"><span data-stu-id="85e82-152">Last run</span></span>     | <span data-ttu-id="85e82-153">上次 hello 時間 hello 時間疑難排解已執行。</span><span class="sxs-lookup"><span data-stu-id="85e82-153">hello time hello last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="85e82-154">hello**動作** 索引標籤提供一般指引 tooresolve hello 問題的方式。</span><span class="sxs-lookup"><span data-stu-id="85e82-154">hello **Action** tab provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="85e82-155">Hello 問題，可以採取的動作，如果是其他指南提供的連結。</span><span class="sxs-lookup"><span data-stu-id="85e82-155">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="85e82-156">Hello 案例中的任何其他指引，hello 回應提供 hello url tooopen 支援案例。</span><span class="sxs-lookup"><span data-stu-id="85e82-156">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="85e82-157">如需回應 hello 和時要包含的 hello 屬性的詳細資訊，請瀏覽[網路監看員疑難排解概觀](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="85e82-157">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="85e82-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85e82-158">Next steps</span></span>

<span data-ttu-id="85e82-159">如果設定已變更為該停止 VPN 連線能力，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack 向 hello 網路安全性群組和安全性規則，可能會有問題。</span><span class="sxs-lookup"><span data-stu-id="85e82-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
