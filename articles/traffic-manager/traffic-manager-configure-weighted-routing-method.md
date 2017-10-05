---
title: "使用 Azure 流量管理員設定加權循環配置資源流量路由方法 | Microsoft Docs"
description: "此文章說明如何在流量管理員中使用循環配置資源方法對流量進行負載平衡"
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
ms.openlocfilehash: 7aa4c9120d44ff1b3e59a57090ea04e3f8021fc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="0c975-103">在流量管理員中設定加權流量路由方法</span><span class="sxs-lookup"><span data-stu-id="0c975-103">Configure the weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="0c975-104">常見的流量路由方法提供一組完全相同的端點 (包括雲端服務和網站)，並以循環配置資源方式將流量傳送到每一個端點。</span><span class="sxs-lookup"><span data-stu-id="0c975-104">A common traffic routing method pattern is to provide a set of identical endpoints, which include cloud services and websites, and send traffic to each in a round-robin fashion.</span></span> <span data-ttu-id="0c975-105">下列步驟概述如何設定這種類型的流量路由方法。</span><span class="sxs-lookup"><span data-stu-id="0c975-105">The following steps outline how to configure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="0c975-106">Azure 網站已為資料中心 (也稱為「區域」) 內的網站提供循環配置資源負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="0c975-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="0c975-107">流量管理員可讓您在不同的資料中心網站中指定循環配置資源流量路由方法。</span><span class="sxs-lookup"><span data-stu-id="0c975-107">Traffic Manager allows you to specify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="to-configure-the-weighted-traffic-routing-method"></a><span data-ttu-id="0c975-108">設定加權流量路由方法</span><span class="sxs-lookup"><span data-stu-id="0c975-108">To configure the weighted traffic routing method</span></span>

1. <span data-ttu-id="0c975-109">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="0c975-109">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="0c975-110">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="0c975-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="0c975-111">在入口網站的搜尋列中，搜尋「流量管理員設定檔」，然後按一下您想要設定路由方法的設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="0c975-111">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="0c975-112">在 [流量管理員設定檔] 刀鋒視窗中，確認您想要納入組態的雲端服務和網站皆存在。</span><span class="sxs-lookup"><span data-stu-id="0c975-112">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="0c975-113">在 [設定] 區段中，按一下 [組態]，並在 [組態] 刀鋒視窗中，完成下列設定：</span><span class="sxs-lookup"><span data-stu-id="0c975-113">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="0c975-114">在 [流量路由方法設定] 中，確認流量路由方法為 [加權]。</span><span class="sxs-lookup"><span data-stu-id="0c975-114">For **traffic routing method settings**, verify that the traffic routing method is **Weighted**.</span></span> <span data-ttu-id="0c975-115">如果不是，按一下下拉式清單中的 [加權]。</span><span class="sxs-lookup"><span data-stu-id="0c975-115">If it is not, click **Weighted** from the dropdown list.</span></span>
    2. <span data-ttu-id="0c975-116">將此設定檔中的所有端點都設定為如下所示的相同「端點監視設定」：</span><span class="sxs-lookup"><span data-stu-id="0c975-116">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="0c975-117">選取適當的 [通訊協定]，並指定 [連接埠] 號碼。</span><span class="sxs-lookup"><span data-stu-id="0c975-117">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="0c975-118">針對 [路徑]，輸入正斜線 */*。</span><span class="sxs-lookup"><span data-stu-id="0c975-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="0c975-119">若要監視端點，您必須指定路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="0c975-119">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="0c975-120">正斜線 "/" 是相對路徑的有效項目，表示檔案位於根目錄 (預設值)。</span><span class="sxs-lookup"><span data-stu-id="0c975-120">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="0c975-121">按一下頁面頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0c975-121">At the top of the page, click **Save**.</span></span>
5. <span data-ttu-id="0c975-122">測試組態中的變更，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0c975-122">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="0c975-123">在入口網站的搜尋列中，搜尋流量管理員設定檔名稱，並按一下於結果中顯示的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="0c975-123">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="0c975-124">在 [流量管理員設定檔] 刀鋒視窗中，按一下 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="0c975-124">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="0c975-125">[流量管理員設定檔] 刀鋒視窗會顯示新建立流量管理員設定檔的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="0c975-125">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="0c975-126">這可由任何用戶端使用 (例如使用網頁瀏覽器進行瀏覽)，以路由傳送到由路由類型所決定的正確端點。</span><span class="sxs-lookup"><span data-stu-id="0c975-126">This can be used by any clients (for example,by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="0c975-127">在此情況下，所有要求都會以循環配置資源方式路由到每個端點。</span><span class="sxs-lookup"><span data-stu-id="0c975-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="0c975-128">在流量管理員設定檔運作後，您可以編輯授權 DNS 伺服器上的 DNS 記錄，以將您的公司網域名稱指向流量管理員網域名稱。</span><span class="sxs-lookup"><span data-stu-id="0c975-128">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![使用流量管理員設定加權流量路由方法][1]

## <a name="next-steps"></a><span data-ttu-id="0c975-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c975-130">Next steps</span></span>

- <span data-ttu-id="0c975-131">深入了解[優先順序流量路由方法](traffic-manager-configure-priority-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="0c975-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="0c975-132">深入了解[效能流量路由方法](traffic-manager-configure-performance-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="0c975-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="0c975-133">深入了解[地理路由方法](traffic-manager-configure-geographic-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="0c975-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="0c975-134">深入了解如何[測試流量管理員設定](traffic-manager-testing-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="0c975-134">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
