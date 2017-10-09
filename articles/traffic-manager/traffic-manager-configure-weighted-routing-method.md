---
title: "aaaConfigure 加權循環流量路由方式，使用 Azure Traffic Manager |Microsoft 文件"
description: "這篇文章說明如何 tooload 平衡流量 Traffic Manager 中使用的循環配置資源方法"
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
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="60ef6-103">設定 Traffic Manager 中的 hello 加權流量路由方法</span><span class="sxs-lookup"><span data-stu-id="60ef6-103">Configure hello weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="60ef6-104">常見的流量路由方法模式是一組相同的端點，包括雲端服務和網站，並以循環配置資源方式傳送流量 tooeach tooprovide。</span><span class="sxs-lookup"><span data-stu-id="60ef6-104">A common traffic routing method pattern is tooprovide a set of identical endpoints, which include cloud services and websites, and send traffic tooeach in a round-robin fashion.</span></span> <span data-ttu-id="60ef6-105">hello 下列步驟概述如何 tooconfigure 這類型的流量路由方法。</span><span class="sxs-lookup"><span data-stu-id="60ef6-105">hello following steps outline how tooconfigure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="60ef6-106">Azure 網站已為資料中心 (也稱為「區域」) 內的網站提供循環配置資源負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="60ef6-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="60ef6-107">Traffic Manager 可讓您網站的 toospecify 循環配置資源的流量路由方法不同資料中心內。</span><span class="sxs-lookup"><span data-stu-id="60ef6-107">Traffic Manager allows you toospecify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a><span data-ttu-id="60ef6-108">tooconfigure hello 加權流量路由方法</span><span class="sxs-lookup"><span data-stu-id="60ef6-108">tooconfigure hello weighted traffic routing method</span></span>

1. <span data-ttu-id="60ef6-109">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="60ef6-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="60ef6-110">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="60ef6-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="60ef6-111">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**，然後按一下您想要針對 tooconfigure hello 路由方法的 hello 設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="60ef6-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="60ef6-112">在 hello **Traffic Manager 設定檔**刀鋒視窗中，確認同時 hello 雲端服務，且您想 tooinclude 組態中的網站都存在。</span><span class="sxs-lookup"><span data-stu-id="60ef6-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="60ef6-113">在 hello**設定**區段中，按一下**組態**，在 hello**組態**刀鋒視窗中，完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="60ef6-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="60ef6-114">如**流量路由方法設定**，確認 hello 流量路由方式**加權**。</span><span class="sxs-lookup"><span data-stu-id="60ef6-114">For **traffic routing method settings**, verify that hello traffic routing method is **Weighted**.</span></span> <span data-ttu-id="60ef6-115">如果沒有，請按一下**加權**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="60ef6-115">If it is not, click **Weighted** from hello dropdown list.</span></span>
    2. <span data-ttu-id="60ef6-116">設定 hello**端點監視設定**所有的每個端點，如下所示的此設定檔內相同：</span><span class="sxs-lookup"><span data-stu-id="60ef6-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="60ef6-117">選取適當的 hello**通訊協定**，並指定 hello**連接埠**數目。</span><span class="sxs-lookup"><span data-stu-id="60ef6-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="60ef6-118">針對 [路徑]，輸入正斜線 */*。</span><span class="sxs-lookup"><span data-stu-id="60ef6-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="60ef6-119">toomonitor 端點，您必須指定路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="60ef6-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="60ef6-120">A 正斜線"/"hello 相對路徑是有效的項目，表示該 hello 檔案位於 hello 根目錄 （預設值） 中。</span><span class="sxs-lookup"><span data-stu-id="60ef6-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="60ef6-121">在 hello hello 頁面頂端，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="60ef6-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="60ef6-122">測試 hello 變更您的組態，如下所示：</span><span class="sxs-lookup"><span data-stu-id="60ef6-122">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="60ef6-123">在 hello 入口網站搜尋列中，搜尋 hello Traffic Manager 設定檔名稱，然後按一下 hello Traffic Manager 設定檔在 hello 結果中的顯示該 hello。</span><span class="sxs-lookup"><span data-stu-id="60ef6-123">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="60ef6-124">在 [hello **Traffic Manager**設定檔] 刀鋒視窗，請按一下**概觀**。</span><span class="sxs-lookup"><span data-stu-id="60ef6-124">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="60ef6-125">hello **Traffic Manager 設定檔**刀鋒視窗會顯示 hello 您新建立的 Traffic Manager 設定檔的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="60ef6-125">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="60ef6-126">這可供任何用戶端 （例如，藉由瀏覽的網頁瀏覽器 tooit） 路由傳送 tooget toohello 右端點 hello 路由類型所決定。</span><span class="sxs-lookup"><span data-stu-id="60ef6-126">This can be used by any clients (for example,by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="60ef6-127">在此情況下，所有要求都會以循環配置資源方式路由到每個端點。</span><span class="sxs-lookup"><span data-stu-id="60ef6-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="60ef6-128">一旦您的 Traffic Manager 設定檔運作正常，編輯 hello DNS 記錄，在您的授權 DNS 伺服器 toopoint 您公司網域名稱 toohello Traffic Manager 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="60ef6-128">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![使用流量管理員設定加權流量路由方法][1]

## <a name="next-steps"></a><span data-ttu-id="60ef6-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60ef6-130">Next steps</span></span>

- <span data-ttu-id="60ef6-131">深入了解[優先順序流量路由方法](traffic-manager-configure-priority-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="60ef6-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="60ef6-132">深入了解[效能流量路由方法](traffic-manager-configure-performance-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="60ef6-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="60ef6-133">深入了解[地理路由方法](traffic-manager-configure-geographic-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="60ef6-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="60ef6-134">了解如何太[測試 Traffic Manager 設定](traffic-manager-testing-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="60ef6-134">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
