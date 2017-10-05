---
title: "在 Azure 中建立流量管理員設定檔 | Microsoft Docs"
description: "本文說明如何建立流量管理員設定檔"
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
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 3792c9eca3d3a281cc12d241d46fbf5e5bc8e6b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="29c75-103">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="29c75-103">Create a Traffic Manager profile</span></span>

<span data-ttu-id="29c75-104">本文說明如何建立具有**優先順序**路由類型的設定檔，用以將使用者路由傳送至兩個 Azure Web Apps 端點。</span><span class="sxs-lookup"><span data-stu-id="29c75-104">This article describes how a profile with **Priority** routing type can be created to route users to two Azure Web Apps endpoints.</span></span> <span data-ttu-id="29c75-105">使用**優先順序**路由類型時，所有流量會路由傳送至第一個端點，而第二個端點會保留做為備份。</span><span class="sxs-lookup"><span data-stu-id="29c75-105">By using the **Priority** routing type, all traffic is routed to the first endpoint while the second is kept as a backup.</span></span> <span data-ttu-id="29c75-106">因此，如果第一個端點變成狀況不良，就可將使用者路由傳送至第二個端點。</span><span class="sxs-lookup"><span data-stu-id="29c75-106">As a result, users can be routed to the second endpoint if the first endpoint becomes unhealthy.</span></span>

<span data-ttu-id="29c75-107">本文中，先前建立的兩個 Azure Web 應用程式端點會與這個新建立的流量管理員設定檔相關聯。</span><span class="sxs-lookup"><span data-stu-id="29c75-107">In this article, two previously created Azure Web App endpoints are associated to this newly created Traffic Manager profile.</span></span> <span data-ttu-id="29c75-108">若要深入了解如何建立 Azure Web 應用程式端點，請瀏覽 [Azure Web Apps 文件頁面](https://docs.microsoft.com/azure/app-service-web/)。</span><span class="sxs-lookup"><span data-stu-id="29c75-108">To learn more about how to create Azure Web App endpoints, visit the [Azure Web Apps documentation page](https://docs.microsoft.com/azure/app-service-web/).</span></span> <span data-ttu-id="29c75-109">您可以新增具有 DNS 名稱且可透過公用網際網路觸達的任何端點，我們使用 Azure Web Apps 端點做為例子。</span><span class="sxs-lookup"><span data-stu-id="29c75-109">You can add any endpoint that has a DNS name and is reachable over the public internet and that we are using Azure Web Apps endpoints as an example.</span></span>

### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="29c75-110">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="29c75-110">Create a Traffic Manager profile</span></span>
1. <span data-ttu-id="29c75-111">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="29c75-111">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="29c75-112">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="29c75-112">If you don’t already have an account, you can sign-up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="29c75-113">在 [中樞] 功能表中，按一下 [新增] > [網路] > [查看全部]**，然後按一下 [流量管理員]****設定檔，以開啟 [建立流量管理員設定檔]** 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="29c75-113">On the **Hub** menu, click **New** > **Networking** > **See all**, click **Traffic Manager** profile to open the **Create Traffic Manager profile** blade, then click **Create**.</span></span>
3. <span data-ttu-id="29c75-114">在 [建立流量管理員設定檔] 刀鋒視窗上，如下所示操作：</span><span class="sxs-lookup"><span data-stu-id="29c75-114">On the **Create Traffic Manager profile** blade, complete as follows:</span></span>
    1. <span data-ttu-id="29c75-115">在 [名稱]中，提供設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="29c75-115">In **Name**, provide a name for your profile.</span></span> <span data-ttu-id="29c75-116">此名稱在 trafficmanager.net 區域內必須是唯一的，而且會產生 DNS 名稱 <name>, trafficmanager.net，用以存取您的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="29c75-116">This name needs to be unique within the trafficmanager.net zone and results in the DNS name <name>,trafficmanager.net which is used to access your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="29c75-117">在 [路由方法] 中，選取 [優先順序]路由方法。</span><span class="sxs-lookup"><span data-stu-id="29c75-117">In **Routing method**, select the **Priority** routing method.</span></span>
    3. <span data-ttu-id="29c75-118">在 [訂用帳戶] 中，選取您要用來建立此設定檔的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="29c75-118">In **Subscription**, select the subscription you want to create this profile under</span></span>
    4. <span data-ttu-id="29c75-119">在 [資源群組]中，建立新的資源群組來放置此設定檔。</span><span class="sxs-lookup"><span data-stu-id="29c75-119">In **Resource Group**, create a new resource group to place this profile under.</span></span>
    5. <span data-ttu-id="29c75-120">在 [資源群組位置] 中，選取資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="29c75-120">In **Resource group location**, select the location of the resource group.</span></span> <span data-ttu-id="29c75-121">這項設定是指資源群組的位置，完全不影響將部署到全球的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="29c75-121">This setting refers to the location of the resource group, and has no impact on the Traffic Manager profile that will be deployed globally.</span></span>
    6. <span data-ttu-id="29c75-122">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="29c75-122">Click **Create**.</span></span>
    7. <span data-ttu-id="29c75-123">當流量管理員設定檔的全球部署完成時，它會列為個別資源群組的其中一個資源。</span><span class="sxs-lookup"><span data-stu-id="29c75-123">When the global deployment of your Traffic Manager profile is complete, it is listed in respective resource group as one of the resources.</span></span>

    ![建立流量管理員設定檔](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a><span data-ttu-id="29c75-125">新增流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="29c75-125">Add Traffic Manager endpoints</span></span>

1. <span data-ttu-id="29c75-126">在入口網站的搜尋列中，搜尋您在上一節建立的**流量管理員設定檔**名稱，然後在顯示的結果中按一下流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="29c75-126">In the portal’s search bar, search for the **Traffic Manager profile** name that you created in the preceding section and click the traffic manager profile in the results that the displayed.</span></span>
2. <span data-ttu-id="29c75-127">在 [流量管理員設定檔] 刀鋒視窗中，請在 [設定] 區段中按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="29c75-127">In the **Traffic Manager profile** blade, in the **Settings** section, click **Endpoints**.</span></span>
3. <span data-ttu-id="29c75-128">在顯示的 [端點] 刀鋒視窗中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="29c75-128">In the **Endpoints** blade that is displayed, click **Add**.</span></span>
4. <span data-ttu-id="29c75-129">在 [新增端點] 刀鋒視窗中，如下所示操作︰</span><span class="sxs-lookup"><span data-stu-id="29c75-129">In the **Add endpoint** blade, complete as follows:</span></span>
    1. <span data-ttu-id="29c75-130">在 [類型] 中，按一下 [Azure 端點]。</span><span class="sxs-lookup"><span data-stu-id="29c75-130">For **Type**, click **Azure endpoint**.</span></span>
    2. <span data-ttu-id="29c75-131">提供您要用來識別這個端點的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="29c75-131">Provide a **Name** by which you want to recognize this endpoint.</span></span>
    3. <span data-ttu-id="29c75-132">在 [目標資源類型] 中，按一下 [App Service]。</span><span class="sxs-lookup"><span data-stu-id="29c75-132">For **Target resource type**, click **App Service**.</span></span>
    4. <span data-ttu-id="29c75-133">在 [目標資源] 中，按一下 [選擇應用程式服務]，顯示相同訂用帳戶下的 Web Apps 清單。</span><span class="sxs-lookup"><span data-stu-id="29c75-133">For **Target resource**, click **Choose an app service** to show the listing of the Web Apps under the same subscription.</span></span> <span data-ttu-id="29c75-134">在顯示的 [資源] 刀鋒視窗中，挑選您想要新增為第一個端點的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="29c75-134">In the **Resource** blade that is displayed, pick the App service that you want to add as the first endpoint.</span></span>
    5. <span data-ttu-id="29c75-135">在 [優先順序] 中，選取 [1]。</span><span class="sxs-lookup"><span data-stu-id="29c75-135">For **Priority**, select as **1**.</span></span> <span data-ttu-id="29c75-136">這會使得所有流量傳送至此端點 (如果狀況良好)。</span><span class="sxs-lookup"><span data-stu-id="29c75-136">This results in all traffic going to this endpoint if it is healthy.</span></span>
    6. <span data-ttu-id="29c75-137">維持不勾選 [新增為已停用]。</span><span class="sxs-lookup"><span data-stu-id="29c75-137">Keep **Add as disabled** unchecked.</span></span>
    7. <span data-ttu-id="29c75-138">按一下 [檔案] &gt; [新增] &gt; [專案] </span><span class="sxs-lookup"><span data-stu-id="29c75-138">Click **OK**</span></span>
5.  <span data-ttu-id="29c75-139">針對下一個 Azure Web Apps 端點，重複步驟 3 和 4。</span><span class="sxs-lookup"><span data-stu-id="29c75-139">Repeat steps 3 and 4 for the next Azure Web Apps endpoint.</span></span> <span data-ttu-id="29c75-140">新增它時務必將 [優先順序] 值設為 [2]。</span><span class="sxs-lookup"><span data-stu-id="29c75-140">Make sure to add it with its **Priority** value set at **2**.</span></span>
6.  <span data-ttu-id="29c75-141">這兩個端點新增完畢後，它們會顯示在 [流量管理員設定檔] 刀鋒視窗中，而且監視狀態是 [線上]。</span><span class="sxs-lookup"><span data-stu-id="29c75-141">When the addition of both endpoints is complete, they are displayed in the **Traffic Manager profile** blade along with their monitoring status as **Online**.</span></span>

    ![新增流量管理員端點](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-the-traffic-manager-profile"></a><span data-ttu-id="29c75-143">使用流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="29c75-143">Use the Traffic Manager profile</span></span>
1.  <span data-ttu-id="29c75-144">在入口網站的搜尋列中，搜尋您在上一節建立的**流量管理員設定檔**名稱。</span><span class="sxs-lookup"><span data-stu-id="29c75-144">In the portal’s search bar, search for the **Traffic Manager profile** name that you created in the preceding section.</span></span> <span data-ttu-id="29c75-145">在顯示的結果中，按一下流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="29c75-145">In the results that are displayed, click the traffic manager profile.</span></span>
2. <span data-ttu-id="29c75-146">在 [流量管理員設定檔] 刀鋒視窗中，按一下 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="29c75-146">In the **Traffic Manager profile** blade, click **Overview**.</span></span>
3. <span data-ttu-id="29c75-147">[流量管理員設定檔] 刀鋒視窗會顯示新建立之流量管理員設定檔的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="29c75-147">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="29c75-148">這可由任何用戶端使用 (例如使用網頁瀏覽器進行瀏覽)，以路由傳送至由路由類型所決定的正確端點。</span><span class="sxs-lookup"><span data-stu-id="29c75-148">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="29c75-149">在此情況下，所有的要求都將路由傳送到第一個端點，且如果流量管理員偵測到端點狀況不良，流量會自動容錯移轉到下一個端點。</span><span class="sxs-lookup"><span data-stu-id="29c75-149">In this case, all requests are routed to the first endpoint and if Traffic Manager detects it be unhealthy, the traffic automatically fails over to the next endpoint.</span></span>

## <a name="delete-the-traffic-manager-profile"></a><span data-ttu-id="29c75-150">刪除流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="29c75-150">Delete the Traffic Manager profile</span></span>
<span data-ttu-id="29c75-151">刪除不再需要的資源群組和您已建立的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="29c75-151">When no longer needed, delete the resource group and the Traffic Manager profile that you have created.</span></span> <span data-ttu-id="29c75-152">若要這樣做，請從 [流量管理員設定檔] 刀鋒視窗中選取資源群組，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="29c75-152">To do so, select the resource group from the **Traffic Manager profile** blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29c75-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="29c75-153">Next steps</span></span>

- <span data-ttu-id="29c75-154">深入了解[路由類型](traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="29c75-154">Learn more about [routing types](traffic-manager-routing-methods.md).</span></span>
- <span data-ttu-id="29c75-155">深入了解端點類型[端點類型](traffic-manager-endpoint-types.md)。</span><span class="sxs-lookup"><span data-stu-id="29c75-155">Learn more about endpoint types [endpoint types](traffic-manager-endpoint-types.md).</span></span>
- <span data-ttu-id="29c75-156">深入了解[端點監視](traffic-manager-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="29c75-156">Learn more about [endpoint monitoring](traffic-manager-monitoring.md).</span></span>



