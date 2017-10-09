---
title: "與 Azure 網路監看員 aaaPacket 檢查 |Microsoft 文件"
description: "本文說明如何從 VM 收集 toouse 網路監看員 tooperform 深度封包檢查"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="bae78-103">使用 Azure 網路監看員進行封包檢查</span><span class="sxs-lookup"><span data-stu-id="bae78-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="bae78-104">使用網路監看員 hello 封包擷取功能，可以起始，並在您的 Azure Vm 從 hello 網站、 PowerShell、 CLI，並以程式設計方式透過 hello SDK 和 REST API 管理擷取工作階段。</span><span class="sxs-lookup"><span data-stu-id="bae78-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="bae78-105">封包擷取可讓您需要藉由提供立即可用的格式中的 hello 資訊的封包層級資料的 tooaddress 案例。</span><span class="sxs-lookup"><span data-stu-id="bae78-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="bae78-106">運用 「 免費工具 tooinspect hello 資料，您可以檢查 tooand 傳送您的 Vm 所傳來的通訊，並深入了解您的網路流量。</span><span class="sxs-lookup"><span data-stu-id="bae78-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="bae78-107">使用封包擷取資料的一些範例包括︰調查網路或應用程式問題、偵測網路遭誤用及入侵嘗試，或維護法規合規性。</span><span class="sxs-lookup"><span data-stu-id="bae78-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="bae78-108">在本文中，我們會示範如何 tooopen 封包擷取檔案所提供網路監看員使用熱門開放原始碼工具。</span><span class="sxs-lookup"><span data-stu-id="bae78-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="bae78-109">我們也會提供範例來示範 toocalculate 連線延遲時間識別異常的流量，並檢查網路統計資料的方式。</span><span class="sxs-lookup"><span data-stu-id="bae78-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bae78-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="bae78-110">Before you begin</span></span>

<span data-ttu-id="bae78-111">本文逐步引導您完成先前執行的封包擷取上之一些預先設定的情況。</span><span class="sxs-lookup"><span data-stu-id="bae78-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="bae78-112">這些案例說明可藉由檢閱封包擷取進行存取的功能。</span><span class="sxs-lookup"><span data-stu-id="bae78-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="bae78-113">此案例使用[WireShark](https://www.wireshark.org/) tooinspect hello 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="bae78-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="bae78-114">本案例假設您已經在虛擬機器上執行封包擷取。</span><span class="sxs-lookup"><span data-stu-id="bae78-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="bae78-115">toolearn toocreate 封包擷取的瀏覽[hello 入口網站擷取管理封包](network-watcher-packet-capture-manage-portal.md)或與其他造訪[使用 REST API 管理封包擷取](network-watcher-packet-capture-manage-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="bae78-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="bae78-116">案例</span><span class="sxs-lookup"><span data-stu-id="bae78-116">Scenario</span></span>

<span data-ttu-id="bae78-117">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="bae78-117">In this scenario, you:</span></span>

* <span data-ttu-id="bae78-118">檢閱封包擷取</span><span class="sxs-lookup"><span data-stu-id="bae78-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="bae78-119">計算網路延遲</span><span class="sxs-lookup"><span data-stu-id="bae78-119">Calculate network latency</span></span>

<span data-ttu-id="bae78-120">在此案例中，我們會示範如何 tooview hello 發生兩個端點之間的傳輸控制通訊協定 (TCP) 交談的初始來回行程時間 (RTT)。</span><span class="sxs-lookup"><span data-stu-id="bae78-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="bae78-121">建立 TCP 連線時，hello 傳送嗨連接中的前三個封包遵循模式一般是指 tooas hello 三向交握。</span><span class="sxs-lookup"><span data-stu-id="bae78-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="bae78-122">藉由檢查傳送的此信號交換、 來自 hello 用戶端的初始要求和伺服器 hello 回應 hello 前兩個封包，我們可以在建立此連接時，計算 hello 延遲。</span><span class="sxs-lookup"><span data-stu-id="bae78-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="bae78-123">這個延遲是參照的 tooas hello 來回行程時間 (RTT)。</span><span class="sxs-lookup"><span data-stu-id="bae78-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="bae78-124">如需 hello TCP 通訊協定和 hello 三向交握的詳細資訊，請參閱 toohello 下列資源。</span><span class="sxs-lookup"><span data-stu-id="bae78-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="bae78-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span><span class="sxs-lookup"><span data-stu-id="bae78-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="bae78-126">步驟 1</span><span class="sxs-lookup"><span data-stu-id="bae78-126">Step 1</span></span>

<span data-ttu-id="bae78-127">啟動 WireShark</span><span class="sxs-lookup"><span data-stu-id="bae78-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="bae78-128">步驟 2</span><span class="sxs-lookup"><span data-stu-id="bae78-128">Step 2</span></span>

<span data-ttu-id="bae78-129">負載 hello **.cap**從封包擷取的檔案。</span><span class="sxs-lookup"><span data-stu-id="bae78-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="bae78-130">這個檔案位於 hello blob 儲存在我們儲存在本機上的虛擬機器 hello，根據您設定的方式。</span><span class="sxs-lookup"><span data-stu-id="bae78-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="bae78-131">步驟 3</span><span class="sxs-lookup"><span data-stu-id="bae78-131">Step 3</span></span>

<span data-ttu-id="bae78-132">tooview hello TCP 交談中的初始來回行程時間 (RTT)，我們將只會查看 hello 前兩個封包參與 hello TCP 交握。</span><span class="sxs-lookup"><span data-stu-id="bae78-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="bae78-133">我們將使用 hello 前兩個封包中 hello 三向信號交換期間，也就是 hello [SYN]、 [SYN、 ACK] 封包。</span><span class="sxs-lookup"><span data-stu-id="bae78-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="bae78-134">Hello TCP 標頭中設定的旗標的名稱。</span><span class="sxs-lookup"><span data-stu-id="bae78-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="bae78-135">hello hello 信號交換期間，[通知] hello 封包來說，在最後一個封包不會用於此案例。</span><span class="sxs-lookup"><span data-stu-id="bae78-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="bae78-136">[同步] hello 封包傳送 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="bae78-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="bae78-137">一旦收到 hello 伺服器 hello [通知] 將封包傳送做為接收從 hello 用戶端 hello SYN 的認可。</span><span class="sxs-lookup"><span data-stu-id="bae78-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="bae78-138">我們運用 hello 回應 hello 伺服器需要極少的額外負荷的事實，計算的 hello hello 用戶端所送出 RTT 減去 hello hello 用戶端已收到 hello [SYN、 ACK] 封包的 hello 時間 [SYN] 封包的時間。</span><span class="sxs-lookup"><span data-stu-id="bae78-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="bae78-139">使用 WireShark，系統會為我們計算此值。</span><span class="sxs-lookup"><span data-stu-id="bae78-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="bae78-140">toomore hello TCP 三向交握中輕鬆地檢視 hello 前兩個封包中，我們將利用 hello 篩選 WireShark 所提供的功能。</span><span class="sxs-lookup"><span data-stu-id="bae78-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="bae78-141">在 WireShark tooapply hello 篩選器展開 hello 「 傳輸控制通訊協定 」 區段的 [同步處理] 中的封包將擷取，並檢查設定 hello TCP 標頭中的 hello 旗標。</span><span class="sxs-lookup"><span data-stu-id="bae78-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="bae78-142">因為我們會查看 toofilter 上所有 [SYN] 和 [SYN、 ACK] 下的旗標的封包 cofirm hello Syn 位元會設 too1，，然後以滑鼠右鍵按一下 hello Syn 元上的-> 套用篩選]-> [選取。</span><span class="sxs-lookup"><span data-stu-id="bae78-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![圖 7][7]

### <a name="step-4"></a><span data-ttu-id="bae78-144">步驟 4</span><span class="sxs-lookup"><span data-stu-id="bae78-144">Step 4</span></span>

<span data-ttu-id="bae78-145">既然您已經篩選 hello 視窗 tooonly，請參閱封包與 hello [SYN] 設定位元，您可以輕鬆地選取您感興趣 tooview 交談 hello 初始 RTT。</span><span class="sxs-lookup"><span data-stu-id="bae78-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="bae78-146">簡單的方式 tooview hello RTT WireShark 中只需按一下 hello 下拉式清單中標示為 「 SEQ/通知 」 分析。</span><span class="sxs-lookup"><span data-stu-id="bae78-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="bae78-147">然後，您會看到 RTT 顯示的 hello。</span><span class="sxs-lookup"><span data-stu-id="bae78-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="bae78-148">在此情況下，hello RTT 已 0.0022114 秒或 2.211 ms。</span><span class="sxs-lookup"><span data-stu-id="bae78-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![圖 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="bae78-150">不必要的通訊協定</span><span class="sxs-lookup"><span data-stu-id="bae78-150">Unwanted protocols</span></span>

<span data-ttu-id="bae78-151">您可以在已部署於 Azure 中的虛擬機器執行個體上執行許多應用程式。</span><span class="sxs-lookup"><span data-stu-id="bae78-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="bae78-152">這些應用程式的許多通訊透過 hello 網路，可能是不明確的權限。</span><span class="sxs-lookup"><span data-stu-id="bae78-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="bae78-153">使用封包擷取 toostore 網路通訊，我們可以研究如何應用程式會提到 hello 網路上尋找有任何問題。</span><span class="sxs-lookup"><span data-stu-id="bae78-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="bae78-154">在此範例中，我們檢視先前執行之不必要通訊協定的封包擷取，其可能表示來自您電腦上執行之應用程式的未授權通訊。</span><span class="sxs-lookup"><span data-stu-id="bae78-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="bae78-155">步驟 1</span><span class="sxs-lookup"><span data-stu-id="bae78-155">Step 1</span></span>

<span data-ttu-id="bae78-156">使用 hello 在 hello 中前一個案例中，按一下相同的擷取**統計資料** > **通訊協定階層**</span><span class="sxs-lookup"><span data-stu-id="bae78-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![通訊協定階層功能表][2]

<span data-ttu-id="bae78-158">hello 通訊協定階層視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="bae78-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="bae78-159">此檢視會提供一份 hello 擷取工作階段和傳輸及使用 hello 通訊協定所接收的封包的 hello 數目期間使用的所有 hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="bae78-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="bae78-160">此檢視可用於找出您的虛擬機器或網路上不需要的網路流量。</span><span class="sxs-lookup"><span data-stu-id="bae78-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![開啟的通訊協定階層][3]

<span data-ttu-id="bae78-162">您可以看到 hello 下列螢幕擷取畫面中，沒有使用 hello BitTorrent 通訊協定，可用於對等 toopeer 檔案共用的流量。</span><span class="sxs-lookup"><span data-stu-id="bae78-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="bae78-163">身為系統管理員不想 toosee BitTorrent 流量這個特定的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="bae78-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="bae78-164">現在您知道這個流量，您可以移除 hello 對等 toopeer 軟體安裝在此虛擬機器或區塊 hello 流量使用網路安全性群組或防火牆。</span><span class="sxs-lookup"><span data-stu-id="bae78-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="bae78-165">此外，您可以選擇 toorun 封包擷取排程，讓您可以 hello 通訊協定使用定期檢閱在您的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="bae78-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="bae78-166">如需 tooautomate 網路瀏覽 azure 中的工作範例[監視網路資源，使用 azure 自動化](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="bae78-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="bae78-167">尋找最上層目的地和連接埠</span><span class="sxs-lookup"><span data-stu-id="bae78-167">Finding top destinations and ports</span></span>

<span data-ttu-id="bae78-168">了解 hello 類型的流量，hello 端點，並透過進行通訊的 hello 連接埠，請務必監視或疑難排解應用程式和網路上的資源時。</span><span class="sxs-lookup"><span data-stu-id="bae78-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="bae78-169">使用上述的封包擷取檔案，我們可以快速地了解 hello 最前面的目的地我們 VM 通訊的與 hello 正在使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bae78-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="bae78-170">步驟 1</span><span class="sxs-lookup"><span data-stu-id="bae78-170">Step 1</span></span>

<span data-ttu-id="bae78-171">使用 hello 在 hello 中前一個案例中，按一下相同的擷取**統計資料** > **IPv4 統計資料** > **目的地和連接埠**</span><span class="sxs-lookup"><span data-stu-id="bae78-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![封包擷取視窗][4]

### <a name="step-2"></a><span data-ttu-id="bae78-173">步驟 2</span><span class="sxs-lookup"><span data-stu-id="bae78-173">Step 2</span></span>

<span data-ttu-id="bae78-174">當我們查看 hello 結果列凸顯出來時，發生多個連接上連接埠 111。</span><span class="sxs-lookup"><span data-stu-id="bae78-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="bae78-175">hello 最常使用的連接埠是 3389，這是遠端桌面，而剩餘的 hello RPC 動態連接埠。</span><span class="sxs-lookup"><span data-stu-id="bae78-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="bae78-176">雖然此流量可能表示執行任何動作，它是連接埠已用於多個連接，並且為未知的 toohello 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="bae78-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![圖 5][5]

### <a name="step-3"></a><span data-ttu-id="bae78-178">步驟 3</span><span class="sxs-lookup"><span data-stu-id="bae78-178">Step 3</span></span>

<span data-ttu-id="bae78-179">既然我們已經決定外的地方我們可以篩選根據 hello 的連接埠我們擷取的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bae78-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="bae78-180">會在此案例中的 hello 篩選：</span><span class="sxs-lookup"><span data-stu-id="bae78-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="bae78-181">我們在 hello 篩選 文字方塊中輸入 hello 上述的篩選條件文字，並按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="bae78-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![圖 6][6]

<span data-ttu-id="bae78-183">從 hello 結果中，我們可以看到所有的 hello 流量來自本機的虛擬機器上 hello 相同子網路。</span><span class="sxs-lookup"><span data-stu-id="bae78-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="bae78-184">如果我們仍不了解此流量發生的原因，我們可以進一步檢查 hello 封包 toodetermine 為什麼它呼叫這些連接埠 111。</span><span class="sxs-lookup"><span data-stu-id="bae78-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="bae78-185">這項資訊可以採取 hello 適當的動作。</span><span class="sxs-lookup"><span data-stu-id="bae78-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bae78-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bae78-186">Next steps</span></span>

<span data-ttu-id="bae78-187">深入了解造訪 hello 網路監看員的其他診斷功能[Azure 網路監視概觀](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bae78-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













