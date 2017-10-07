---
title: "aaaManage 端點在 Azure Traffic Manager |Microsoft 文件"
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
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a><span data-ttu-id="d21d7-103">新增、停用、啟用或刪除端點</span><span class="sxs-lookup"><span data-stu-id="d21d7-103">Add, disable, enable, or delete endpoints</span></span>

<span data-ttu-id="d21d7-104">Azure App Service 中的 hello Web 應用程式功能已提供容錯移轉和循環配置資源流量路由功能的網站內的資料中心，無論 hello 網站模式為何。</span><span class="sxs-lookup"><span data-stu-id="d21d7-104">hello Web Apps feature in Azure App Service already provides failover and round-robin traffic routing functionality for websites within a datacenter, regardless of hello website mode.</span></span> <span data-ttu-id="d21d7-105">Azure Traffic Manager 可讓您 toospecify 容錯移轉和循環配置資源的流量路由的不同資料中心內的網站和雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d21d7-105">Azure Traffic Manager allows you toospecify failover and round-robin traffic routing for websites and cloud services in different datacenters.</span></span> <span data-ttu-id="d21d7-106">hello 第一個步驟所需 tooprovide 功能是 tooadd hello 雲端服務或網站端點 tooTraffic 管理員。</span><span class="sxs-lookup"><span data-stu-id="d21d7-106">hello first step necessary tooprovide that functionality is tooadd hello cloud service or website endpoint tooTraffic Manager.</span></span>

<span data-ttu-id="d21d7-107">您也可以停用屬於流量管理員設定檔一部分的個別端點。</span><span class="sxs-lookup"><span data-stu-id="d21d7-107">You can also disable individual endpoints that are part of a Traffic Manager profile.</span></span> <span data-ttu-id="d21d7-108">停用端點會讓它 hello 設定檔的一部分，但是 hello 設定檔行為會如同 hello 端點並未包含在內般。</span><span class="sxs-lookup"><span data-stu-id="d21d7-108">Disabling an endpoint leaves it as part of hello profile, but hello profile acts as if hello endpoint is not included in it.</span></span> <span data-ttu-id="d21d7-109">此動作對於暫時移除處於維護模式、或被重新部署的端點而言很有用。</span><span class="sxs-lookup"><span data-stu-id="d21d7-109">This action is useful for temporarily removing an endpoint that is in maintenance mode or being redeployed.</span></span> <span data-ttu-id="d21d7-110">Hello 端點一旦再次啟動並執行，它可以啟用它。</span><span class="sxs-lookup"><span data-stu-id="d21d7-110">Once hello endpoint is up and running again, it can be enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="d21d7-111">停用端點會執行任何動作 toodo 與 Azure 中的部署狀態。</span><span class="sxs-lookup"><span data-stu-id="d21d7-111">Disabling an endpoint has nothing toodo with its deployment state in Azure.</span></span> <span data-ttu-id="d21d7-112">狀況良好的端點保持為最新，而且要能 tooreceive 流量，即使停用 Traffic Manager 中。</span><span class="sxs-lookup"><span data-stu-id="d21d7-112">A healthy endpoint remains up and able tooreceive traffic even when disabled in Traffic Manager.</span></span> <span data-ttu-id="d21d7-113">此外，在一個設定檔中停用端點並不會影響它在另一個設定檔中的狀態。</span><span class="sxs-lookup"><span data-stu-id="d21d7-113">Additionally, disabling an endpoint in one profile does not affect its status in another profile.</span></span>

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a><span data-ttu-id="d21d7-114">tooadd 雲端服務或應用程式服務端點 tooa Traffic Manager 設定檔</span><span class="sxs-lookup"><span data-stu-id="d21d7-114">tooadd a cloud service or an App service endpoint tooa Traffic Manager profile</span></span>

1. <span data-ttu-id="d21d7-115">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d21d7-115">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="d21d7-116">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下hello hello Traffic Manager 設定檔的名稱會顯示該 hello。</span><span class="sxs-lookup"><span data-stu-id="d21d7-116">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that hello displayed.</span></span>
3. <span data-ttu-id="d21d7-117">在 hello **Traffic Manager 設定檔**刀鋒視窗中的，在 hello**設定**區段中，按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-117">In hello **Traffic Manager profile** blade, in hello **Settings** section, click **Endpoints**.</span></span>
4. <span data-ttu-id="d21d7-118">在 hello**端點**刀鋒視窗，其中會顯示按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-118">In hello **Endpoints** blade that is displayed, click **Add**.</span></span>
5. <span data-ttu-id="d21d7-119">在 hello**加入端點**刀鋒視窗中，完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d21d7-119">In hello **Add endpoint** blade, complete as follows:</span></span>
    1. <span data-ttu-id="d21d7-120">在 [類型] 中，按一下 [Azure 端點]。</span><span class="sxs-lookup"><span data-stu-id="d21d7-120">For **Type**, click **Azure endpoint**.</span></span>
    2. <span data-ttu-id="d21d7-121">提供**名稱**要 toorecognize 此端點。</span><span class="sxs-lookup"><span data-stu-id="d21d7-121">Provide a **Name** by which you want toorecognize this endpoint.</span></span>
    3. <span data-ttu-id="d21d7-122">如**目標資源類型**、 從 hello 下拉式清單中，選擇 hello 適當的資源類型。</span><span class="sxs-lookup"><span data-stu-id="d21d7-122">For **Target resource type**, from hello drop-down, choose hello appropriate resource type.</span></span>
    4. <span data-ttu-id="d21d7-123">如**目標資源**、 從 hello 下拉式清單中，選擇適當的目標資源，hello tooshow hello 清單下的資源 hello 相同的訂用帳戶中 hello**資源刀鋒視窗**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-123">For **Target resource**, from hello drop-down, choose hello appropriate target resource tooshow hello listing resources under hello same subscription in hello **Resources blade**.</span></span> <span data-ttu-id="d21d7-124">在 hello**資源**刀鋒視窗，其中會顯示您想 tooadd，如 hello 第一個端點挑選 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d21d7-124">In hello **Resource** blade that is displayed, pick hello service that you want tooadd as hello first endpoint.</span></span>
    5. <span data-ttu-id="d21d7-125">在 [優先順序] 中，選取 [1]。</span><span class="sxs-lookup"><span data-stu-id="d21d7-125">For **Priority**, select as **1**.</span></span> <span data-ttu-id="d21d7-126">這會導致所有流量 toothis 端點是否狀況良好。</span><span class="sxs-lookup"><span data-stu-id="d21d7-126">This results in all traffic going toothis endpoint if it is healthy.</span></span>
    6. <span data-ttu-id="d21d7-127">維持不勾選 [新增為已停用]。</span><span class="sxs-lookup"><span data-stu-id="d21d7-127">Keep **Add as disabled** unchecked.</span></span>
    7. <span data-ttu-id="d21d7-128">按一下 [檔案] &gt; [新增] &gt; [專案] </span><span class="sxs-lookup"><span data-stu-id="d21d7-128">Click **OK**</span></span>
6.  <span data-ttu-id="d21d7-129">重複步驟 4 和 5 tooadd hello 下一個 Azure 端點。</span><span class="sxs-lookup"><span data-stu-id="d21d7-129">Repeat steps 4 and 5 tooadd hello next Azure endpoint.</span></span> <span data-ttu-id="d21d7-130">請確定 tooadd 使用其**優先順序**在設定值**2**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-130">Make sure tooadd it with its **Priority** value set at **2**.</span></span>
7.  <span data-ttu-id="d21d7-131">這兩個端點的 hello 加法完成時，它們會顯示在 hello **Traffic Manager 設定檔**刀鋒視窗，以及其監視的狀態為**線上**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-131">When hello addition of both endpoints is complete, they are displayed in hello **Traffic Manager profile** blade along with their monitoring status as **Online**.</span></span>

> [!NOTE]
> <span data-ttu-id="d21d7-132">在新增或移除端點，從使用 hello 設定檔之後*容錯移轉*流量路由方法、 hello 容錯移轉優先順序清單可能無法排序它們您想要的方式。</span><span class="sxs-lookup"><span data-stu-id="d21d7-132">After you add or remove an endpoint from a profile using hello *Failover* traffic routing method, hello failover priority list may not be ordered they way you want.</span></span> <span data-ttu-id="d21d7-133">您可以調整 hello hello 組態 頁面上的 hello 容錯移轉優先順序清單順序。</span><span class="sxs-lookup"><span data-stu-id="d21d7-133">You can adjust hello order of hello Failover Priority List on hello Configuration page.</span></span> <span data-ttu-id="d21d7-134">如需詳細資訊，請參閱 [設定容錯移轉流量路由](traffic-manager-configure-failover-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="d21d7-134">For more information, see [Configure Failover traffic routing](traffic-manager-configure-failover-routing-method.md).</span></span>

## <a name="toodisable-an-endpoint"></a><span data-ttu-id="d21d7-135">toodisable 端點</span><span class="sxs-lookup"><span data-stu-id="d21d7-135">toodisable an endpoint</span></span>

1. <span data-ttu-id="d21d7-136">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d21d7-136">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="d21d7-137">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下顯示 hello 結果 hello Traffic Manager 設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="d21d7-137">In hello portal’s search bar, search for hello  **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that are displayed.</span></span>
3. <span data-ttu-id="d21d7-138">在 hello **Traffic Manager 設定檔**刀鋒視窗中的，在 hello**設定**區段中，按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-138">In hello **Traffic Manager profile** blade, in hello **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="d21d7-139">按一下您想 toodisable，hello 端點，然後在 hello**端點**刀鋒視窗，其中會顯示按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-139">Click hello endpoint that you want toodisable, and then on hello **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="d21d7-140">在 hello**端點**刀鋒視窗中，也變更 hello 端點狀態**已停用**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-140">In hello **Endpoint** blade, change hello endpoint status too**Disabled**, and then click **Save**.</span></span>
6. <span data-ttu-id="d21d7-141">用戶端會繼續 toosend 流量 toohello 端點 hello 持續時間內的存留時間 (TTL)。</span><span class="sxs-lookup"><span data-stu-id="d21d7-141">Clients continue toosend traffic toohello endpoint for hello duration of Time-to-Live (TTL).</span></span> <span data-ttu-id="d21d7-142">您可以變更 hello TTL hello 的 hello Traffic Manager 設定檔設定 頁面上。</span><span class="sxs-lookup"><span data-stu-id="d21d7-142">You can change hello TTL on hello Configuration page of hello Traffic Manager profile.</span></span>

## <a name="tooenable-an-endpoint"></a><span data-ttu-id="d21d7-143">tooenable 端點</span><span class="sxs-lookup"><span data-stu-id="d21d7-143">tooenable an endpoint</span></span>

1. <span data-ttu-id="d21d7-144">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d21d7-144">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="d21d7-145">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下顯示 hello 結果 hello Traffic Manager 設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="d21d7-145">In hello portal’s search bar, search for hello  **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that are displayed.</span></span>
3. <span data-ttu-id="d21d7-146">在 hello **Traffic Manager 設定檔**刀鋒視窗中的，在 hello**設定**區段中，按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-146">In hello **Traffic Manager profile** blade, in hello **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="d21d7-147">按一下您想 toodisable，hello 端點，然後在 hello**端點**刀鋒視窗，其中會顯示按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-147">Click hello endpoint that you want toodisable, and then on hello **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="d21d7-148">在 hello**端點**刀鋒視窗中，也變更 hello 端點狀態**啟用**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-148">In hello **Endpoint** blade, change hello endpoint status too**Enabled**, and then click **Save**.</span></span>
6. <span data-ttu-id="d21d7-149">用戶端會繼續 toosend 流量 toohello 端點 hello 持續時間內的存留時間 (TTL)。</span><span class="sxs-lookup"><span data-stu-id="d21d7-149">Clients continue toosend traffic toohello endpoint for hello duration of Time-to-Live (TTL).</span></span> <span data-ttu-id="d21d7-150">您可以變更 hello TTL hello 的 hello Traffic Manager 設定檔設定 頁面上。</span><span class="sxs-lookup"><span data-stu-id="d21d7-150">You can change hello TTL on hello Configuration page of hello Traffic Manager profile.</span></span>

## <a name="toodelete-an-endpoint"></a><span data-ttu-id="d21d7-151">toodelete 端點</span><span class="sxs-lookup"><span data-stu-id="d21d7-151">toodelete an endpoint</span></span>

1. <span data-ttu-id="d21d7-152">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d21d7-152">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="d21d7-153">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下顯示 hello 結果 hello Traffic Manager 設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="d21d7-153">In hello portal’s search bar, search for hello  **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that are displayed.</span></span>
3. <span data-ttu-id="d21d7-154">在 hello **Traffic Manager 設定檔**刀鋒視窗中的，在 hello**設定**區段中，按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-154">In hello **Traffic Manager profile** blade, in hello **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="d21d7-155">按一下您想 toodisable，hello 端點，然後在 hello**端點**刀鋒視窗，其中會顯示按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-155">Click hello endpoint that you want toodisable, and then on hello **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="d21d7-156">在 hello**端點**刀鋒視窗中，也變更 hello 端點狀態**啟用**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="d21d7-156">In hello **Endpoint** blade, change hello endpoint status too**Enabled**, and then click **Save**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d21d7-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d21d7-157">Next steps</span></span>

* [<span data-ttu-id="d21d7-158">管理流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="d21d7-158">Manage Traffic Manager profiles</span></span>](traffic-manager-manage-profiles.md)
* [<span data-ttu-id="d21d7-159">設定路由方法</span><span class="sxs-lookup"><span data-stu-id="d21d7-159">Configure routing methods</span></span>](traffic-manager-configure-routing-method.md)
* [<span data-ttu-id="d21d7-160">疑難排解流量管理員的已降級狀態</span><span class="sxs-lookup"><span data-stu-id="d21d7-160">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
* [<span data-ttu-id="d21d7-161">流量管理員的效能考量</span><span class="sxs-lookup"><span data-stu-id="d21d7-161">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="d21d7-162">流量管理員的相關作業 (REST API 參考)</span><span class="sxs-lookup"><span data-stu-id="d21d7-162">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=313584)

