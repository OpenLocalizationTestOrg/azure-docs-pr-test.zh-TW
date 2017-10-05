---
title: "使用 Azure 流量管理員設定地理流量路由方法 | Microsoft Docs"
description: "本文說明如何使用 Azure 流量管理員設定地理流量路由方法"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 13190189074b24b2d28cd3ce46cf8571f3e1e1d1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="configure-the-geographic-traffic-routing-method-using-traffic-manager"></a><span data-ttu-id="ae660-103">使用流量管理員設定地理流量路由方法</span><span class="sxs-lookup"><span data-stu-id="ae660-103">Configure the geographic traffic routing method using Traffic Manager</span></span>

<span data-ttu-id="ae660-104">地理流量路由方法可讓您根據要求的來源地理位置，將流量導向特定的端點位置。</span><span class="sxs-lookup"><span data-stu-id="ae660-104">The Geographic traffic routing method allows you to direct traffic to specific endpoints based on the geographic location where the requests originate.</span></span> <span data-ttu-id="ae660-105">本教學課程示範如何使用這個路由方法來建立流量管理員設定檔，並設定端點以接收來自特定地理位置的流量。</span><span class="sxs-lookup"><span data-stu-id="ae660-105">This tutorial shows you how to create a Traffic Manager profile with this routing method and configure the endpoints to receive traffic from specific geographies.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="ae660-106">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="ae660-106">Create a Traffic Manager Profile</span></span>

1. <span data-ttu-id="ae660-107">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ae660-107">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="ae660-108">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="ae660-108">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span>
2. <span data-ttu-id="ae660-109">在 [中樞] 功能表中，按一下 [新增] > [網路] > [查看全部]，然後按一下 [流量管理員設定檔] 開啟 [建立流量管理員設定檔] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ae660-109">On the Hub menu, click **New** > **Networking** > **See all**, and then click **Traffic Manager profile** to open the **Create Traffic Manager profile** blade.</span></span>
3. <span data-ttu-id="ae660-110">在 [建立流量管理員設定檔] 刀鋒視窗上：</span><span class="sxs-lookup"><span data-stu-id="ae660-110">On the **Create Traffic Manager profile** blade:</span></span>
    1. <span data-ttu-id="ae660-111">提供設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="ae660-111">Provide a name for your profile.</span></span> <span data-ttu-id="ae660-112">此名稱在 trafficmanager.net 區域內必須是唯一的，將會產生 DNS 名稱 <profilename>, trafficmanager.net，用以存取您的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="ae660-112">This name needs to be unique within the trafficmanager.net zone and will result in the DNS name <profilename>,trafficmanager.net which will be used to access your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="ae660-113">選取 [地理] 路由方法。</span><span class="sxs-lookup"><span data-stu-id="ae660-113">Select the **Geographic** routing method.</span></span>
    3. <span data-ttu-id="ae660-114">選取您要用來建立此設定檔的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae660-114">Select the subscription you want to create this profile under.</span></span>
    4. <span data-ttu-id="ae660-115">使用現有的資源群組，或建立新的資源群組來放置此設定檔。</span><span class="sxs-lookup"><span data-stu-id="ae660-115">Use an existing resource group or create a new resource group to place this profile under.</span></span> <span data-ttu-id="ae660-116">如果您選擇建立新的資源群組，請使用 [資源群組位置] 下拉式清單來指定資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="ae660-116">If you choose to create a new resource group, use the **Resource Group location** dropdown to specify the location of the resource group.</span></span> <span data-ttu-id="ae660-117">這項設定是指資源群組的位置，完全不影響將部署到全球的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="ae660-117">This setting refers to the location of the resource group, and has no impact on the Traffic Manager profile which will be deployed globally.</span></span>
    5. <span data-ttu-id="ae660-118">按一下 [建立] 之後，就會建立流量管理員設定檔並部署到全球。</span><span class="sxs-lookup"><span data-stu-id="ae660-118">After you click **Create**, your Traffic Manager profile is created and deployed globally.</span></span>

![建立流量管理員設定檔](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a><span data-ttu-id="ae660-120">新增端點</span><span class="sxs-lookup"><span data-stu-id="ae660-120">Add endpoints</span></span>

1. <span data-ttu-id="ae660-121">在入口網站的 [搜尋] 列中，搜尋您剛才建立的流量管理員設定檔名稱，然後在結果出現時按一下。</span><span class="sxs-lookup"><span data-stu-id="ae660-121">Search for the Traffic Manager profile name you just created in the portal’s search bar and click on the result when it is shown.</span></span>
2. <span data-ttu-id="ae660-122">在 [流量管理員] 刀鋒視窗中，瀏覽至 [設定] -> **[端點]**。</span><span class="sxs-lookup"><span data-stu-id="ae660-122">Navigate to **Settings** -> **Endpoints** in the Traffic Manager blade.</span></span>
3. <span data-ttu-id="ae660-123">按一下 [新增] 顯示 [新增端點] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ae660-123">Click **Add** to show the **Add Endpoint** blade.</span></span>
3. <span data-ttu-id="ae660-124">在 [端點] 刀鋒視窗中，按一下 [新增]，在出現的 **[新增端點]** 刀鋒視窗中，如下所示操作︰</span><span class="sxs-lookup"><span data-stu-id="ae660-124">In the **Endpoints** blade, click **Add** and in the **Add endpoint** blade that is displayed, complete as follows:</span></span>
4. <span data-ttu-id="ae660-125">根據您要新增的端點類型而定，選取 [類型]。</span><span class="sxs-lookup"><span data-stu-id="ae660-125">Select **Type** depending upon the type of endpoint you are adding.</span></span> <span data-ttu-id="ae660-126">針對生產環境中使用的地理路由設定檔，我們強烈建議使用巢狀端點類型，而且包含的子設定檔中有多個端點。</span><span class="sxs-lookup"><span data-stu-id="ae660-126">For geographic routing profiles used in production, we strongly recommend using nested endpoint types containing a child profile with more than one endpoint.</span></span> <span data-ttu-id="ae660-127">如需詳細資訊，請參閱[地理流量路由方法的常見問題集](traffic-manager-FAQs.md)。</span><span class="sxs-lookup"><span data-stu-id="ae660-127">For more details, see [FAQs about geographic traffic routing methods](traffic-manager-FAQs.md).</span></span>
5. <span data-ttu-id="ae660-128">提供您要用來識別這個端點的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="ae660-128">Provide a **Name** by which you want to recognize this endpoint.</span></span>
6. <span data-ttu-id="ae660-129">此刀鋒視窗中的某些欄位，取決於您要新增的端點類型︰</span><span class="sxs-lookup"><span data-stu-id="ae660-129">Certain fields in this blade depend on the type of endpoint you are adding:</span></span>
    1. <span data-ttu-id="ae660-130">如果您要新增 Azure 端點，請根據您想要將流量導向的資源，選取 [目標資源類型] 和 [目標]</span><span class="sxs-lookup"><span data-stu-id="ae660-130">If you are adding an Azure endpoint, select the **Target resource type** and the **Target** based on the resource you want to direct traffic to</span></span>
    2. <span data-ttu-id="ae660-131">如果您要新增**外部** 端點，請提供 [完整網域名稱 (FQDN)] 端點。</span><span class="sxs-lookup"><span data-stu-id="ae660-131">If you are adding an **External** endpoint, provide the **Fully-qualified domain name (FQDN)** for your endpoint.</span></span>
    3. <span data-ttu-id="ae660-132">如果您要新增**巢狀端點**，請選取對應至您想要使用之子設定檔的 [目標資源]，並指定 [子端點計數下限]。</span><span class="sxs-lookup"><span data-stu-id="ae660-132">If you are adding a **Nested endpoint**, select the **Target resource** that corresponds to the child profile you want to use and specify the **Minimum child endpoints count**.</span></span>
7. <span data-ttu-id="ae660-133">在 [地區對應] 區段中，使用下拉式清單新增區域，表示您想要將這些區域的流量傳送至此端點。</span><span class="sxs-lookup"><span data-stu-id="ae660-133">In the Geo-mapping section, use the drop down to add the regions from where you want traffic to be sent to this endpoint.</span></span> <span data-ttu-id="ae660-134">您必須新增至少一個區域，而且可以對應多個區域。</span><span class="sxs-lookup"><span data-stu-id="ae660-134">You must add at least one region, and you can have multiple regions mapped.</span></span>
8. <span data-ttu-id="ae660-135">針對您想要在此設定檔下新增的所有端點，重複此步驟</span><span class="sxs-lookup"><span data-stu-id="ae660-135">Repeat this for all endpoints you want to add under this profile</span></span>

![新增流量管理員端點](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-the-traffic-manager-profile"></a><span data-ttu-id="ae660-137">使用流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="ae660-137">Use the Traffic Manager profile</span></span>
1.  <span data-ttu-id="ae660-138">在入口網站的搜尋列中，搜尋您在上一節建立的**流量管理員設定檔**名稱，然後在顯示的結果中按一下流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="ae660-138">In the portal’s search bar, search for the **Traffic Manager profile** name that you created in the preceding section and click on the traffic manager profile in the results that the displayed.</span></span>
2. <span data-ttu-id="ae660-139">在 [流量管理員設定檔] 刀鋒視窗中，按一下 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="ae660-139">In the **Traffic Manager profile** blade, click **Overview**.</span></span>
3. <span data-ttu-id="ae660-140">[流量管理員設定檔] 刀鋒視窗會顯示新建立之流量管理員設定檔的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="ae660-140">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="ae660-141">這可由任何用戶端使用 (例如使用網頁瀏覽器進行瀏覽)，以路由傳送至由路由類型所決定的正確端點。</span><span class="sxs-lookup"><span data-stu-id="ae660-141">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span>  <span data-ttu-id="ae660-142">如果是地理路由，流量管理員會查看連入要求的來源 IP ，判斷其來源區域。</span><span class="sxs-lookup"><span data-stu-id="ae660-142">In the case of geographic routing, Traffic Manager looks at the source IP of the incoming request and determines the region from which it is originating.</span></span> <span data-ttu-id="ae660-143">如果該區域對應至端點，流量會路由傳送至該處。</span><span class="sxs-lookup"><span data-stu-id="ae660-143">If that region is mapped to an endpoint, traffic is routed to there.</span></span> <span data-ttu-id="ae660-144">如果此區域未對應至端點，流量管理員會傳回 NODATA 查詢回應。</span><span class="sxs-lookup"><span data-stu-id="ae660-144">If this region is not mapped to an endpoint, then Traffic Manager returns a NODATA query response.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae660-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae660-145">Next steps</span></span>

- <span data-ttu-id="ae660-146">深入了解[地理流量路由方法](traffic-manager-routing-methods.md#geographic)。</span><span class="sxs-lookup"><span data-stu-id="ae660-146">Learn more about [Geographic traffic routing method](traffic-manager-routing-methods.md#geographic).</span></span>
- <span data-ttu-id="ae660-147">深入了解如何[測試流量管理員設定](traffic-manager-testing-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="ae660-147">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>
