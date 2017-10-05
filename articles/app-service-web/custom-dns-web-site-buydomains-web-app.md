---
title: "針對 Azure Web Apps 購買自訂網域名稱"
description: "了解如何在 Azure App Service 中購買搭配 Web 應用程式的自訂網域名稱。"
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
ms.openlocfilehash: 3cb22b935624041ab51e64028a1b668fd694f9b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="09862-103">針對 Azure Web Apps 購買自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="09862-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="09862-104">App Service 網域 (預覽) 是直接在 Azure 中管理的頂層網域。</span><span class="sxs-lookup"><span data-stu-id="09862-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="09862-105">它們可以讓 [Azure Web Apps](app-service-web-overview.md) 的自訂網域管理作業變得很簡單。</span><span class="sxs-lookup"><span data-stu-id="09862-105">They make it easy to manage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="09862-106">本教學課程會示範如何購買 App Service 網域，並將 DNS 名稱指派給 Azure Web Apps。</span><span class="sxs-lookup"><span data-stu-id="09862-106">This tutorial shows you how to buy an App Service domain and assign DNS names to Azure Web Apps.</span></span>

<span data-ttu-id="09862-107">本文適用於 Azure App Service (Web Apps、API Apps、Mobile Apps、Logic Apps)。</span><span class="sxs-lookup"><span data-stu-id="09862-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="09862-108">若為 Azure VM 或 Azure 儲存體，請參閱[將 App Service 網域指派給 Azure VM 或 Azure 儲存體](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/)。</span><span class="sxs-lookup"><span data-stu-id="09862-108">For Azure VM or Azure Storage, see [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="09862-109">若為雲端服務，請參閱[設定 Azure 雲端服務的自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="09862-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09862-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="09862-110">Prerequisites</span></span>

<span data-ttu-id="09862-111">若要完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="09862-111">To complete this tutorial:</span></span>

* <span data-ttu-id="09862-112">[建立 App Service 應用程式](/azure/app-service/)，或使用您針對另一個教學課程建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="09862-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-the-app"></a><span data-ttu-id="09862-113">準備應用程式</span><span class="sxs-lookup"><span data-stu-id="09862-113">Prepare the app</span></span>

<span data-ttu-id="09862-114">若要在 Azure Web Apps 中使用自訂網域，Web 應用程式的 [App Service 方案](https://azure.microsoft.com/pricing/details/app-service/)必須是付費層 (「共用」、「基本」、「標準」或「進階」)。</span><span class="sxs-lookup"><span data-stu-id="09862-114">To use custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="09862-115">在此步驟中，您要確定 Web 應用程式位於支援的定價層。</span><span class="sxs-lookup"><span data-stu-id="09862-115">In this step, you make sure that the web app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="09862-116">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="09862-116">Sign in to Azure</span></span>

<span data-ttu-id="09862-117">開啟 [Azure 入口網站](https://portal.azure.com)並使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="09862-117">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="09862-118">瀏覽至 Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="09862-118">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="09862-119">從左側功能表，選取 [App Service]，然後選取應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="09862-119">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![入口網站瀏覽至 Azure 應用程式](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="09862-121">您看到 App Service 應用程式的管理分頁。</span><span class="sxs-lookup"><span data-stu-id="09862-121">You see the management page of the App Service app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="09862-122">檢查定價層</span><span class="sxs-lookup"><span data-stu-id="09862-122">Check the pricing tier</span></span>

<span data-ttu-id="09862-123">在應用程式分頁的左側導覽中，捲動到 [設定] 區段，然後選取 [相應增加 (App Service 方案)]。</span><span class="sxs-lookup"><span data-stu-id="09862-123">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![相應增加功能表](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="09862-125">會以藍色框線醒目顯示應用程式目前的層。</span><span class="sxs-lookup"><span data-stu-id="09862-125">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="09862-126">請檢查以確定您的應用程式不是位於**免費**層。</span><span class="sxs-lookup"><span data-stu-id="09862-126">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="09862-127">**免費**層不支援自訂 DNS。</span><span class="sxs-lookup"><span data-stu-id="09862-127">Custom DNS is not supported in the **Free** tier.</span></span> 

![檢查定價層](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="09862-129">如果 App Service 方案不是「免費」，請關閉 [選擇定價層] 頁面，然後跳至[購買網域](#buy-the-domain)。</span><span class="sxs-lookup"><span data-stu-id="09862-129">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Buy the domain](#buy-the-domain).</span></span>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="09862-130">相應增加 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="09862-130">Scale up the App Service plan</span></span>

<span data-ttu-id="09862-131">選取任一個非免費層 (**共用**、**基本**、**標準**或**進階**)。</span><span class="sxs-lookup"><span data-stu-id="09862-131">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="09862-132">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="09862-132">Click **Select**.</span></span>

![檢查定價層](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="09862-134">當您看見下列通知時，表示擴充作業已完成。</span><span class="sxs-lookup"><span data-stu-id="09862-134">When you see the following notification, the scale operation is complete.</span></span>

![擴充作業確認](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-the-domain"></a><span data-ttu-id="09862-136">購買網域</span><span class="sxs-lookup"><span data-stu-id="09862-136">Buy the domain</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="09862-137">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="09862-137">Sign in to Azure</span></span>
<span data-ttu-id="09862-138">開啟 [Azure 入口網站](https://portal.azure.com/)並使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="09862-138">Open the [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="09862-139">啟動購買網域</span><span class="sxs-lookup"><span data-stu-id="09862-139">Launch Buy domains</span></span>
<span data-ttu-id="09862-140">在 [Web Apps] 索引標籤中，按一下您 Web 應用程式的名稱，並選取 [設定]，然後選取 [自訂網域]</span><span class="sxs-lookup"><span data-stu-id="09862-140">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="09862-141">在 [自訂網域] 頁面中，按一下 [購買網域]。</span><span class="sxs-lookup"><span data-stu-id="09862-141">In the **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-the-domain-purchase"></a><span data-ttu-id="09862-142">設定網域購買</span><span class="sxs-lookup"><span data-stu-id="09862-142">Configure the domain purchase</span></span>

<span data-ttu-id="09862-143">在 [App Service 網域] 頁面的 [搜尋網域] 方塊中，輸入要購買的網域名稱，然後輸入 `Enter`。</span><span class="sxs-lookup"><span data-stu-id="09862-143">In the **App Service Domain** page, in the **Search for domain** box, type the domain name you want to buy and type `Enter`.</span></span> <span data-ttu-id="09862-144">建議的可用網域會顯示在文字方塊下方。</span><span class="sxs-lookup"><span data-stu-id="09862-144">The suggested available domains are shown just below the text box.</span></span> <span data-ttu-id="09862-145">選取一或多個要購買的網域。</span><span class="sxs-lookup"><span data-stu-id="09862-145">Select one or more domains you want to buy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="09862-146">按一下 [連絡人資訊]，然後填寫網域的連絡人資訊表單。</span><span class="sxs-lookup"><span data-stu-id="09862-146">Click the **Contact Information** and fill out the domain's contact information form.</span></span> <span data-ttu-id="09862-147">完成之後，請按一下 [確定] 以返回 [App Service 網域] 頁面。</span><span class="sxs-lookup"><span data-stu-id="09862-147">When finished, click **OK** to return to the App Service Domain page.</span></span>
   
<span data-ttu-id="09862-148">請務必填寫所有必要欄位，並盡可能正確填寫。</span><span class="sxs-lookup"><span data-stu-id="09862-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="09862-149">連絡資訊的資料若不正確，可能會導致無法購買網域。</span><span class="sxs-lookup"><span data-stu-id="09862-149">Incorrect data for contact information can result in failure to purchase domains.</span></span> 

<span data-ttu-id="09862-150">接下來，請為網域選取所需選項。</span><span class="sxs-lookup"><span data-stu-id="09862-150">Next, select the desired options for your domain.</span></span> <span data-ttu-id="09862-151">請參閱下表中的說明：</span><span class="sxs-lookup"><span data-stu-id="09862-151">See the following table for explanations:</span></span>

| <span data-ttu-id="09862-152">設定</span><span class="sxs-lookup"><span data-stu-id="09862-152">Setting</span></span> | <span data-ttu-id="09862-153">建議的值</span><span class="sxs-lookup"><span data-stu-id="09862-153">Suggested Value</span></span> | <span data-ttu-id="09862-154">說明</span><span class="sxs-lookup"><span data-stu-id="09862-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="09862-155">自動續訂</span><span class="sxs-lookup"><span data-stu-id="09862-155">Auto renew</span></span> | <span data-ttu-id="09862-156">**啟用**</span><span class="sxs-lookup"><span data-stu-id="09862-156">**Enable**</span></span> | <span data-ttu-id="09862-157">每年自動續訂 App Service 網域。</span><span class="sxs-lookup"><span data-stu-id="09862-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="09862-158">我們會在每次續訂時向您的信用卡收取相同的購買費用。</span><span class="sxs-lookup"><span data-stu-id="09862-158">Your credit card is charged the same purchase price at the time of renewal.</span></span> |
|<span data-ttu-id="09862-159">隱私權保護</span><span class="sxs-lookup"><span data-stu-id="09862-159">Privacy protection</span></span> | <span data-ttu-id="09862-160">啟用</span><span class="sxs-lookup"><span data-stu-id="09862-160">Enable</span></span> | <span data-ttu-id="09862-161">選擇加入「隱私權保護」，此服務已「免費」包含在購買價格中 (除了其登錄不支援隱私權保護的頂層網域以外，例如 _.co.in_、_.co.uk_ 等)。</span><span class="sxs-lookup"><span data-stu-id="09862-161">Opt in to "Privacy protection", which is included in the purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="09862-162">指派預設主機名稱</span><span class="sxs-lookup"><span data-stu-id="09862-162">Assign default hostnames</span></span> | <span data-ttu-id="09862-163">**www** 和 **@**</span><span class="sxs-lookup"><span data-stu-id="09862-163">**www** and **@**</span></span> | <span data-ttu-id="09862-164">如有需要，請選取所需的主機名稱繫結。</span><span class="sxs-lookup"><span data-stu-id="09862-164">Select the desired hostname bindings, if desired.</span></span> <span data-ttu-id="09862-165">網域購買作業完成時，Web 應用程式就可以從選取的主機名稱存取。</span><span class="sxs-lookup"><span data-stu-id="09862-165">When the domain purchase operation is complete, your web app can be accessed at the selected hostnames.</span></span> <span data-ttu-id="09862-166">如果 Web 應用程式受 [Azure 流量管理員](https://azure.microsoft.com/services/traffic-manager/)管理，您就不會看到指派根網域 (@) 的選項，因為流量管理員不支援 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="09862-166">If the web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see the option to assign the root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="09862-167">您可以在網域購買完成之後變更主機名稱指派。</span><span class="sxs-lookup"><span data-stu-id="09862-167">You can make changes to the hostname assignments after the domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="09862-168">接受條款並購買</span><span class="sxs-lookup"><span data-stu-id="09862-168">Accept terms and purchase</span></span>

<span data-ttu-id="09862-169">按一下 [法律條款] 來檢閱條款與費用，然後按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="09862-169">Click **Legal Terms** to review the terms and the charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="09862-170">App Service 網域使用 Azure DNS 來裝載網域。</span><span class="sxs-lookup"><span data-stu-id="09862-170">App Service Domains use Azure DNS to host the domains.</span></span> <span data-ttu-id="09862-171">除了網域註冊費之外，您也必須支付 Azure DNS 的使用費用。</span><span class="sxs-lookup"><span data-stu-id="09862-171">In addition to the domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="09862-172">如需相關資訊，請參閱 [Azure DNS 定價](https://azure.microsoft.com/pricing/details/dns/)。</span><span class="sxs-lookup"><span data-stu-id="09862-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="09862-173">回到 [App Service 網域] 頁面，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="09862-173">Back in the **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="09862-174">作業進行中時，您會看到下列通知：</span><span class="sxs-lookup"><span data-stu-id="09862-174">While the operation is in progress, you see the following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="09862-175">測試主機名稱</span><span class="sxs-lookup"><span data-stu-id="09862-175">Test the hostnames</span></span>

<span data-ttu-id="09862-176">如果您已經指派預設主機名稱給 Web 應用程式，也會看見針對每個選取主機名稱的成功通知。</span><span class="sxs-lookup"><span data-stu-id="09862-176">If you have assigned default hostnames to your web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="09862-177">您也會在 [自訂網域] 頁面的 [主機名稱] 區段中看到選取的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="09862-177">You also see the selected hostnames in the **Custom domains** page, in the **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="09862-178">若要測試主機名稱，請在瀏覽器中瀏覽至列出的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="09862-178">To test the hostnames, navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="09862-179">在上方螢幕擷取畫面的範例中，嘗試瀏覽至 _kontoso.net_ 和 _www.kontoso.net_。</span><span class="sxs-lookup"><span data-stu-id="09862-179">In the example in the preceding screenshot, try navigating to _kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-to-web-app"></a><span data-ttu-id="09862-180">將主機名稱指派給 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="09862-180">Assign hostnames to web app</span></span>

<span data-ttu-id="09862-181">如果您在購買程序期間選擇不指派一或多個預設主機名稱給 Web 應用程式，或是需要指派未列出的主機名稱，您隨時都可以指派主機名稱。</span><span class="sxs-lookup"><span data-stu-id="09862-181">If you choose not to assign one or more default hostnames to your web app during the purchase process, or if you need to assign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="09862-182">您也可以將 App Service 網域中的主機名稱指派給任何其他 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="09862-182">You can also assign hostnames in the App Service Domain to any other web app.</span></span> <span data-ttu-id="09862-183">其步驟需視 App Service 網域和 Web 應用程式是否屬於同一訂用帳戶而定。</span><span class="sxs-lookup"><span data-stu-id="09862-183">The steps depend on whether the App Service Domain and the web app belong to the same subscription.</span></span>

- <span data-ttu-id="09862-184">不同的訂用帳戶：以和對應外部購買的網域相同的方式，將來自 App Service 網域的自訂 DNS 記錄對應至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="09862-184">Different subscription: Map custom DNS records from the App Service Domain to the web app like an externally purchased domain.</span></span> <span data-ttu-id="09862-185">如需將自訂 DNS 名稱新增至 App Service 網域的相關資訊，請參閱[管理自訂 DNS 記錄](#custom)。</span><span class="sxs-lookup"><span data-stu-id="09862-185">For information on adding custom DNS names to an App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="09862-186">若要將外部購買的網域對應至 Web 應用程式，請參閱[將現有的自訂 DNS 名稱對應至 Azure Web Apps](app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="09862-186">To map an external purchased domain to a web app, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="09862-187">相同的訂用帳戶：請使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="09862-187">Same subscription: Use the following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="09862-188">啟動新增主機名稱</span><span class="sxs-lookup"><span data-stu-id="09862-188">Launch add hostname</span></span>
<span data-ttu-id="09862-189">在 [應用程式服務] 頁面中，選取要指派主機名稱的 Web 應用程式名稱，選取 [設定]，然後選取 [自訂網域]。</span><span class="sxs-lookup"><span data-stu-id="09862-189">In the **App Services** page, select the name of your web app that you want to assign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="09862-190">請確定您所購買的網域已列於 [App Service 網域] 區段中，但請不要選取它。</span><span class="sxs-lookup"><span data-stu-id="09862-190">Make sure that your purchased domain is listed in the **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="09862-191">相同訂用帳戶中的所有 App Service 網域，都會顯示在 Web 應用程式的 [自訂網域] 頁面中。</span><span class="sxs-lookup"><span data-stu-id="09862-191">All App Service Domains in the same subscription are shown in the web app's **Custom domains** page.</span></span> <span data-ttu-id="09862-192">如果您的網域已位於 Web 應用程式的訂用帳戶中，但您在 Web 應用程式的 [自訂網域] 頁面中看不到該網域，請嘗試重新開啟 [自訂網域] 頁面，或是重新整理該網頁。</span><span class="sxs-lookup"><span data-stu-id="09862-192">If your domain is in the web app's subscription, but you cannot see it in the web app's **Custom domains** page, try reopening the **Custom domains** page or refresh the webpage.</span></span> <span data-ttu-id="09862-193">此外，請透過檢查位於 Azure 入口網站頂端的通知鈴，來取得進度或建立失敗的訊息。</span><span class="sxs-lookup"><span data-stu-id="09862-193">Also, check the notification bell at the top of the Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="09862-194">選取 [新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="09862-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="09862-195">設定主機名稱</span><span class="sxs-lookup"><span data-stu-id="09862-195">Configure hostname</span></span>
<span data-ttu-id="09862-196">在 [新增主機名稱] 對話方塊中，輸入 App Service 網域或任何子網域的完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="09862-196">In the **Add hostname** dialog, type the fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="09862-197">例如：</span><span class="sxs-lookup"><span data-stu-id="09862-197">For example:</span></span>

- <span data-ttu-id="09862-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="09862-198">kontoso.net</span></span>
- <span data-ttu-id="09862-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="09862-199">www.kontoso.net</span></span>
- <span data-ttu-id="09862-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="09862-200">abc.kontoso.net</span></span>

<span data-ttu-id="09862-201">完成之後，請選取 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="09862-201">When finished, select **Validate**.</span></span> <span data-ttu-id="09862-202">系統會自動為您選取主機名稱記錄類型。</span><span class="sxs-lookup"><span data-stu-id="09862-202">The hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="09862-203">選取 [新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="09862-203">Select **Add hostname**.</span></span>

<span data-ttu-id="09862-204">作業完成之後，您會看到成功指派主機名稱的通知。</span><span class="sxs-lookup"><span data-stu-id="09862-204">When the operation is complete, you see a success notification for the assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="09862-205">關閉新增主機名稱</span><span class="sxs-lookup"><span data-stu-id="09862-205">Close add hostname</span></span>
<span data-ttu-id="09862-206">在 [新增主機名稱] 頁面中，視需求將任何其他主機名稱指派給您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="09862-206">In the **Add hostname** page, assign any other hostname to your web app, as desired.</span></span> <span data-ttu-id="09862-207">完成之後，請關閉 [新增主機名稱] 頁面。</span><span class="sxs-lookup"><span data-stu-id="09862-207">When finished, close the **Add hostname** page.</span></span>

<span data-ttu-id="09862-208">您現在應該會在應用程式的 [自訂網域] 頁面中看到新指派的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="09862-208">You should now see the newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="09862-209">測試主機名稱</span><span class="sxs-lookup"><span data-stu-id="09862-209">Test the hostnames</span></span>

<span data-ttu-id="09862-210">請在瀏覽器中瀏覽至列出的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="09862-210">Navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="09862-211">在上方螢幕擷取畫面的範例中，嘗試瀏覽至 _abc.kontoso.net_。</span><span class="sxs-lookup"><span data-stu-id="09862-211">In the example in the preceding screenshot, try navigating to _abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="09862-212">管理自訂 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="09862-212">Manage custom DNS records</span></span>

<span data-ttu-id="09862-213">在 Azure 中，App Service 網域的 DNS 記錄是使用 [Azure DNS](https://azure.microsoft.com/services/dns/) 來管理。</span><span class="sxs-lookup"><span data-stu-id="09862-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="09862-214">和針對外部購買的網域一樣，您可以新增、移除及更新 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="09862-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="09862-215">開啟 App Service 網域</span><span class="sxs-lookup"><span data-stu-id="09862-215">Open App Service Domain</span></span>

<span data-ttu-id="09862-216">從 Azure 入口網站中的左側功能表，選取 [更多服務] > [App Service 網域]。</span><span class="sxs-lookup"><span data-stu-id="09862-216">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="09862-217">選取要管理的網域。</span><span class="sxs-lookup"><span data-stu-id="09862-217">Select the domain to manage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="09862-218">存取 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="09862-218">Access DNS zone</span></span>

<span data-ttu-id="09862-219">在網域的左側功能表中，選取 [DNS 區域]。</span><span class="sxs-lookup"><span data-stu-id="09862-219">In the domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="09862-220">這個動作會開啟您在 Azure DNS 中之 App Service 網域的 [DNS 區域](../dns/dns-zones-records.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="09862-220">This action opens the [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="09862-221">如需如何編輯 DNS 記錄的相關資訊，請參閱[如何在 Azure 入口網站中管理 DNS 區域](../dns/dns-operations-dnszones-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="09862-221">For information on how to edit DNS records, see [How to manage DNS Zones in the Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="09862-222">取消購買 (刪除網域)</span><span class="sxs-lookup"><span data-stu-id="09862-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="09862-223">在您購買 App Service 網域之後，可以在五天內取消購買並獲得全額退費。</span><span class="sxs-lookup"><span data-stu-id="09862-223">After you purchase the App Service Domain, you have five days to cancel your purchase for a full refund.</span></span> <span data-ttu-id="09862-224">您也可以在五天之後刪除 App Service 網域，但無法收到退款。</span><span class="sxs-lookup"><span data-stu-id="09862-224">After five days, you can delete the App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="09862-225">開啟 App Service 網域</span><span class="sxs-lookup"><span data-stu-id="09862-225">Open App Service Domain</span></span>

<span data-ttu-id="09862-226">從 Azure 入口網站中的左側功能表，選取 [更多服務] > [App Service 網域]。</span><span class="sxs-lookup"><span data-stu-id="09862-226">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="09862-227">選取您要取消或刪除的網域。</span><span class="sxs-lookup"><span data-stu-id="09862-227">Select the domain to you want to cancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="09862-228">刪除主機名稱繫結</span><span class="sxs-lookup"><span data-stu-id="09862-228">Delete hostname bindings</span></span>

<span data-ttu-id="09862-229">在網域的左側功能表中，選取 [主機名稱繫結]。</span><span class="sxs-lookup"><span data-stu-id="09862-229">In the domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="09862-230">這裡會列出來自所有 Azure 服務的主機名稱繫結。</span><span class="sxs-lookup"><span data-stu-id="09862-230">The hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="09862-231">您必須先刪除所有主機名稱繫結，才能刪除 App Service 網域。</span><span class="sxs-lookup"><span data-stu-id="09862-231">You cannot delete the App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="09862-232">請透過選取 **...** > [刪除].來刪除每個主機名稱繫結。</span><span class="sxs-lookup"><span data-stu-id="09862-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="09862-233">刪除所有繫結之後，請選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="09862-233">After all the bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="09862-234">取消或刪除</span><span class="sxs-lookup"><span data-stu-id="09862-234">Cancel or delete</span></span>

<span data-ttu-id="09862-235">在網域的左側功能表中，選取 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="09862-235">In the domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="09862-236">如果已購買網域的取消期間尚未到期，請選取 [取消購買]。</span><span class="sxs-lookup"><span data-stu-id="09862-236">If the cancellation period on the purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="09862-237">否則，您會看到 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="09862-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="09862-238">若要在不退款情況下刪除網域，請選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="09862-238">To delete the domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="09862-239">選取 [確定] 來確認作業。</span><span class="sxs-lookup"><span data-stu-id="09862-239">Select **OK** to confirm the operation.</span></span> <span data-ttu-id="09862-240">如果您不想繼續，請按一下確認對話方塊之外的任何位置。</span><span class="sxs-lookup"><span data-stu-id="09862-240">If you don't want to proceed, click anywhere outside of the confirmation dialog.</span></span>

<span data-ttu-id="09862-241">作業完成之後，該網域就會從您的訂用帳戶中釋放，並可再次供任何人購買。</span><span class="sxs-lookup"><span data-stu-id="09862-241">After the operation is complete, the domain is released from your subscription and available for anyone to purchase again.</span></span> 
