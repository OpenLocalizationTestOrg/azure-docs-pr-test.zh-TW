---
title: "與 Azure 網路監看員-Azure 入口網站的 aaaCheck 連線 |Microsoft 文件"
description: "此頁面說明 toouse 連線如何與網路監看員使用 hello Azure 入口網站檢查"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="a6fae-103">請檢查與 Azure 網路監看員使用 hello Azure 入口網站的連線</span><span class="sxs-lookup"><span data-stu-id="a6fae-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a6fae-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="a6fae-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="a6fae-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6fae-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="a6fae-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a6fae-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="a6fae-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="a6fae-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="a6fae-108">了解可以如何建立 toouse 連線 tooverify 如果從虛擬機器 tooa 指定端點的直接 TCP 連接。</span><span class="sxs-lookup"><span data-stu-id="a6fae-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a6fae-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="a6fae-109">Before you begin</span></span>

<span data-ttu-id="a6fae-110">本文假設您擁有 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="a6fae-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="a6fae-111">執行個體要 toocheck 連線的網路監看員 hello 區域中。</span><span class="sxs-lookup"><span data-stu-id="a6fae-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="a6fae-112">虛擬機器與 toocheck 連線。</span><span class="sxs-lookup"><span data-stu-id="a6fae-112">Virtual machines toocheck connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6fae-113">連線檢查需要虛擬機器延伸模組 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="a6fae-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="a6fae-114">Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="a6fae-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="a6fae-115">請檢查連線 tooa 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a6fae-115">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="a6fae-116">這個範例會檢查透過連接埠 80 連線 tooa 目的地虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a6fae-116">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

<span data-ttu-id="a6fae-117">瀏覽 tooyour 網路監看員，並按一下**連線能力檢查 （預覽）**。</span><span class="sxs-lookup"><span data-stu-id="a6fae-117">Navigate tooyour Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="a6fae-118">從虛擬機器 toocheck 連線選取 hello。</span><span class="sxs-lookup"><span data-stu-id="a6fae-118">Select hello virtual machine toocheck connectivity from.</span></span> <span data-ttu-id="a6fae-119">在 hello**目的地**區段中，選擇**選取虛擬機器**，並選擇 hello 正確的虛擬機器與連接埠 tootest。</span><span class="sxs-lookup"><span data-stu-id="a6fae-119">In hello **Destination** section choose **Select a virtual machine** and choose hello correct virtual machine and port tootest.</span></span>

<span data-ttu-id="a6fae-120">一旦您按一下**檢查**，會檢查 hello hello hello 指定的連接埠上的虛擬機器之間的連線。</span><span class="sxs-lookup"><span data-stu-id="a6fae-120">Once you click **Check**, hello connectivity between hello virtual machines on hello port specified are checked.</span></span> <span data-ttu-id="a6fae-121">在 hello 範例 hello 目的地 VM 是無法連線，躍點的清單會顯示。</span><span class="sxs-lookup"><span data-stu-id="a6fae-121">In hello example, hello destination VM is unreachable, a listing of hops are shown.</span></span>

![查看虛擬機器的連線能力結果][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="a6fae-123">檢查遠端端點的連線能力</span><span class="sxs-lookup"><span data-stu-id="a6fae-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="a6fae-124">toocheck hello 連線和延遲 tooa 遠端端點，請選擇 hello**手動指定**hello 中的選項按鈕**目的地**區段中，輸入 hello url 和 hello 連接埠並按一下**檢查**.</span><span class="sxs-lookup"><span data-stu-id="a6fae-124">toocheck hello connectivity and latency tooa remote endpoint, choose hello **Specify manually** radio button in hello **Destination** section, input hello url and hello port and click **Check**.</span></span>  <span data-ttu-id="a6fae-125">這會用於網站與儲存體端點之類的遠端端點。</span><span class="sxs-lookup"><span data-stu-id="a6fae-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![查看網站的連線能力結果][2]

## <a name="next-steps"></a><span data-ttu-id="a6fae-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6fae-127">Next steps</span></span>

<span data-ttu-id="a6fae-128">了解如何 tooautomate 封包擷取虛擬機器警示藉由檢視[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="a6fae-128">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="a6fae-129">造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出</span><span class="sxs-lookup"><span data-stu-id="a6fae-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
