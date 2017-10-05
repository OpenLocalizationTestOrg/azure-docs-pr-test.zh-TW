---
title: "針對 SAP HANA on Azure (大型執行個體) 進行疑難排解和監視 | Microsoft Docs"
description: "針對 SAP HANA on Azure (大型執行個體) 進行疑難排解和監視。"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee5be707b443cbe42bf4a492d79390e534d4b91f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="87242-103">如何針對 Azure 上 SAP HANA (大型執行個體) 進行疑難排解和監視</span><span class="sxs-lookup"><span data-stu-id="87242-103">How to troubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="87242-104">SAP HANA on Azure (大型執行個體) 中的監視</span><span class="sxs-lookup"><span data-stu-id="87242-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="87242-105">SAP HANA on Azure (大型執行個體) 與任何其他 IaaS 部署並無不同 - 您必須監視 OS 和應用程式在執行什麼作業，以及這些作業如何耗用下列資源：</span><span class="sxs-lookup"><span data-stu-id="87242-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need to monitor what the OS and the application is doing and how these consume the following resources:</span></span>

- <span data-ttu-id="87242-106">CPU</span><span class="sxs-lookup"><span data-stu-id="87242-106">CPU</span></span>
- <span data-ttu-id="87242-107">記憶體</span><span class="sxs-lookup"><span data-stu-id="87242-107">Memory</span></span>
- <span data-ttu-id="87242-108">網路頻寬</span><span class="sxs-lookup"><span data-stu-id="87242-108">Network bandwidth</span></span>
- <span data-ttu-id="87242-109">磁碟空間</span><span class="sxs-lookup"><span data-stu-id="87242-109">Disk space</span></span>

<span data-ttu-id="87242-110">與使用「Azure 虛擬機器」一樣，您必須了解上述資源類別是否足夠，或它們是否已耗盡。</span><span class="sxs-lookup"><span data-stu-id="87242-110">As with Azure Virtual Machines you need to figure out whether the resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="87242-111">以下提供每個這些不同類別的更多詳細資料：</span><span class="sxs-lookup"><span data-stu-id="87242-111">Here is more detail on each of the different classes:</span></span>

<span data-ttu-id="87242-112">**CPU 資源耗用量：**系統會強制執行 SAP 為針對 HANA 的特定工作負載定義的比例，以確保有足夠的 CPU 資源可用來處理儲存在記憶體中的資料。</span><span class="sxs-lookup"><span data-stu-id="87242-112">**CPU resource consumption:** The ratio that SAP defined for certain workload against HANA is enforced to make sure that there should be enough CPU resources available to work through the data that is stored in memory.</span></span> <span data-ttu-id="87242-113">不過，可能會有因為遺漏索引或類似的問題，而導致 HANA 耗用許多執行查詢的 CPU 的情況。</span><span class="sxs-lookup"><span data-stu-id="87242-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due to missing indexes or similar issues.</span></span> <span data-ttu-id="87242-114">這意謂著您不僅應該監視特定 HANA 服務所耗用的 CPU 資源，也應該監視 HANA 大型執行個體單位的 CPU 資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="87242-114">This means you should monitor CPU resource consumption of the HANA large instance unit as well as CPU resources consumed by the specific HANA services.</span></span>

<span data-ttu-id="87242-115">**記憶體耗用量：**從 HANA 內部監視與從 HANA 外部在單位上監視一樣重要。</span><span class="sxs-lookup"><span data-stu-id="87242-115">**Memory consumption:** Is important to monitor from within HANA, as well as outside of HANA on the unit.</span></span> <span data-ttu-id="87242-116">在 HANA 內，您可以監視資料如何耗用 HANA 已配置的記憶體，以便保持在 SAP 所要求的大小指導方針限制內。</span><span class="sxs-lookup"><span data-stu-id="87242-116">Within HANA, monitor how the data is consuming HANA allocated memory in order to stay within the required sizing guidelines of SAP.</span></span> <span data-ttu-id="87242-117">您也可以監視「大型執行個體」層級的記憶體耗用量，以確保所安裝的額外非 HANA 軟體不會耗用太多記憶體而與 HANA 爭用記憶體。</span><span class="sxs-lookup"><span data-stu-id="87242-117">You also want to monitor memory consumption on the Large Instance level to make sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="87242-118">**網路頻寬：**Azure VNet 閘道對於將資料移入 Azure VNet 的頻寬方面有所限制，因此監視 VNet 內所有 Azure VM 所接收的資料相當有用，可了解您有多接近所選 Azure 閘道 SKU 的限制。</span><span class="sxs-lookup"><span data-stu-id="87242-118">**Network bandwidth:** The Azure VNet gateway is limited in bandwidth of data moving into the Azure VNet, so it is helpful to monitor the data received by all the Azure VMs within a VNet to figure out how close you are to the limits of the Azure gateway SKU you selected.</span></span> <span data-ttu-id="87242-119">在「HANA 大型執行個體」單位上，監視連入和連出網路流量，並隨著時間記錄所處理的磁碟區，是有意義的。</span><span class="sxs-lookup"><span data-stu-id="87242-119">On the HANA Large Instance unit, it does make sense to monitor incoming and outgoing network traffic as well, and to keep track of the volumes that are handled over time.</span></span>

<span data-ttu-id="87242-120">**磁碟空間：**磁碟空間耗用量通常會隨著時間增加。</span><span class="sxs-lookup"><span data-stu-id="87242-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="87242-121">其原因有許多，但最重要的包括：資料量增加、執行交易記錄備份、儲存追蹤檔案，以及執行儲存體快照。</span><span class="sxs-lookup"><span data-stu-id="87242-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="87242-122">因此，監視磁碟空間使用量並管理與「HANA 大型執行個體」單位關聯的磁碟空間相當重要。</span><span class="sxs-lookup"><span data-stu-id="87242-122">Therefore, it is important to monitor disk space usage and manage the disk space associated with the HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="87242-123">從 HANA 端進行監視和疑難排解</span><span class="sxs-lookup"><span data-stu-id="87242-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="87242-124">為了有效分析與 SAP HANA on Azure (大型執行個體) 相關的問題，縮小問題的根本原因範圍會相當有用。</span><span class="sxs-lookup"><span data-stu-id="87242-124">In order to effectively analyze problems related to SAP HANA on Azure (Large Instances), it is useful to narrow down the root cause of a problem.</span></span> <span data-ttu-id="87242-125">SAP 已發佈大量文件來協助您。</span><span class="sxs-lookup"><span data-stu-id="87242-125">SAP has published a large amount of documentation to help you.</span></span>

<span data-ttu-id="87242-126">您可以在下列 SAP 附註中找到與 SAP HANA 效能相關的適用常見問題集：</span><span class="sxs-lookup"><span data-stu-id="87242-126">Applicable FAQs related to SAP HANA performance can be found in the following SAP Notes:</span></span>

- [<span data-ttu-id="87242-127">SAP 附註 #2222200 - 常見問題集：SAP HANA 網路</span><span class="sxs-lookup"><span data-stu-id="87242-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="87242-128">SAP 附註 #2100040 - 常見問題集：SAP HANA CPU</span><span class="sxs-lookup"><span data-stu-id="87242-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="87242-129">SAP 附註 #199997 - 常見問題集：SAP HANA 記憶體</span><span class="sxs-lookup"><span data-stu-id="87242-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="87242-130">SAP 附註 #200000 - 常見問題集：SAP HANA 效能最佳化</span><span class="sxs-lookup"><span data-stu-id="87242-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="87242-131">SAP 附註 #199930 - 常見問題集：SAP HANA I/O 分析</span><span class="sxs-lookup"><span data-stu-id="87242-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="87242-132">SAP 附註 #2177064 - 常見問題集：SAP HANA 服務重新啟動和當機</span><span class="sxs-lookup"><span data-stu-id="87242-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="87242-133">**SAP HANA 警示**</span><span class="sxs-lookup"><span data-stu-id="87242-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="87242-134">第一個步驟是查看目前的 SAP HANA 警示記錄。</span><span class="sxs-lookup"><span data-stu-id="87242-134">As a first step, check the current SAP HANA alert logs.</span></span> <span data-ttu-id="87242-135">在 SAP HANA Studio 中，移至 [Administration Console: Alerts: Show: all alerts] (管理主控台：警示：顯示：所有警示)。</span><span class="sxs-lookup"><span data-stu-id="87242-135">In SAP HANA Studio, go to **Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="87242-136">此索引標籤會顯示在所設定最小和最大臨界值範圍外之特定值的所有 SAP HANA 警示 (可用實體記憶體、CPU 使用率等)。</span><span class="sxs-lookup"><span data-stu-id="87242-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of the set minimum and maximum thresholds.</span></span> <span data-ttu-id="87242-137">根據預設，檢查會每隔 15 分鐘自動重新整理一次。</span><span class="sxs-lookup"><span data-stu-id="87242-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![在 SAP HANA Studio 中，移至 [Administration Console: Alerts: Show: all alerts] (管理主控台：警示：顯示：所有警示)。](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="87242-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="87242-139">**CPU**</span></span>

<span data-ttu-id="87242-140">對於因不適當的臨界值設定而觸發的警示，解決方式是重設為預設值或更合理的臨界值。</span><span class="sxs-lookup"><span data-stu-id="87242-140">For an alert triggered due to improper threshold setting, a resolution is to reset to the default value or a more reasonable threshold value.</span></span>

![重設為預設值或更合理的臨界值](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="87242-142">下列警示可能表示有 CPU 資源問題：</span><span class="sxs-lookup"><span data-stu-id="87242-142">The following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="87242-143">Host CPU Usage (Alert 5) (主機 CPU 使用率 (警示 5))</span><span class="sxs-lookup"><span data-stu-id="87242-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="87242-144">Most recent savepoint operation (Alert 28) (最新的儲存點作業 (警示 28))</span><span class="sxs-lookup"><span data-stu-id="87242-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="87242-145">Savepoint duration (Alert 54) (儲存點持續時間 (警示 54))</span><span class="sxs-lookup"><span data-stu-id="87242-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="87242-146">您可以從下列其中一種情況察覺到 SAP HANA 資料庫的 CPU 耗用量過高：</span><span class="sxs-lookup"><span data-stu-id="87242-146">You may notice high CPU consumption on your SAP HANA database from one of the following:</span></span>

- <span data-ttu-id="87242-147">針對目前和過去的 CPU 使用率，引發了「警示 5」(主機 CPU 使用率)</span><span class="sxs-lookup"><span data-stu-id="87242-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="87242-148">概觀畫面上顯示的 CPU 使用率</span><span class="sxs-lookup"><span data-stu-id="87242-148">The displayed CPU usage on the overview screen</span></span>

![概觀畫面上顯示的 CPU 使用率](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="87242-150">Load (負載) 圖表可能會顯示 CPU 耗用量過高，或過去耗用量過高：</span><span class="sxs-lookup"><span data-stu-id="87242-150">The Load graph might show high CPU consumption, or high consumption in the past:</span></span>

![Load (負載) 圖表可能會顯示 CPU 耗用量過高，或過去耗用量過高](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="87242-152">因 CPU 使用率過高而觸發的警示可能由數個原因造成，包括但不限於：執行特定交易、載入資料、作業死當、長時間執行的 SQL 陳述式，以及查詢效能太差 (例如使用 BW on HANA Cube 時)。</span><span class="sxs-lookup"><span data-stu-id="87242-152">An alert triggered due to high CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="87242-153">如需詳細的疑難排解步驟，請參考 [SAP HANA 疑難排解：CPU 相關的原因和解決方案](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false)網站。</span><span class="sxs-lookup"><span data-stu-id="87242-153">Refer to the [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="87242-154">**作業系統**</span><span class="sxs-lookup"><span data-stu-id="87242-154">**Operating System**</span></span>

<span data-ttu-id="87242-155">SAP HANA on Linux 的其中一項最重要檢查就是要確保停用 Transparent Huge Pages (透明大型頁面)，請參閱 [SAP 附註 #2131662 - SAP HANA 伺服器上的 Transparent Huge Pages (THP)](https://launchpad.support.sap.com/#/notes/2131662)。</span><span class="sxs-lookup"><span data-stu-id="87242-155">One of the most important checks for SAP HANA on Linux is to make sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="87242-156">您可以透過下列 Linux 命令來檢查是否已啟用 Transparent Huge Pages：**cat /sys/kernel/mm/transparent\_hugepage/enabled**</span><span class="sxs-lookup"><span data-stu-id="87242-156">You can check if Transparent Huge Pages are enabled through the following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="87242-157">如果將 _always_ 依下列方式包含在括弧中，即表示啟用 Transparent Huge Pages：[always] madvise never；如果將 _never_ 依下列方式包含在括弧中，則表示停用 Transparent Huge Pages：always madvise [never]</span><span class="sxs-lookup"><span data-stu-id="87242-157">If _always_ is enclosed in brackets as below, it means that the Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that the Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="87242-158">以下 Linux 命令應該不會傳回任何項目：**rpm -qa | grep ulimit**。</span><span class="sxs-lookup"><span data-stu-id="87242-158">The following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="87242-159">如果顯示安裝的是 _ulimit_，請立即將它解除安裝。</span><span class="sxs-lookup"><span data-stu-id="87242-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="87242-160">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="87242-160">**Memory**</span></span>

<span data-ttu-id="87242-161">您可能會注意到 SAP HANA 資料庫所配置的記憶體數量高於預期。</span><span class="sxs-lookup"><span data-stu-id="87242-161">You may observe that the amount of memory allocated by the SAP HANA database is higher than expected.</span></span> <span data-ttu-id="87242-162">下列警示表示有記憶體使用量過高的問題：</span><span class="sxs-lookup"><span data-stu-id="87242-162">The following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="87242-163">Host physical memory usage (Alert 1) (主機實體記憶體使用量 (警示 1))</span><span class="sxs-lookup"><span data-stu-id="87242-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="87242-164">Memory usage of name server (Alert 12) (名稱伺服器的記憶體使用量 (警示 12))</span><span class="sxs-lookup"><span data-stu-id="87242-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="87242-165">Total memory usage of Column Store tables (Alert 40) (資料行存放區資料表的總記憶體使用量 (警示 40))</span><span class="sxs-lookup"><span data-stu-id="87242-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="87242-166">Memory usage of services (Alert 43) (服務的記憶體使用量 (警示 43))</span><span class="sxs-lookup"><span data-stu-id="87242-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="87242-167">Memory usage of main storage of Column Store tables (Alert 45) (資料行存放區資料表的主要儲存體記憶體使用量 (警示 45))</span><span class="sxs-lookup"><span data-stu-id="87242-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="87242-168">Runtime dump files (Alert 46) (執行階段傾印檔案 (警示 46))</span><span class="sxs-lookup"><span data-stu-id="87242-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="87242-169">如需詳細的疑難排解步驟，請參考 [SAP HANA 疑難排解：記憶體問題](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false)網站。</span><span class="sxs-lookup"><span data-stu-id="87242-169">Refer to the [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="87242-170">**網路**</span><span class="sxs-lookup"><span data-stu-id="87242-170">**Network**</span></span>

<span data-ttu-id="87242-171">請參考 [SAP HANA #2081065 - 針對 SAP HANA 網路進行疑難排解](https://launchpad.support.sap.com/#/notes/2081065)，並執行此 SAP 附註中的網路疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="87242-171">Refer to [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform the network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="87242-172">分析伺服器與用戶端之間的來回時間。</span><span class="sxs-lookup"><span data-stu-id="87242-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="87242-173">A.</span><span class="sxs-lookup"><span data-stu-id="87242-173">A.</span></span> <span data-ttu-id="87242-174">執行 SQL 指令碼 [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_。_</span><span class="sxs-lookup"><span data-stu-id="87242-174">Run the SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="87242-175">分析節點間的通訊。</span><span class="sxs-lookup"><span data-stu-id="87242-175">Analyze internode communication.</span></span>
  <span data-ttu-id="87242-176">A.</span><span class="sxs-lookup"><span data-stu-id="87242-176">A.</span></span> <span data-ttu-id="87242-177">執行 SQL 指令碼 [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_。_</span><span class="sxs-lookup"><span data-stu-id="87242-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="87242-178">執行 Linux 命令 **ifconfig** (輸出會顯示是否有發生任何封包遺失的情況)。</span><span class="sxs-lookup"><span data-stu-id="87242-178">Run Linux command **ifconfig** (the output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="87242-179">執行 Linux 命令 **tcpdump**。</span><span class="sxs-lookup"><span data-stu-id="87242-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="87242-180">此外，請使用開放原始碼 [IPERF](https://iperf.fr/) 工具 (或類似的工具) 來測量實際的應用程式網路效能。</span><span class="sxs-lookup"><span data-stu-id="87242-180">Also, use the open source [IPERF](https://iperf.fr/) tool (or similar) to measure real application network performance.</span></span>

<span data-ttu-id="87242-181">如需詳細的疑難排解步驟，請參考 [SAP HANA 疑難排解：網路效能和連線問題](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false)網站。</span><span class="sxs-lookup"><span data-stu-id="87242-181">Refer to the [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="87242-182">**儲存體**</span><span class="sxs-lookup"><span data-stu-id="87242-182">**Storage**</span></span>

<span data-ttu-id="87242-183">從使用者的觀點來看，當發生 I/O 效能問題時，應用程式 (或系統整體) 會執行緩慢、沒有回應，或甚至看似死當。</span><span class="sxs-lookup"><span data-stu-id="87242-183">From an end-user perspective, an application (or the system as a whole) runs sluggishly, is unresponsive, or can even seem to hang if there are issues with I/O performance.</span></span> <span data-ttu-id="87242-184">在 SAP HANA Studio 的 [Volumes] (磁碟區) 索引標籤中，您可以看到連接的磁碟區，以及每個服務使用哪些磁碟區。</span><span class="sxs-lookup"><span data-stu-id="87242-184">In the **Volumes** tab in SAP HANA Studio, you can see the attached volumes, and what volumes are used by each service.</span></span>

![在 SAP HANA Studio 的 [Volumes] (磁碟區) 索引標籤中，您可以看到連接的磁碟區，以及每個服務使用哪些磁碟區。](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="87242-186">在畫面下半部中有連接的磁碟區，您可以看到磁碟區的詳細資料，例如檔案和 I/O 統計資料。</span><span class="sxs-lookup"><span data-stu-id="87242-186">Attached volumes in the lower part of the screen you can see details of the volumes, such as files and I/O statistics.</span></span>

![在畫面下半部中有連接的磁碟區，您可以看到磁碟區的詳細資料，例如檔案和 I/O 統計資料](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="87242-188">如需詳細的疑難排解步驟，請參考 [SAP HANA 疑難排解：I/O 相關的根本原因和解決方案](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false)和 [SAP HANA 疑難排解：磁碟相關的根本原因和解決方案](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false)網站。</span><span class="sxs-lookup"><span data-stu-id="87242-188">Refer to the [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="87242-189">**診斷工具**</span><span class="sxs-lookup"><span data-stu-id="87242-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="87242-190">您可以透過 HANA\_Configuration\_Minichecks 執行「SAP HANA 健康情況檢查」。</span><span class="sxs-lookup"><span data-stu-id="87242-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="87242-191">此工具會傳回應該已在 SAP HANA Studio 中引發成警示的潛在重大技術問題。</span><span class="sxs-lookup"><span data-stu-id="87242-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="87242-192">請參考 [SAP 附註 #1969700 - SAP HANA 的 SQL 陳述式集合](https://launchpad.support.sap.com/#/notes/1969700)，並下載該附註隨附的 SQL Statements.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="87242-192">Refer to [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download the SQL Statements.zip file attached to that note.</span></span> <span data-ttu-id="87242-193">請將這個 .zip 檔案儲存在本機硬碟。</span><span class="sxs-lookup"><span data-stu-id="87242-193">Store this .zip file on the local hard drive.</span></span>

<span data-ttu-id="87242-194">在 SAP HANA Studio 的 [System Information] (系統資訊) 索引標籤上，於 [Name] (名稱) 資料行上按一下滑鼠右鍵，然後選取 [Import SQL Statements] (匯入 SQL 陳述式)。</span><span class="sxs-lookup"><span data-stu-id="87242-194">In SAP HANA Studio, on the **System Information** tab, right-click in the **Name** column and select **Import SQL Statements**.</span></span>

![在 SAP HANA Studio 的 [System Information] (系統資訊) 索引標籤上，於 [Name] (名稱) 資料行上按一下滑鼠右鍵，然後選取 [Import SQL Statements] (匯入 SQL 陳述式)](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="87242-196">選取儲存在本機的 SQL Statements.zip 檔案，將會匯入含有對應的 SQL 陳述式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="87242-196">Select the SQL Statements.zip file stored locally, and a folder with the corresponding SQL statements will be imported.</span></span> <span data-ttu-id="87242-197">此時，可以使用這些 SQL 陳述式來執行許多不同的診斷檢查。</span><span class="sxs-lookup"><span data-stu-id="87242-197">At this point, the many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="87242-198">例如，若要測試「SAP HANA 系統複寫」頻寬需求，請在 [Replication: Bandwidth] (複寫：頻寬) 底下的 [Bandwidth] (頻寬) 陳述式上按一下滑鼠右鍵，然後在 SQL Console (SQL 主控台) 中選取 [Open] (開啟)。</span><span class="sxs-lookup"><span data-stu-id="87242-198">For example, to test SAP HANA System Replication bandwidth requirements, right-click the **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="87242-199">將會開啟完整的 SQL 陳述式，讓您變更輸入參數 (modification 區段)，然後加以執行。</span><span class="sxs-lookup"><span data-stu-id="87242-199">The complete SQL statement opens allowing input parameters (modification section) to be changed and then executed.</span></span>

![將會開啟完整的 SQL 陳述式，讓您變更輸入參數 (modification 區段)，然後加以執行](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="87242-201">另一個範例是在 [Replication: Overview] (複寫：概觀) 底下的陳述式上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="87242-201">Another example is right-clicking on the statements under **Replication: Overview**.</span></span> <span data-ttu-id="87242-202">從操作功能表中，選取 [Execute] (執行)：</span><span class="sxs-lookup"><span data-stu-id="87242-202">Select **Execute** from the context menu:</span></span>

![另一個範例是在 [Replication: Overview] (複寫：概觀) 底下的陳述式上按一下滑鼠右鍵。](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="87242-205">這會產生可協助進行疑難排解的資訊：</span><span class="sxs-lookup"><span data-stu-id="87242-205">This results in information that helps with troubleshooting:</span></span>

![這會產生可協助進行疑難排解的資訊](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="87242-207">針對 HANA\_Configuration\_Minichecks 進行相同的操作，然後檢查 [C] (重大) 資料行中是否有任何 _X_ 標記。</span><span class="sxs-lookup"><span data-stu-id="87242-207">Do the same for HANA\_Configuration\_Minichecks and check for any _X_ marks in the _C_ (Critical) column.</span></span>

<span data-ttu-id="87242-208">範例輸出：</span><span class="sxs-lookup"><span data-stu-id="87242-208">Sample outputs:</span></span>

<span data-ttu-id="87242-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1**：適用於一般 SAP HANA 檢查。</span><span class="sxs-lookup"><span data-stu-id="87242-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01+1：適用於一般 SAP HANA 檢查](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="87242-211">**HANA\_Services\_Overview**：適用於 SAP HANA 服務目前執行情況的概觀。</span><span class="sxs-lookup"><span data-stu-id="87242-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview：適用於 SAP HANA 服務目前執行情況的概觀](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="87242-213">**HANA\_Services\_Statistics**：適用於 SAP HANA 服務資訊 (CPU、記憶體等)。</span><span class="sxs-lookup"><span data-stu-id="87242-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="87242-214">HANA\_Services\_Statistics：適用於 SAP HANA 服務資訊</span><span class="sxs-lookup"><span data-stu-id="87242-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="87242-215">**HANA\_Configuration\_Overview\_Rev110+**：適用於 SAP HANA 執行個體的一般相關資訊。</span><span class="sxs-lookup"><span data-stu-id="87242-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on the SAP HANA instance.</span></span>

![HANA\_Configuration\_Overview\_Rev110+：：適用於 SAP HANA 執行個體的一般相關資訊](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="87242-217">**HANA\_Configuration\_Parameters\_Rev70+**：用來檢查 SAP HANA 參數。</span><span class="sxs-lookup"><span data-stu-id="87242-217">**HANA\_Configuration\_Parameters\_Rev70+** to check SAP HANA parameters.</span></span>

![HANA\_Configuration\_Parameters\_Rev70+：用來檢查 SAP HANA 參數](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

