---
title: "使用 Power BI 將 Azure 網路安全性群組流程記錄視覺化 | Microsoft Docs"
description: "此頁面說明如何使用 Power BI 將 NSG 流程記錄視覺化。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d8c61ca2a3bd5affe02e8f9500655db6699a245f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="59f48-103">使用 Power BI 將網路安全性群組流程記錄視覺化</span><span class="sxs-lookup"><span data-stu-id="59f48-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="59f48-104">網路安全性群組流程記錄可讓您檢視網路安全性群組上輸入和輸出 IP 流量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="59f48-104">Network Security Group flow logs allow you to view information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="59f48-105">這些流程記錄顯示每一個規則的輸出和輸入流程、套用流程的 NIC、有關流程的 5 組資訊 (來源/目的地 IP、來源/目的地連接埠、通訊協定)，以及允許或拒絕流量。</span><span class="sxs-lookup"><span data-stu-id="59f48-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="59f48-106">手動搜尋記錄檔很難深入探索流程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="59f48-106">It can be difficult to gain insights into flow logging data by manually searching the log files.</span></span> <span data-ttu-id="59f48-107">在本文中，我們提供解決方案將最近的流程記錄視覺化，並了解您網路上的流量。</span><span class="sxs-lookup"><span data-stu-id="59f48-107">In this article, we provide a solution to visualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="59f48-108">案例</span><span class="sxs-lookup"><span data-stu-id="59f48-108">Scenario</span></span>

<span data-ttu-id="59f48-109">在下列案例中，我們將 Power BI Desktop 連線至我們已設定的儲存體帳戶，做為 NSG 流程記錄資料的接收器。</span><span class="sxs-lookup"><span data-stu-id="59f48-109">In the following scenario, we connect Power BI desktop to the storage account we have configured as the sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="59f48-110">當我們連線至儲存體帳戶之後，Power BI 會下載並剖析記錄，以視覺表示法呈現網路安全性群組所記錄的流量。</span><span class="sxs-lookup"><span data-stu-id="59f48-110">After we connect to our storage account, Power BI downloads and parses the logs to provide a visual representation of the traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="59f48-111">您可以使用範本中提供的視覺效果來檢查︰</span><span class="sxs-lookup"><span data-stu-id="59f48-111">Using the visuals supplied in the template you can examine:</span></span>

* <span data-ttu-id="59f48-112">熱門 IP</span><span class="sxs-lookup"><span data-stu-id="59f48-112">Top Talkers</span></span>
* <span data-ttu-id="59f48-113">依方向和規則決策的時間序列資料流程</span><span class="sxs-lookup"><span data-stu-id="59f48-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="59f48-114">依網路介面 MAC 位址的流程</span><span class="sxs-lookup"><span data-stu-id="59f48-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="59f48-115">依 NSG 和規則的流程</span><span class="sxs-lookup"><span data-stu-id="59f48-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="59f48-116">依目的地連接埠的流程</span><span class="sxs-lookup"><span data-stu-id="59f48-116">Flows by Destination Port</span></span>

<span data-ttu-id="59f48-117">提供的範本是可編輯的，您可以修改它來新增資料、視覺效果或編輯查詢，以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="59f48-117">The template provided is editable so you can modify it to add new data, visuals, or edit queries to suit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="59f48-118">設定</span><span class="sxs-lookup"><span data-stu-id="59f48-118">Setup</span></span>

<span data-ttu-id="59f48-119">開始之前，您必須在帳戶中的一或多個網路安全性群組上，啟用網路安全性群組流程記錄。</span><span class="sxs-lookup"><span data-stu-id="59f48-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="59f48-120">如需有關啟用網路安全性流程記錄的指示，請參閱下列文章︰[網路安全性群組的流程記錄簡介](network-watcher-nsg-flow-logging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="59f48-120">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="59f48-121">您也必須在機器上安裝 Power BI Desktop 用戶端，而且機器上要有足夠的可用空間，以下載和載入儲存體帳戶中在存的記錄資料。</span><span class="sxs-lookup"><span data-stu-id="59f48-121">You must also have the Power BI Desktop client installed on your machine, and enough free space on your machine to download and load the log data that exists in your storage account.</span></span>

![Visio 圖表][1]

### <a name="steps"></a><span data-ttu-id="59f48-123">步驟</span><span class="sxs-lookup"><span data-stu-id="59f48-123">Steps</span></span>

1. <span data-ttu-id="59f48-124">在 Power BI Desktop 應用程式的[網路監看員 PowerBI 流程記錄範本](https://aka.ms/networkwatcherpowerbiflowlogstemplate)中，下載並開啟下列 Power BI 範本</span><span class="sxs-lookup"><span data-stu-id="59f48-124">Download and open the following Power BI template in the Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="59f48-125">輸入必要的查詢參數</span><span class="sxs-lookup"><span data-stu-id="59f48-125">Enter the required Query parameters</span></span>
    1. <span data-ttu-id="59f48-126">**StorageAccountName** – 指定儲存體帳戶的名稱，此帳戶包含您想要載入和視覺化的 NSG 流程記錄。</span><span class="sxs-lookup"><span data-stu-id="59f48-126">**StorageAccountName** – Specifies to the name of the storage account containing the NSG flow logs that you would like to load and visualize.</span></span>
    1. <span data-ttu-id="59f48-127">**NumberOfLogFiles** – 指定您想要在 Power BI 中下載和視覺化的記錄檔數目。</span><span class="sxs-lookup"><span data-stu-id="59f48-127">**NumberOfLogFiles** – Specifies the number of log files that you would like to download and visualize in Power BI.</span></span> <span data-ttu-id="59f48-128">例如，指定 50 代表最新的 50 個記錄檔。</span><span class="sxs-lookup"><span data-stu-id="59f48-128">For example, if 50 is specified, the 50 latest log files.</span></span> <span data-ttu-id="59f48-129">如果我們有 2 個 NSG 已啟用並設定為將 NSG 流程記錄傳送至這個帳戶，則可以檢視過去 25 小時的記錄。</span><span class="sxs-lookup"><span data-stu-id="59f48-129">Ff we have 2 NSGs enabled and configured to send NSG flow logs to this account, then the past 25 hours of logs can be viewed.</span></span>

    ![power BI 主畫面][2]

1. <span data-ttu-id="59f48-131">輸入儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="59f48-131">Enter the Access Key for your storage account.</span></span> <span data-ttu-id="59f48-132">您可以在 Azure 入口網站瀏覽至您的儲存體帳戶，然後從 [設定] 功能表選取 [存取金鑰]，即可找到有效的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="59f48-132">You can find valid access keys by navigating to your storage account in the Azure portal and selecting **Access Keys** from the Settings menu.</span></span> <span data-ttu-id="59f48-133">按一下 [連線]，然後套用變更。</span><span class="sxs-lookup"><span data-stu-id="59f48-133">Click **Connect** then apply changes.</span></span>

    ![access keys][3]

    ![存取金鑰 2][4]

4.  <span data-ttu-id="59f48-136">您的記錄已下載和剖析，現在可以利用預先建立的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="59f48-136">Your logs are download and parsed and you can now utilize the pre-created visuals.</span></span>

## <a name="understanding-the-visuals"></a><span data-ttu-id="59f48-137">了解視覺效果</span><span class="sxs-lookup"><span data-stu-id="59f48-137">Understanding the visuals</span></span>

<span data-ttu-id="59f48-138">範本中提供幾組視覺效果，有助於理解 NSG 流程記錄資料的意義。</span><span class="sxs-lookup"><span data-stu-id="59f48-138">Provided in the template are a set of visuals that help make sense of the NSG Flow Log data.</span></span> <span data-ttu-id="59f48-139">下圖示範儀表板填入資料後的樣貌。</span><span class="sxs-lookup"><span data-stu-id="59f48-139">The following images show a sample of what the dashboard looks like when populated with data.</span></span> <span data-ttu-id="59f48-140">接下來，我們更詳細地探討每個視覺效果</span><span class="sxs-lookup"><span data-stu-id="59f48-140">Below we examine each visual in greater detail</span></span> 

![powerbi][5]
 
<span data-ttu-id="59f48-142">「熱門 IP」視覺效果顯示指定期間內起始最多連線的 IP。</span><span class="sxs-lookup"><span data-stu-id="59f48-142">The Top Talkers visual shows the IPs that have initiated the most connections over the period specified.</span></span> <span data-ttu-id="59f48-143">方塊大小代表相對的連線數。</span><span class="sxs-lookup"><span data-stu-id="59f48-143">The size of the boxes corresponds to the relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="59f48-145">下列時間序列圖表顯示期間內的流程數。</span><span class="sxs-lookup"><span data-stu-id="59f48-145">The following time series graphs show the number of flows over the period.</span></span> <span data-ttu-id="59f48-146">上方圖表依流程方向切割，下方圖表依所做決策 (允許或拒絕) 分割。</span><span class="sxs-lookup"><span data-stu-id="59f48-146">The upper graph is segmented by the flow direction, and the lower is segmented by the decision made (allow or deny).</span></span> <span data-ttu-id="59f48-147">此視覺效果可讓您檢查一段時間的流量趨勢，並找出流量或流量分割中的任何異常暴增或遽減情況。</span><span class="sxs-lookup"><span data-stu-id="59f48-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="59f48-149">下列圖表顯示每個網路介面的流程，上方是依流程方向分割，下方是依所做決策分割。</span><span class="sxs-lookup"><span data-stu-id="59f48-149">The following graphs show the flows per Network interface, with the upper segmented by flow direction and the lower segmented by decision made.</span></span> <span data-ttu-id="59f48-150">此資訊可讓您深入探索通訊量最大的 VM，以及是否已允許或拒絕流向特定 VM 的流量。</span><span class="sxs-lookup"><span data-stu-id="59f48-150">With this information, you can gain insights into which of your VMs communicated the most relative to others, and if traffic to a specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="59f48-152">下列環圈圖顯示「依目的地連接埠的流程」分解。</span><span class="sxs-lookup"><span data-stu-id="59f48-152">The following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="59f48-153">此資訊可讓您檢視指定期間內最常使用的目的地連接埠。</span><span class="sxs-lookup"><span data-stu-id="59f48-153">With this information, you can view the most commonly used destination ports used within the specified period.</span></span>

![環圈][9]

<span data-ttu-id="59f48-155">下列長條圖顯示依 NSG 和規則的流程。</span><span class="sxs-lookup"><span data-stu-id="59f48-155">The following bar chart shows the Flow by NSG and Rule.</span></span> <span data-ttu-id="59f48-156">此資訊可讓您看到引起最多流量的 NSG，並依規則查看 NSG 的流量分解。</span><span class="sxs-lookup"><span data-stu-id="59f48-156">With this information, you can see the NSGs responsible for the most traffic, and the breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="59f48-158">下列資訊圖表顯示出現在記錄中的 NSG 相關資訊、期間擷取的流程數，以及最早記錄的擷取日期。</span><span class="sxs-lookup"><span data-stu-id="59f48-158">The following informational charts display information about the NSGs present in the logs, the number of Flows captured over the period, and the date of the earliest log captured.</span></span> <span data-ttu-id="59f48-159">此資訊可讓您了解記錄哪些 NSG 和流程的日期範圍。</span><span class="sxs-lookup"><span data-stu-id="59f48-159">This information gives you an idea of what NSGs are being logged and the date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="59f48-162">此範本包括下列交叉分析篩選器，可讓您只檢視最感興趣的資料。</span><span class="sxs-lookup"><span data-stu-id="59f48-162">This template includes the following slicers to allow you to view only the data you are most interested in.</span></span> <span data-ttu-id="59f48-163">您可以依資源群組、NSG 和規則來篩選。</span><span class="sxs-lookup"><span data-stu-id="59f48-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="59f48-164">您也可以依 5 組資訊、決策和記錄的寫入時間來篩選。</span><span class="sxs-lookup"><span data-stu-id="59f48-164">You can also filter on 5-tuple information, decision, and the time the log was written.</span></span>

![交叉分析篩選器][13]

## <a name="conclusion"></a><span data-ttu-id="59f48-166">結論</span><span class="sxs-lookup"><span data-stu-id="59f48-166">Conclusion</span></span>

<span data-ttu-id="59f48-167">我們在此案例中說明，藉由使用網路監看員和 Power BI 所提供的網路安全性群組流程記錄，我們就能夠視覺化並了解流量。</span><span class="sxs-lookup"><span data-stu-id="59f48-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able to visualize and understand the traffic.</span></span> <span data-ttu-id="59f48-168">使用提供的範本時，Power BI 會直接從儲存體下載記錄，然後在本機處理。</span><span class="sxs-lookup"><span data-stu-id="59f48-168">Using the provided template, Power BI downloads the logs directly from storage and processes them locally.</span></span> <span data-ttu-id="59f48-169">載入範本所花費的時間，取決於所要求的檔案數目和下載的檔案大小總計。</span><span class="sxs-lookup"><span data-stu-id="59f48-169">Time taken to load the template varies depending on the number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="59f48-170">請儘管自訂此範本以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="59f48-170">Feel free to customize this template for your needs.</span></span> <span data-ttu-id="59f48-171">Power BI 和網路安全性群組流程記錄互相搭配有許多做法。</span><span class="sxs-lookup"><span data-stu-id="59f48-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="59f48-172">注意事項</span><span class="sxs-lookup"><span data-stu-id="59f48-172">Notes</span></span>

* <span data-ttu-id="59f48-173">記錄依預設儲存於 `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="59f48-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="59f48-174">如果其他資料存在於另一個目錄，則必須修改查詢來提取和處理資料。</span><span class="sxs-lookup"><span data-stu-id="59f48-174">If other data exists in another directory they the queries to pull and process the data must be modified.</span></span>

* <span data-ttu-id="59f48-175">提供的範本不建議用於 1 GB 以上的記錄。</span><span class="sxs-lookup"><span data-stu-id="59f48-175">The provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="59f48-176">如果您有大量的記錄，我們建議您探尋使用其他資料存放區的解決方案，例如 Data Lake 或 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="59f48-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59f48-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59f48-177">Next Steps</span></span>

<span data-ttu-id="59f48-178">請瀏覽[使用開放原始碼工具將往返於 VM 的網路流量模式視覺化](network-watcher-using-open-source-tools.md)，以了解如何以 Elastick Stack 將 NSG 流程記錄視覺化</span><span class="sxs-lookup"><span data-stu-id="59f48-178">Learn how to visualize your NSG flow logs with the Elastick Stack by visiting [Visualize network traffic patterns to and from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
