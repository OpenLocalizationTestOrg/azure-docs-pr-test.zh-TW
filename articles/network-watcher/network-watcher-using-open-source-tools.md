---
title: "Azure 網路監看員與開放原始碼工具 aaaVisualize 網路流量模式 |Microsoft 文件"
description: "此頁面描述 toouse 網路監看員封包如何擷取與 Capanalysis toovisualize 流量模式 tooand 從您的 Vm。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="15253-103">以視覺化方式檢視您使用開放原始碼工具的 Vm 所傳來的網路流量模式 tooand</span><span class="sxs-lookup"><span data-stu-id="15253-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="15253-104">封包擷取包含 tooperform 網路鑑證和深度封包檢查可讓您的網路資料。</span><span class="sxs-lookup"><span data-stu-id="15253-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="15253-105">有許多開啟原始碼工具，您可以使用 tooanalyze 封包擷取 toogain insights 解您的網路。</span><span class="sxs-lookup"><span data-stu-id="15253-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="15253-106">例如 CapAnalysis，一個開放原始碼封包擷取視覺效果工具。</span><span class="sxs-lookup"><span data-stu-id="15253-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="15253-107">視覺化封包擷取資料是 tooquickly 衍生的模式和網路中的異常狀況的洞察能力的重要方法。</span><span class="sxs-lookup"><span data-stu-id="15253-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="15253-108">視覺效果也可讓您輕鬆分享這種深入解析。</span><span class="sxs-lookup"><span data-stu-id="15253-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="15253-109">Azure 的網路監看員會提供您在網路上 hello 能力 toocapture 此寶貴的資料，可讓您 tooperform 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="15253-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="15253-110">在本文中，我們會提供 toovisualize 並取得深入資訊從封包擷取 CapAnalysis 使用網路監看員的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="15253-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="15253-111">案例</span><span class="sxs-lookup"><span data-stu-id="15253-111">Scenario</span></span>

<span data-ttu-id="15253-112">您已部署的簡單 web 應用程式上的 VM 中 Azure 想 toouse 開放原始碼工具 toovisualize 其網路流量 tooquickly 識別流量模式和可能的異常狀況。</span><span class="sxs-lookup"><span data-stu-id="15253-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="15253-113">您可以利用網路監看員取得網路環境的封包擷取，並直接儲存在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="15253-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="15253-114">CapAnalysis 可以內嵌 hello 封包擷取直接從 hello 儲存體 blob，並以視覺化方式檢視其內容。</span><span class="sxs-lookup"><span data-stu-id="15253-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![案例][1]

## <a name="steps"></a><span data-ttu-id="15253-116">步驟</span><span class="sxs-lookup"><span data-stu-id="15253-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="15253-117">安裝 CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="15253-117">Install CapAnalysis</span></span>

<span data-ttu-id="15253-118">tooinstall CapAnalysis 虛擬機器上的，您可以參考 toohello 官方指示這裡 https://www.capanalysis.net/ca/how-to-install-capanalysis。</span><span class="sxs-lookup"><span data-stu-id="15253-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="15253-119">順序 CapAnalysis 遠端存取，我們需要您的 VM 上 tooopen 連接埠 9877 藉由新增新的連入的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="15253-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="15253-120">如需建立網路安全性群組中的規則相關資訊，請參閱太[建立現有 NSG 中的規則](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg)。</span><span class="sxs-lookup"><span data-stu-id="15253-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="15253-121">已成功新增 hello 規則，您應該能夠 tooaccess CapAnalysis 從`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="15253-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="15253-122">使用 Azure 網路監看員 toostart 封包擷取工作階段</span><span class="sxs-lookup"><span data-stu-id="15253-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="15253-123">網路監看員，可讓您 toocapture 封包 tootrack 流量進出虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="15253-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="15253-124">您可以使用參照 toohello 指示[網路監看員擷取管理封包](network-watcher-packet-capture-manage-portal.md)toostart 封包擷取工作階段。</span><span class="sxs-lookup"><span data-stu-id="15253-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="15253-125">此封包擷取可以儲存在儲存體 blob toobe CapAnalysis 所存取。</span><span class="sxs-lookup"><span data-stu-id="15253-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="15253-126">上傳封包擷取 tooCapAnalysis</span><span class="sxs-lookup"><span data-stu-id="15253-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="15253-127">您可以直接上傳所網路監看員使用 hello 「 匯入從 URL 索引標籤並提供連結 toohello 儲存體 blob 儲存 hello 封包擷取封包擷取。</span><span class="sxs-lookup"><span data-stu-id="15253-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="15253-128">當提供連結 tooCapAnalysis，請確定 tooappend SAS 權杖 toohello 儲存體 blob URL。</span><span class="sxs-lookup"><span data-stu-id="15253-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="15253-129">toodo，導覽 tooShared hello 儲存體帳戶的存取簽章、 指定 hello 允許權限，然後按 hello 產生 SAS 按鈕 toocreate 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="15253-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="15253-130">然後，您可以附加此 SAS 權杖 toohello 封包擷取儲存體 blob URL。</span><span class="sxs-lookup"><span data-stu-id="15253-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="15253-131">hello 產生 URL 看起來會像這樣： http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="15253-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="15253-132">分析封包擷取</span><span class="sxs-lookup"><span data-stu-id="15253-132">Analyzing packet captures</span></span>

<span data-ttu-id="15253-133">CapAnalysis 提供各種選項 toovisualize 封包擷取，每個提供的分析，以不同的觀點。</span><span class="sxs-lookup"><span data-stu-id="15253-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="15253-134">這些視覺化摘要可讓您了解網路流量趨勢，並快速找出任何不尋常的活動。</span><span class="sxs-lookup"><span data-stu-id="15253-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="15253-135">這些功能的一些顯示 hello 清單後面：</span><span class="sxs-lookup"><span data-stu-id="15253-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="15253-136">流程資料表</span><span class="sxs-lookup"><span data-stu-id="15253-136">Flow Tables</span></span>

    <span data-ttu-id="15253-137">此資料表提供 hello hello 封包資料流的清單、 hello 與 hello 流程相關聯的時間戳記和 hello 與 hello 流程，以及來源和目的地 IP 相關聯的各種通訊協定。</span><span class="sxs-lookup"><span data-stu-id="15253-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![capanalysis 流程頁面][5]

1. <span data-ttu-id="15253-139">通訊協定概觀</span><span class="sxs-lookup"><span data-stu-id="15253-139">Protocol Overview</span></span>

    <span data-ttu-id="15253-140">此窗格可讓您 tooquickly 會查看一段 hello 網路流量的 hello 分佈各種通訊協定和地理位置。</span><span class="sxs-lookup"><span data-stu-id="15253-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![capanalysis 通訊協定概觀][6]

1. <span data-ttu-id="15253-142">統計資料</span><span class="sxs-lookup"><span data-stu-id="15253-142">Statistics</span></span>

    <span data-ttu-id="15253-143">此窗格可讓您 tooview 網路流量統計資料-位元組傳送並接收來自來源和目的地的 hello 來源和目的地 Ip 時，每個流量的 Ip 通訊協定用於各種流程和流程 hello 持續時間。</span><span class="sxs-lookup"><span data-stu-id="15253-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![capanalysis 統計資料][7]

1. <span data-ttu-id="15253-145">Geomap</span><span class="sxs-lookup"><span data-stu-id="15253-145">Geomap</span></span>

    <span data-ttu-id="15253-146">這個窗格您提供的網路流量，地圖檢視使用色彩調整 toohello 磁碟區中每個國家/地區的流量。</span><span class="sxs-lookup"><span data-stu-id="15253-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="15253-147">您可以選取反白顯示國家/地區 tooview 其他流程統計資料，例如 hello 比例的資料傳送和接收從該國家/地區中的 Ip。</span><span class="sxs-lookup"><span data-stu-id="15253-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="15253-149">篩選器</span><span class="sxs-lookup"><span data-stu-id="15253-149">Filters</span></span>

    <span data-ttu-id="15253-150">CapAnalysis 提供一組可快速分析特定封包的篩選器。</span><span class="sxs-lookup"><span data-stu-id="15253-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="15253-151">例如，您可以選擇 toofilter hello 資料由該子集的傳輸通訊協定 toogain 特定 insights。</span><span class="sxs-lookup"><span data-stu-id="15253-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="15253-153">請瀏覽[https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn 深入了解所有 CapAnalysis 功能。</span><span class="sxs-lookup"><span data-stu-id="15253-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="15253-154">結論</span><span class="sxs-lookup"><span data-stu-id="15253-154">Conclusion</span></span>

<span data-ttu-id="15253-155">監看員網路封包擷取功能可讓您 toocapture hello 資料所需的 tooperform 網路鑑識調查，並深入了解您的網路流量。</span><span class="sxs-lookup"><span data-stu-id="15253-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="15253-156">在此案例中，我們示範如何使用開放原始碼視覺效果工具，輕鬆地整合來自網路監看員的封包擷取。</span><span class="sxs-lookup"><span data-stu-id="15253-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="15253-157">使用開放原始碼工具，例如 CapAnalysis toovisualize 封包擷取，您可以執行深度封包檢查，並快速識別在您的網路流量的趨勢。</span><span class="sxs-lookup"><span data-stu-id="15253-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15253-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15253-158">Next steps</span></span>

<span data-ttu-id="15253-159">toolearn 進一步了解 NSG 流程記錄檔，請瀏覽[NSG 流程記錄](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="15253-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="15253-160">了解 toovisualize NSG 流程記錄的方式有了 Power BI 瀏覽[視覺化 NSG 流動 Power BI 的記錄檔](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="15253-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
