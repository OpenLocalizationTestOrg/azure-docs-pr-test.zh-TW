---
title: "aaaNested Traffic Manager 設定檔 |Microsoft 文件"
description: "這篇文章說明 hello ' 巢狀設定檔 功能的 Azure 流量管理員"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a><span data-ttu-id="7cfb5-103">巢狀流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="7cfb5-103">Nested Traffic Manager profiles</span></span>

<span data-ttu-id="7cfb5-104">Traffic Manager 會包含某個範圍的流量路由方法可讓您 toocontrol Traffic Manager 如何選擇哪一個端點應該從每位使用者接收流量。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-104">Traffic Manager includes a range of traffic-routing methods that allow you toocontrol how Traffic Manager chooses which endpoint should receive traffic from each end user.</span></span> <span data-ttu-id="7cfb5-105">如需詳細資訊，請參閱 [流量管理員流量路由方法](traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-105">For more information, see [Traffic Manager traffic-routing methods](traffic-manager-routing-methods.md).</span></span>

<span data-ttu-id="7cfb5-106">每個「流量管理員」設定檔皆指定一個流量路由方法。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-106">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="7cfb5-107">不過，有一些需要更複雜的流量路由比 hello 路由單一 Traffic Manager 設定檔所提供的案例。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-107">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="7cfb5-108">您可以巢狀多個流量路由方法的 Traffic Manager 設定檔 toocombine hello 優點。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-108">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="7cfb5-109">巢狀設定檔可讓您 toooverride hello 預設 Traffic Manager 行為 toosupport 較大和更複雜的應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-109">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span>

<span data-ttu-id="7cfb5-110">hello 遵循範例說明如何 toouse 巢狀在各種情況中的 Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-110">hello following examples illustrate how toouse nested Traffic Manager profiles in various scenarios.</span></span>

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a><span data-ttu-id="7cfb5-111">範例 1︰結合「效能」和「加權」流量路由</span><span class="sxs-lookup"><span data-stu-id="7cfb5-111">Example 1: Combining 'Performance' and 'Weighted' traffic routing</span></span>

<span data-ttu-id="7cfb5-112">假設您部署的應用程式在下列 Azure 區域的 hello： 美國西部，西歐、 東亞。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-112">Suppose that you deployed an application in hello following Azure regions: West US, West Europe, and East Asia.</span></span> <span data-ttu-id="7cfb5-113">您可以使用 Traffic Manager 的 「 效能 」 流量路由方法 toodistribute 流量 toohello 區域最接近 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-113">You use Traffic Manager's 'Performance' traffic-routing method toodistribute traffic toohello region closest toohello user.</span></span>

![單一流量管理員設定檔][4]

<span data-ttu-id="7cfb5-115">現在，假設您想要 tootest 更新 tooyour 服務然後再發送更廣泛。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-115">Now, suppose you wish tootest an update tooyour service before rolling it out more widely.</span></span> <span data-ttu-id="7cfb5-116">您想 toouse hello 「 加權 」 流量路由方法 toodirect 一小部分的流量 tooyour 測試部署。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-116">You want toouse hello 'weighted' traffic-routing method toodirect a small percentage of traffic tooyour test deployment.</span></span> <span data-ttu-id="7cfb5-117">您在西歐設定 hello 測試部署，連同 hello 現有生產環境部署。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-117">You set up hello test deployment alongside hello existing production deployment in West Europe.</span></span>

<span data-ttu-id="7cfb5-118">您無法在單一設定檔中結合「加權」和「效能」流量路由。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-118">You cannot combine both 'Weighted' and 'Performance traffic-routing in a single profile.</span></span> <span data-ttu-id="7cfb5-119">toosupport 此案例中，建立使用兩個 hello 西歐端點和 hello '加權' 流量路由方法的 Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-119">toosupport this scenario, you create a Traffic Manager profile using hello two West Europe endpoints and hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="7cfb5-120">接下來，您會加入此 'child' 設定檔為端點 toohello 'parent' 設定檔。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-120">Next, you add this 'child' profile as an endpoint toohello 'parent' profile.</span></span> <span data-ttu-id="7cfb5-121">hello 父系設定檔仍會使用 hello 效能 」 流量路由方法和含有 hello 全域部署的其他端點。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-121">hello parent profile still uses hello Performance traffic-routing method and contains hello other global deployments as endpoints.</span></span>

<span data-ttu-id="7cfb5-122">hello 下列圖表說明此範例中：</span><span class="sxs-lookup"><span data-stu-id="7cfb5-122">hello following diagram illustrates this example:</span></span>

![巢狀流量管理員設定檔][2]

<span data-ttu-id="7cfb5-124">在此組態中，透過 hello 父系設定檔導向流量將流量分散到區域通常。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-124">In this configuration, traffic directed via hello parent profile distributes traffic across regions normally.</span></span> <span data-ttu-id="7cfb5-125">在西歐，hello 巢狀設定檔會將流量 toohello 生產與測試端點根據 toohello 權重。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-125">Within West Europe, hello nested profile distributes traffic toohello production and test endpoints according toohello weights assigned.</span></span>

<span data-ttu-id="7cfb5-126">當 hello 父系設定檔使用 hello 「 效能 」 流量路由方法時，每個端點必須指派一個位置。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-126">When hello parent profile uses hello 'Performance' traffic-routing method, each endpoint must be assigned a location.</span></span> <span data-ttu-id="7cfb5-127">當您設定 hello 端點時，會指派 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-127">hello location is assigned when you configure hello endpoint.</span></span> <span data-ttu-id="7cfb5-128">選擇 hello Azure 地區最接近 tooyour 部署。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-128">Choose hello Azure region closest tooyour deployment.</span></span> <span data-ttu-id="7cfb5-129">hello Azure 區域是 hello hello 網際網路延遲表格所支援的位置值。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-129">hello Azure regions are hello location values supported by hello Internet Latency Table.</span></span> <span data-ttu-id="7cfb5-130">如需詳細資訊，請參閱[流量管理員「效能」流量路由方法](traffic-manager-routing-methods.md#performance)。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-130">For more information, see [Traffic Manager 'Performance' traffic-routing method](traffic-manager-routing-methods.md#performance).</span></span>

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a><span data-ttu-id="7cfb5-131">範例 2︰巢狀設定檔中的端點監視</span><span class="sxs-lookup"><span data-stu-id="7cfb5-131">Example 2: Endpoint monitoring in Nested Profiles</span></span>

<span data-ttu-id="7cfb5-132">Traffic Manager 會主動監視每個服務端點的 hello 健全的狀況。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-132">Traffic Manager actively monitors hello health of each service endpoint.</span></span> <span data-ttu-id="7cfb5-133">如果端點為狀況不良，Traffic Manager 會指示使用者 tooalternative 端點 toopreserve hello 可用性的服務。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-133">If an endpoint is unhealthy, Traffic Manager directs users tooalternative endpoints toopreserve hello availability of your service.</span></span> <span data-ttu-id="7cfb5-134">此端點監視和容錯移轉行為適用於 tooall 流量路由方法。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-134">This endpoint monitoring and failover behavior applies tooall traffic-routing methods.</span></span> <span data-ttu-id="7cfb5-135">如需詳細資訊，請參閱 [流量管理員端點監視](traffic-manager-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-135">For more information, see [Traffic Manager Endpoint Monitoring](traffic-manager-monitoring.md).</span></span> <span data-ttu-id="7cfb5-136">巢狀設定檔的端點監視有不同的運作方式。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-136">Endpoint monitoring works differently for nested profiles.</span></span> <span data-ttu-id="7cfb5-137">巢狀設定檔，請 hello 父系設定檔不會直接執行 hello 子系上的健康情況檢查。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-137">With nested profiles, hello parent profile doesn't perform health checks on hello child directly.</span></span> <span data-ttu-id="7cfb5-138">相反地，hello hello 子項設定檔的端點健全狀況是使用的 toocalculate hello hello 子項設定檔的整體健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-138">Instead, hello health of hello child profile's endpoints is used toocalculate hello overall health of hello child profile.</span></span> <span data-ttu-id="7cfb5-139">此健全狀況資訊會 hello 巢狀設定檔的階層中往上傳播。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-139">This health information is propagated up hello nested profile hierarchy.</span></span> <span data-ttu-id="7cfb5-140">hello 父系設定檔會使用此彙總健全狀況 toodetermine 是否 toodirect 流量 toohello 子項設定檔。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-140">hello parent profile uses this aggregated health toodetermine whether toodirect traffic toohello child profile.</span></span> <span data-ttu-id="7cfb5-141">請參閱 hello[常見問題集](traffic-manager-FAQs.md#traffic-manager-nested-profiles)的健全狀況監視的巢狀設定檔的完整詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-141">See hello [FAQ](traffic-manager-FAQs.md#traffic-manager-nested-profiles) for full details on health monitoring of nested profiles.</span></span>

<span data-ttu-id="7cfb5-142">傳回 toohello 上例，假設在西歐 hello 生產環境部署就會失敗。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-142">Returning toohello previous example, suppose hello production deployment in West Europe fails.</span></span> <span data-ttu-id="7cfb5-143">根據預設，hello 'child' 設定檔會指示所有流量 toohello 測試部署。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-143">By default, hello 'child' profile directs all traffic toohello test deployment.</span></span> <span data-ttu-id="7cfb5-144">如果 hello 測試部署也會失敗，hello 父系設定檔會決定 hello 子系的設定檔應該不接收流量因為所有的子端點的狀況不良。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-144">If hello test deployment also fails, hello parent profile determines that hello child profile should not receive traffic since all child endpoints are unhealthy.</span></span> <span data-ttu-id="7cfb5-145">然後，hello 父系設定檔會將流量 toohello 其他區域。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-145">Then, hello parent profile distributes traffic toohello other regions.</span></span>

![巢狀設定檔容錯移轉 (預設行為)][3]

<span data-ttu-id="7cfb5-147">您可能喜歡這種做法。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-147">You might be happy with this arrangement.</span></span> <span data-ttu-id="7cfb5-148">或者，您可能會考慮所有流量，如西歐現在都即將 toohello 測試部署，而不是有限的子集流量。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-148">Or you might be concerned that all traffic for West Europe is now going toohello test deployment instead of a limited subset traffic.</span></span> <span data-ttu-id="7cfb5-149">不論 hello hello 健全狀況測試部署，您會想 toofail toohello 透過其他區域在西歐 hello 生產環境部署失敗時。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-149">Regardless of hello health of hello test deployment, you want toofail over toohello other regions when hello production deployment in West Europe fails.</span></span> <span data-ttu-id="7cfb5-150">tooenable 此容錯移轉，設定為 hello 父系設定檔中端點的 hello 子系的設定檔時，可以指定 hello 'MinChildEndpoints' 參數。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-150">tooenable this failover, you can specify hello 'MinChildEndpoints' parameter when configuring hello child profile as an endpoint in hello parent profile.</span></span> <span data-ttu-id="7cfb5-151">hello 參數會決定 hello hello 子項設定檔中可用的端點數目下限。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-151">hello parameter determines hello minimum number of available endpoints in hello child profile.</span></span> <span data-ttu-id="7cfb5-152">hello 預設值為 '1'。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-152">hello default value is '1'.</span></span> <span data-ttu-id="7cfb5-153">此案例中，您可以設定 hello MinChildEndpoints 值 too2。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-153">For this scenario, you set hello MinChildEndpoints value too2.</span></span> <span data-ttu-id="7cfb5-154">低於此閾值 hello 父系設定檔會認為 hello 整個子系設定檔 toobe 無法使用，並指示流量 toohello 其他端點。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-154">Below this threshold, hello parent profile considers hello entire child profile toobe unavailable and directs traffic toohello other endpoints.</span></span>

<span data-ttu-id="7cfb5-155">hello 下圖說明這項設定：</span><span class="sxs-lookup"><span data-stu-id="7cfb5-155">hello following figure illustrates this configuration:</span></span>

![以 'MinChildEndpoints' = 2 進行容錯移轉的巢狀設定檔][4]

> [!NOTE]
> <span data-ttu-id="7cfb5-157">hello 'Priority' 流量路由方法會將所有流量 tooa 單一端點。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-157">hello 'Priority' traffic-routing method distributes all traffic tooa single endpoint.</span></span> <span data-ttu-id="7cfb5-158">因此，如果子設定檔的 MinChildEndpoints 不是設為 '1'，則作用不大。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-158">Thus there is little purpose in a MinChildEndpoints setting other than '1' for a child profile.</span></span>

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a><span data-ttu-id="7cfb5-159">範例 3︰設定「效能」流量路由中容錯移轉區域的優先順序</span><span class="sxs-lookup"><span data-stu-id="7cfb5-159">Example 3: Prioritized failover regions in 'Performance' traffic routing</span></span>

<span data-ttu-id="7cfb5-160">hello hello 「 效能 」 流量路由方法的預設行為是設計的 tooavoid 過度最接近端點接著載入 hello 和造成串聯的一連串的失敗。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-160">hello default behavior for hello 'Performance' traffic-routing method is designed tooavoid over-loading hello next nearest endpoint and causing a cascading series of failures.</span></span> <span data-ttu-id="7cfb5-161">當端點失敗時，會指示 toothat 端點是平均的所有流量都分散 toohello 其他端點的所有區域。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-161">When an endpoint fails, all traffic that would have been directed toothat endpoint is evenly distributed toohello other endpoints across all regions.</span></span>

![搭配預設容錯移轉的「效能」流量路由][5]

<span data-ttu-id="7cfb5-163">不過，假設您偏好 hello 西歐流量容錯移轉 tooWest 我們，並只在兩個端點都無法使用時直接流量 tooother 區域。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-163">However, suppose you prefer hello West Europe traffic failover tooWest US, and only direct traffic tooother regions when both endpoints are unavailable.</span></span> <span data-ttu-id="7cfb5-164">您可以建立此解決方案使用 hello 'Priority' 流量路由方法的子系的設定檔。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-164">You can create this solution using a child profile with hello 'Priority' traffic-routing method.</span></span>

![搭配優先性容錯移轉的「效能」流量路由][6]

<span data-ttu-id="7cfb5-166">Hello 西歐端點的優先順序高於 hello 美國西部端點，因為所有流量會在這兩個端點都在線上時都傳送 toohello 西歐端點。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-166">Since hello West Europe endpoint has higher priority than hello West US endpoint, all traffic is sent toohello West Europe endpoint when both endpoints are online.</span></span> <span data-ttu-id="7cfb5-167">如果西歐失敗，其流量會導向的 tooWest 美國。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-167">If West Europe fails, its traffic is directed tooWest US.</span></span> <span data-ttu-id="7cfb5-168">巢狀的 hello 設定檔，流量西歐和美國西部失敗時，才會導向的 tooEast 亞洲。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-168">With hello nested profile, traffic is directed tooEast Asia only when both West Europe and West US fail.</span></span>

<span data-ttu-id="7cfb5-169">您可以對所有區域重複此模式。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-169">You can repeat this pattern for all regions.</span></span> <span data-ttu-id="7cfb5-170">取代 hello 父系設定檔中的所有三個端點具有三個子項設定檔，每個提供優先順序的容錯移轉順序。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-170">Replace all three endpoints in hello parent profile with three child profiles, each providing a prioritized failover sequence.</span></span>

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a><span data-ttu-id="7cfb5-171">範例 4： 控制 「 效能 」 流量路由 hello 中的多個端點之間相同區域</span><span class="sxs-lookup"><span data-stu-id="7cfb5-171">Example 4: Controlling 'Performance' traffic routing between multiple endpoints in hello same region</span></span>

<span data-ttu-id="7cfb5-172">假設 hello 「 效能 」 流量路由方法用在特定區域中有多個端點的設定檔。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-172">Suppose hello 'Performance' traffic-routing method is used in a profile that has more than one endpoint in a particular region.</span></span> <span data-ttu-id="7cfb5-173">根據預設，流量會導向 toothat 區域平均分散在該區域中所有可用的端點。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-173">By default, traffic directed toothat region is distributed evenly across all available endpoints in that region.</span></span>

![「效能」流量路由區域內流量分配 (預設行為)][7]

<span data-ttu-id="7cfb5-175">我們不是在西歐新增多個端點，而是將這些端點封入個別的子設定檔中。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-175">Instead of adding multiple endpoints in West Europe, those endpoints are enclosed in a separate child profile.</span></span> <span data-ttu-id="7cfb5-176">hello 子系的設定檔會成為 toohello 父 hello 西歐中唯一的端點。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-176">hello child profile is added toohello parent as hello only endpoint in West Europe.</span></span> <span data-ttu-id="7cfb5-177">hello hello 子項設定檔上的設定可以控制與西歐 hello 流量發佈啟用該區域內的優先權為基礎或加權的流量路由。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-177">hello settings on hello child profile can control hello traffic distribution with West Europe by enabling priority-based or weighted traffic routing within that region.</span></span>

![搭配自訂區域內流量分配的「效能」流量路由][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a><span data-ttu-id="7cfb5-179">範例 5︰每個端點的監視設定</span><span class="sxs-lookup"><span data-stu-id="7cfb5-179">Example 5: Per-endpoint monitoring settings</span></span>

<span data-ttu-id="7cfb5-180">假設您使用 Traffic Manager toosmoothly 流量從傳統內部部署網站 tooa 新雲端架構版本移轉裝載於 Azure。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-180">Suppose you are using Traffic Manager toosmoothly migrate traffic from a legacy on-premises web site tooa new Cloud-based version hosted in Azure.</span></span> <span data-ttu-id="7cfb5-181">Hello 舊版的站台，您會想 toouse hello 首頁 URI toomonitor 站台健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-181">For hello legacy site, you want toouse hello home page URI toomonitor site health.</span></span> <span data-ttu-id="7cfb5-182">但如 hello 新雲端架構的版本，您要實作自訂監視的頁面 (路徑 ' / monitor.aspx')，其中包含額外的檢查。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-182">But for hello new Cloud-based version, you are implementing a custom monitoring page (path '/monitor.aspx') that includes additional checks.</span></span>

![流量管理員端點監視 (預設行為)][9]

<span data-ttu-id="7cfb5-184">Traffic Manager 設定檔中的 hello 監視設定會套用 tooall 單一設定檔中的端點。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-184">hello monitoring settings in a Traffic Manager profile apply tooall endpoints within a single profile.</span></span> <span data-ttu-id="7cfb5-185">與巢狀設定檔，您可以使用不同的子系設定檔，每個站台 toodefine 不同監視設定。</span><span class="sxs-lookup"><span data-stu-id="7cfb5-185">With nested profiles, you use a different child profile per site toodefine different monitoring settings.</span></span>

![搭配每個設定的流量管理員端點監視][10]

## <a name="next-steps"></a><span data-ttu-id="7cfb5-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7cfb5-187">Next steps</span></span>

<span data-ttu-id="7cfb5-188">深入了解[流量管理員設定檔](traffic-manager-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7cfb5-188">Learn more about [Traffic Manager profiles](traffic-manager-overview.md)</span></span>

<span data-ttu-id="7cfb5-189">了解如何太[建立 Traffic Manager 設定檔](traffic-manager-create-profile.md)</span><span class="sxs-lookup"><span data-stu-id="7cfb5-189">Learn how too[create a Traffic Manager profile](traffic-manager-create-profile.md)</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png
