---
title: "管理 Azure 流量管理員設定檔 | Microsoft Docs"
description: "本文會協助您建立、停用、啟用及刪除 Azure 流量管理員設定檔。"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: a5164282264124835692bc72a4ab61891aa7af9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a><span data-ttu-id="22c17-103">管理 Azure 流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="22c17-103">Manage an Azure Traffic Manager profile</span></span>

<span data-ttu-id="22c17-104">流量管理員設定檔會使用流量路由方法來控制分散到您雲端服務或網站端點的流量。</span><span class="sxs-lookup"><span data-stu-id="22c17-104">Traffic Manager profiles use traffic-routing methods to control the distribution of traffic to your cloud services or website endpoints.</span></span> <span data-ttu-id="22c17-105">本文說明如何建立及管理這些設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-105">This article explains how to create and manage these profiles.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="22c17-106">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="22c17-106">Create a Traffic Manager profile</span></span>

<span data-ttu-id="22c17-107">您可以使用 Azure 入口網站來建立流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-107">You can create a Traffic Manager profile by using the Azure portal.</span></span> <span data-ttu-id="22c17-108">建立設定檔之後，您就可以在 Azure 入口網站中設定端點、監視及其他設定。</span><span class="sxs-lookup"><span data-stu-id="22c17-108">After creating your profile, you can configure endpoints, monitoring, and other settings in the Azure portal.</span></span> <span data-ttu-id="22c17-109">流量管理員每個設定檔最多支援 200 個端點。</span><span class="sxs-lookup"><span data-stu-id="22c17-109">Traffic Manager supports up to 200 endpoints per profile.</span></span> <span data-ttu-id="22c17-110">不過，大部分的使用案例僅需要少量的端點。</span><span class="sxs-lookup"><span data-stu-id="22c17-110">However, most usage scenarios require only a few of endpoints.</span></span>

### <a name="to-create-a-traffic-manager-profile"></a><span data-ttu-id="22c17-111">若要建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="22c17-111">To create a Traffic Manager profile</span></span>

1. <span data-ttu-id="22c17-112">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="22c17-112">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="22c17-113">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="22c17-113">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="22c17-114">在 [中樞] 功能表中，按一下 [新增] > [網路] > [查看全部]**，然後按一下 [流量管理員]****設定檔，以開啟 [建立流量管理員設定檔]** 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="22c17-114">On the **Hub** menu, click **New** > **Networking** > **See all**, click **Traffic Manager** profile to open the **Create Traffic Manager profile** blade, then click **Create**.</span></span>
3. <span data-ttu-id="22c17-115">在 [建立流量管理員設定檔] 刀鋒視窗上，如下所示操作：</span><span class="sxs-lookup"><span data-stu-id="22c17-115">On the **Create Traffic Manager profile** blade, complete as follows:</span></span>
    1. <span data-ttu-id="22c17-116">在 [名稱]中，提供設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="22c17-116">In **Name**, provide a name for your profile.</span></span> <span data-ttu-id="22c17-117">此名稱在 trafficmanager.net 區域內必須是唯一的，而且會產生 DNS 名稱 <name>, trafficmanager.net，用以存取您的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-117">This name needs to be unique within the trafficmanager.net zone and results in the DNS name <name>, trafficmanager.net, that is used to access your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="22c17-118">在 [路由方法] 中，選取 [優先順序]路由方法。</span><span class="sxs-lookup"><span data-stu-id="22c17-118">In **Routing method**, select the **Priority** routing method.</span></span>
    3. <span data-ttu-id="22c17-119">在 [訂用帳戶] 中，選取您要用來建立此設定檔的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="22c17-119">In **Subscription**, select the subscription you want to create this profile under</span></span>
    4. <span data-ttu-id="22c17-120">在 [資源群組]中，建立新的資源群組來放置此設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-120">In **Resource Group**, create a new resource group to place this profile under.</span></span>
    5. <span data-ttu-id="22c17-121">在 [資源群組位置] 中，選取資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="22c17-121">In **Resource group location**, select the location of the resource group.</span></span> <span data-ttu-id="22c17-122">這項設定是指資源群組的位置，完全不影響將部署到全球的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-122">This setting refers to the location of the resource group, and has no impact on the Traffic Manager profile that will be deployed globally.</span></span>
    6. <span data-ttu-id="22c17-123">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="22c17-123">Click **Create**.</span></span>
    7. <span data-ttu-id="22c17-124">當流量管理員設定檔的全球部署完成時，它會列為個別資源群組的其中一個資源。</span><span class="sxs-lookup"><span data-stu-id="22c17-124">When the global deployment of your Traffic Manager profile is complete, it is listed in respective resource group as one of the resources.</span></span>

## <a name="disable-enable-or-delete-a-profile"></a><span data-ttu-id="22c17-125">停用、啟用或刪除設定檔</span><span class="sxs-lookup"><span data-stu-id="22c17-125">Disable, enable, or delete a profile</span></span>

<span data-ttu-id="22c17-126">您可以停用現有的設定檔，流量管理員就不會將使用者要求轉介到設定的端點。</span><span class="sxs-lookup"><span data-stu-id="22c17-126">You can disable an existing profile so that Traffic Manager does not refer user requests to the configured endpoints.</span></span> <span data-ttu-id="22c17-127">當您停用流量管理員設定檔時，設定檔和設定檔內含的資訊將保持不變，而且可在流量管理員介面中進行編輯。</span><span class="sxs-lookup"><span data-stu-id="22c17-127">When you disable a Traffic Manager profile, the profile and the information contained in the profile remain intact and can be edited in the Traffic Manager interface.</span></span>  <span data-ttu-id="22c17-128">當您重新啟用設定檔時，就會繼續轉介。</span><span class="sxs-lookup"><span data-stu-id="22c17-128">Referrals resume when you re-enable the profile.</span></span> <span data-ttu-id="22c17-129">當您在 Azure 入口網站中建立流量管理員設定檔時，它會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="22c17-129">When you create a Traffic Manager profile in the Azure portal, it's automatically enabled.</span></span> <span data-ttu-id="22c17-130">如果您決定不再需要某個設定檔，可以將它刪除。</span><span class="sxs-lookup"><span data-stu-id="22c17-130">If you decide a profile is no longer necessary, you can delete it.</span></span>

### <a name="to-disable-a-profile"></a><span data-ttu-id="22c17-131">停用設定檔</span><span class="sxs-lookup"><span data-stu-id="22c17-131">To disable a profile</span></span>

1. <span data-ttu-id="22c17-132">如果您使用的是自訂網域名稱，則變更網際網路 DNS 伺服器上的 CNAME 記錄，它就不會再指向流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-132">If you are using a custom domain name, change the CNAME record on your Internet DNS server so that it no longer points to your Traffic Manager profile.</span></span>
2. <span data-ttu-id="22c17-133">流量會停止導向至透過流量管理員設定檔設定的端點。</span><span class="sxs-lookup"><span data-stu-id="22c17-133">Traffic stops being directed to the endpoints through the Traffic Manager profile settings.</span></span>
3. <span data-ttu-id="22c17-134">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="22c17-134">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="22c17-135">在入口網站的搜尋列中，搜尋您想要修改的**流量管理員設定檔**名稱，然後按一下結果中顯示的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-135">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span></span>
3. <span data-ttu-id="22c17-136">在 [流量管理員設定檔] 刀鋒視窗中，按一下 [概觀]，在 [概觀] 刀鋒視窗中按一下 [停用]，然後確認停用流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-136">In the **Traffic Manager profile** blade, click **Overview**, in the Overview blade click **Disable**, and then confirm to disable the Traffic Manager profile.</span></span>

### <a name="to-enable-a-profile"></a><span data-ttu-id="22c17-137">啟用設定檔</span><span class="sxs-lookup"><span data-stu-id="22c17-137">To enable a profile</span></span>

1. <span data-ttu-id="22c17-138">從瀏覽器登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="22c17-138">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="22c17-139">在入口網站的搜尋列中，搜尋您想要修改的**流量管理員設定檔**名稱，然後按一下結果中顯示的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-139">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span></span>
3. <span data-ttu-id="22c17-140">在 [流量管理員設定檔] 刀鋒視窗中，按一下 [概觀]，然後在 [概觀] 刀鋒視窗中按一下 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="22c17-140">In the **Traffic Manager profile** blade, click **Overview**, and then in the Overview blade click **Enable**.</span></span>
5. <span data-ttu-id="22c17-141">如果您使用的是自訂網域名稱，請在網際網路 DNS 伺服器上建立 CNAME 資源記錄，以指向流量管理員設定檔的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="22c17-141">If you are using a custom domain name, create a CNAME resource record on your Internet DNS server to point to the domain name of your Traffic Manager profile.</span></span>
6. <span data-ttu-id="22c17-142">流量會再次導向至各端點。</span><span class="sxs-lookup"><span data-stu-id="22c17-142">Traffic is directed to the endpoints again.</span></span>

### <a name="to-delete-a-profile"></a><span data-ttu-id="22c17-143">刪除設定檔</span><span class="sxs-lookup"><span data-stu-id="22c17-143">To delete a profile</span></span>

1. <span data-ttu-id="22c17-144">請確定網際網路 DNS 伺服器上的 DNS 資源記錄所使用的 CNAME 資源記錄，不再指向流量管理員設定檔的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="22c17-144">Ensure that the DNS resource record on your Internet DNS server no longer uses a CNAME resource record that points to the domain name of your Traffic Manager profile.</span></span>
2. <span data-ttu-id="22c17-145">在入口網站的搜尋列中，搜尋您想要修改的**流量管理員設定檔**名稱，然後按一下結果中顯示的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-145">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span></span>
3. <span data-ttu-id="22c17-146">在 [流量管理員設定檔] 刀鋒視窗中，按一下 [概觀]，在 [概觀] 刀鋒視窗中按一下 [刪除]，然後確認刪除流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="22c17-146">In the **Traffic Manager profile** blade, click **Overview**, in the Overview blade click **Delete**, and then confirm to delete the Traffic Manager profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22c17-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22c17-147">Next steps</span></span>

* [<span data-ttu-id="22c17-148">新增端點。</span><span class="sxs-lookup"><span data-stu-id="22c17-148">Add an endpoint</span></span>](traffic-manager-endpoints.md)
* [<span data-ttu-id="22c17-149">設定優先順序路由方法</span><span class="sxs-lookup"><span data-stu-id="22c17-149">Configure Priority routing method</span></span>](traffic-manager-configure-priority-routing-method.md)
* [<span data-ttu-id="22c17-150">設定地理路由方法</span><span class="sxs-lookup"><span data-stu-id="22c17-150">Configure Geographic routing method</span></span>](traffic-manager-configure-geographic-routing-method.md) 
* [<span data-ttu-id="22c17-151">設定加權路由方法</span><span class="sxs-lookup"><span data-stu-id="22c17-151">Configure Weighted routing method</span></span>](traffic-manager-configure-weighted-routing-method.md)
* [<span data-ttu-id="22c17-152">設定效能路由方法</span><span class="sxs-lookup"><span data-stu-id="22c17-152">Configure Performance routing method</span></span>](traffic-manager-configure-performance-routing-method.md)
