---
title: "使用 Azure 流量管理員設定優先順序流量路由方法 | Microsoft Docs"
description: "此文章說明如何在流量管理員中設定優先順序流量路由方法"
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
ms.openlocfilehash: 0db83cde6facc89b8b8aa72e6419129ec868235c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="945e4-103">在流量管理員中設定優先順序流量路由方法</span><span class="sxs-lookup"><span data-stu-id="945e4-103">Configure priority traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="945e4-104">不論網站模式為何，Azure 網站已為資料中心 (也稱為「區域」) 內的網站提供容錯移轉功能。</span><span class="sxs-lookup"><span data-stu-id="945e4-104">Regardless of the website mode, Azure Websites already provide failover functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="945e4-105">流量管理員會在不同資料中心為網站提供容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="945e4-105">Traffic Manager provides failover for websites in different datacenters.</span></span>

<span data-ttu-id="945e4-106">服務容錯移轉的一個常見模式是將流量傳送到主要服務，並提供一組完全相同的備份服務以供容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="945e4-106">A common pattern for service failover is to send traffic to a primary service and provide a set of identical backup services for failover.</span></span> <span data-ttu-id="945e4-107">下列步驟說明如何使用 Azure 雲端服務和網站，設定此優先順序容錯移轉︰</span><span class="sxs-lookup"><span data-stu-id="945e4-107">The following steps explain how to configure this prioritized failover with Azure cloud services and websites:</span></span>

## <a name="to-configure-the-priority-traffic-routing-method"></a><span data-ttu-id="945e4-108">設定優先順序流量路由方法</span><span class="sxs-lookup"><span data-stu-id="945e4-108">To configure the priority traffic routing method</span></span>

1. <span data-ttu-id="945e4-109">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="945e4-109">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="945e4-110">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="945e4-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="945e4-111">在入口網站的搜尋列中，搜尋「流量管理員設定檔」，然後按一下您想要設定路由方法的設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="945e4-111">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="945e4-112">在 [流量管理員設定檔] 刀鋒視窗中，確認您想要納入組態的雲端服務和網站皆存在。</span><span class="sxs-lookup"><span data-stu-id="945e4-112">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="945e4-113">在 [設定] 區段中，按一下 [組態]，並在 [組態] 刀鋒視窗中，完成下列設定：</span><span class="sxs-lookup"><span data-stu-id="945e4-113">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="945e4-114">針對 [流量路由方法設定]，請確認流量路由方法為 [優先順序]。</span><span class="sxs-lookup"><span data-stu-id="945e4-114">For **traffic routing method settings**, verify that the traffic routing method is **Priority**.</span></span> <span data-ttu-id="945e4-115">如果不是，請按一下下拉式清單中的 [優先順序]。</span><span class="sxs-lookup"><span data-stu-id="945e4-115">If it is not, click **Priority** from the dropdown list.</span></span>
    2. <span data-ttu-id="945e4-116">將此設定檔中的所有端點都設定為如下所示的相同「端點監視設定」：</span><span class="sxs-lookup"><span data-stu-id="945e4-116">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="945e4-117">選取適當的 [通訊協定]，並指定 [連接埠] 號碼。</span><span class="sxs-lookup"><span data-stu-id="945e4-117">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="945e4-118">針對 [路徑]，輸入正斜線 */*。</span><span class="sxs-lookup"><span data-stu-id="945e4-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="945e4-119">若要監視端點，您必須指定路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="945e4-119">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="945e4-120">正斜線 "/" 是相對路徑的有效項目，表示檔案位於根目錄 (預設值)。</span><span class="sxs-lookup"><span data-stu-id="945e4-120">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="945e4-121">按一下頁面頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="945e4-121">At the top of the page, click **Save**.</span></span>
5. <span data-ttu-id="945e4-122">在 [設定] 區段中，按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="945e4-122">In the **Settings** section, click **Endpoints**.</span></span>
6. <span data-ttu-id="945e4-123">在 [端點] 刀鋒視窗中，檢閱端點的優先順序。</span><span class="sxs-lookup"><span data-stu-id="945e4-123">In the **Endpoints** blade, review the priority order for your endpoints.</span></span> <span data-ttu-id="945e4-124">當您選取 [優先順序] 流量路由方法時，所選端點的順序便很重要。</span><span class="sxs-lookup"><span data-stu-id="945e4-124">When you select the **Priority** traffic routing method, the order of the selected endpoints matters.</span></span> <span data-ttu-id="945e4-125">確認端點的優先順序。</span><span class="sxs-lookup"><span data-stu-id="945e4-125">Verify the priority order of endpoints.</span></span>  <span data-ttu-id="945e4-126">主要端點會位於最上方。</span><span class="sxs-lookup"><span data-stu-id="945e4-126">The primary endpoint is on top.</span></span> <span data-ttu-id="945e4-127">請重複檢查顯示的順序。</span><span class="sxs-lookup"><span data-stu-id="945e4-127">Double-check on the order it is displayed.</span></span> <span data-ttu-id="945e4-128">所有的要求都將路由傳送到第一個端點，且如果流量管理員偵測到端點狀況不良，流量會自動容錯移轉到下一個端點。</span><span class="sxs-lookup"><span data-stu-id="945e4-128">all requests will be routed to the first endpoint and if Traffic Manager detects it be unhealthy, the traffic automatically fails over to the next endpoint.</span></span> 
7. <span data-ttu-id="945e4-129">若要變更端點的優先順序，請按一下端點，然後在顯示的 [端點] 刀鋒視窗中，按一下 [編輯] 並依所需變更 [優先順序] 值。</span><span class="sxs-lookup"><span data-stu-id="945e4-129">To change the endpoint priority order, click the endpoint, and in the **Endpoint** blade that is displayed, click **Edit** and change the **Priority** value as needed.</span></span> 
8. <span data-ttu-id="945e4-130">按一下 [儲存] 以儲存端點設定的變更。</span><span class="sxs-lookup"><span data-stu-id="945e4-130">Click **Save** to save change the endpoint settings.</span></span>
9. <span data-ttu-id="945e4-131">完成組態變更之後，請按一下頁面底部的 [ **儲存** ]。</span><span class="sxs-lookup"><span data-stu-id="945e4-131">After you complete your configuration changes, click **Save** at the bottom of the page.</span></span>
10. <span data-ttu-id="945e4-132">測試組態中的變更，如下所示：</span><span class="sxs-lookup"><span data-stu-id="945e4-132">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="945e4-133">在入口網站的搜尋列中，搜尋流量管理員設定檔名稱，並按一下於結果中顯示的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="945e4-133">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="945e4-134">在 [流量管理員設定檔] 刀鋒視窗中，按一下 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="945e4-134">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="945e4-135">[流量管理員設定檔] 刀鋒視窗會顯示新建立流量管理員設定檔的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="945e4-135">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="945e4-136">這可由任何用戶端使用 (例如使用網頁瀏覽器進行瀏覽)，以路由傳送到由路由類型所決定的正確端點。</span><span class="sxs-lookup"><span data-stu-id="945e4-136">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="945e4-137">在此情況下，所有的要求都將路由傳送到第一個端點，且如果流量管理員偵測到端點狀況不良，流量會自動容錯移轉到下一個端點。</span><span class="sxs-lookup"><span data-stu-id="945e4-137">In this case all requests are routed to the first endpoint and if Traffic Manager detects it be unhealthy, the traffic automatically fails over to the next endpoint.</span></span>
11. <span data-ttu-id="945e4-138">在流量管理員設定檔運作後，您可以編輯授權 DNS 伺服器上的 DNS 記錄，以將您的公司網域名稱指向流量管理員網域名稱。</span><span class="sxs-lookup"><span data-stu-id="945e4-138">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![使用流量管理員設定優先順序流量路由方法][1]

## <a name="next-steps"></a><span data-ttu-id="945e4-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="945e4-140">Next steps</span></span>


- <span data-ttu-id="945e4-141">深入了解[加權流量路由方法](traffic-manager-configure-weighted-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="945e4-141">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="945e4-142">深入了解[效能路由方法](traffic-manager-configure-performance-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="945e4-142">Learn about [performance routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="945e4-143">深入了解[地理路由方法](traffic-manager-configure-geographic-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="945e4-143">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="945e4-144">深入了解如何[測試流量管理員設定](traffic-manager-testing-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="945e4-144">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png