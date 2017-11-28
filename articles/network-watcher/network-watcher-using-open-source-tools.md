---
title: "使用 Azure 網路監看員和開放原始碼工具將網路流量模式視覺化 | Microsoft Docs"
description: "此頁面描述如何使用網路監看員封包擷取並搭配 Capanalysis，將往返於 VM 的流量模式視覺化。"
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
ms.openlocfilehash: e27bb694d0cbcf1ff7c9d8ca4682a79c8b5c5cb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-network-traffic-patterns-to-and-from-your-vms-using-open-source-tools"></a><span data-ttu-id="a0ff5-103">使用開放原始碼工具將往返於 VM 的網路流量模式視覺化</span><span class="sxs-lookup"><span data-stu-id="a0ff5-103">Visualize network traffic patterns to and from your VMs using open source tools</span></span>

<span data-ttu-id="a0ff5-104">封包擷取包含的網路資料可讓您執行網路鑑識和深入的封包檢查。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-104">Packet captures contain network data that allow you to perform network forensics and deep packet inspection.</span></span> <span data-ttu-id="a0ff5-105">有許多開啟原始碼工具可用來分析封包擷取，以深入探索您的網路。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-105">There are many opens source tools you can use to analyze packet captures to gain insights about your network.</span></span> <span data-ttu-id="a0ff5-106">例如 CapAnalysis，一個開放原始碼封包擷取視覺效果工具。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="a0ff5-107">將封包擷取資料視覺化有助於快速深入探索網路內的模式和異常。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-107">Visualizing packet capture data is a valuable way to quickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="a0ff5-108">視覺效果也可讓您輕鬆分享這種深入解析。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="a0ff5-109">Azure 的網路監看員可讓您在網路上執行封包擷取，以擷取這項重要資料。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-109">Azure’s Network Watcher provides you the ability to capture this valuable data by allowing you to perform packet captures on your network.</span></span> <span data-ttu-id="a0ff5-110">在本文中，我們提供逐步解說，示範如何使用 CapAnalysis 搭配網路監看員，以視覺化和深入探索封包擷取。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-110">In this article, we provide a walkthrough of how to visualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="a0ff5-111">案例</span><span class="sxs-lookup"><span data-stu-id="a0ff5-111">Scenario</span></span>

<span data-ttu-id="a0ff5-112">您在 Azure 的 VM 上部署簡單的 Web 應用程式，而且想要使用開放原始碼工具將網路流量視覺化，以快速識別流程模式和任何可能異常情況。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-112">You have a simple web application deployed on a VM in Azure want to use open source tools to visualize its network traffic to quickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="a0ff5-113">您可以利用網路監看員取得網路環境的封包擷取，並直接儲存在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="a0ff5-114">然後，CapAnalysis 可以直接從儲存體 blob 內嵌封包擷取，並將其內容視覺化。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-114">CapAnalysis can then ingest the packet capture directly from the storage blob and visualize its contents.</span></span>

![案例][1]

## <a name="steps"></a><span data-ttu-id="a0ff5-116">步驟</span><span class="sxs-lookup"><span data-stu-id="a0ff5-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="a0ff5-117">安裝 CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="a0ff5-117">Install CapAnalysis</span></span>

<span data-ttu-id="a0ff5-118">若要在虛擬機器上安裝 CapAnalysis，您可以參考此處理的官方指示：https://www.capanalysis.net/ca/how-to-install-capanalysis。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-118">To install CapAnalysis on a virtual machine, you can refer to the official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="a0ff5-119">為了從遠端存取 CapAnalysis，我們需要在 VM 上新增輸入安全性規則，以開啟連接埠 9877。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-119">In order access CapAnalysis remotely, we need to open port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="a0ff5-120">如需有關在網路安全性群組中建立規則的詳細資訊，請參閱[在現有 NSG 中建立規則](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg)。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-120">For more about creating rules in Network Security Groups, refer to [Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="a0ff5-121">成功新增規則之後，您應該能夠從 `http://<PublicIP>:9877` 存取CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="a0ff5-121">Once the rule has been successfully added, you should be able to access CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-to-start-a-packet-capture-session"></a><span data-ttu-id="a0ff5-122">使用 Azure 網路監看員啟動封包擷取工作階段</span><span class="sxs-lookup"><span data-stu-id="a0ff5-122">Use Azure Network Watcher to start a packet capture session</span></span>

<span data-ttu-id="a0ff5-123">網路監看員可讓您擷取封包，以追蹤進出虛擬機器的流量。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-123">Network Watcher allows you to capture packets to track traffic in and out of a virtual machine.</span></span> <span data-ttu-id="a0ff5-124">您可以參考[使用網路監看員管理封包擷取](network-watcher-packet-capture-manage-portal.md)中的指示，啟動封包擷取工作階段。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-124">You can refer to the instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) to start a packet capture session.</span></span> <span data-ttu-id="a0ff5-125">此封包擷取可以儲存在儲存體 blob 中，供 CapAnalysis 存取。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-125">This packet capture can be stored in a storage blob to be accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-to-capanalysis"></a><span data-ttu-id="a0ff5-126">將封包擷取上傳至 CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="a0ff5-126">Upload a packet capture to CapAnalysis</span></span>
<span data-ttu-id="a0ff5-127">您可以使用 [從 URL 匯入] 索引標籤，並提供儲存封包擷取的儲存體 blob 連結，以直接上傳網路監看員所產生的封包擷取。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-127">You can directly upload a packet capture taken by network watcher using the “Import from URL” tab and providing a link to the storage blob where the packet capture is stored.</span></span>

<span data-ttu-id="a0ff5-128">提供 CapAnalysis 的連結時，請務必將 SAS 權杖附加至儲存體 blob URL。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-128">When providing a link to CapAnalysis, make sure to append a SAS token to the storage blob URL.</span></span>  <span data-ttu-id="a0ff5-129">若要這樣做，請從儲存體帳戶瀏覽至共用存取簽章，指定允許的權限，然後按下 [產生 SAS] 按鈕以建立權杖。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-129">To do this, navigate to Shared access signature from the storage account, designate the allowed permissions, and press the Generate SAS button to create a token.</span></span> <span data-ttu-id="a0ff5-130">接著，您可以將此 SAS 權杖附加至封包擷取儲存體 blob URL。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-130">You can then append this SAS token to the packet capture storage blob URL.</span></span>

<span data-ttu-id="a0ff5-131">產生的 URL 如下︰http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="a0ff5-131">The resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="a0ff5-132">分析封包擷取</span><span class="sxs-lookup"><span data-stu-id="a0ff5-132">Analyzing packet captures</span></span>

<span data-ttu-id="a0ff5-133">CapAnalysis 提供各種選項將封包擷取視覺化，各以不同的觀點提供分析。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-133">CapAnalysis offers various options to visualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="a0ff5-134">這些視覺化摘要可讓您了解網路流量趨勢，並快速找出任何不尋常的活動。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="a0ff5-135">下列清單顯示其中幾項功能︰</span><span class="sxs-lookup"><span data-stu-id="a0ff5-135">A few of these features are shown in the following list:</span></span>

1. <span data-ttu-id="a0ff5-136">流程資料表</span><span class="sxs-lookup"><span data-stu-id="a0ff5-136">Flow Tables</span></span>

    <span data-ttu-id="a0ff5-137">下表提供封包資料中的流程清單、流程相關聯的時間戳記和流程相關聯的各種通訊協定，以及來源和目的地 IP。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-137">This table gives you the list of flows in the packet data, the time stamp associated with the flows and the various protocols associated with the flow, as well as source and destination IP.</span></span>

    ![capanalysis 流程頁面][5]

1. <span data-ttu-id="a0ff5-139">通訊協定概觀</span><span class="sxs-lookup"><span data-stu-id="a0ff5-139">Protocol Overview</span></span>

    <span data-ttu-id="a0ff5-140">此窗格可讓您快速查看各種通訊協定和地理位置的網路流量分佈。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-140">This pane allows you to quickly see the distribution of network traffic over the various protocols and geographies.</span></span>

    ![capanalysis 通訊協定概觀][6]

1. <span data-ttu-id="a0ff5-142">統計資料</span><span class="sxs-lookup"><span data-stu-id="a0ff5-142">Statistics</span></span>

    <span data-ttu-id="a0ff5-143">此窗格可讓您檢視網路流量統計資料 – 從來源和目的地 IP 傳送和接收的位元組、每個來源和目的地 IP 的流程、用於各種流程的通訊協定，以及流程的持續時間。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-143">This pane allows you to view network traffic statistics – bytes sent and received from source and destination IPs, flows for each of the source and destination IPs, protocol used for various flows, and the duration of flows.</span></span>

    ![capanalysis 統計資料][7]

1. <span data-ttu-id="a0ff5-145">Geomap</span><span class="sxs-lookup"><span data-stu-id="a0ff5-145">Geomap</span></span>

    <span data-ttu-id="a0ff5-146">此窗格提供網路流量的地圖檢視，並依據每個國家/地區的流量大小而改變顏色。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-146">This pane provides you with a map view of your network traffic, with colors scaling to the volume of traffic from each country.</span></span> <span data-ttu-id="a0ff5-147">您可以選取醒目提示的國家/地區，以檢視其他流程統計資料，例如從該國家/地區中的 IP 傳送和接收的資料比例。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-147">You can select highlighted countries to view additional flow statistics such as the proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="a0ff5-149">篩選器</span><span class="sxs-lookup"><span data-stu-id="a0ff5-149">Filters</span></span>

    <span data-ttu-id="a0ff5-150">CapAnalysis 提供一組可快速分析特定封包的篩選器。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="a0ff5-151">例如，您可以選擇依通訊協定來篩選資料，以具體深入探索該流量子集。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-151">For example, you can choose to filter the data by protocol to gain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="a0ff5-153">請瀏覽 [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about)，深入了解 CapAnalysis 的所有功能。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) to learn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="a0ff5-154">結論</span><span class="sxs-lookup"><span data-stu-id="a0ff5-154">Conclusion</span></span>

<span data-ttu-id="a0ff5-155">網路監看員的封包擷取功能可讓您擷取執行網路鑑識所需的資料，並深入了解您的網路流量。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-155">Network Watcher’s packet capture feature allows you to capture the data necessary to perform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="a0ff5-156">在此案例中，我們示範如何使用開放原始碼視覺效果工具，輕鬆地整合來自網路監看員的封包擷取。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="a0ff5-157">使用 CapAnalysis 之類的開放原始碼工具將封包擷取視覺化，可讓您執行深入的封包檢查，並快速識別網路流量的趨勢。</span><span class="sxs-lookup"><span data-stu-id="a0ff5-157">By using open source tools such as CapAnalysis to visualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0ff5-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0ff5-158">Next steps</span></span>

<span data-ttu-id="a0ff5-159">若要深入了解 NSG 流程記錄，請參閱 [NSG 流程記錄](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a0ff5-159">To learn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="a0ff5-160">若要了解如何利用 Power BI 將 NSG 流量記錄視覺化，請瀏覽[利用 Power BI 將 NSG 流量記錄視覺](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="a0ff5-160">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
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
