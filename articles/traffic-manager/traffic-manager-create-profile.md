---
title: "aaaCreate Azure Traffic Manager 設定檔 |Microsoft 文件"
description: "本文說明如何 toocreate Traffic Manager 設定檔"
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
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="8bb5f-103">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="8bb5f-103">Create a Traffic Manager profile</span></span>

<span data-ttu-id="8bb5f-104">本文說明如何使用設定檔**優先順序**tooroute 使用者 tootwo Azure Web 應用程式端點可以建立路由類型。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-104">This article describes how a profile with **Priority** routing type can be created tooroute users tootwo Azure Web Apps endpoints.</span></span> <span data-ttu-id="8bb5f-105">使用 hello**優先順序**路由類型，所有流量都是路由的 toohello 第一個端點而第二個 hello 將保留做為備份。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-105">By using hello **Priority** routing type, all traffic is routed toohello first endpoint while hello second is kept as a backup.</span></span> <span data-ttu-id="8bb5f-106">如此一來，使用者可以是路由的 toohello 第二個端點，如果 hello 第一個端點會變為狀況不良。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-106">As a result, users can be routed toohello second endpoint if hello first endpoint becomes unhealthy.</span></span>

<span data-ttu-id="8bb5f-107">在本文中，兩個先前建立的 Azure Web 應用程式端點會是新建立的關聯的 toothis Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-107">In this article, two previously created Azure Web App endpoints are associated toothis newly created Traffic Manager profile.</span></span> <span data-ttu-id="8bb5f-108">深入了解如何 toolearn toocreate Azure Web 應用程式端點，請瀏覽 hello [Azure Web 應用程式的文件頁面](https://docs.microsoft.com/azure/app-service-web/)。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-108">toolearn more about how toocreate Azure Web App endpoints, visit hello [Azure Web Apps documentation page](https://docs.microsoft.com/azure/app-service-web/).</span></span> <span data-ttu-id="8bb5f-109">您可以加入任何端點具有 DNS 名稱，並可透過連線 hello 公用網際網路，我們使用 Azure Web 應用程式端點做為範例。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-109">You can add any endpoint that has a DNS name and is reachable over hello public internet and that we are using Azure Web Apps endpoints as an example.</span></span>

### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="8bb5f-110">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="8bb5f-110">Create a Traffic Manager profile</span></span>
1. <span data-ttu-id="8bb5f-111">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-111">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="8bb5f-112">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-112">If you don’t already have an account, you can sign-up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="8bb5f-113">在 hello**中樞**功能表上，按一下**新增** > **網路** > **查看所有**，按一下**流量管理員**設定檔 tooopen hello**建立 Traffic Manager 設定檔**刀鋒視窗中，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-113">On hello **Hub** menu, click **New** > **Networking** > **See all**, click **Traffic Manager** profile tooopen hello **Create Traffic Manager profile** blade, then click **Create**.</span></span>
3. <span data-ttu-id="8bb5f-114">在 hello**建立 Traffic Manager 設定檔**刀鋒視窗中，完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bb5f-114">On hello **Create Traffic Manager profile** blade, complete as follows:</span></span>
    1. <span data-ttu-id="8bb5f-115">在 [名稱]中，提供設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-115">In **Name**, provide a name for your profile.</span></span> <span data-ttu-id="8bb5f-116">此名稱必須 toobe hello trafficmanager.net 區域內的唯一和 hello DNS 名稱會導致<name>，也就是使用的 tooaccess trafficmanager.net 您的 Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-116">This name needs toobe unique within hello trafficmanager.net zone and results in hello DNS name <name>,trafficmanager.net which is used tooaccess your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="8bb5f-117">在**路由方法**，選取 hello**優先順序**路由方法。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-117">In **Routing method**, select hello **Priority** routing method.</span></span>
    3. <span data-ttu-id="8bb5f-118">在**訂用帳戶**，選取您想在此設定檔 toocreate hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8bb5f-118">In **Subscription**, select hello subscription you want toocreate this profile under</span></span>
    4. <span data-ttu-id="8bb5f-119">在**資源群組**，建立新的資源群組 tooplace 下的這個設定檔。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-119">In **Resource Group**, create a new resource group tooplace this profile under.</span></span>
    5. <span data-ttu-id="8bb5f-120">在**資源群組位置**，選取 hello hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-120">In **Resource group location**, select hello location of hello resource group.</span></span> <span data-ttu-id="8bb5f-121">此設定是指 toohello hello 資源群組、 位置及 hello 將全域部署的流量管理員設定檔沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-121">This setting refers toohello location of hello resource group, and has no impact on hello Traffic Manager profile that will be deployed globally.</span></span>
    6. <span data-ttu-id="8bb5f-122">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-122">Click **Create**.</span></span>
    7. <span data-ttu-id="8bb5f-123">Hello 全域部署，您的 Traffic Manager 設定檔完成時，它是個別資源群組中顯示為 hello 資源的其中一個。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-123">When hello global deployment of your Traffic Manager profile is complete, it is listed in respective resource group as one of hello resources.</span></span>

    ![建立流量管理員設定檔](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a><span data-ttu-id="8bb5f-125">新增流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="8bb5f-125">Add Traffic Manager endpoints</span></span>

1. <span data-ttu-id="8bb5f-126">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**在 hello hello 中前一節，然後按一下 hello 流量管理員設定檔中所建立的名稱會顯示該 hello。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-126">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you created in hello preceding section and click hello traffic manager profile in hello results that hello displayed.</span></span>
2. <span data-ttu-id="8bb5f-127">在 hello **Traffic Manager 設定檔**刀鋒視窗中的，在 hello**設定**區段中，按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-127">In hello **Traffic Manager profile** blade, in hello **Settings** section, click **Endpoints**.</span></span>
3. <span data-ttu-id="8bb5f-128">在 hello**端點**刀鋒視窗，其中會顯示按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-128">In hello **Endpoints** blade that is displayed, click **Add**.</span></span>
4. <span data-ttu-id="8bb5f-129">在 hello**加入端點**刀鋒視窗中，完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bb5f-129">In hello **Add endpoint** blade, complete as follows:</span></span>
    1. <span data-ttu-id="8bb5f-130">在 [類型] 中，按一下 [Azure 端點]。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-130">For **Type**, click **Azure endpoint**.</span></span>
    2. <span data-ttu-id="8bb5f-131">提供**名稱**要 toorecognize 此端點。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-131">Provide a **Name** by which you want toorecognize this endpoint.</span></span>
    3. <span data-ttu-id="8bb5f-132">在 [目標資源類型] 中，按一下 [App Service]。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-132">For **Target resource type**, click **App Service**.</span></span>
    4. <span data-ttu-id="8bb5f-133">如**目標資源**，按一下 **選擇 app service** tooshow hello 清單下 hello hello Web 應用程式的相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-133">For **Target resource**, click **Choose an app service** tooshow hello listing of hello Web Apps under hello same subscription.</span></span> <span data-ttu-id="8bb5f-134">在 hello**資源**刀鋒視窗，其中會顯示，挑選 hello 您想 tooadd，如 hello 第一個端點的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-134">In hello **Resource** blade that is displayed, pick hello App service that you want tooadd as hello first endpoint.</span></span>
    5. <span data-ttu-id="8bb5f-135">在 [優先順序] 中，選取 [1]。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-135">For **Priority**, select as **1**.</span></span> <span data-ttu-id="8bb5f-136">這會導致所有流量 toothis 端點是否狀況良好。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-136">This results in all traffic going toothis endpoint if it is healthy.</span></span>
    6. <span data-ttu-id="8bb5f-137">維持不勾選 [新增為已停用]。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-137">Keep **Add as disabled** unchecked.</span></span>
    7. <span data-ttu-id="8bb5f-138">按一下 [檔案] &gt; [新增] &gt; [專案] </span><span class="sxs-lookup"><span data-stu-id="8bb5f-138">Click **OK**</span></span>
5.  <span data-ttu-id="8bb5f-139">重複步驟 3 和 4 hello 下一個 Azure Web 應用程式端點。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-139">Repeat steps 3 and 4 for hello next Azure Web Apps endpoint.</span></span> <span data-ttu-id="8bb5f-140">請確定 tooadd 使用其**優先順序**在設定值**2**。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-140">Make sure tooadd it with its **Priority** value set at **2**.</span></span>
6.  <span data-ttu-id="8bb5f-141">這兩個端點的 hello 加法完成時，它們會顯示在 hello **Traffic Manager 設定檔**刀鋒視窗，以及其監視的狀態為**線上**。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-141">When hello addition of both endpoints is complete, they are displayed in hello **Traffic Manager profile** blade along with their monitoring status as **Online**.</span></span>

    ![新增流量管理員端點](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a><span data-ttu-id="8bb5f-143">使用 hello Traffic Manager 設定檔</span><span class="sxs-lookup"><span data-stu-id="8bb5f-143">Use hello Traffic Manager profile</span></span>
1.  <span data-ttu-id="8bb5f-144">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**在 hello 前面一節中所建立的名稱。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-144">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you created in hello preceding section.</span></span> <span data-ttu-id="8bb5f-145">在顯示 hello 結果中，按一下 hello 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-145">In hello results that are displayed, click hello traffic manager profile.</span></span>
2. <span data-ttu-id="8bb5f-146">在 hello **Traffic Manager 設定檔**刀鋒視窗中，按一下 **概觀**。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-146">In hello **Traffic Manager profile** blade, click **Overview**.</span></span>
3. <span data-ttu-id="8bb5f-147">hello **Traffic Manager 設定檔**刀鋒視窗會顯示 hello 您新建立的 Traffic Manager 設定檔的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-147">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="8bb5f-148">這可供任何用戶端 （例如，藉由瀏覽的網頁瀏覽器 tooit） 路由傳送 tooget toohello 右端點 hello 路由類型所決定。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-148">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="8bb5f-149">在此情況下，所有要求會路由的 toohello 第一個端點，並且如果 Traffic Manager 偵測到它處於狀況不良狀態，hello 流量自動容錯移轉 toohello 下一個端點。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-149">In this case, all requests are routed toohello first endpoint and if Traffic Manager detects it be unhealthy, hello traffic automatically fails over toohello next endpoint.</span></span>

## <a name="delete-hello-traffic-manager-profile"></a><span data-ttu-id="8bb5f-150">刪除 hello Traffic Manager 設定檔</span><span class="sxs-lookup"><span data-stu-id="8bb5f-150">Delete hello Traffic Manager profile</span></span>
<span data-ttu-id="8bb5f-151">當不再需要請刪除 hello 資源群組和您所建立的 hello Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-151">When no longer needed, delete hello resource group and hello Traffic Manager profile that you have created.</span></span> <span data-ttu-id="8bb5f-152">因此，從 hello 選取 hello 資源群組的 toodo **Traffic Manager 設定檔**刀鋒視窗，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-152">toodo so, select hello resource group from hello **Traffic Manager profile** blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bb5f-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8bb5f-153">Next steps</span></span>

- <span data-ttu-id="8bb5f-154">深入了解[路由類型](traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-154">Learn more about [routing types](traffic-manager-routing-methods.md).</span></span>
- <span data-ttu-id="8bb5f-155">深入了解端點類型[端點類型](traffic-manager-endpoint-types.md)。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-155">Learn more about endpoint types [endpoint types](traffic-manager-endpoint-types.md).</span></span>
- <span data-ttu-id="8bb5f-156">深入了解[端點監視](traffic-manager-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="8bb5f-156">Learn more about [endpoint monitoring](traffic-manager-monitoring.md).</span></span>



