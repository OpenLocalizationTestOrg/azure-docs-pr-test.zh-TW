---
title: "Azure 網路監看員中的封包擷取簡介 | Microsoft Docs"
description: "本頁提供網路監看員封包擷取功能的概觀"
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
ms.openlocfilehash: 4fdd007c2cfad7b42f26ab2cacfba06d95c8dad3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-variable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="cb2b6-103">Azure 網路監看員中的變數封包擷取簡介</span><span class="sxs-lookup"><span data-stu-id="cb2b6-103">Introduction to variable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="cb2b6-104">網路監看員變數封包擷取可讓您建立封包擷取工作階段來追蹤虛擬機器的流入和流出流量。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="cb2b6-105">封包擷取有助於被動和主動地診斷網路異常。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="cb2b6-106">其他用途包括收集網路統計資料、取得有關網路入侵的資訊，以及偵錯用戶端與伺服器間的通訊等等。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="cb2b6-107">封包擷取是透過網路監看員從遠端啟動的虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="cb2b6-108">這項功能可以減輕在所需虛擬機器上手動執行封包擷取的工作負擔，進而省下寶貴的時間。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="cb2b6-109">可以透過入口網站、PowerShell、CLI 或 REST API 觸發封包擷取。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="cb2b6-110">觸發封包擷取方式的其中一個範例是使用虛擬機器警示。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="cb2b6-111">系統會為擷取工作階段提供篩選器，以確保您擷取到您想要監視的流量。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span></span> <span data-ttu-id="cb2b6-112">篩選是根據 5 個 Tuple (通訊協定、本機 IP 位址、遠端 IP 位址、本機連接埠，以及遠端連接埠) 的資訊。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="cb2b6-113">擷取的資料會儲存在本機磁碟或儲存體 blob。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-113">The captured data is stored in the local disk or a storage blob.</span></span> <span data-ttu-id="cb2b6-114">每個訂用帳戶在每個區域皆有 10 個封包擷取工作階段的限制。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="cb2b6-115">此限制僅適用於工作階段，且不會套用到已儲存的封包擷取檔案，無論該檔案是位於 VM 本機上還是位於儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb2b6-116">封包擷取需要虛擬機器擴充功能 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="cb2b6-117">若要在 Windows VM 上安裝擴充功能，請瀏覽[適用於 Windows 的 Azure 網路監看員代理程式虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)，若要在 Linux VM 上安裝，則請瀏覽[適用於 Linux 的 Azure 網路監看員代理程式虛擬機器擴充功能](../virtual-machines/linux/extensions-nwa.md)。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="cb2b6-118">若要將擷取的資訊減少為只有您想要的資訊，可以針對封包擷取工作階段使用下列選項︰</span><span class="sxs-lookup"><span data-stu-id="cb2b6-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span></span>

<span data-ttu-id="cb2b6-119">**擷取設定**</span><span class="sxs-lookup"><span data-stu-id="cb2b6-119">**Capture configuration**</span></span>

|<span data-ttu-id="cb2b6-120">屬性</span><span class="sxs-lookup"><span data-stu-id="cb2b6-120">Property</span></span>|<span data-ttu-id="cb2b6-121">說明</span><span class="sxs-lookup"><span data-stu-id="cb2b6-121">Description</span></span>|
|---|---|
|<span data-ttu-id="cb2b6-122">**每個封包的最大位元組 (位元組)**</span><span class="sxs-lookup"><span data-stu-id="cb2b6-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="cb2b6-123">來自每個封包所擷取的位元組，如果保留空白，會擷取所有位元組。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="cb2b6-124">來自每個封包所擷取的位元組，如果保留空白，會擷取所有位元組。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="cb2b6-125">如果您僅需要 IPv4 標頭 – 請在這裡指定 34</span><span class="sxs-lookup"><span data-stu-id="cb2b6-125">If you need only the IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="cb2b6-126">**每個工作階段的最大位元組 (位元組)**</span><span class="sxs-lookup"><span data-stu-id="cb2b6-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="cb2b6-127">所擷取其中的位元組總數，一旦達到值時工作階段隨即結束。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-127">Total number of bytes in that are captured, once the value is reached the session ends.</span></span>|
|<span data-ttu-id="cb2b6-128">**時間限制 (秒)**</span><span class="sxs-lookup"><span data-stu-id="cb2b6-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="cb2b6-129">在封包擷取工作階段上設定時間限制。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-129">Sets a time constraint on the packet capture session.</span></span> <span data-ttu-id="cb2b6-130">預設值為 18000 秒或 5 小時。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-130">The default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="cb2b6-131">**篩選 (選用)**</span><span class="sxs-lookup"><span data-stu-id="cb2b6-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="cb2b6-132">屬性</span><span class="sxs-lookup"><span data-stu-id="cb2b6-132">Property</span></span>|<span data-ttu-id="cb2b6-133">說明</span><span class="sxs-lookup"><span data-stu-id="cb2b6-133">Description</span></span>|
|---|---|
|<span data-ttu-id="cb2b6-134">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="cb2b6-134">**Protocol**</span></span> | <span data-ttu-id="cb2b6-135">用來篩選封包擷取的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-135">The protocol to filter for the packet capture.</span></span> <span data-ttu-id="cb2b6-136">可用的值為 TCP、UDP 和 All。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-136">The available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="cb2b6-137">**本機 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="cb2b6-137">**Local IP address**</span></span> | <span data-ttu-id="cb2b6-138">這個值會將封包擷取篩選為其中本機 IP 位址符合此篩選值的封包。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>|
|<span data-ttu-id="cb2b6-139">**本機連接埠**</span><span class="sxs-lookup"><span data-stu-id="cb2b6-139">**Local port**</span></span> | <span data-ttu-id="cb2b6-140">這個值會將封包擷取篩選為其中本機連接埠符合此篩選值的封包。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-140">This value filters the packet capture to packets where the local port matches this filter value.</span></span>|
|<span data-ttu-id="cb2b6-141">**遠端 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="cb2b6-141">**Remote IP address**</span></span> | <span data-ttu-id="cb2b6-142">這個值會將封包擷取篩選為其中遠端 IP 符合此篩選值的封包。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>|
|<span data-ttu-id="cb2b6-143">**遠端連接埠**</span><span class="sxs-lookup"><span data-stu-id="cb2b6-143">**Remote port**</span></span> | <span data-ttu-id="cb2b6-144">這個值會將封包擷取篩選為其中遠端連接埠符合此篩選值的封包。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-144">This value filters the packet capture to packets where the remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="cb2b6-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb2b6-145">Next steps</span></span>

<span data-ttu-id="cb2b6-146">了解如何透過入口網站管理封包擷取，請造訪[在 Azure 入口網站中管理封包擷取](network-watcher-packet-capture-manage-portal.md)或若使用 PowerShell，請造訪[使用 PowerShell 管理封包擷取](network-watcher-packet-capture-manage-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="cb2b6-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="cb2b6-147">請造訪[建立觸發的警示封包擷取](network-watcher-alert-triggered-packet-capture.md)來了解如何根據虛擬機器警示建立主動式封包擷取</span><span class="sxs-lookup"><span data-stu-id="cb2b6-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













