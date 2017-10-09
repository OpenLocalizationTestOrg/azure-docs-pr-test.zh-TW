---
title: "在 Azure 網路監看員 aaaIntroduction tooPacket 擷取 |Microsoft 文件"
description: "此頁面提供 hello 網路監看員封包擷取功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="fdf01-103">在 Azure 網路監看員的簡介 toovariable 封包擷取</span><span class="sxs-lookup"><span data-stu-id="fdf01-103">Introduction toovariable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="fdf01-104">網路監看員變數的封包擷取可讓您 toocreate 封包擷取工作階段 tootrack 流量 tooand 從虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fdf01-104">Network Watcher variable packet capture allows you toocreate packet capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="fdf01-105">封包擷取協助 toodiagnose 網路異常這兩個被動和 proactivity。</span><span class="sxs-lookup"><span data-stu-id="fdf01-105">Packet capture helps toodiagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="fdf01-106">其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。</span><span class="sxs-lookup"><span data-stu-id="fdf01-106">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span>

<span data-ttu-id="fdf01-107">封包擷取是透過網路監看員從遠端啟動的虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="fdf01-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="fdf01-108">這項功能可以減輕工作 hello 負擔 hello 預期虛擬機器上，以節省寶貴的時間手動執行封包擷取。</span><span class="sxs-lookup"><span data-stu-id="fdf01-108">This capability eases hello burden of running a packet capture manually on hello desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="fdf01-109">透過 hello 入口網站、 PowerShell、 CLI 或 REST API，可以觸發封包擷取。</span><span class="sxs-lookup"><span data-stu-id="fdf01-109">Packet capture can be triggered through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="fdf01-110">觸發封包擷取方式的其中一個範例是使用虛擬機器警示。</span><span class="sxs-lookup"><span data-stu-id="fdf01-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="fdf01-111">篩選器會提供如 hello 擷取工作階段 tooensure 您擷取您想要 toomonitor 的流量。</span><span class="sxs-lookup"><span data-stu-id="fdf01-111">Filters are provided for hello capture session tooensure you capture traffic you want toomonitor.</span></span> <span data-ttu-id="fdf01-112">篩選是根據 5 個 Tuple (通訊協定、本機 IP 位址、遠端 IP 位址、本機連接埠，以及遠端連接埠) 的資訊。</span><span class="sxs-lookup"><span data-stu-id="fdf01-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="fdf01-113">hello 擷取的資料會儲存在 hello 本機磁碟或儲存體 blob。</span><span class="sxs-lookup"><span data-stu-id="fdf01-113">hello captured data is stored in hello local disk or a storage blob.</span></span> <span data-ttu-id="fdf01-114">每個訂用帳戶在每個區域皆有 10 個封包擷取工作階段的限制。</span><span class="sxs-lookup"><span data-stu-id="fdf01-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="fdf01-115">這項限制適用於只有 toohello 工作階段，但不適用於 toohello hello VM 在本機或儲存體帳戶中儲存封包擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="fdf01-115">This limit applies only toohello sessions and does not apply toohello saved packet capture files either locally on hello VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdf01-116">封包擷取需要虛擬機器擴充功能 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="fdf01-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="fdf01-117">Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="fdf01-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="fdf01-118">tooreduce hello 資訊擷取您想要的 tooonly hello 資訊、 hello 有下列選項的封包擷取工作階段：</span><span class="sxs-lookup"><span data-stu-id="fdf01-118">tooreduce hello information you capture tooonly hello information you want, hello following options are available for a packet capture session:</span></span>

<span data-ttu-id="fdf01-119">**擷取設定**</span><span class="sxs-lookup"><span data-stu-id="fdf01-119">**Capture configuration**</span></span>

|<span data-ttu-id="fdf01-120">屬性</span><span class="sxs-lookup"><span data-stu-id="fdf01-120">Property</span></span>|<span data-ttu-id="fdf01-121">說明</span><span class="sxs-lookup"><span data-stu-id="fdf01-121">Description</span></span>|
|---|---|
|<span data-ttu-id="fdf01-122">**每個封包的最大位元組 (位元組)**</span><span class="sxs-lookup"><span data-stu-id="fdf01-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="fdf01-123">hello 數目的每個封包所擷取的位元組，如果保留空白，會擷取所有位元組。</span><span class="sxs-lookup"><span data-stu-id="fdf01-123">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="fdf01-124">hello 數目的每個封包所擷取的位元組，如果保留空白，會擷取所有位元組。</span><span class="sxs-lookup"><span data-stu-id="fdf01-124">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="fdf01-125">如果您需要唯一的 hello IPv4 標頭 – 表示這裡 34</span><span class="sxs-lookup"><span data-stu-id="fdf01-125">If you need only hello IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="fdf01-126">**每個工作階段的最大位元組 (位元組)**</span><span class="sxs-lookup"><span data-stu-id="fdf01-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="fdf01-127">Hello 值達到 hello 工作階段結束之後，會擷取中的位元組總數。</span><span class="sxs-lookup"><span data-stu-id="fdf01-127">Total number of bytes in that are captured, once hello value is reached hello session ends.</span></span>|
|<span data-ttu-id="fdf01-128">**時間限制 (秒)**</span><span class="sxs-lookup"><span data-stu-id="fdf01-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="fdf01-129">設定時間限制，在 hello 封包擷取工作階段。</span><span class="sxs-lookup"><span data-stu-id="fdf01-129">Sets a time constraint on hello packet capture session.</span></span> <span data-ttu-id="fdf01-130">hello 預設值是 18000 秒或 5 小時。</span><span class="sxs-lookup"><span data-stu-id="fdf01-130">hello default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="fdf01-131">**篩選 (選用)**</span><span class="sxs-lookup"><span data-stu-id="fdf01-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="fdf01-132">屬性</span><span class="sxs-lookup"><span data-stu-id="fdf01-132">Property</span></span>|<span data-ttu-id="fdf01-133">說明</span><span class="sxs-lookup"><span data-stu-id="fdf01-133">Description</span></span>|
|---|---|
|<span data-ttu-id="fdf01-134">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="fdf01-134">**Protocol**</span></span> | <span data-ttu-id="fdf01-135">hello 通訊協定 toofilter hello 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="fdf01-135">hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="fdf01-136">hello 可用的值為 TCP、 UDP 和所有。</span><span class="sxs-lookup"><span data-stu-id="fdf01-136">hello available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="fdf01-137">**本機 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="fdf01-137">**Local IP address**</span></span> | <span data-ttu-id="fdf01-138">這個值會篩選 hello 封包擷取 toopackets 其中 hello 本機 IP 位址必須符合此篩選值。</span><span class="sxs-lookup"><span data-stu-id="fdf01-138">This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>|
|<span data-ttu-id="fdf01-139">**本機連接埠**</span><span class="sxs-lookup"><span data-stu-id="fdf01-139">**Local port**</span></span> | <span data-ttu-id="fdf01-140">這個值篩選 hello 封包擷取的 toopackets hello 本機連接埠符合此篩選值的位置。</span><span class="sxs-lookup"><span data-stu-id="fdf01-140">This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>|
|<span data-ttu-id="fdf01-141">**遠端 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="fdf01-141">**Remote IP address**</span></span> | <span data-ttu-id="fdf01-142">這個值篩選 hello 封包擷取的 toopackets hello 遠端 IP 符合此篩選值的位置。</span><span class="sxs-lookup"><span data-stu-id="fdf01-142">This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>|
|<span data-ttu-id="fdf01-143">**遠端連接埠**</span><span class="sxs-lookup"><span data-stu-id="fdf01-143">**Remote port**</span></span> | <span data-ttu-id="fdf01-144">這個值篩選 hello 封包擷取的 toopackets hello 遠端連接埠符合此篩選值的位置。</span><span class="sxs-lookup"><span data-stu-id="fdf01-144">This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="fdf01-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fdf01-145">Next steps</span></span>

<span data-ttu-id="fdf01-146">了解管理封包擷取透過 hello 入口網站，造訪[管理 hello Azure 入口網站中的封包擷取](network-watcher-packet-capture-manage-portal.md)或 PowerShell 造訪[使用 PowerShell 管理封包擷取](network-watcher-packet-capture-manage-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="fdf01-146">Learn how you can manage packet captures through hello portal by visiting [Manage packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="fdf01-147">深入了解如何 toocreate 主動式封包擷取根據虛擬機器警示造訪[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="fdf01-147">Learn how toocreate proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













