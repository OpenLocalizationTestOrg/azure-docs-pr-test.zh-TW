---
title: "在 Azure 流量管理員中管理端點 | Microsoft Docs"
description: "本文將協助您從 Azure 流量管理員加入、移除、啟用和停用端點。"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: 765d12bc283d991783fb3190ce7917b573f9fc78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a><span data-ttu-id="a153c-103">新增、停用、啟用或刪除端點</span><span class="sxs-lookup"><span data-stu-id="a153c-103">Add, disable, enable, or delete endpoints</span></span>

<span data-ttu-id="a153c-104">不論網站模式為何，Azure App Service 中的 Web Apps 功能已為資料中心內的網站提供容錯移轉和循環配置資源流量路由功能。</span><span class="sxs-lookup"><span data-stu-id="a153c-104">The Web Apps feature in Azure App Service already provides failover and round-robin traffic routing functionality for websites within a datacenter, regardless of the website mode.</span></span> <span data-ttu-id="a153c-105">Azure 流量管理員可讓您在不同的資料中心的網站和雲端服務中指定容錯移轉和循環配置資源流量路由。</span><span class="sxs-lookup"><span data-stu-id="a153c-105">Azure Traffic Manager allows you to specify failover and round-robin traffic routing for websites and cloud services in different datacenters.</span></span> <span data-ttu-id="a153c-106">提供該項功能的首要步驟是將雲端服務或網站端點新增至流量管理員。</span><span class="sxs-lookup"><span data-stu-id="a153c-106">The first step necessary to provide that functionality is to add the cloud service or website endpoint to Traffic Manager.</span></span>

<span data-ttu-id="a153c-107">您也可以停用屬於流量管理員設定檔一部分的個別端點。</span><span class="sxs-lookup"><span data-stu-id="a153c-107">You can also disable individual endpoints that are part of a Traffic Manager profile.</span></span> <span data-ttu-id="a153c-108">停用端點會將端點做為設定檔的一部分保留，但是設定檔會以好像未包含端點的方式運作。</span><span class="sxs-lookup"><span data-stu-id="a153c-108">Disabling an endpoint leaves it as part of the profile, but the profile acts as if the endpoint is not included in it.</span></span> <span data-ttu-id="a153c-109">此動作對於暫時移除處於維護模式、或被重新部署的端點而言很有用。</span><span class="sxs-lookup"><span data-stu-id="a153c-109">This action is useful for temporarily removing an endpoint that is in maintenance mode or being redeployed.</span></span> <span data-ttu-id="a153c-110">在重新啟動並執行端點之後，您可以將它啟用。</span><span class="sxs-lookup"><span data-stu-id="a153c-110">Once the endpoint is up and running again, it can be enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="a153c-111">停用端點會與其在 Azure 中的部署狀態無關。</span><span class="sxs-lookup"><span data-stu-id="a153c-111">Disabling an endpoint has nothing to do with its deployment state in Azure.</span></span> <span data-ttu-id="a153c-112">健全的端點將會持續運作，並且即使在流量管理員中停用該服務時仍然可以接收流量。</span><span class="sxs-lookup"><span data-stu-id="a153c-112">A healthy endpoint remains up and able to receive traffic even when disabled in Traffic Manager.</span></span> <span data-ttu-id="a153c-113">此外，在一個設定檔中停用端點並不會影響它在另一個設定檔中的狀態。</span><span class="sxs-lookup"><span data-stu-id="a153c-113">Additionally, disabling an endpoint in one profile does not affect its status in another profile.</span></span>

## <a name="to-add-a-cloud-service-or-an-app-service-endpoint-to-a-traffic-manager-profile"></a><span data-ttu-id="a153c-114">若要將雲端服務或應用程式服務端點新增至流量管理員設定檔：</span><span class="sxs-lookup"><span data-stu-id="a153c-114">To add a cloud service or an App service endpoint to a Traffic Manager profile</span></span>

1. <span data-ttu-id="a153c-115">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a153c-115">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="a153c-116">在入口網站的搜尋列中，搜尋您想要修改的**流量管理員設定檔**名稱，然後按一下結果中顯示的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="a153c-116">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span></span>
3. <span data-ttu-id="a153c-117">在 [流量管理員設定檔] 刀鋒視窗中，請在 [設定] 區段中按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="a153c-117">In the **Traffic Manager profile** blade, in the **Settings** section, click **Endpoints**.</span></span>
4. <span data-ttu-id="a153c-118">在顯示的 [端點] 刀鋒視窗中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a153c-118">In the **Endpoints** blade that is displayed, click **Add**.</span></span>
5. <span data-ttu-id="a153c-119">在 [新增端點] 刀鋒視窗中，如下所示操作︰</span><span class="sxs-lookup"><span data-stu-id="a153c-119">In the **Add endpoint** blade, complete as follows:</span></span>
    1. <span data-ttu-id="a153c-120">在 [類型] 中，按一下 [Azure 端點]。</span><span class="sxs-lookup"><span data-stu-id="a153c-120">For **Type**, click **Azure endpoint**.</span></span>
    2. <span data-ttu-id="a153c-121">提供您要用來識別這個端點的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="a153c-121">Provide a **Name** by which you want to recognize this endpoint.</span></span>
    3. <span data-ttu-id="a153c-122">對於 [目標資源類型]，從下拉式清單中選擇適當的資源類型。</span><span class="sxs-lookup"><span data-stu-id="a153c-122">For **Target resource type**, from the drop-down, choose the appropriate resource type.</span></span>
    4. <span data-ttu-id="a153c-123">對於 [目標資源]，從下拉式清單中選擇適當的目標資源，以在 [資源] 刀鋒視窗中顯示相同訂用帳戶下的清單資源。</span><span class="sxs-lookup"><span data-stu-id="a153c-123">For **Target resource**, from the drop-down, choose the appropriate target resource to show the listing resources under the same subscription in the **Resources blade**.</span></span> <span data-ttu-id="a153c-124">在顯示的 [資源] 刀鋒視窗中，挑選您想要新增為第一個端點的服務。</span><span class="sxs-lookup"><span data-stu-id="a153c-124">In the **Resource** blade that is displayed, pick the service that you want to add as the first endpoint.</span></span>
    5. <span data-ttu-id="a153c-125">在 [優先順序] 中，選取 [1]。</span><span class="sxs-lookup"><span data-stu-id="a153c-125">For **Priority**, select as **1**.</span></span> <span data-ttu-id="a153c-126">這會使得所有流量傳送至此端點 (如果狀況良好)。</span><span class="sxs-lookup"><span data-stu-id="a153c-126">This results in all traffic going to this endpoint if it is healthy.</span></span>
    6. <span data-ttu-id="a153c-127">維持不勾選 [新增為已停用]。</span><span class="sxs-lookup"><span data-stu-id="a153c-127">Keep **Add as disabled** unchecked.</span></span>
    7. <span data-ttu-id="a153c-128">按一下 [確定] </span><span class="sxs-lookup"><span data-stu-id="a153c-128">Click **OK**</span></span>
6.  <span data-ttu-id="a153c-129">重複步驟 4 和 5，新增下一個 Azure 端點。</span><span class="sxs-lookup"><span data-stu-id="a153c-129">Repeat steps 4 and 5 to add the next Azure endpoint.</span></span> <span data-ttu-id="a153c-130">新增它時務必將 [優先順序] 值設為 [2]。</span><span class="sxs-lookup"><span data-stu-id="a153c-130">Make sure to add it with its **Priority** value set at **2**.</span></span>
7.  <span data-ttu-id="a153c-131">這兩個端點新增完畢後，它們會顯示在 [流量管理員設定檔] 刀鋒視窗中，而且監視狀態是 [線上]。</span><span class="sxs-lookup"><span data-stu-id="a153c-131">When the addition of both endpoints is complete, they are displayed in the **Traffic Manager profile** blade along with their monitoring status as **Online**.</span></span>

> [!NOTE]
> <span data-ttu-id="a153c-132">在使用容錯移轉流量路由方法從設定檔新增或移除端點後，容錯移轉優先權清單可能無法依您想要的方式排序。</span><span class="sxs-lookup"><span data-stu-id="a153c-132">After you add or remove an endpoint from a profile using the *Failover* traffic routing method, the failover priority list may not be ordered they way you want.</span></span> <span data-ttu-id="a153c-133">您可以在 [組態] 頁面上調整容錯移轉優先順序清單的順序。</span><span class="sxs-lookup"><span data-stu-id="a153c-133">You can adjust the order of the Failover Priority List on the Configuration page.</span></span> <span data-ttu-id="a153c-134">如需詳細資訊，請參閱 [設定容錯移轉流量路由](traffic-manager-configure-failover-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="a153c-134">For more information, see [Configure Failover traffic routing](traffic-manager-configure-failover-routing-method.md).</span></span>

## <a name="to-disable-an-endpoint"></a><span data-ttu-id="a153c-135">若要停用端點</span><span class="sxs-lookup"><span data-stu-id="a153c-135">To disable an endpoint</span></span>

1. <span data-ttu-id="a153c-136">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a153c-136">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="a153c-137">在入口網站的搜尋列中，搜尋您想要修改的**流量管理員設定檔**名稱，然後按一下結果中顯示的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="a153c-137">In the portal’s search bar, search for the  **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that are displayed.</span></span>
3. <span data-ttu-id="a153c-138">在 [流量管理員設定檔] 刀鋒視窗中，請在 [設定] 區段中按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="a153c-138">In the **Traffic Manager profile** blade, in the **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="a153c-139">按一下您要停用的端點，然後在顯示的 [端點] 刀鋒視窗上，按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="a153c-139">Click the endpoint that you want to disable, and then on the **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="a153c-140">在 [端點] 刀鋒視窗中，將端點狀態變更為 [已停用]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a153c-140">In the **Endpoint** blade, change the endpoint status to **Disabled**, and then click **Save**.</span></span>
6. <span data-ttu-id="a153c-141">用戶端會繼續將流量傳送至端點以取得存留時間 (TTL) 持續時間。</span><span class="sxs-lookup"><span data-stu-id="a153c-141">Clients continue to send traffic to the endpoint for the duration of Time-to-Live (TTL).</span></span> <span data-ttu-id="a153c-142">您可以在流量管理員設定檔的 [組態] 頁面上變更 TTL。</span><span class="sxs-lookup"><span data-stu-id="a153c-142">You can change the TTL on the Configuration page of the Traffic Manager profile.</span></span>

## <a name="to-enable-an-endpoint"></a><span data-ttu-id="a153c-143">若要啟用端點</span><span class="sxs-lookup"><span data-stu-id="a153c-143">To enable an endpoint</span></span>

1. <span data-ttu-id="a153c-144">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a153c-144">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="a153c-145">在入口網站的搜尋列中，搜尋您想要修改的**流量管理員設定檔**名稱，然後按一下結果中顯示的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="a153c-145">In the portal’s search bar, search for the  **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that are displayed.</span></span>
3. <span data-ttu-id="a153c-146">在 [流量管理員設定檔] 刀鋒視窗中，請在 [設定] 區段中按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="a153c-146">In the **Traffic Manager profile** blade, in the **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="a153c-147">按一下您要停用的端點，然後在顯示的 [端點] 刀鋒視窗上，按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="a153c-147">Click the endpoint that you want to disable, and then on the **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="a153c-148">在 [端點] 刀鋒視窗中，將端點狀態變更為 [已啟用]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a153c-148">In the **Endpoint** blade, change the endpoint status to **Enabled**, and then click **Save**.</span></span>
6. <span data-ttu-id="a153c-149">用戶端會繼續將流量傳送至端點以取得存留時間 (TTL) 持續時間。</span><span class="sxs-lookup"><span data-stu-id="a153c-149">Clients continue to send traffic to the endpoint for the duration of Time-to-Live (TTL).</span></span> <span data-ttu-id="a153c-150">您可以在流量管理員設定檔的 [組態] 頁面上變更 TTL。</span><span class="sxs-lookup"><span data-stu-id="a153c-150">You can change the TTL on the Configuration page of the Traffic Manager profile.</span></span>

## <a name="to-delete-an-endpoint"></a><span data-ttu-id="a153c-151">若要刪除端點：</span><span class="sxs-lookup"><span data-stu-id="a153c-151">To delete an endpoint</span></span>

1. <span data-ttu-id="a153c-152">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a153c-152">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="a153c-153">在入口網站的搜尋列中，搜尋您想要修改的**流量管理員設定檔**名稱，然後按一下結果中顯示的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="a153c-153">In the portal’s search bar, search for the  **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that are displayed.</span></span>
3. <span data-ttu-id="a153c-154">在 [流量管理員設定檔] 刀鋒視窗中，請在 [設定] 區段中按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="a153c-154">In the **Traffic Manager profile** blade, in the **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="a153c-155">按一下您要停用的端點，然後在顯示的 [端點] 刀鋒視窗上，按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="a153c-155">Click the endpoint that you want to disable, and then on the **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="a153c-156">在 [端點] 刀鋒視窗中，將端點狀態變更為 [已啟用]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a153c-156">In the **Endpoint** blade, change the endpoint status to **Enabled**, and then click **Save**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a153c-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a153c-157">Next steps</span></span>

* [<span data-ttu-id="a153c-158">管理流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="a153c-158">Manage Traffic Manager profiles</span></span>](traffic-manager-manage-profiles.md)
* [<span data-ttu-id="a153c-159">設定路由方法</span><span class="sxs-lookup"><span data-stu-id="a153c-159">Configure routing methods</span></span>](traffic-manager-configure-routing-method.md)
* [<span data-ttu-id="a153c-160">疑難排解流量管理員的已降級狀態</span><span class="sxs-lookup"><span data-stu-id="a153c-160">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
* [<span data-ttu-id="a153c-161">流量管理員的效能考量</span><span class="sxs-lookup"><span data-stu-id="a153c-161">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="a153c-162">流量管理員的相關作業 (REST API 參考)</span><span class="sxs-lookup"><span data-stu-id="a153c-162">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=313584)

