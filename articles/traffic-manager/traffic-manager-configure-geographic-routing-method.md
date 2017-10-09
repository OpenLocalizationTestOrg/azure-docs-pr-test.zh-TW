---
title: "地理 aaaConfigure 流量路由方式，使用 Azure Traffic Manager |Microsoft 文件"
description: "這篇文章說明如何 tooconfigure hello 地理流量路由方式使用 Azure Traffic Manager"
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
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a><span data-ttu-id="2c1f8-103">設定使用 Traffic Manager hello 地理流量路由方法</span><span class="sxs-lookup"><span data-stu-id="2c1f8-103">Configure hello geographic traffic routing method using Traffic Manager</span></span>

<span data-ttu-id="2c1f8-104">hello 地理流量路由方法可讓您 toodirect 流量 toospecific hello hello 要求產生的位置的地理位置為基礎的端點。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-104">hello Geographic traffic routing method allows you toodirect traffic toospecific endpoints based on hello geographic location where hello requests originate.</span></span> <span data-ttu-id="2c1f8-105">本教學課程示範如何 toocreate Traffic Manager 設定檔與此路由的方法，並設定 hello 端點 tooreceive 流量從特定地理位置。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-105">This tutorial shows you how toocreate a Traffic Manager profile with this routing method and configure hello endpoints tooreceive traffic from specific geographies.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="2c1f8-106">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="2c1f8-106">Create a Traffic Manager Profile</span></span>

1. <span data-ttu-id="2c1f8-107">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-107">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="2c1f8-108">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-108">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span>
2. <span data-ttu-id="2c1f8-109">在 hello 中樞功能表中，按一下 **新增** > **網路** > **查看所有**，然後按一下 **Traffic Manager 設定檔**tooopen hello**建立 Traffic Manager 設定檔**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-109">On hello Hub menu, click **New** > **Networking** > **See all**, and then click **Traffic Manager profile** tooopen hello **Create Traffic Manager profile** blade.</span></span>
3. <span data-ttu-id="2c1f8-110">在 hello**建立 Traffic Manager 設定檔**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="2c1f8-110">On hello **Create Traffic Manager profile** blade:</span></span>
    1. <span data-ttu-id="2c1f8-111">提供設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-111">Provide a name for your profile.</span></span> <span data-ttu-id="2c1f8-112">此名稱必須 toobe hello trafficmanager.net 區域內的唯一，而且會導致 hello DNS 名稱<profilename>，trafficmanager.net 將會使用的 tooaccess 您的 Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-112">This name needs toobe unique within hello trafficmanager.net zone and will result in hello DNS name <profilename>,trafficmanager.net which will be used tooaccess your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="2c1f8-113">選取 hello**地理**路由方法。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-113">Select hello **Geographic** routing method.</span></span>
    3. <span data-ttu-id="2c1f8-114">選取您想在此設定檔 toocreate hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-114">Select hello subscription you want toocreate this profile under.</span></span>
    4. <span data-ttu-id="2c1f8-115">使用現有的資源群組或建立新的資源群組 tooplace 底下的這個設定檔。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-115">Use an existing resource group or create a new resource group tooplace this profile under.</span></span> <span data-ttu-id="2c1f8-116">如果您選擇 toocreate 新的資源群組，使用 hello**資源群組位置**hello 資源群組的下拉式清單中 toospecify hello 位置。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-116">If you choose toocreate a new resource group, use hello **Resource Group location** dropdown toospecify hello location of hello resource group.</span></span> <span data-ttu-id="2c1f8-117">此設定是指 toohello hello 資源群組、 位置及 hello 將全域部署的 Traffic Manager 設定檔沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-117">This setting refers toohello location of hello resource group, and has no impact on hello Traffic Manager profile which will be deployed globally.</span></span>
    5. <span data-ttu-id="2c1f8-118">按一下 [建立] 之後，就會建立流量管理員設定檔並部署到全球。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-118">After you click **Create**, your Traffic Manager profile is created and deployed globally.</span></span>

![建立流量管理員設定檔](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a><span data-ttu-id="2c1f8-120">新增端點</span><span class="sxs-lookup"><span data-stu-id="2c1f8-120">Add endpoints</span></span>

1. <span data-ttu-id="2c1f8-121">搜尋您剛才建立 hello 入口網站的 [搜尋] 列中的 hello Traffic Manager 設定檔名稱，其顯示時按一下 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-121">Search for hello Traffic Manager profile name you just created in hello portal’s search bar and click on hello result when it is shown.</span></span>
2. <span data-ttu-id="2c1f8-122">瀏覽過**設定** -> **端點**hello Traffic Manager 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-122">Navigate too**Settings** -> **Endpoints** in hello Traffic Manager blade.</span></span>
3. <span data-ttu-id="2c1f8-123">按一下**新增**tooshow hello**加入端點**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-123">Click **Add** tooshow hello **Add Endpoint** blade.</span></span>
3. <span data-ttu-id="2c1f8-124">在 hello**端點**刀鋒視窗中，按一下**新增**在 hello**加入端點**刀鋒視窗，其中會顯示完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2c1f8-124">In hello **Endpoints** blade, click **Add** and in hello **Add endpoint** blade that is displayed, complete as follows:</span></span>
4. <span data-ttu-id="2c1f8-125">選取**類型**取決於您要加入的端點的 hello 型別而定。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-125">Select **Type** depending upon hello type of endpoint you are adding.</span></span> <span data-ttu-id="2c1f8-126">針對生產環境中使用的地理路由設定檔，我們強烈建議使用巢狀端點類型，而且包含的子設定檔中有多個端點。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-126">For geographic routing profiles used in production, we strongly recommend using nested endpoint types containing a child profile with more than one endpoint.</span></span> <span data-ttu-id="2c1f8-127">如需詳細資訊，請參閱[地理流量路由方法的常見問題集](traffic-manager-FAQs.md)。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-127">For more details, see [FAQs about geographic traffic routing methods](traffic-manager-FAQs.md).</span></span>
5. <span data-ttu-id="2c1f8-128">提供**名稱**要 toorecognize 此端點。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-128">Provide a **Name** by which you want toorecognize this endpoint.</span></span>
6. <span data-ttu-id="2c1f8-129">此刀鋒視窗中的某些欄位，取決於您要加入的端點 hello 類型：</span><span class="sxs-lookup"><span data-stu-id="2c1f8-129">Certain fields in this blade depend on hello type of endpoint you are adding:</span></span>
    1. <span data-ttu-id="2c1f8-130">如果您要新增的 Azure 端點，請選取 hello**目標資源類型**和 hello**目標**hello 資源為基礎您想讓 toodirect 流量</span><span class="sxs-lookup"><span data-stu-id="2c1f8-130">If you are adding an Azure endpoint, select hello **Target resource type** and hello **Target** based on hello resource you want toodirect traffic to</span></span>
    2. <span data-ttu-id="2c1f8-131">如果您要新增**外部**端點，提供 hello**完整網域名稱 (FQDN)**端點。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-131">If you are adding an **External** endpoint, provide hello **Fully-qualified domain name (FQDN)** for your endpoint.</span></span>
    3. <span data-ttu-id="2c1f8-132">如果您要新增**巢狀端點**，選取 hello**目標資源**對應 toohello 子系設定檔 toouse 並指定 hello**最少子端點計數**.</span><span class="sxs-lookup"><span data-stu-id="2c1f8-132">If you are adding a **Nested endpoint**, select hello **Target resource** that corresponds toohello child profile you want toouse and specify hello **Minimum child endpoints count**.</span></span>
7. <span data-ttu-id="2c1f8-133">Hello 地理對應區段中，使用 hello 下拉式功能表中與您想要的流量傳送 toobe toothis 端點 tooadd hello 區域。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-133">In hello Geo-mapping section, use hello drop down tooadd hello regions from where you want traffic toobe sent toothis endpoint.</span></span> <span data-ttu-id="2c1f8-134">您必須新增至少一個區域，而且可以對應多個區域。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-134">You must add at least one region, and you can have multiple regions mapped.</span></span>
8. <span data-ttu-id="2c1f8-135">重複此步驟之所有端點您想要在此設定檔之下 tooadd</span><span class="sxs-lookup"><span data-stu-id="2c1f8-135">Repeat this for all endpoints you want tooadd under this profile</span></span>

![新增流量管理員端點](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a><span data-ttu-id="2c1f8-137">使用 hello Traffic Manager 設定檔</span><span class="sxs-lookup"><span data-stu-id="2c1f8-137">Use hello Traffic Manager profile</span></span>
1.  <span data-ttu-id="2c1f8-138">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**名稱在 hello 前面一節中所建立，並按一下 hello 中的 hello 流量管理員設定檔結果顯示該 hello。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-138">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you created in hello preceding section and click on hello traffic manager profile in hello results that hello displayed.</span></span>
2. <span data-ttu-id="2c1f8-139">在 hello **Traffic Manager 設定檔**刀鋒視窗中，按一下 **概觀**。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-139">In hello **Traffic Manager profile** blade, click **Overview**.</span></span>
3. <span data-ttu-id="2c1f8-140">hello **Traffic Manager 設定檔**刀鋒視窗會顯示 hello 您新建立的 Traffic Manager 設定檔的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-140">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="2c1f8-141">這可供任何用戶端 （例如，藉由瀏覽的網頁瀏覽器 tooit） 路由傳送 tooget toohello 右端點 hello 路由類型所決定。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-141">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span>  <span data-ttu-id="2c1f8-142">在地理路由的 hello 情況下，Traffic Manager 會查看 hello 連入要求的 hello 來源 IP，並判斷它從中產生 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-142">In hello case of geographic routing, Traffic Manager looks at hello source IP of hello incoming request and determines hello region from which it is originating.</span></span> <span data-ttu-id="2c1f8-143">如果該地區對應的 tooan 端點，則流量是路由的 toothere。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-143">If that region is mapped tooan endpoint, traffic is routed toothere.</span></span> <span data-ttu-id="2c1f8-144">如果此區域不是對應的 tooan 端點，Traffic Manager 會傳回為 NODATA 查詢回應。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-144">If this region is not mapped tooan endpoint, then Traffic Manager returns a NODATA query response.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c1f8-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c1f8-145">Next steps</span></span>

- <span data-ttu-id="2c1f8-146">深入了解[地理流量路由方法](traffic-manager-routing-methods.md#geographic)。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-146">Learn more about [Geographic traffic routing method](traffic-manager-routing-methods.md#geographic).</span></span>
- <span data-ttu-id="2c1f8-147">了解如何太[測試 Traffic Manager 設定](traffic-manager-testing-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="2c1f8-147">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>
