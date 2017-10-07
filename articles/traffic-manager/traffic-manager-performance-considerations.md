---
title: "aaaPerformance 考量 Azure Traffic Manager |Microsoft 文件"
description: "了解效能 Traffic Manager 以及 tootest 效能，您的網站時使用流量管理員"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a><span data-ttu-id="c205f-103">流量管理員的效能考量</span><span class="sxs-lookup"><span data-stu-id="c205f-103">Performance considerations for Traffic Manager</span></span>

<span data-ttu-id="c205f-104">此頁面說明使用流量管理員的效能考量。</span><span class="sxs-lookup"><span data-stu-id="c205f-104">This page explains performance considerations using Traffic Manager.</span></span> <span data-ttu-id="c205f-105">請考慮下列案例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="c205f-105">Consider hello following scenario:</span></span>

<span data-ttu-id="c205f-106">您必須在 hello Uswest 網站的執行個體和 EastAsia 區域。</span><span class="sxs-lookup"><span data-stu-id="c205f-106">You have instances of your website in hello WestUS and EastAsia regions.</span></span> <span data-ttu-id="c205f-107">其中一個 hello 執行個體失敗 hello 流量管理員探查 hello 健全狀況的檢查。</span><span class="sxs-lookup"><span data-stu-id="c205f-107">One of hello instances is failing hello health check for hello traffic manager probe.</span></span> <span data-ttu-id="c205f-108">應用程式流量會導向的 toohello 狀況良好的區域。</span><span class="sxs-lookup"><span data-stu-id="c205f-108">Application traffic is directed toohello healthy region.</span></span> <span data-ttu-id="c205f-109">預期此容錯移轉，但效能可能會產生根據 hello 流量現在旅行 tooa 遠方區域的 hello 延遲問題。</span><span class="sxs-lookup"><span data-stu-id="c205f-109">This failover is expected but performance can be a problem based on hello latency of hello traffic now traveling tooa distant region.</span></span>

## <a name="performance-considerations-for-traffic-manager"></a><span data-ttu-id="c205f-110">流量管理員的效能考量</span><span class="sxs-lookup"><span data-stu-id="c205f-110">Performance considerations for Traffic Manager</span></span>

<span data-ttu-id="c205f-111">hello 唯一效能的影響的流量管理員能在您的網站是 hello 初始 DNS 查閱。</span><span class="sxs-lookup"><span data-stu-id="c205f-111">hello only performance impact that Traffic Manager can have on your website is hello initial DNS lookup.</span></span> <span data-ttu-id="c205f-112">該主機 hello trafficmanager.net 區域時，是由 hello Microsoft DNS 根伺服器處理 hello Traffic Manager 設定檔名稱的 DNS 要求。</span><span class="sxs-lookup"><span data-stu-id="c205f-112">A DNS request for hello name of your Traffic Manager profile is handled by hello Microsoft DNS root server that hosts hello trafficmanager.net zone.</span></span> <span data-ttu-id="c205f-113">Traffic Manager 會填入，且會定期更新，根據 hello Traffic Manager 原則及 hello 探查結果 hello Microsoft DNS 根伺服器。</span><span class="sxs-lookup"><span data-stu-id="c205f-113">Traffic Manager populates, and regularly updates, hello Microsoft's DNS root servers based on hello Traffic Manager policy and hello probe results.</span></span> <span data-ttu-id="c205f-114">因此即使在 hello 初始 DNS 查閱期間沒有 DNS 查詢傳送 tooTraffic 管理員。</span><span class="sxs-lookup"><span data-stu-id="c205f-114">So even during hello initial DNS lookup, no DNS queries are sent tooTraffic Manager.</span></span>

<span data-ttu-id="c205f-115">Traffic Manager 由數個元件所組成： DNS 名稱伺服器、 API 服務、 hello 儲存層和監視服務的端點。</span><span class="sxs-lookup"><span data-stu-id="c205f-115">Traffic Manager is made up of several components: DNS name servers, an API service, hello storage layer, and an endpoint monitoring service.</span></span> <span data-ttu-id="c205f-116">如果 Traffic Manager 服務元件失敗，則不會影響您的 Traffic Manager 設定檔相關聯的 hello DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="c205f-116">If a Traffic Manager service component fails, there is no effect on hello DNS name associated with your Traffic Manager profile.</span></span> <span data-ttu-id="c205f-117">hello Microsoft DNS 伺服器中的 hello 記錄維持不變。</span><span class="sxs-lookup"><span data-stu-id="c205f-117">hello records in hello Microsoft DNS servers remain unchanged.</span></span> <span data-ttu-id="c205f-118">不過，端點監視和 DNS 更新不會發生。</span><span class="sxs-lookup"><span data-stu-id="c205f-118">However, endpoint monitoring and DNS updating do not happen.</span></span> <span data-ttu-id="c205f-119">因此，Traffic Manager 不是能 tooupdate DNS toopoint tooyour 容錯移轉站台您主要站台關閉而發生。</span><span class="sxs-lookup"><span data-stu-id="c205f-119">Therefore, Traffic Manager is not able tooupdate DNS toopoint tooyour failover site when your primary site goes down.</span></span>

<span data-ttu-id="c205f-120">系統會快速解析 DNS 名稱並快取結果。</span><span class="sxs-lookup"><span data-stu-id="c205f-120">DNS name resolution is fast and results are cached.</span></span> <span data-ttu-id="c205f-121">hello hello 初始 DNS 查閱速度取決於 hello 進行名稱解析的 DNS 伺服器 hello 用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="c205f-121">hello speed of hello initial DNS lookup depends on hello DNS servers hello client uses for name resolution.</span></span> <span data-ttu-id="c205f-122">一般而言，用戶端可以在大約 50 毫秒內完成 DNS 查閱。</span><span class="sxs-lookup"><span data-stu-id="c205f-122">Typically, a client can complete a DNS lookup within ~50 ms.</span></span> <span data-ttu-id="c205f-123">DNS--存留時間 (TTL) 的 hello hello 持續時間內會快取 hello 查閱 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="c205f-123">hello results of hello lookup are cached for hello duration of hello DNS Time-to-live (TTL).</span></span> <span data-ttu-id="c205f-124">hello 預設 Traffic Manager 的 TTL 是 300 秒。</span><span class="sxs-lookup"><span data-stu-id="c205f-124">hello default TTL for Traffic Manager is 300 seconds.</span></span>

<span data-ttu-id="c205f-125">流量不會透過流量管理員流動。</span><span class="sxs-lookup"><span data-stu-id="c205f-125">Traffic does NOT flow through Traffic Manager.</span></span> <span data-ttu-id="c205f-126">Hello DNS 查閱完成之後，hello 用戶端有一個 IP 位址之網站的執行個體。</span><span class="sxs-lookup"><span data-stu-id="c205f-126">Once hello DNS lookup completes, hello client has an IP address for an instance of your web site.</span></span> <span data-ttu-id="c205f-127">hello 用戶端會直接連接 toothat 位址，並透過 Traffic Manager 未通過。</span><span class="sxs-lookup"><span data-stu-id="c205f-127">hello client connects directly toothat address and does not pass through Traffic Manager.</span></span> <span data-ttu-id="c205f-128">hello 您選擇的 Traffic Manager 原則已在 hello DNS 效能上的沒有影響。</span><span class="sxs-lookup"><span data-stu-id="c205f-128">hello Traffic Manager policy you choose has no influence on hello DNS performance.</span></span> <span data-ttu-id="c205f-129">不過，效能路由方法會造成負面影響 hello 應用程式體驗。</span><span class="sxs-lookup"><span data-stu-id="c205f-129">However, a Performance routing-method can negatively impact hello application experience.</span></span> <span data-ttu-id="c205f-130">比方說，如果您的原則重新導向流量從裝載於亞洲 North America tooan 執行個體，這些工作階段的 hello 網路延遲可能是效能問題。</span><span class="sxs-lookup"><span data-stu-id="c205f-130">For example, if your policy redirects traffic from North America tooan instance hosted in Asia, hello network latency for those sessions may be a performance issue.</span></span>

## <a name="measuring-traffic-manager-performance"></a><span data-ttu-id="c205f-131">測試流量管理員效能</span><span class="sxs-lookup"><span data-stu-id="c205f-131">Measuring Traffic Manager Performance</span></span>

<span data-ttu-id="c205f-132">有數個網站，您可以使用 toounderstand hello 效能與流量管理員設定檔的行為。</span><span class="sxs-lookup"><span data-stu-id="c205f-132">There are several websites you can use toounderstand hello performance and behavior of a Traffic Manager profile.</span></span> <span data-ttu-id="c205f-133">這些網站其中許多都是免費，但可能有限制。</span><span class="sxs-lookup"><span data-stu-id="c205f-133">Many of these sites are free but may have limitations.</span></span> <span data-ttu-id="c205f-134">某些網站提供付費的監視與報告增強功能。</span><span class="sxs-lookup"><span data-stu-id="c205f-134">Some sites offer enhanced monitoring and reporting for a fee.</span></span>

<span data-ttu-id="c205f-135">在這些站台上的 hello 工具測量 DNS 延遲，並顯示 hello 解析 hello 世界各地的用戶端位置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c205f-135">hello tools on these sites measure DNS latencies and display hello resolved IP addresses for client locations around hello world.</span></span> <span data-ttu-id="c205f-136">這些工具大部分都不會快取 hello 的 DNS 結果。</span><span class="sxs-lookup"><span data-stu-id="c205f-136">Most of these tools do not cache hello DNS results.</span></span> <span data-ttu-id="c205f-137">因此，hello 工具顯示 hello 完整的 DNS 查閱每次執行測試。</span><span class="sxs-lookup"><span data-stu-id="c205f-137">Therefore, hello tools show hello full DNS lookup each time a test is run.</span></span> <span data-ttu-id="c205f-138">當您測試自己的用戶端中時，您只會遇到 hello 完整 DNS 查閱的效能一次期間 hello TTL。</span><span class="sxs-lookup"><span data-stu-id="c205f-138">When you test from your own client, you only experience hello full DNS lookup performance once during hello TTL duration.</span></span>

## <a name="sample-tools-toomeasure-dns-performance"></a><span data-ttu-id="c205f-139">範例工具 toomeasure DNS 效能</span><span class="sxs-lookup"><span data-stu-id="c205f-139">Sample tools toomeasure DNS performance</span></span>

* [<span data-ttu-id="c205f-140">SolveDNS</span><span class="sxs-lookup"><span data-stu-id="c205f-140">SolveDNS</span></span>](http://www.solvedns.com/dns-comparison/)

    <span data-ttu-id="c205f-141">SolveDNS 提供許多效能工具。</span><span class="sxs-lookup"><span data-stu-id="c205f-141">SolveDNS offers many performance tools.</span></span> <span data-ttu-id="c205f-142">hello DNS 比較工具可以顯示您要花多久 tooresolve 您的 DNS 名稱，以及如何以比較 tooother DNS 服務提供者。</span><span class="sxs-lookup"><span data-stu-id="c205f-142">hello DNS Comparison tool can show you how long it takes tooresolve your DNS name and how that compares tooother DNS service providers.</span></span>

* [<span data-ttu-id="c205f-143">WebSitePulse</span><span class="sxs-lookup"><span data-stu-id="c205f-143">WebSitePulse</span></span>](http://www.websitepulse.com/help/tools.php)

    <span data-ttu-id="c205f-144">WebSitePulse 其中一個 hello 最簡單工具。</span><span class="sxs-lookup"><span data-stu-id="c205f-144">One of hello simplest tools is WebSitePulse.</span></span> <span data-ttu-id="c205f-145">輸入 hello URL toosee DNS 解析時間、 第一個位元組、 最後一個位元組和其他效能統計資料。</span><span class="sxs-lookup"><span data-stu-id="c205f-145">Enter hello URL toosee DNS resolution time, First Byte, Last Byte, and other performance statistics.</span></span> <span data-ttu-id="c205f-146">您可以從三個不同的測試位置中選擇。</span><span class="sxs-lookup"><span data-stu-id="c205f-146">You can choose from three different test locations.</span></span> <span data-ttu-id="c205f-147">在此範例中，您會看到 hello 第一次執行示範 DNS 查閱採用 0.204 秒。</span><span class="sxs-lookup"><span data-stu-id="c205f-147">In this example, you see that hello first execution shows that DNS lookup takes 0.204 sec.</span></span>

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    <span data-ttu-id="c205f-149">因為結果會快取，hello hello 第二個測試 hello 相同 Traffic Manager 端點 hello DNS 查閱會 0.002 秒。</span><span class="sxs-lookup"><span data-stu-id="c205f-149">Because hello results are cached, hello second test for hello same Traffic Manager endpoint hello DNS lookup takes 0.002 sec.</span></span>

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [<span data-ttu-id="c205f-151">CA App Synthetic Monitor</span><span class="sxs-lookup"><span data-stu-id="c205f-151">CA App Synthetic Monitor</span></span>](https://asm.ca.com/en/checkit.php)

    <span data-ttu-id="c205f-152">此站台先前稱為 hello Watchmouse 檢查網站工具，顯示您的 DNS 解析 hello 同時時間從多個地理區域。</span><span class="sxs-lookup"><span data-stu-id="c205f-152">Formerly known as hello Watchmouse Check Website tool, this site show you hello DNS resolution time from multiple geographic regions simultaneously.</span></span> <span data-ttu-id="c205f-153">從數個地理位置中，輸入 hello URL toosee DNS 解析時間，連線時間，速度。</span><span class="sxs-lookup"><span data-stu-id="c205f-153">Enter hello URL toosee DNS resolution time, connection time, and speed from several geographic locations.</span></span> <span data-ttu-id="c205f-154">使用哪一種裝載的服務會傳回此測試 toosee hello 世界各地的不同位置。</span><span class="sxs-lookup"><span data-stu-id="c205f-154">Use this test toosee which hosted service is returned for different locations around hello world.</span></span>

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [<span data-ttu-id="c205f-156">Pingdom</span><span class="sxs-lookup"><span data-stu-id="c205f-156">Pingdom</span></span>](http://tools.pingdom.com/)

    <span data-ttu-id="c205f-157">這項工具提供網頁每個項目的效能統計資料。</span><span class="sxs-lookup"><span data-stu-id="c205f-157">This tool provides performance statistics for each element of a web page.</span></span> <span data-ttu-id="c205f-158">hello 頁面分析 索引標籤會顯示 hello 花費的時間百分比上 DNS 查閱。</span><span class="sxs-lookup"><span data-stu-id="c205f-158">hello Page Analysis tab shows hello percentage of time spent on DNS lookup.</span></span>

* [<span data-ttu-id="c205f-159">What's My DNS?</span><span class="sxs-lookup"><span data-stu-id="c205f-159">What's My DNS?</span></span>](http://www.whatsmydns.net/)

    <span data-ttu-id="c205f-160">此站台從 20 個不同位置中沒有 DNS 查閱，並在地圖上顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="c205f-160">This site does a DNS lookup from 20 different locations and displays hello results on a map.</span></span>

* [<span data-ttu-id="c205f-161">Dig Web Interface</span><span class="sxs-lookup"><span data-stu-id="c205f-161">Dig Web Interface</span></span>](http://www.digwebinterface.com)

    <span data-ttu-id="c205f-162">這個網站會顯示更詳細的 DNS 資訊，包括 CNAME 和 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="c205f-162">This site shows more detailed DNS information including CNAMEs and A records.</span></span> <span data-ttu-id="c205f-163">請確定您在 [選項] 檢查 hello 'Colorize output' 和 '統計資料' 並選取 'All' Nameservers 底下。</span><span class="sxs-lookup"><span data-stu-id="c205f-163">Make sure you check hello 'Colorize output' and 'Stats' under options, and select 'All' under Nameservers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c205f-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c205f-164">Next Steps</span></span>

[<span data-ttu-id="c205f-165">關於流量管理員流量路由方法</span><span class="sxs-lookup"><span data-stu-id="c205f-165">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="c205f-166">測試流量管理員設定</span><span class="sxs-lookup"><span data-stu-id="c205f-166">Test your Traffic Manager settings</span></span>](traffic-manager-testing-settings.md)

[<span data-ttu-id="c205f-167">流量管理員的相關作業 (REST API 參考)</span><span class="sxs-lookup"><span data-stu-id="c205f-167">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

[<span data-ttu-id="c205f-168">Azure 流量管理員 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="c205f-168">Azure Traffic Manager Cmdlets</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=400769)

