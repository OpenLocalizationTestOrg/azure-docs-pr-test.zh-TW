---
title: "Azure 網路監看員-Azure 入口網站擷取 aaaManage 封包 |Microsoft 文件"
description: "此頁面可讓您說明如何 toomanage hello 封包擷取功能，使用 Azure 入口網站的網路監看員"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="71ca8-103">使用 Azure 網路監看員使用 hello 入口網站管理封包擷取</span><span class="sxs-lookup"><span data-stu-id="71ca8-103">Manage packet captures with Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="71ca8-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="71ca8-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="71ca8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="71ca8-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="71ca8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="71ca8-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="71ca8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="71ca8-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="71ca8-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="71ca8-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="71ca8-109">網路監看員封包擷取可讓您 toocreate 擷取工作階段 tootrack 流量 tooand 從虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="71ca8-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="71ca8-110">篩選器可供 hello 擷取工作階段 tooensure 擷取您想要只 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="71ca8-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="71ca8-111">封包擷取可在主動和被動協助 toodiagnose 網路異常狀況。</span><span class="sxs-lookup"><span data-stu-id="71ca8-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="71ca8-112">其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。</span><span class="sxs-lookup"><span data-stu-id="71ca8-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="71ca8-113">透過無法 tooremotely 觸發程序封包擷取，這項功能可以減輕工作 hello 負擔的手動和 hello 想要在電腦上，以節省寶貴的時間執行封包擷取。</span><span class="sxs-lookup"><span data-stu-id="71ca8-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="71ca8-114">這篇文章帶領您完成 hello 封包擷取目前可用的不同的管理工作。</span><span class="sxs-lookup"><span data-stu-id="71ca8-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="71ca8-115">**啟動封包擷取**</span><span class="sxs-lookup"><span data-stu-id="71ca8-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="71ca8-116">**停止封包擷取**</span><span class="sxs-lookup"><span data-stu-id="71ca8-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="71ca8-117">**刪除封包擷取**</span><span class="sxs-lookup"><span data-stu-id="71ca8-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="71ca8-118">**下載封包擷取**</span><span class="sxs-lookup"><span data-stu-id="71ca8-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="71ca8-119">開始之前</span><span class="sxs-lookup"><span data-stu-id="71ca8-119">Before you begin</span></span>

<span data-ttu-id="71ca8-120">本文假設您擁有 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="71ca8-120">This article assumes that you have hello following resources:</span></span>

- <span data-ttu-id="71ca8-121">執行個體要在 hello 區域網路監看員的 toocreate 封包擷取</span><span class="sxs-lookup"><span data-stu-id="71ca8-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="71ca8-122">虛擬機器與 hello 封包擷取啟用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="71ca8-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71ca8-123">封包擷取需要虛擬機器擴充功能 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="71ca8-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="71ca8-124">Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="71ca8-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-hello-portal"></a><span data-ttu-id="71ca8-125">透過 hello 入口網站的封包擷取代理程式延伸</span><span class="sxs-lookup"><span data-stu-id="71ca8-125">Packet Capture agent extension through hello portal</span></span>

<span data-ttu-id="71ca8-126">tooinstall hello 封包擷取 VM 代理程式，透過 hello 入口網站，瀏覽 tooyour 虛擬機器，按一下**延伸** > **新增**並搜尋**網路監看員的代理程式 」Windows**</span><span class="sxs-lookup"><span data-stu-id="71ca8-126">tooinstall hello packet capture VM agent through hello portal, navigate tooyour virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![代理程式檢視][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="71ca8-128">封包擷取概觀</span><span class="sxs-lookup"><span data-stu-id="71ca8-128">Packet Capture overview</span></span>

<span data-ttu-id="71ca8-129">瀏覽 toohello [Azure 入口網站](https://portal.azure.com)按一下**網路** > **網路監看員** > **封包擷取**</span><span class="sxs-lookup"><span data-stu-id="71ca8-129">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="71ca8-130">hello 概觀頁面會顯示一份所有封包擷取存在於無論 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="71ca8-130">hello overview page shows a list of all packet captures that exist no matter hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="71ca8-131">封包擷取需要透過連接埠 443 的連線能力 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="71ca8-131">Packet capture requires connectivity toohello storage account over port 443.</span></span>

![封包擷取概觀畫面][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="71ca8-133">啟動封包擷取</span><span class="sxs-lookup"><span data-stu-id="71ca8-133">Start a packet capture</span></span>

<span data-ttu-id="71ca8-134">按一下**新增**toocreate 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="71ca8-134">Click **Add** toocreate a packet capture.</span></span>

<span data-ttu-id="71ca8-135">您可以定義封包擷取的 hello 屬性如下：</span><span class="sxs-lookup"><span data-stu-id="71ca8-135">hello properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="71ca8-136">**主要設定**</span><span class="sxs-lookup"><span data-stu-id="71ca8-136">**Main settings**</span></span>

- <span data-ttu-id="71ca8-137">**訂用帳戶**-此值為 hello 訂用帳戶時，需要每個訂用帳戶中的網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="71ca8-137">**Subscription** - This value is hello subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="71ca8-138">**資源群組**-hello hello 做為目標的虛擬機器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="71ca8-138">**Resource group** - hello resource group of hello virtual machine that is being targeted.</span></span>
- <span data-ttu-id="71ca8-139">**目標虛擬機器**-hello 虛擬機器執行 hello 封包擷取</span><span class="sxs-lookup"><span data-stu-id="71ca8-139">**Target virtual machine** - hello virtual machine that is running hello packet capture</span></span>
- <span data-ttu-id="71ca8-140">**封包擷取名稱**-這個值是 hello hello 封包擷取名稱。</span><span class="sxs-lookup"><span data-stu-id="71ca8-140">**Packet capture name** - This value is hello name of hello packet capture.</span></span>

<span data-ttu-id="71ca8-141">**擷取設定**</span><span class="sxs-lookup"><span data-stu-id="71ca8-141">**Capture configuration**</span></span>

- <span data-ttu-id="71ca8-142">**儲存體帳戶** - 決定封包擷取是否會儲存在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="71ca8-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="71ca8-143">**檔案**-決定是否封包擷取本機儲存在 hello 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="71ca8-143">**File** - Determines if a packet capture is saved locally on hello virtual machine.</span></span>
- <span data-ttu-id="71ca8-144">**儲存體帳戶**-hello 選取儲存體帳戶 toosave hello 封包中的擷取。</span><span class="sxs-lookup"><span data-stu-id="71ca8-144">**Storage Accounts** - hello selected storage account toosave hello packet capture in.</span></span> <span data-ttu-id="71ca8-145">預設位置是 https://{儲存體帳戶名稱}.blob.core.windows.net/network-watcher-logs/subscriptions/{訂用帳戶識別碼}/resourcegroups/{資源群組名稱}/providers/microsoft.compute/virtualmachines/{虛擬機器名稱}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap。</span><span class="sxs-lookup"><span data-stu-id="71ca8-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="71ca8-146">(只在選取**儲存體**時才會啟用)</span><span class="sxs-lookup"><span data-stu-id="71ca8-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="71ca8-147">**本機檔案路徑**-hello 本機路徑上的虛擬機器 toosave hello 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="71ca8-147">**Local file path** - hello local path on a virtual machine toosave hello packet capture.</span></span> <span data-ttu-id="71ca8-148">(只在選取**檔案**時才會啟用)。</span><span class="sxs-lookup"><span data-stu-id="71ca8-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="71ca8-149">必須提供有效的路徑</span><span class="sxs-lookup"><span data-stu-id="71ca8-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="71ca8-150">**每個封包的最大位元組**-hello 數目的每個封包所擷取的位元組，如果保留空白，會擷取所有位元組。</span><span class="sxs-lookup"><span data-stu-id="71ca8-150">**Maximum bytes per packet** - hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="71ca8-151">**每個工作階段的最大位元組**-總計的擷取，一旦達到 hello 封包擷取停駐點 hello 值的位元組數。</span><span class="sxs-lookup"><span data-stu-id="71ca8-151">**Maximum bytes per session** - Total number of bytes that are captured, once hello value is reached hello packet capture stops.</span></span>
- <span data-ttu-id="71ca8-152">**時間限制 （秒）** -設定 hello 封包擷取 toostop 時間限制。</span><span class="sxs-lookup"><span data-stu-id="71ca8-152">**Time limit (seconds)** - Sets a time limit for hello packet capture toostop.</span></span> <span data-ttu-id="71ca8-153">預設值為 18000 秒。</span><span class="sxs-lookup"><span data-stu-id="71ca8-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="71ca8-154">儲存封包擷取目前不支援進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="71ca8-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="71ca8-155">**篩選 (選用)**</span><span class="sxs-lookup"><span data-stu-id="71ca8-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="71ca8-156">**通訊協定**-hello 通訊協定 toofilter hello 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="71ca8-156">**Protocol** - hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="71ca8-157">hello 可用的值為 TCP、 UDP 和任何。</span><span class="sxs-lookup"><span data-stu-id="71ca8-157">hello available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="71ca8-158">**本機 IP 位址**-這個值會篩選 hello 封包擷取 toopackets 其中 hello 本機 IP 位址必須符合此篩選值。</span><span class="sxs-lookup"><span data-stu-id="71ca8-158">**Local IP address** - This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>
- <span data-ttu-id="71ca8-159">**本機連接埠**-這個值會篩選 hello 封包擷取 toopackets hello 本機連接埠符合此篩選值的位置。</span><span class="sxs-lookup"><span data-stu-id="71ca8-159">**Local port** - This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>
- <span data-ttu-id="71ca8-160">**遠端 IP 位址**-這個值會篩選 hello 封包擷取 toopackets hello 遠端 IP 符合此篩選值的位置。</span><span class="sxs-lookup"><span data-stu-id="71ca8-160">**Remote IP address** - This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>
- <span data-ttu-id="71ca8-161">**遠端連接埠**-這個值會篩選 hello 封包擷取 toopackets hello 遠端連接埠符合此篩選值的位置。</span><span class="sxs-lookup"><span data-stu-id="71ca8-161">**Remote port** - This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="71ca8-162">連接埠和 IP 位址的值可以是單一值、值的範圍或一組。</span><span class="sxs-lookup"><span data-stu-id="71ca8-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="71ca8-163">(也就是連接埠的 80-1024) 您可以定義所有您想要的篩選。</span><span class="sxs-lookup"><span data-stu-id="71ca8-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="71ca8-164">一旦 hello 值都已填寫，按一下 **確定**toocreate hello 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="71ca8-164">Once hello values are filled out, click **OK** toocreate hello packet capture.</span></span>

![建立封包擷取][2]

<span data-ttu-id="71ca8-166">在設定 hello 時限後 hello 封包擷取已過期，hello 封包擷取將會停止，而且可以進行檢閱。</span><span class="sxs-lookup"><span data-stu-id="71ca8-166">After hello time limit set on hello packet capture has expired, hello packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="71ca8-167">您可以手動停止 hello 封包擷取工作階段。</span><span class="sxs-lookup"><span data-stu-id="71ca8-167">You can also manually stop hello packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="71ca8-168">刪除封包擷取</span><span class="sxs-lookup"><span data-stu-id="71ca8-168">Delete a packet capture</span></span>

<span data-ttu-id="71ca8-169">在 hello 封包擷取檢視中，按一下 hello**操作功能表**（...） 或以滑鼠右鍵按一下，然後按一下**刪除**toostop hello 封包擷取</span><span class="sxs-lookup"><span data-stu-id="71ca8-169">In hello packet capture view, click hello **context menu** (...) or right click, and click **delete** toostop hello packet capture</span></span>

![刪除封包擷取][3]

> [!NOTE]
> <span data-ttu-id="71ca8-171">刪除封包擷取並不會刪除 hello 儲存體帳戶中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="71ca8-171">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

<span data-ttu-id="71ca8-172">系統會要求您按一下您想要 toodelete hello 封包擷取，tooconfirm **[是]**</span><span class="sxs-lookup"><span data-stu-id="71ca8-172">You are asked tooconfirm you want toodelete hello packet capture, click **Yes**</span></span>

![確認][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="71ca8-174">停止封包擷取</span><span class="sxs-lookup"><span data-stu-id="71ca8-174">Stop a packet capture</span></span>

<span data-ttu-id="71ca8-175">在 hello 封包擷取檢視中，按一下 hello**操作功能表**（...） 或以滑鼠右鍵按一下，然後按一下**停止**toostop hello 封包擷取</span><span class="sxs-lookup"><span data-stu-id="71ca8-175">In hello packet capture view, click hello **context menu** (...) or right click, and click **Stop** toostop hello packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="71ca8-176">下載封包擷取</span><span class="sxs-lookup"><span data-stu-id="71ca8-176">Download a packet capture</span></span>

<span data-ttu-id="71ca8-177">您的封包擷取工作階段完成後，請 hello 擷取檔案是上傳的 tooblob 儲存體或 tooa 本機檔案 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="71ca8-177">Once your packet capture session has completed, hello capture file is uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="71ca8-178">hello 封包擷取 hello 儲存位置被定義在 hello 工作階段的建立。</span><span class="sxs-lookup"><span data-stu-id="71ca8-178">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="71ca8-179">方便的工具 tooaccess 這些擷取的檔案儲存的 tooa 儲存體帳戶是 Microsoft Azure 儲存體總管 中，這可以在這裡下載： http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="71ca8-179">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="71ca8-180">如果指定的儲存體帳戶，則封包擷取檔案會儲存在下列位置的 hello tooa 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="71ca8-180">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="71ca8-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71ca8-181">Next steps</span></span>

<span data-ttu-id="71ca8-182">了解如何 tooautomate 封包擷取虛擬機器警示藉由檢視[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="71ca8-182">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="71ca8-183">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="71ca8-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













