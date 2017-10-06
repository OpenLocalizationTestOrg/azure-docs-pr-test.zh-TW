---
title: "使用 Power BI 記錄 aaaVisualizing Azure 網路安全性小組流程 |Microsoft 文件"
description: "此頁面描述 toovisualize NSG 流程記錄使用 Power BI 的方式。"
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
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="45027-103">使用 Power BI 將網路安全性群組流程記錄視覺化</span><span class="sxs-lookup"><span data-stu-id="45027-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="45027-104">網路安全性小組流程記錄檔可讓您 tooview 資訊 ingress 和 egress IP 流量的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="45027-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="45027-105">這些流程記錄檔會顯示輸出，以每個規則為基礎的輸入的流量，hello NIC hello 流程套，hello 流程 (來源/目的地 IP，來源/目的地連接埠通訊協定)，和如果允許或拒絕 hello 流量的 5 個 tuple 資訊。</span><span class="sxs-lookup"><span data-stu-id="45027-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="45027-106">可能很難 toogain 深入了解藉由手動搜尋 hello 記錄檔記錄資料的資料流程。</span><span class="sxs-lookup"><span data-stu-id="45027-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="45027-107">在本文中，我們會提供方案 toovisualize 您最新流程記錄，並了解您的網路上的流量。</span><span class="sxs-lookup"><span data-stu-id="45027-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="45027-108">案例</span><span class="sxs-lookup"><span data-stu-id="45027-108">Scenario</span></span>

<span data-ttu-id="45027-109">在 hello 遵照案例，我們連接 Power BI 桌面 toohello 儲存體帳戶，我們已經設定成 hello 接收 NSG 流程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="45027-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="45027-110">我們連接 tooour 儲存體帳戶之後，Power BI 會下載並剖析 hello 記錄 tooprovide hello 流量記錄的網路安全性群組的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="45027-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="45027-111">使用中，您可以檢查 hello 範本所提供的 hello 視覺效果：</span><span class="sxs-lookup"><span data-stu-id="45027-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="45027-112">熱門 IP</span><span class="sxs-lookup"><span data-stu-id="45027-112">Top Talkers</span></span>
* <span data-ttu-id="45027-113">依方向和規則決策的時間序列資料流程</span><span class="sxs-lookup"><span data-stu-id="45027-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="45027-114">依網路介面 MAC 位址的流程</span><span class="sxs-lookup"><span data-stu-id="45027-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="45027-115">依 NSG 和規則的流程</span><span class="sxs-lookup"><span data-stu-id="45027-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="45027-116">依目的地連接埠的流程</span><span class="sxs-lookup"><span data-stu-id="45027-116">Flows by Destination Port</span></span>

<span data-ttu-id="45027-117">提供 hello 範本是可編輯，因此您可以修改它 tooadd 新資料，視覺效果，或編輯查詢 toosuit 您的需求。</span><span class="sxs-lookup"><span data-stu-id="45027-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="45027-118">設定</span><span class="sxs-lookup"><span data-stu-id="45027-118">Setup</span></span>

<span data-ttu-id="45027-119">開始之前，您必須在帳戶中的一或多個網路安全性群組上，啟用網路安全性群組流程記錄。</span><span class="sxs-lookup"><span data-stu-id="45027-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="45027-120">如需有關啟用網路安全性指示傳送記錄檔，請參閱下列文章 toohello:[網路安全性群組的簡介 tooflow 記錄](network-watcher-nsg-flow-logging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="45027-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="45027-121">您也必須 hello Power BI Desktop 用戶端安裝在您的電腦，以及足夠可用空間對機器 toodownload 和負載 hello 記錄資料位於儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45027-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Visio 圖表][1]

### <a name="steps"></a><span data-ttu-id="45027-123">步驟</span><span class="sxs-lookup"><span data-stu-id="45027-123">Steps</span></span>

1. <span data-ttu-id="45027-124">下載並開啟下列 hello Power BI Desktop 的應用程式中的 Power BI 範本的 hello[網路監看員 PowerBI 流程記錄範本](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="45027-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="45027-125">輸入所需的 hello 查詢參數</span><span class="sxs-lookup"><span data-stu-id="45027-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="45027-126">**StorageAccountName** – hello 包含 hello NSG 流程記錄，您的儲存體帳戶指定 toohello 名稱會喜歡 tooload 和視覺化。</span><span class="sxs-lookup"><span data-stu-id="45027-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="45027-127">**NumberOfLogFiles** – 指定記錄檔，您會想 toodownload，並在 Power BI 中視覺化的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="45027-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="45027-128">例如，如果指定 50，則 hello 50 個最新的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="45027-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="45027-129">我們有 2 Nsg ff 啟用並設定 toosend NSG 流量記錄 toothis 帳戶，然後 hello 過去 25 小時的記錄檔可以檢視。</span><span class="sxs-lookup"><span data-stu-id="45027-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![power BI 主畫面][2]

1. <span data-ttu-id="45027-131">輸入 hello 儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="45027-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="45027-132">您可以藉由瀏覽 tooyour hello Azure 入口網站與選取的儲存體帳戶中找到有效的存取金鑰**便捷鍵**hello 設定 功能表中。</span><span class="sxs-lookup"><span data-stu-id="45027-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="45027-133">按一下 [連線]，然後套用變更。</span><span class="sxs-lookup"><span data-stu-id="45027-133">Click **Connect** then apply changes.</span></span>

    ![access keys][3]

    ![存取金鑰 2][4]

4.  <span data-ttu-id="45027-136">您記錄已下載並剖析，現在，您可以利用 hello 預先建立視覺效果。</span><span class="sxs-lookup"><span data-stu-id="45027-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="45027-137">了解 hello 視覺效果</span><span class="sxs-lookup"><span data-stu-id="45027-137">Understanding hello visuals</span></span>

<span data-ttu-id="45027-138">提供在 hello 範本是一組視覺效果，協助意義的 hello NSG 流程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="45027-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="45027-139">hello 下列影像顯示哪些 hello 儀表板看起來像當填入資料的範例。</span><span class="sxs-lookup"><span data-stu-id="45027-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="45027-140">接下來，我們更詳細地探討每個視覺效果</span><span class="sxs-lookup"><span data-stu-id="45027-140">Below we examine each visual in greater detail</span></span> 

![powerbi][5]
 
<span data-ttu-id="45027-142">hello 頂端說話者包括代表視覺顯示 hello Ip 已起始的一段指定期間的 hello hello 大多數的連線。</span><span class="sxs-lookup"><span data-stu-id="45027-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="45027-143">hello hello 方塊大小對應 toohello 相對連接數目。</span><span class="sxs-lookup"><span data-stu-id="45027-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="45027-145">hello 下列時間序列圖形顯示 hello hello 段流程數目。</span><span class="sxs-lookup"><span data-stu-id="45027-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="45027-146">hello 文字方向，區隔 hello 上方圖表和較低的 hello hello 決定 （允許或拒絕） 區隔。</span><span class="sxs-lookup"><span data-stu-id="45027-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="45027-147">此視覺效果可讓您檢查一段時間的流量趨勢，並找出流量或流量分割中的任何異常暴增或遽減情況。</span><span class="sxs-lookup"><span data-stu-id="45027-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="45027-149">hello 下圖顯示 hello 流量每個網路介面，hello 左上區隔文字方向與 hello 較低的區隔所做的決策。</span><span class="sxs-lookup"><span data-stu-id="45027-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="45027-150">使用這項資訊，您可以取得深入了解哪些 Vm 通訊 hello 大部分相對 tooothers，而且如果流量 tooa 特定 VM 是允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="45027-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="45027-152">hello 遵循甜甜圈滾輪圖表會顯示由目的地連接埠的流量的細目。</span><span class="sxs-lookup"><span data-stu-id="45027-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="45027-153">利用此資訊，您可以檢視最常用的 hello 目的地連接埠中指定的 hello 使用期限。</span><span class="sxs-lookup"><span data-stu-id="45027-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![環圈][9]

<span data-ttu-id="45027-155">hello 下列橫條圖顯示 hello NSG 及規則的流量。</span><span class="sxs-lookup"><span data-stu-id="45027-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="45027-156">利用此資訊，您可以看到 hello Nsg 負責 hello 大部分的流量，以及 hello 分解的流量上 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="45027-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="45027-158">hello 下列參考用的圖表顯示 hello Nsg hello 記錄檔中、 資訊 hello 流程擷取透過 hello 期間 hello 的日期和 hello 擷取最早的記錄數目。</span><span class="sxs-lookup"><span data-stu-id="45027-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="45027-159">這項資訊可讓您了解哪些 Nsg 會記錄和 hello 流程的日期範圍。</span><span class="sxs-lookup"><span data-stu-id="45027-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="45027-162">此範本包括 hello 下列交叉分析篩選器 tooallow 您 tooview 您最感興趣只有 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="45027-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="45027-163">您可以依資源群組、NSG 和規則來篩選。</span><span class="sxs-lookup"><span data-stu-id="45027-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="45027-164">您也可以篩選 5-tuple 資訊、 決策、 hello hello 記錄寫入時和時間。</span><span class="sxs-lookup"><span data-stu-id="45027-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![交叉分析篩選器][13]

## <a name="conclusion"></a><span data-ttu-id="45027-166">結論</span><span class="sxs-lookup"><span data-stu-id="45027-166">Conclusion</span></span>

<span data-ttu-id="45027-167">我們也示範了在此案例中，藉由使用網路安全性群組流網路監看員和 Power BI 所提供的記錄檔，我們可以 toovisualize 而了解 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="45027-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="45027-168">使用提供的 hello 範本時，Power BI 直接從儲存體下載 hello 記錄檔，並在本機處理它們。</span><span class="sxs-lookup"><span data-stu-id="45027-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="45027-169">所花費時間 tooload hello 範本而有所不同 hello 數目所要求的檔案和下載檔案的大小總計。</span><span class="sxs-lookup"><span data-stu-id="45027-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="45027-170">您可用 toocustomize 此範本符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="45027-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="45027-171">Power BI 和網路安全性群組流程記錄互相搭配有許多做法。</span><span class="sxs-lookup"><span data-stu-id="45027-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="45027-172">注意事項</span><span class="sxs-lookup"><span data-stu-id="45027-172">Notes</span></span>

* <span data-ttu-id="45027-173">記錄依預設儲存於 `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="45027-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="45027-174">如果有另一個目錄中的其他資料在 hello 查詢 toopull，必須修改處理程序 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="45027-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="45027-175">提供的 hello 範本不是建議使用具有 1 GB 以上的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="45027-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="45027-176">如果您有大量的記錄，我們建議您探尋使用其他資料存放區的解決方案，例如 Data Lake 或 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="45027-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45027-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45027-177">Next Steps</span></span>

<span data-ttu-id="45027-178">了解 toovisualize NSG 流程記錄的方式以 hello Elastick 堆疊造訪[視覺化網路流量模式 tooand 從您的 Vm 使用開放原始碼工具](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="45027-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

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
