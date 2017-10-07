---
title: "aaaBuy Azure Web 應用程式的自訂網域名稱"
description: "了解如何 toobuy 自訂網域名稱在 Azure App Service web 應用程式。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="669a3-103">針對 Azure Web Apps 購買自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="669a3-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="669a3-104">App Service 網域 (預覽) 是直接在 Azure 中管理的頂層網域。</span><span class="sxs-lookup"><span data-stu-id="669a3-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="669a3-105">它們可讓您輕鬆 toomanage 自訂網域[Azure Web Apps](app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="669a3-105">They make it easy toomanage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="669a3-106">本教學課程會示範如何 toobuy 應用程式服務網域並指派 DNS 名稱 tooAzure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="669a3-106">This tutorial shows you how toobuy an App Service domain and assign DNS names tooAzure Web Apps.</span></span>

<span data-ttu-id="669a3-107">本文適用於 Azure App Service (Web Apps、API Apps、Mobile Apps、Logic Apps)。</span><span class="sxs-lookup"><span data-stu-id="669a3-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="669a3-108">針對 Azure VM 或 Azure 儲存體，請參閱[指派應用程式服務網域 tooAzure VM 或 Azure 儲存體](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/)。</span><span class="sxs-lookup"><span data-stu-id="669a3-108">For Azure VM or Azure Storage, see [Assign App Service domain tooAzure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="669a3-109">若為雲端服務，請參閱[設定 Azure 雲端服務的自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="669a3-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="669a3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="669a3-110">Prerequisites</span></span>

<span data-ttu-id="669a3-111">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="669a3-111">toocomplete this tutorial:</span></span>

* <span data-ttu-id="669a3-112">[建立 App Service 應用程式](/azure/app-service/)，或使用您針對另一個教學課程建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="669a3-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-hello-app"></a><span data-ttu-id="669a3-113">準備 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="669a3-113">Prepare hello app</span></span>

<span data-ttu-id="669a3-114">在 Azure Web 應用程式，您的 web 應用程式的 toouse 自訂網域[App Service 方案](https://azure.microsoft.com/pricing/details/app-service/)必須付費的層 (**共用**，**基本**，**標準**，或**Premium**)。</span><span class="sxs-lookup"><span data-stu-id="669a3-114">toouse custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="669a3-115">在此步驟中，您確定該 hello web 應用程式在 hello 支援定價層。</span><span class="sxs-lookup"><span data-stu-id="669a3-115">In this step, you make sure that hello web app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="669a3-116">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="669a3-116">Sign in tooAzure</span></span>

<span data-ttu-id="669a3-117">開啟 hello [Azure 入口網站](https://portal.azure.com)並以您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="669a3-117">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="669a3-118">瀏覽 toohello hello Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="669a3-118">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="669a3-119">從 hello 左窗格中，選取**應用程式服務**，然後選取 hello hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="669a3-119">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="669a3-121">您會看到 hello hello App Service 應用程式管理頁面。</span><span class="sxs-lookup"><span data-stu-id="669a3-121">You see hello management page of hello App Service app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="669a3-122">核取 hello 定價層</span><span class="sxs-lookup"><span data-stu-id="669a3-122">Check hello pricing tier</span></span>

<span data-ttu-id="669a3-123">在 hello 左瀏覽的 hello 應用程式頁面，捲動 toohello**設定**區段，然後選取**向上擴充 （應用程式服務方案）**。</span><span class="sxs-lookup"><span data-stu-id="669a3-123">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![相應增加功能表](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="669a3-125">hello 應用程式目前的階層會以藍色框線反白顯示。</span><span class="sxs-lookup"><span data-stu-id="669a3-125">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="669a3-126">請確定該 hello 應用程式不在 hello toomake**免費**層。</span><span class="sxs-lookup"><span data-stu-id="669a3-126">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="669a3-127">不支援自訂 DNS hello**免費**層。</span><span class="sxs-lookup"><span data-stu-id="669a3-127">Custom DNS is not supported in hello **Free** tier.</span></span> 

![檢查定價層](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="669a3-129">如果 hello App Service 方案不**免費**，請關閉 hello**選擇定價層**頁面上，並略過太[購買 hello 網域](#buy-the-domain)。</span><span class="sxs-lookup"><span data-stu-id="669a3-129">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Buy hello domain](#buy-the-domain).</span></span>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="669a3-130">向上擴充 hello App Service 方案</span><span class="sxs-lookup"><span data-stu-id="669a3-130">Scale up hello App Service plan</span></span>

<span data-ttu-id="669a3-131">選取任何 hello 非可用層 (**共用**，**基本**，**標準**，或**Premium**)。</span><span class="sxs-lookup"><span data-stu-id="669a3-131">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="669a3-132">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="669a3-132">Click **Select**.</span></span>

![檢查定價層](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="669a3-134">當您看到下列通知 hello 時，hello 調整規模作業已完成。</span><span class="sxs-lookup"><span data-stu-id="669a3-134">When you see hello following notification, hello scale operation is complete.</span></span>

![擴充作業確認](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a><span data-ttu-id="669a3-136">購買 hello 網域</span><span class="sxs-lookup"><span data-stu-id="669a3-136">Buy hello domain</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="669a3-137">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="669a3-137">Sign in tooAzure</span></span>
<span data-ttu-id="669a3-138">開啟 hello [Azure 入口網站](https://portal.azure.com/)並以您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="669a3-138">Open hello [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="669a3-139">啟動購買網域</span><span class="sxs-lookup"><span data-stu-id="669a3-139">Launch Buy domains</span></span>
<span data-ttu-id="669a3-140">在 hello **Web 應用程式**索引標籤上，按一下您 web 應用程式，選取 hello 名稱**設定**，然後選取**自訂網域**</span><span class="sxs-lookup"><span data-stu-id="669a3-140">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="669a3-141">在 hello**自訂網域**頁面上，按一下**購買網域**。</span><span class="sxs-lookup"><span data-stu-id="669a3-141">In hello **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a><span data-ttu-id="669a3-142">設定 hello 網域購買</span><span class="sxs-lookup"><span data-stu-id="669a3-142">Configure hello domain purchase</span></span>

<span data-ttu-id="669a3-143">在 hello**應用程式服務網域** 頁面的 hello**網域搜尋**中，輸入 hello 網域名稱，而您想要 toobuy 和型別`Enter`。</span><span class="sxs-lookup"><span data-stu-id="669a3-143">In hello **App Service Domain** page, in hello **Search for domain** box, type hello domain name you want toobuy and type `Enter`.</span></span> <span data-ttu-id="669a3-144">hello 建議可用的定義域會顯示 hello 文字 方塊的正下方。</span><span class="sxs-lookup"><span data-stu-id="669a3-144">hello suggested available domains are shown just below hello text box.</span></span> <span data-ttu-id="669a3-145">選取您想要 toobuy 的一或多個定義域。</span><span class="sxs-lookup"><span data-stu-id="669a3-145">Select one or more domains you want toobuy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="669a3-146">按一下 hello**連絡人資訊**並填寫 hello 網域的連絡人資訊表單。</span><span class="sxs-lookup"><span data-stu-id="669a3-146">Click hello **Contact Information** and fill out hello domain's contact information form.</span></span> <span data-ttu-id="669a3-147">完成後，請按一下**確定**tooreturn toohello 應用程式服務網域 頁面。</span><span class="sxs-lookup"><span data-stu-id="669a3-147">When finished, click **OK** tooreturn toohello App Service Domain page.</span></span>
   
<span data-ttu-id="669a3-148">請務必填寫所有必要欄位，並盡可能正確填寫。</span><span class="sxs-lookup"><span data-stu-id="669a3-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="669a3-149">如需連絡資訊不正確的資料可能會導致失敗 toopurchase 網域。</span><span class="sxs-lookup"><span data-stu-id="669a3-149">Incorrect data for contact information can result in failure toopurchase domains.</span></span> 

<span data-ttu-id="669a3-150">接下來，選取 hello 所需的選項，為您的網域。</span><span class="sxs-lookup"><span data-stu-id="669a3-150">Next, select hello desired options for your domain.</span></span> <span data-ttu-id="669a3-151">請參閱下表說明 hello:</span><span class="sxs-lookup"><span data-stu-id="669a3-151">See hello following table for explanations:</span></span>

| <span data-ttu-id="669a3-152">設定</span><span class="sxs-lookup"><span data-stu-id="669a3-152">Setting</span></span> | <span data-ttu-id="669a3-153">建議的值</span><span class="sxs-lookup"><span data-stu-id="669a3-153">Suggested Value</span></span> | <span data-ttu-id="669a3-154">說明</span><span class="sxs-lookup"><span data-stu-id="669a3-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="669a3-155">自動續訂</span><span class="sxs-lookup"><span data-stu-id="669a3-155">Auto renew</span></span> | <span data-ttu-id="669a3-156">**啟用**</span><span class="sxs-lookup"><span data-stu-id="669a3-156">**Enable**</span></span> | <span data-ttu-id="669a3-157">每年自動續訂 App Service 網域。</span><span class="sxs-lookup"><span data-stu-id="669a3-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="669a3-158">您的信用卡收取次更新的 hello hello 相同購買的價格。</span><span class="sxs-lookup"><span data-stu-id="669a3-158">Your credit card is charged hello same purchase price at hello time of renewal.</span></span> |
|<span data-ttu-id="669a3-159">隱私權保護</span><span class="sxs-lookup"><span data-stu-id="669a3-159">Privacy protection</span></span> | <span data-ttu-id="669a3-160">啟用</span><span class="sxs-lookup"><span data-stu-id="669a3-160">Enable</span></span> | <span data-ttu-id="669a3-161">太參加 「 隱私權保護 」，其隨附於 hello 購買價格_免費_(頂層網域登錄這類不支援隱私權保護，除了_。 co.in_， _。co.uk_等等)。</span><span class="sxs-lookup"><span data-stu-id="669a3-161">Opt in too"Privacy protection", which is included in hello purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="669a3-162">指派預設主機名稱</span><span class="sxs-lookup"><span data-stu-id="669a3-162">Assign default hostnames</span></span> | <span data-ttu-id="669a3-163">**www** 和 **@**</span><span class="sxs-lookup"><span data-stu-id="669a3-163">**www** and **@**</span></span> | <span data-ttu-id="669a3-164">選取 hello 所需的主機名稱繫結，如有需要。</span><span class="sxs-lookup"><span data-stu-id="669a3-164">Select hello desired hostname bindings, if desired.</span></span> <span data-ttu-id="669a3-165">Hello 網域採購作業完成時，可以在 hello 選取的主機名稱存取您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="669a3-165">When hello domain purchase operation is complete, your web app can be accessed at hello selected hostnames.</span></span> <span data-ttu-id="669a3-166">如果 hello web 應用程式是後面[Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/)，您沒有看到 hello 選項 tooassign hello 根網域 (@)，因為 Traffic Manager 不支援 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="669a3-166">If hello web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see hello option tooassign hello root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="669a3-167">您可以變更 toohello 主機名稱指派 hello 網域購買完成之後。</span><span class="sxs-lookup"><span data-stu-id="669a3-167">You can make changes toohello hostname assignments after hello domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="669a3-168">接受條款並購買</span><span class="sxs-lookup"><span data-stu-id="669a3-168">Accept terms and purchase</span></span>

<span data-ttu-id="669a3-169">按一下**法律條款**tooreview hello 條款及 hello 費用，然後按一下**購買**。</span><span class="sxs-lookup"><span data-stu-id="669a3-169">Click **Legal Terms** tooreview hello terms and hello charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="669a3-170">應用程式服務網域使用 Azure DNS toohost hello 定義域。</span><span class="sxs-lookup"><span data-stu-id="669a3-170">App Service Domains use Azure DNS toohost hello domains.</span></span> <span data-ttu-id="669a3-171">此外 toohello 網域註冊費，使用 Azure DNS 的費用。</span><span class="sxs-lookup"><span data-stu-id="669a3-171">In addition toohello domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="669a3-172">如需相關資訊，請參閱 [Azure DNS 定價](https://azure.microsoft.com/pricing/details/dns/)。</span><span class="sxs-lookup"><span data-stu-id="669a3-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="669a3-173">在 hello**應用程式服務網域**頁面上，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="669a3-173">Back in hello **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="669a3-174">在 hello 作業正在進行中，您會看到下列通知 hello:</span><span class="sxs-lookup"><span data-stu-id="669a3-174">While hello operation is in progress, you see hello following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="669a3-175">測試 hello 主機名稱</span><span class="sxs-lookup"><span data-stu-id="669a3-175">Test hello hostnames</span></span>

<span data-ttu-id="669a3-176">如果您已指派預設主機名稱 tooyour web 應用程式，您也可以看到每個選取的主機名稱的成功通知。</span><span class="sxs-lookup"><span data-stu-id="669a3-176">If you have assigned default hostnames tooyour web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="669a3-177">另請參閱 hello 選取的主機名稱在 hello**自訂網域** 頁面的 hello **Hostname** > 一節。</span><span class="sxs-lookup"><span data-stu-id="669a3-177">You also see hello selected hostnames in hello **Custom domains** page, in hello **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="669a3-178">tootest hello 主機名稱，瀏覽列 toohello hello 瀏覽器中的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="669a3-178">tootest hello hostnames, navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="669a3-179">Hello hello 範例中前面螢幕擷取畫面，再試一次瀏覽 too_kontoso.net_ 和_www.kontoso.net_。</span><span class="sxs-lookup"><span data-stu-id="669a3-179">In hello example in hello preceding screenshot, try navigating too_kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-tooweb-app"></a><span data-ttu-id="669a3-180">指定主機名稱 tooweb 應用程式</span><span class="sxs-lookup"><span data-stu-id="669a3-180">Assign hostnames tooweb app</span></span>

<span data-ttu-id="669a3-181">如果您選擇不 tooassign 其中一個或多個預設主機名稱 tooyour web 應用程式期間 hello 購買程序，或如果您不需要 tooassign 主機名稱列出，您可以在任何時間指派主機名稱。</span><span class="sxs-lookup"><span data-stu-id="669a3-181">If you choose not tooassign one or more default hostnames tooyour web app during hello purchase process, or if you need tooassign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="669a3-182">您也可以指派主機名稱在 hello 應用程式服務網域 tooany 其他 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="669a3-182">You can also assign hostnames in hello App Service Domain tooany other web app.</span></span> <span data-ttu-id="669a3-183">hello 步驟取決於 hello 應用程式服務網域與 hello web 應用程式是否屬於 toohello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="669a3-183">hello steps depend on whether hello App Service Domain and hello web app belong toohello same subscription.</span></span>

- <span data-ttu-id="669a3-184">不同的訂用帳戶： 對應 hello 應用程式服務網域 toohello web 應用程式，例如外部所購買的網域中的自訂 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="669a3-184">Different subscription: Map custom DNS records from hello App Service Domain toohello web app like an externally purchased domain.</span></span> <span data-ttu-id="669a3-185">有關新增自訂的 DNS 名稱 tooan 應用程式服務網域，請參閱[管理自訂 DNS 記錄](#custom)。</span><span class="sxs-lookup"><span data-stu-id="669a3-185">For information on adding custom DNS names tooan App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="669a3-186">toomap 外部購買的網域 tooa web 應用程式，請參閱[對應現有自訂 DNS 名稱 tooAzure Web 應用程式](app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="669a3-186">toomap an external purchased domain tooa web app, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="669a3-187">相同的訂用帳戶： 使用 hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="669a3-187">Same subscription: Use hello following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="669a3-188">啟動新增主機名稱</span><span class="sxs-lookup"><span data-stu-id="669a3-188">Launch add hostname</span></span>
<span data-ttu-id="669a3-189">在 hello**應用程式服務**頁面、 選取 hello 想 tooassign 主機名稱、 選取您 web 應用程式名稱**設定**，然後選取**自訂網域**。</span><span class="sxs-lookup"><span data-stu-id="669a3-189">In hello **App Services** page, select hello name of your web app that you want tooassign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="669a3-190">請確定您已購買的網域列在 hello**應用程式服務網域**區段，但不要選取它。</span><span class="sxs-lookup"><span data-stu-id="669a3-190">Make sure that your purchased domain is listed in hello **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="669a3-191">Hello 顯示 hello web 應用程式的相同訂用帳戶中的所有應用程式服務網域**自訂網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="669a3-191">All App Service Domains in hello same subscription are shown in hello web app's **Custom domains** page.</span></span> <span data-ttu-id="669a3-192">如果您的網域是在 hello web 應用程式的訂用帳戶，但看不到在 hello web 應用程式的**自訂網域**頁面上，再次嘗試重新開啟 hello**自訂網域**頁面上，或重新整理 hello 網頁。</span><span class="sxs-lookup"><span data-stu-id="669a3-192">If your domain is in hello web app's subscription, but you cannot see it in hello web app's **Custom domains** page, try reopening hello **Custom domains** page or refresh hello webpage.</span></span> <span data-ttu-id="669a3-193">另請檢查 hello 通知鈴鐺在 hello hello Azure 入口網站頂端的進度或建立失敗。</span><span class="sxs-lookup"><span data-stu-id="669a3-193">Also, check hello notification bell at hello top of hello Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="669a3-194">選取 [新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="669a3-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="669a3-195">設定主機名稱</span><span class="sxs-lookup"><span data-stu-id="669a3-195">Configure hostname</span></span>
<span data-ttu-id="669a3-196">在 hello**新增主機名稱**對話方塊中，您的應用程式服務網域或任何子網域的型別 hello 完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="669a3-196">In hello **Add hostname** dialog, type hello fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="669a3-197">例如：</span><span class="sxs-lookup"><span data-stu-id="669a3-197">For example:</span></span>

- <span data-ttu-id="669a3-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="669a3-198">kontoso.net</span></span>
- <span data-ttu-id="669a3-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="669a3-199">www.kontoso.net</span></span>
- <span data-ttu-id="669a3-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="669a3-200">abc.kontoso.net</span></span>

<span data-ttu-id="669a3-201">完成之後，請選取 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="669a3-201">When finished, select **Validate**.</span></span> <span data-ttu-id="669a3-202">hello 主機名稱記錄類型會自動為您選擇。</span><span class="sxs-lookup"><span data-stu-id="669a3-202">hello hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="669a3-203">選取 [新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="669a3-203">Select **Add hostname**.</span></span>

<span data-ttu-id="669a3-204">Hello 作業完成時，您會看到指派主機名稱的 hello 的成功通知。</span><span class="sxs-lookup"><span data-stu-id="669a3-204">When hello operation is complete, you see a success notification for hello assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="669a3-205">關閉新增主機名稱</span><span class="sxs-lookup"><span data-stu-id="669a3-205">Close add hostname</span></span>
<span data-ttu-id="669a3-206">在 hello**新增主機名稱**頁面中，指派任何其他主機名稱 tooyour web 應用程式，視需要。</span><span class="sxs-lookup"><span data-stu-id="669a3-206">In hello **Add hostname** page, assign any other hostname tooyour web app, as desired.</span></span> <span data-ttu-id="669a3-207">完成後，關閉 hello**新增 hostname**頁面。</span><span class="sxs-lookup"><span data-stu-id="669a3-207">When finished, close hello **Add hostname** page.</span></span>

<span data-ttu-id="669a3-208">您現在應該會在您的應用程式中看到新指派的 hello hostname(s)**自訂網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="669a3-208">You should now see hello newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="669a3-209">測試 hello 主機名稱</span><span class="sxs-lookup"><span data-stu-id="669a3-209">Test hello hostnames</span></span>

<span data-ttu-id="669a3-210">瀏覽列 toohello hello 瀏覽器中的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="669a3-210">Navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="669a3-211">在 hello hello 前面螢幕擷取畫面中的範例，請嘗試瀏覽 too_abc.kontoso.net_。</span><span class="sxs-lookup"><span data-stu-id="669a3-211">In hello example in hello preceding screenshot, try navigating too_abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="669a3-212">管理自訂 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="669a3-212">Manage custom DNS records</span></span>

<span data-ttu-id="669a3-213">在 Azure 中，App Service 網域的 DNS 記錄是使用 [Azure DNS](https://azure.microsoft.com/services/dns/) 來管理。</span><span class="sxs-lookup"><span data-stu-id="669a3-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="669a3-214">和針對外部購買的網域一樣，您可以新增、移除及更新 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="669a3-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="669a3-215">開啟 App Service 網域</span><span class="sxs-lookup"><span data-stu-id="669a3-215">Open App Service Domain</span></span>

<span data-ttu-id="669a3-216">在 hello Azure 入口網站，從 hello 左窗格中，選取 **更服務** > **應用程式服務網域**。</span><span class="sxs-lookup"><span data-stu-id="669a3-216">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="669a3-217">選取 hello 網域 toomanage。</span><span class="sxs-lookup"><span data-stu-id="669a3-217">Select hello domain toomanage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="669a3-218">存取 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="669a3-218">Access DNS zone</span></span>

<span data-ttu-id="669a3-219">在 hello 網域的左窗格中，選取  **DNS 區域**。</span><span class="sxs-lookup"><span data-stu-id="669a3-219">In hello domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="669a3-220">這個動作會開啟 hello [DNS 區域](../dns/dns-zones-records.md)Azure DNS 中的應用程式服務網域的頁面。</span><span class="sxs-lookup"><span data-stu-id="669a3-220">This action opens hello [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="669a3-221">如需詳細資訊 tooedit DNS 記錄，請參閱[toomanage DNS 區域 hello Azure 入口網站的方式](../dns/dns-operations-dnszones-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="669a3-221">For information on how tooedit DNS records, see [How toomanage DNS Zones in hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="669a3-222">取消購買 (刪除網域)</span><span class="sxs-lookup"><span data-stu-id="669a3-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="669a3-223">購買 hello 應用程式服務網域後，您有五天 toocancel 全額退款購買。</span><span class="sxs-lookup"><span data-stu-id="669a3-223">After you purchase hello App Service Domain, you have five days toocancel your purchase for a full refund.</span></span> <span data-ttu-id="669a3-224">五天之後，您可以刪除 hello 應用程式服務網域，但無法獲得退款。</span><span class="sxs-lookup"><span data-stu-id="669a3-224">After five days, you can delete hello App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="669a3-225">開啟 App Service 網域</span><span class="sxs-lookup"><span data-stu-id="669a3-225">Open App Service Domain</span></span>

<span data-ttu-id="669a3-226">在 hello Azure 入口網站，從 hello 左窗格中，選取 **更服務** > **應用程式服務網域**。</span><span class="sxs-lookup"><span data-stu-id="669a3-226">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="669a3-227">選取 hello 網域 tooyou 想 toocancel 或刪除。</span><span class="sxs-lookup"><span data-stu-id="669a3-227">Select hello domain tooyou want toocancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="669a3-228">刪除主機名稱繫結</span><span class="sxs-lookup"><span data-stu-id="669a3-228">Delete hostname bindings</span></span>

<span data-ttu-id="669a3-229">在 hello 網域的左窗格中，選取 **主機名稱繫結**。</span><span class="sxs-lookup"><span data-stu-id="669a3-229">In hello domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="669a3-230">以下列出 hello 從所有 Azure 服務的主機名稱繫結。</span><span class="sxs-lookup"><span data-stu-id="669a3-230">hello hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="669a3-231">您無法刪除 hello 應用程式服務網域，您必須刪除所有的主機名稱繫結。</span><span class="sxs-lookup"><span data-stu-id="669a3-231">You cannot delete hello App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="669a3-232">請透過選取 **...** > [刪除].來刪除每個主機名稱繫結。</span><span class="sxs-lookup"><span data-stu-id="669a3-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="669a3-233">刪除所有 hello 繫結之後，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="669a3-233">After all hello bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="669a3-234">取消或刪除</span><span class="sxs-lookup"><span data-stu-id="669a3-234">Cancel or delete</span></span>

<span data-ttu-id="669a3-235">在 hello 網域的左窗格中，選取 **概觀**。</span><span class="sxs-lookup"><span data-stu-id="669a3-235">In hello domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="669a3-236">如果尚未經過 hello 取消期間 hello 購買網域上的，選取**取消購買**。</span><span class="sxs-lookup"><span data-stu-id="669a3-236">If hello cancellation period on hello purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="669a3-237">否則，您會看到 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="669a3-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="669a3-238">toodelete hello 網域不退款，選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="669a3-238">toodelete hello domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="669a3-239">選取**確定**tooconfirm hello 作業。</span><span class="sxs-lookup"><span data-stu-id="669a3-239">Select **OK** tooconfirm hello operation.</span></span> <span data-ttu-id="669a3-240">如果您不想 tooproceed，按一下之外 hello 確認對話方塊中的任何位置。</span><span class="sxs-lookup"><span data-stu-id="669a3-240">If you don't want tooproceed, click anywhere outside of hello confirmation dialog.</span></span>

<span data-ttu-id="669a3-241">Hello 網域 hello 作業已完成之後，會從您的訂用帳戶已釋放及可供任何人 toopurchase 一次。</span><span class="sxs-lookup"><span data-stu-id="669a3-241">After hello operation is complete, hello domain is released from your subscription and available for anyone toopurchase again.</span></span> 
