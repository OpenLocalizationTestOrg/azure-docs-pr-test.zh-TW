---
title: "aaaConfigure 優先順序流量路由方式，使用 Azure Traffic Manager |Microsoft 文件"
description: "這篇文章說明如何 tooconfigure hello 優先順序流量路由方法 Traffic Manager 中"
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
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="6deab-103">在流量管理員中設定優先順序流量路由方法</span><span class="sxs-lookup"><span data-stu-id="6deab-103">Configure priority traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="6deab-104">不論 hello 網站模式，Azure 網站已提供容錯移轉功能，對於資料中心 （也稱為區域） 內的網站。</span><span class="sxs-lookup"><span data-stu-id="6deab-104">Regardless of hello website mode, Azure Websites already provide failover functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="6deab-105">流量管理員會在不同資料中心為網站提供容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="6deab-105">Traffic Manager provides failover for websites in different datacenters.</span></span>

<span data-ttu-id="6deab-106">常見的服務容錯移轉模式是 toosend 流量 tooa 主要服務，並提供一組完全相同的備份服務的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="6deab-106">A common pattern for service failover is toosend traffic tooa primary service and provide a set of identical backup services for failover.</span></span> <span data-ttu-id="6deab-107">hello 下列步驟說明如何 tooconfigure 這排定優先順序與 Azure 雲端服務和網站的容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="6deab-107">hello following steps explain how tooconfigure this prioritized failover with Azure cloud services and websites:</span></span>

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a><span data-ttu-id="6deab-108">tooconfigure hello 優先順序流量路由方法</span><span class="sxs-lookup"><span data-stu-id="6deab-108">tooconfigure hello priority traffic routing method</span></span>

1. <span data-ttu-id="6deab-109">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6deab-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="6deab-110">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="6deab-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="6deab-111">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**，然後按一下您想要針對 tooconfigure hello 路由方法的 hello 設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="6deab-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="6deab-112">在 hello **Traffic Manager 設定檔**刀鋒視窗中，確認同時 hello 雲端服務，且您想 tooinclude 組態中的網站都存在。</span><span class="sxs-lookup"><span data-stu-id="6deab-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="6deab-113">在 hello**設定**區段中，按一下**組態**，在 hello**組態**刀鋒視窗中，完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6deab-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="6deab-114">如**流量路由方法設定**，確認 hello 流量路由方式**優先順序**。</span><span class="sxs-lookup"><span data-stu-id="6deab-114">For **traffic routing method settings**, verify that hello traffic routing method is **Priority**.</span></span> <span data-ttu-id="6deab-115">如果沒有，請按一下**優先順序**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="6deab-115">If it is not, click **Priority** from hello dropdown list.</span></span>
    2. <span data-ttu-id="6deab-116">設定 hello**端點監視設定**所有的每個端點，如下所示的此設定檔內相同：</span><span class="sxs-lookup"><span data-stu-id="6deab-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="6deab-117">選取適當的 hello**通訊協定**，並指定 hello**連接埠**數目。</span><span class="sxs-lookup"><span data-stu-id="6deab-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="6deab-118">針對 [路徑]，輸入正斜線 */*。</span><span class="sxs-lookup"><span data-stu-id="6deab-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="6deab-119">toomonitor 端點，您必須指定路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6deab-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="6deab-120">A 正斜線"/"hello 相對路徑是有效的項目，表示該 hello 檔案位於 hello 根目錄 （預設值） 中。</span><span class="sxs-lookup"><span data-stu-id="6deab-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="6deab-121">在 hello hello 頁面頂端，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="6deab-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="6deab-122">在 hello**設定**區段中，按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="6deab-122">In hello **Settings** section, click **Endpoints**.</span></span>
6. <span data-ttu-id="6deab-123">在 hello**端點**刀鋒視窗中，檢閱 hello 優先順序的端點。</span><span class="sxs-lookup"><span data-stu-id="6deab-123">In hello **Endpoints** blade, review hello priority order for your endpoints.</span></span> <span data-ttu-id="6deab-124">當您選取 hello**優先順序**流量路由方式，hello 選取端點的 hello 順序很重要。</span><span class="sxs-lookup"><span data-stu-id="6deab-124">When you select hello **Priority** traffic routing method, hello order of hello selected endpoints matters.</span></span> <span data-ttu-id="6deab-125">請確認 hello 優先順序排列的端點。</span><span class="sxs-lookup"><span data-stu-id="6deab-125">Verify hello priority order of endpoints.</span></span>  <span data-ttu-id="6deab-126">hello 主要端點位於最上方。</span><span class="sxs-lookup"><span data-stu-id="6deab-126">hello primary endpoint is on top.</span></span> <span data-ttu-id="6deab-127">請仔細檢查 hello 順序顯示。</span><span class="sxs-lookup"><span data-stu-id="6deab-127">Double-check on hello order it is displayed.</span></span> <span data-ttu-id="6deab-128">所有要求將會是路由的 toohello 第一個端點，並且如果 Traffic Manager 偵測到它處於狀況不良狀態，hello 流量自動容錯移轉 toohello 下一個端點。</span><span class="sxs-lookup"><span data-stu-id="6deab-128">all requests will be routed toohello first endpoint and if Traffic Manager detects it be unhealthy, hello traffic automatically fails over toohello next endpoint.</span></span> 
7. <span data-ttu-id="6deab-129">toochange hello 端點優先順序，請按一下 hello 端點在 hello**端點**刀鋒視窗，其中會顯示按一下**編輯**並變更 hello**優先順序**值視.</span><span class="sxs-lookup"><span data-stu-id="6deab-129">toochange hello endpoint priority order, click hello endpoint, and in hello **Endpoint** blade that is displayed, click **Edit** and change hello **Priority** value as needed.</span></span> 
8. <span data-ttu-id="6deab-130">按一下**儲存**toosave 變更 hello 端點設定。</span><span class="sxs-lookup"><span data-stu-id="6deab-130">Click **Save** toosave change hello endpoint settings.</span></span>
9. <span data-ttu-id="6deab-131">完成您的組態變更之後，請按一下**儲存**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="6deab-131">After you complete your configuration changes, click **Save** at hello bottom of hello page.</span></span>
10. <span data-ttu-id="6deab-132">測試 hello 變更您的組態，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6deab-132">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="6deab-133">在 hello 入口網站搜尋列中，搜尋 hello Traffic Manager 設定檔名稱，然後按一下 hello Traffic Manager 設定檔在 hello 結果中的顯示該 hello。</span><span class="sxs-lookup"><span data-stu-id="6deab-133">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="6deab-134">在 [hello **Traffic Manager**設定檔] 刀鋒視窗，請按一下**概觀**。</span><span class="sxs-lookup"><span data-stu-id="6deab-134">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="6deab-135">hello **Traffic Manager 設定檔**刀鋒視窗會顯示 hello 您新建立的 Traffic Manager 設定檔的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="6deab-135">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="6deab-136">這可供任何用戶端 （例如，藉由瀏覽的網頁瀏覽器 tooit） 路由傳送 tooget toohello 右端點 hello 路由類型所決定。</span><span class="sxs-lookup"><span data-stu-id="6deab-136">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="6deab-137">在此情況下的所有要求路由的 toohello 第一個端點，而且如果 Traffic Manager 偵測到它處於狀況不良狀態，hello 流量自動容錯移轉 toohello 下一個端點。</span><span class="sxs-lookup"><span data-stu-id="6deab-137">In this case all requests are routed toohello first endpoint and if Traffic Manager detects it be unhealthy, hello traffic automatically fails over toohello next endpoint.</span></span>
11. <span data-ttu-id="6deab-138">一旦您的 Traffic Manager 設定檔運作正常，編輯 hello DNS 記錄，在您的授權 DNS 伺服器 toopoint 您公司網域名稱 toohello Traffic Manager 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="6deab-138">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![使用流量管理員設定優先順序流量路由方法][1]

## <a name="next-steps"></a><span data-ttu-id="6deab-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6deab-140">Next steps</span></span>


- <span data-ttu-id="6deab-141">深入了解[加權流量路由方法](traffic-manager-configure-weighted-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="6deab-141">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="6deab-142">深入了解[效能路由方法](traffic-manager-configure-performance-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="6deab-142">Learn about [performance routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="6deab-143">深入了解[地理路由方法](traffic-manager-configure-geographic-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="6deab-143">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="6deab-144">了解如何太[測試 Traffic Manager 設定](traffic-manager-testing-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="6deab-144">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png