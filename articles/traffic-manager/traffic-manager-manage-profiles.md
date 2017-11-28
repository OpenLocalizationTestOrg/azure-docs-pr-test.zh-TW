---
title: "aaaManage Azure Traffic Manager 設定檔 |Microsoft 文件"
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
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a><span data-ttu-id="f65a6-103">管理 Azure 流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="f65a6-103">Manage an Azure Traffic Manager profile</span></span>

<span data-ttu-id="f65a6-104">Traffic Manager 設定檔使用流量 tooyour 雲端服務或網站端點的流量路由方法 toocontrol hello 分佈。</span><span class="sxs-lookup"><span data-stu-id="f65a6-104">Traffic Manager profiles use traffic-routing methods toocontrol hello distribution of traffic tooyour cloud services or website endpoints.</span></span> <span data-ttu-id="f65a6-105">這篇文章說明如何 toocreate 和管理這些設定檔。</span><span class="sxs-lookup"><span data-stu-id="f65a6-105">This article explains how toocreate and manage these profiles.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="f65a6-106">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="f65a6-106">Create a Traffic Manager profile</span></span>

<span data-ttu-id="f65a6-107">您可以使用 hello Azure 入口網站來建立流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="f65a6-107">You can create a Traffic Manager profile by using hello Azure portal.</span></span> <span data-ttu-id="f65a6-108">建立您的設定檔之後, 您可以在 hello Azure 入口網站中設定端點、 監視和其他設定。</span><span class="sxs-lookup"><span data-stu-id="f65a6-108">After creating your profile, you can configure endpoints, monitoring, and other settings in hello Azure portal.</span></span> <span data-ttu-id="f65a6-109">Traffic Manager 支援個 too200 端點，每個設定檔。</span><span class="sxs-lookup"><span data-stu-id="f65a6-109">Traffic Manager supports up too200 endpoints per profile.</span></span> <span data-ttu-id="f65a6-110">不過，大部分的使用案例僅需要少量的端點。</span><span class="sxs-lookup"><span data-stu-id="f65a6-110">However, most usage scenarios require only a few of endpoints.</span></span>

### <a name="toocreate-a-traffic-manager-profile"></a><span data-ttu-id="f65a6-111">toocreate Traffic Manager 設定檔</span><span class="sxs-lookup"><span data-stu-id="f65a6-111">toocreate a Traffic Manager profile</span></span>

1. <span data-ttu-id="f65a6-112">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f65a6-112">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="f65a6-113">如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="f65a6-113">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="f65a6-114">在 hello**中樞**功能表上，按一下**新增** > **網路** > **查看所有**，按一下**流量管理員**設定檔 tooopen hello**建立 Traffic Manager 設定檔**刀鋒視窗中，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="f65a6-114">On hello **Hub** menu, click **New** > **Networking** > **See all**, click **Traffic Manager** profile tooopen hello **Create Traffic Manager profile** blade, then click **Create**.</span></span>
3. <span data-ttu-id="f65a6-115">在 hello**建立 Traffic Manager 設定檔**刀鋒視窗中，完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f65a6-115">On hello **Create Traffic Manager profile** blade, complete as follows:</span></span>
    1. <span data-ttu-id="f65a6-116">在 [名稱]中，提供設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="f65a6-116">In **Name**, provide a name for your profile.</span></span> <span data-ttu-id="f65a6-117">此名稱必須 toobe hello trafficmanager.net 區域內的唯一和 hello DNS 名稱會導致<name>，trafficmanager.net 所使用的 tooaccess 您的 Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="f65a6-117">This name needs toobe unique within hello trafficmanager.net zone and results in hello DNS name <name>, trafficmanager.net, that is used tooaccess your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="f65a6-118">在**路由方法**，選取 hello**優先順序**路由方法。</span><span class="sxs-lookup"><span data-stu-id="f65a6-118">In **Routing method**, select hello **Priority** routing method.</span></span>
    3. <span data-ttu-id="f65a6-119">在**訂用帳戶**，選取您想在此設定檔 toocreate hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f65a6-119">In **Subscription**, select hello subscription you want toocreate this profile under</span></span>
    4. <span data-ttu-id="f65a6-120">在**資源群組**，建立新的資源群組 tooplace 下的這個設定檔。</span><span class="sxs-lookup"><span data-stu-id="f65a6-120">In **Resource Group**, create a new resource group tooplace this profile under.</span></span>
    5. <span data-ttu-id="f65a6-121">在**資源群組位置**，選取 hello hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="f65a6-121">In **Resource group location**, select hello location of hello resource group.</span></span> <span data-ttu-id="f65a6-122">此設定是指 toohello hello 資源群組、 位置及 hello 將全域部署的流量管理員設定檔沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="f65a6-122">This setting refers toohello location of hello resource group, and has no impact on hello Traffic Manager profile that will be deployed globally.</span></span>
    6. <span data-ttu-id="f65a6-123">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f65a6-123">Click **Create**.</span></span>
    7. <span data-ttu-id="f65a6-124">Hello 全域部署，您的 Traffic Manager 設定檔完成時，它是個別資源群組中顯示為 hello 資源的其中一個。</span><span class="sxs-lookup"><span data-stu-id="f65a6-124">When hello global deployment of your Traffic Manager profile is complete, it is listed in respective resource group as one of hello resources.</span></span>

## <a name="disable-enable-or-delete-a-profile"></a><span data-ttu-id="f65a6-125">停用、啟用或刪除設定檔</span><span class="sxs-lookup"><span data-stu-id="f65a6-125">Disable, enable, or delete a profile</span></span>

<span data-ttu-id="f65a6-126">您可以停用現有的設定檔，讓 Traffic Manager 不是指使用者要求 toohello 設定端點。</span><span class="sxs-lookup"><span data-stu-id="f65a6-126">You can disable an existing profile so that Traffic Manager does not refer user requests toohello configured endpoints.</span></span> <span data-ttu-id="f65a6-127">當您停用流量管理員設定檔時，hello 設定檔與 hello hello 設定檔中包含的資訊仍維持不變，可以在 hello Traffic Manager 介面中進行編輯。</span><span class="sxs-lookup"><span data-stu-id="f65a6-127">When you disable a Traffic Manager profile, hello profile and hello information contained in hello profile remain intact and can be edited in hello Traffic Manager interface.</span></span>  <span data-ttu-id="f65a6-128">當您重新啟用 hello 設定檔，就會繼續轉介。</span><span class="sxs-lookup"><span data-stu-id="f65a6-128">Referrals resume when you re-enable hello profile.</span></span> <span data-ttu-id="f65a6-129">當您在 hello Azure 入口網站中建立流量管理員設定檔時，它會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="f65a6-129">When you create a Traffic Manager profile in hello Azure portal, it's automatically enabled.</span></span> <span data-ttu-id="f65a6-130">如果您決定不再需要某個設定檔，可以將它刪除。</span><span class="sxs-lookup"><span data-stu-id="f65a6-130">If you decide a profile is no longer necessary, you can delete it.</span></span>

### <a name="toodisable-a-profile"></a><span data-ttu-id="f65a6-131">toodisable 設定檔</span><span class="sxs-lookup"><span data-stu-id="f65a6-131">toodisable a profile</span></span>

1. <span data-ttu-id="f65a6-132">如果您使用自訂網域名稱，變更您的網際網路 DNS 伺服器上的 hello CNAME 記錄，使它不再指向 tooyour Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="f65a6-132">If you are using a custom domain name, change hello CNAME record on your Internet DNS server so that it no longer points tooyour Traffic Manager profile.</span></span>
2. <span data-ttu-id="f65a6-133">流量會停止正在執行導向 toohello hello Traffic Manager 設定檔所設定的端點。</span><span class="sxs-lookup"><span data-stu-id="f65a6-133">Traffic stops being directed toohello endpoints through hello Traffic Manager profile settings.</span></span>
3. <span data-ttu-id="f65a6-134">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f65a6-134">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="f65a6-135">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下hello hello Traffic Manager 設定檔的名稱會顯示該 hello。</span><span class="sxs-lookup"><span data-stu-id="f65a6-135">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that hello displayed.</span></span>
3. <span data-ttu-id="f65a6-136">在 hello **Traffic Manager 設定檔**刀鋒視窗中，按一下**概觀**，hello 概觀刀鋒視窗中按一下**停用**，然後確認 toodisable hello Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="f65a6-136">In hello **Traffic Manager profile** blade, click **Overview**, in hello Overview blade click **Disable**, and then confirm toodisable hello Traffic Manager profile.</span></span>

### <a name="tooenable-a-profile"></a><span data-ttu-id="f65a6-137">tooenable 設定檔</span><span class="sxs-lookup"><span data-stu-id="f65a6-137">tooenable a profile</span></span>

1. <span data-ttu-id="f65a6-138">從瀏覽器中，登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f65a6-138">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="f65a6-139">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下hello hello Traffic Manager 設定檔的名稱會顯示該 hello。</span><span class="sxs-lookup"><span data-stu-id="f65a6-139">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that hello displayed.</span></span>
3. <span data-ttu-id="f65a6-140">在 hello **Traffic Manager 設定檔**刀鋒視窗中，按一下**概觀**，然後在 hello 概觀刀鋒視窗中按一下**啟用**。</span><span class="sxs-lookup"><span data-stu-id="f65a6-140">In hello **Traffic Manager profile** blade, click **Overview**, and then in hello Overview blade click **Enable**.</span></span>
5. <span data-ttu-id="f65a6-141">如果您使用自訂網域名稱，請對您網際網路 DNS 伺服器 toopoint toohello 網域名稱 Traffic Manager 設定檔建立的 CNAME 資源記錄。</span><span class="sxs-lookup"><span data-stu-id="f65a6-141">If you are using a custom domain name, create a CNAME resource record on your Internet DNS server toopoint toohello domain name of your Traffic Manager profile.</span></span>
6. <span data-ttu-id="f65a6-142">流量會導向的 toohello 端點的一次。</span><span class="sxs-lookup"><span data-stu-id="f65a6-142">Traffic is directed toohello endpoints again.</span></span>

### <a name="toodelete-a-profile"></a><span data-ttu-id="f65a6-143">toodelete 設定檔</span><span class="sxs-lookup"><span data-stu-id="f65a6-143">toodelete a profile</span></span>

1. <span data-ttu-id="f65a6-144">請確定您的網際網路 DNS 伺服器上的 hello DNS 資源記錄不會再使用的 CNAME 資源記錄指向 Traffic Manager 設定檔 toohello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="f65a6-144">Ensure that hello DNS resource record on your Internet DNS server no longer uses a CNAME resource record that points toohello domain name of your Traffic Manager profile.</span></span>
2. <span data-ttu-id="f65a6-145">在 hello 入口網站的 搜尋 列，搜尋 hello **Traffic Manager 設定檔**您想 toomodify，，，然後按一下hello hello Traffic Manager 設定檔的名稱會顯示該 hello。</span><span class="sxs-lookup"><span data-stu-id="f65a6-145">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that hello displayed.</span></span>
3. <span data-ttu-id="f65a6-146">在 hello **Traffic Manager 設定檔**刀鋒視窗中，按一下**概觀**，hello 概觀刀鋒視窗中按一下**刪除**，然後確認 toodelete hello Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="f65a6-146">In hello **Traffic Manager profile** blade, click **Overview**, in hello Overview blade click **Delete**, and then confirm toodelete hello Traffic Manager profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f65a6-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f65a6-147">Next steps</span></span>

* [<span data-ttu-id="f65a6-148">新增端點。</span><span class="sxs-lookup"><span data-stu-id="f65a6-148">Add an endpoint</span></span>](traffic-manager-endpoints.md)
* [<span data-ttu-id="f65a6-149">設定優先順序路由方法</span><span class="sxs-lookup"><span data-stu-id="f65a6-149">Configure Priority routing method</span></span>](traffic-manager-configure-priority-routing-method.md)
* [<span data-ttu-id="f65a6-150">設定地理路由方法</span><span class="sxs-lookup"><span data-stu-id="f65a6-150">Configure Geographic routing method</span></span>](traffic-manager-configure-geographic-routing-method.md) 
* [<span data-ttu-id="f65a6-151">設定加權路由方法</span><span class="sxs-lookup"><span data-stu-id="f65a6-151">Configure Weighted routing method</span></span>](traffic-manager-configure-weighted-routing-method.md)
* [<span data-ttu-id="f65a6-152">設定效能路由方法</span><span class="sxs-lookup"><span data-stu-id="f65a6-152">Configure Performance routing method</span></span>](traffic-manager-configure-performance-routing-method.md)
