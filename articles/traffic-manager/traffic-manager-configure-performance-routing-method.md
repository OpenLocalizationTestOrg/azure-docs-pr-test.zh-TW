---
title: "aaaConfigure 效能流量路由方式，使用 Azure Traffic Manager |Microsoft 文件"
description: "這篇文章說明如何 tooconfigure Traffic Manager tooroute 具有最低延遲的流量 toohello 端點"
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a><span data-ttu-id="b96fb-103">設定 hello 效能流量路由方法</span><span class="sxs-lookup"><span data-stu-id="b96fb-103">Configure hello performance traffic routing method</span></span>

<span data-ttu-id="b96fb-104">hello 效能 」 流量路由方法可讓您 toodirect 流量 toohello 端點與 hello 與 hello 用戶端的網路延遲最低。</span><span class="sxs-lookup"><span data-stu-id="b96fb-104">hello Performance traffic routing method allows you toodirect traffic toohello endpoint with hello lowest latency from hello client's network.</span></span> <span data-ttu-id="b96fb-105">一般而言，hello 與 hello 最低延遲的資料中心是地理距離最接近的 hello。</span><span class="sxs-lookup"><span data-stu-id="b96fb-105">Typically, hello datacenter with hello lowest latency is hello closest in geographic distance.</span></span> <span data-ttu-id="b96fb-106">此流量路由方法無法考慮到網路組態或負載的即時變更。</span><span class="sxs-lookup"><span data-stu-id="b96fb-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="tooconfigure-performance-routing-method"></a><span data-ttu-id="b96fb-107">tooconfigure 效能路由方法</span><span class="sxs-lookup"><span data-stu-id="b96fb-107">tooconfigure performance routing method</span></span>

1. <span data-ttu-id="b96fb-108">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b96fb-108">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="b96fb-109">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="b96fb-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="b96fb-110">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**，然後按一下您想要針對 tooconfigure hello 路由方法的 hello 設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="b96fb-110">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="b96fb-111">在 hello **Traffic Manager 設定檔**刀鋒視窗中，確認同時 hello 雲端服務，且您想 tooinclude 組態中的網站都存在。</span><span class="sxs-lookup"><span data-stu-id="b96fb-111">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="b96fb-112">在 hello**設定**區段中，按一下**組態**，在 hello**組態**刀鋒視窗中，完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b96fb-112">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="b96fb-113">在 [流量路由方法設定] 中，針對 [路由方法] 選取 [效能]。</span><span class="sxs-lookup"><span data-stu-id="b96fb-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="b96fb-114">設定 hello**端點監視設定**所有的每個端點，如下所示的此設定檔內相同：</span><span class="sxs-lookup"><span data-stu-id="b96fb-114">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="b96fb-115">選取適當的 hello**通訊協定**，並指定 hello**連接埠**數目。</span><span class="sxs-lookup"><span data-stu-id="b96fb-115">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="b96fb-116">針對 [路徑]，輸入正斜線 */*。</span><span class="sxs-lookup"><span data-stu-id="b96fb-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="b96fb-117">toomonitor 端點，您必須指定路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="b96fb-117">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="b96fb-118">A 正斜線"/"hello 相對路徑是有效的項目，表示該 hello 檔案位於 hello 根目錄 （預設值） 中。</span><span class="sxs-lookup"><span data-stu-id="b96fb-118">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="b96fb-119">在 hello hello 頁面頂端，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="b96fb-119">At hello top of hello page, click **Save**.</span></span>
5.  <span data-ttu-id="b96fb-120">測試 hello 變更您的組態，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b96fb-120">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="b96fb-121">在 hello 入口網站搜尋列中，搜尋 hello Traffic Manager 設定檔名稱，然後按一下 hello Traffic Manager 設定檔在 hello 結果中的顯示該 hello。</span><span class="sxs-lookup"><span data-stu-id="b96fb-121">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="b96fb-122">在 [hello **Traffic Manager**設定檔] 刀鋒視窗，請按一下**概觀**。</span><span class="sxs-lookup"><span data-stu-id="b96fb-122">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="b96fb-123">hello **Traffic Manager 設定檔**刀鋒視窗會顯示 hello 您新建立的 Traffic Manager 設定檔的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="b96fb-123">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="b96fb-124">這可供任何用戶端 （例如，藉由瀏覽的網頁瀏覽器 tooit） 路由傳送 tooget toohello 右端點 hello 路由類型所決定。</span><span class="sxs-lookup"><span data-stu-id="b96fb-124">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="b96fb-125">在此情況下的所有要求都都具有 hello 與 hello 用戶端的網路延遲最低的路由的 toohello 端點。</span><span class="sxs-lookup"><span data-stu-id="b96fb-125">In this case all requests are routed toohello endpoint with hello lowest latency from hello client's network.</span></span>
6. <span data-ttu-id="b96fb-126">一旦您的 Traffic Manager 設定檔運作正常，編輯 hello DNS 記錄，在您的授權 DNS 伺服器 toopoint 您公司網域名稱 toohello Traffic Manager 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="b96fb-126">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![使用流量管理員設定效能流量路由方法][1]

## <a name="next-steps"></a><span data-ttu-id="b96fb-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b96fb-128">Next steps</span></span>

- <span data-ttu-id="b96fb-129">深入了解[加權流量路由方法](traffic-manager-configure-weighted-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="b96fb-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="b96fb-130">深入了解[優先順序路由方法](traffic-manager-configure-priority-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="b96fb-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="b96fb-131">深入了解[地理路由方法](traffic-manager-configure-geographic-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="b96fb-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="b96fb-132">了解如何太[測試 Traffic Manager 設定](traffic-manager-testing-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="b96fb-132">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png