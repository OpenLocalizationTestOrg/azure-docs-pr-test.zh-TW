---
title: "使用 Azure 流量管理員設定效能流量路由方法 | Microsoft Docs"
description: "此文章說明如何設定流量管理員，以最低的延遲將流量路由傳送到端點"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 014aa646459cd64fca7c697419324caa3edaeeea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-performance-traffic-routing-method"></a><span data-ttu-id="64e02-103">設定效能流量路由方法</span><span class="sxs-lookup"><span data-stu-id="64e02-103">Configure the performance traffic routing method</span></span>

<span data-ttu-id="64e02-104">效能流量路由方法可讓您將流量從用戶端的網路導向具有最低延遲的端點。</span><span class="sxs-lookup"><span data-stu-id="64e02-104">The Performance traffic routing method allows you to direct traffic to the endpoint with the lowest latency from the client's network.</span></span> <span data-ttu-id="64e02-105">通常，具有最低延遲的資料中心即為最短地理距離的資料中心。</span><span class="sxs-lookup"><span data-stu-id="64e02-105">Typically, the datacenter with the lowest latency is the closest in geographic distance.</span></span> <span data-ttu-id="64e02-106">此流量路由方法無法考慮到網路組態或負載的即時變更。</span><span class="sxs-lookup"><span data-stu-id="64e02-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="to-configure-performance-routing-method"></a><span data-ttu-id="64e02-107">設定效能路由方法</span><span class="sxs-lookup"><span data-stu-id="64e02-107">To configure performance routing method</span></span>

1. <span data-ttu-id="64e02-108">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="64e02-108">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="64e02-109">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="64e02-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="64e02-110">在入口網站的搜尋列中，搜尋「流量管理員設定檔」，然後按一下您想要設定路由方法的設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="64e02-110">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="64e02-111">在 [流量管理員設定檔] 刀鋒視窗中，確認您想要納入組態的雲端服務和網站皆存在。</span><span class="sxs-lookup"><span data-stu-id="64e02-111">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="64e02-112">在 [設定] 區段中，按一下 [組態]，並在 [組態] 刀鋒視窗中，完成下列設定：</span><span class="sxs-lookup"><span data-stu-id="64e02-112">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="64e02-113">在 [流量路由方法設定] 中，針對 [路由方法] 選取 [效能]。</span><span class="sxs-lookup"><span data-stu-id="64e02-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="64e02-114">將此設定檔中的所有端點都設定為如下所示的相同「端點監視設定」：</span><span class="sxs-lookup"><span data-stu-id="64e02-114">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="64e02-115">選取適當的 [通訊協定]，並指定 [連接埠] 號碼。</span><span class="sxs-lookup"><span data-stu-id="64e02-115">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="64e02-116">針對 [路徑]，輸入正斜線 */*。</span><span class="sxs-lookup"><span data-stu-id="64e02-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="64e02-117">若要監視端點，您必須指定路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="64e02-117">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="64e02-118">正斜線 "/" 是相對路徑的有效項目，表示檔案位於根目錄 (預設值)。</span><span class="sxs-lookup"><span data-stu-id="64e02-118">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="64e02-119">按一下頁面頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="64e02-119">At the top of the page, click **Save**.</span></span>
5.  <span data-ttu-id="64e02-120">測試組態中的變更，如下所示：</span><span class="sxs-lookup"><span data-stu-id="64e02-120">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="64e02-121">在入口網站的搜尋列中，搜尋流量管理員設定檔名稱，並按一下於結果中顯示的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="64e02-121">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="64e02-122">在 [流量管理員設定檔] 刀鋒視窗中，按一下 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="64e02-122">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="64e02-123">[流量管理員設定檔] 刀鋒視窗會顯示新建立流量管理員設定檔的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="64e02-123">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="64e02-124">這可由任何用戶端使用 (例如使用網頁瀏覽器進行瀏覽)，以路由傳送到由路由類型所決定的正確端點。</span><span class="sxs-lookup"><span data-stu-id="64e02-124">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="64e02-125">在此情況下，所有要求都會路由傳送到用戶端網路具有最低延遲的端點。</span><span class="sxs-lookup"><span data-stu-id="64e02-125">In this case all requests are routed to the endpoint with the lowest latency from the client's network.</span></span>
6. <span data-ttu-id="64e02-126">在流量管理員設定檔運作後，您可以編輯授權 DNS 伺服器上的 DNS 記錄，以將您的公司網域名稱指向流量管理員網域名稱。</span><span class="sxs-lookup"><span data-stu-id="64e02-126">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![使用流量管理員設定效能流量路由方法][1]

## <a name="next-steps"></a><span data-ttu-id="64e02-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64e02-128">Next steps</span></span>

- <span data-ttu-id="64e02-129">深入了解[加權流量路由方法](traffic-manager-configure-weighted-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="64e02-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="64e02-130">深入了解[優先順序路由方法](traffic-manager-configure-priority-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="64e02-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="64e02-131">深入了解[地理路由方法](traffic-manager-configure-geographic-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="64e02-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="64e02-132">深入了解如何[測試流量管理員設定](traffic-manager-testing-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="64e02-132">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png