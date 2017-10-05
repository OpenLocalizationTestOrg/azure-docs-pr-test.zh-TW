---
title: "建立及使用內部負載平衡器與 Azure App Service Environment"
description: "如何建立及使用隔離網際網路之 Azure App Service Environment 的詳細資料"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: e7f85aaf2d940f114248d5925a1e97fe0f6bda6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="e741c-103">建立及使用內部負載平衡器與 App Service Environment</span><span class="sxs-lookup"><span data-stu-id="e741c-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="e741c-104">Azure App Service Environment (ASE) 是將 Azure App Service 部署到客戶 Azure 虛擬網路 (VNet) 中子網路的一種部署。</span><span class="sxs-lookup"><span data-stu-id="e741c-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="e741c-105">部署 App Service Environment (ASE) 有二種方法：</span><span class="sxs-lookup"><span data-stu-id="e741c-105">There are two ways to deploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="e741c-106">使用外部 IP 位址上的 VIP，通常稱為「外部 ASE」。</span><span class="sxs-lookup"><span data-stu-id="e741c-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="e741c-107">使用內部 IP 位址上的 VIP，通常稱為 「ILB ASE」，因為內部端點是內部負載平衡器 (ILB)。</span><span class="sxs-lookup"><span data-stu-id="e741c-107">With a VIP on an internal IP address, often called an ILB ASE because the internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="e741c-108">本文說明如何建立 ILB ASE。</span><span class="sxs-lookup"><span data-stu-id="e741c-108">This article shows you how to create an ILB ASE.</span></span> <span data-ttu-id="e741c-109">如需 ASE 的概述，請參閱 [App Service Environment 簡介][Intro]。</span><span class="sxs-lookup"><span data-stu-id="e741c-109">For an overview on the ASE, see [Introduction to App Service environments][Intro].</span></span> <span data-ttu-id="e741c-110">若要深了解如何建立外部 ASE，請參閱[建立外部 ASE][MakeExternalASE]。</span><span class="sxs-lookup"><span data-stu-id="e741c-110">To learn how to create an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="e741c-111">概觀</span><span class="sxs-lookup"><span data-stu-id="e741c-111">Overview</span></span> ##

<span data-ttu-id="e741c-112">您可以使用網際網路可存取端點或是您的 VNet 中的 IP 位址來部署 ASE。</span><span class="sxs-lookup"><span data-stu-id="e741c-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="e741c-113">為了將 IP 位址設定為 VNet 位址，ASE 必須與 ILB 一起部署。</span><span class="sxs-lookup"><span data-stu-id="e741c-113">To set the IP address to a VNet address, the ASE must be deployed with an ILB.</span></span> <span data-ttu-id="e741c-114">在部署 ASE 與 ILB 時，必須提供：</span><span class="sxs-lookup"><span data-stu-id="e741c-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="e741c-115">當您建立您的應用程式時，所使用的您自己的網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="e741c-116">用於 HTTPS 的憑證。</span><span class="sxs-lookup"><span data-stu-id="e741c-116">The certificate used for HTTPS.</span></span>
-   <span data-ttu-id="e741c-117">您的網域的 DNS 管理。</span><span class="sxs-lookup"><span data-stu-id="e741c-117">DNS management for your domain.</span></span>

<span data-ttu-id="e741c-118">相對的，您可以執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="e741c-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="e741c-119">在您可以透過「端對端」或 Azure ExpressRoute VPN 存取的雲端，安全地裝載內部網路應用程式。</span><span class="sxs-lookup"><span data-stu-id="e741c-119">Host intranet applications securely in the cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="e741c-120">在雲端裝載未在公用 DNS 伺服器中列出的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e741c-120">Host apps in the cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="e741c-121">建立與網際網路隔離，且您的前端 app 可以安全地與之整合的後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="e741c-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="e741c-122">已停用的功能</span><span class="sxs-lookup"><span data-stu-id="e741c-122">Disabled functionality</span></span> ###

<span data-ttu-id="e741c-123">使用 ILB ASE 時，有一些動作您無法執行：</span><span class="sxs-lookup"><span data-stu-id="e741c-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="e741c-124">使用以 IP 為主的 SSL。</span><span class="sxs-lookup"><span data-stu-id="e741c-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="e741c-125">將 IP 位址指派給特定應用程式。</span><span class="sxs-lookup"><span data-stu-id="e741c-125">Assign IP addresses to specific apps.</span></span>
-   <span data-ttu-id="e741c-126">透過 Azure 入口網站購買憑證並搭配應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="e741c-126">Buy and use a certificate with an app through the Azure portal.</span></span> <span data-ttu-id="e741c-127">您可以直接透過「憑證授權單位」取得憑證並搭配您的應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="e741c-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="e741c-128">您無法透過 Azure 入口網站取得它們。</span><span class="sxs-lookup"><span data-stu-id="e741c-128">You can't obtain them through the Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="e741c-129">建立 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="e741c-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="e741c-130">若要建立 ILB ASE：</span><span class="sxs-lookup"><span data-stu-id="e741c-130">To create an ILB ASE:</span></span>

1. <span data-ttu-id="e741c-131">在 Azure 入口網站中選取 [新增]  >  [Web + 行動]  >  [App Service Environment]。</span><span class="sxs-lookup"><span data-stu-id="e741c-131">In the Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="e741c-132">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e741c-132">Select your subscription.</span></span>

3. <span data-ttu-id="e741c-133">選取或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="e741c-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="e741c-134">選取或建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="e741c-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="e741c-135">如果您選取現有的 VNet，則需要建立子網路來存放 ASE。</span><span class="sxs-lookup"><span data-stu-id="e741c-135">If you select an existing VNet, you need to create a subnet to hold the ASE.</span></span> <span data-ttu-id="e741c-136">確定將子網路的大小設為足以容納 ASE 的任何未來成長。</span><span class="sxs-lookup"><span data-stu-id="e741c-136">Make sure to set a subnet size large enough to accommodate any future growth of your ASE.</span></span> <span data-ttu-id="e741c-137">建議的大小是 `/25`，具有 128 個位址，而且可以處理最大大小的 ASE。</span><span class="sxs-lookup"><span data-stu-id="e741c-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="e741c-138">您可以選取的大小下限是 `/28`。</span><span class="sxs-lookup"><span data-stu-id="e741c-138">The minimum size you can select is a `/28`.</span></span> <span data-ttu-id="e741c-139">滿足基礎結構的需求之後，這個大小可以調整至最多 11 個執行個體。</span><span class="sxs-lookup"><span data-stu-id="e741c-139">After infrastructure needs, this size can be scaled to a maximum of 11 instances.</span></span>

    * <span data-ttu-id="e741c-140">超過您的 App Service 方案中的預設上限 100 個執行個體。</span><span class="sxs-lookup"><span data-stu-id="e741c-140">Go beyond the default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="e741c-141">調整至接近 100，但其中較多快速前端調整。</span><span class="sxs-lookup"><span data-stu-id="e741c-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="e741c-142">選取 [虛擬網路/位置]  >  [虛擬網路設定]，</span><span class="sxs-lookup"><span data-stu-id="e741c-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="e741c-143">並將 [VIP 類型] 設定為 [內部]。</span><span class="sxs-lookup"><span data-stu-id="e741c-143">Set the **VIP Type** to **Internal**.</span></span>

7. <span data-ttu-id="e741c-144">輸入網域名稱。</span><span class="sxs-lookup"><span data-stu-id="e741c-144">Enter a domain name.</span></span> <span data-ttu-id="e741c-145">這個網域會成為在此 ASE 中建立之應用程式所使用的網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-145">This domain is the one used for apps created in this ASE.</span></span> <span data-ttu-id="e741c-146">有某些限制。</span><span class="sxs-lookup"><span data-stu-id="e741c-146">There are some restrictions.</span></span> <span data-ttu-id="e741c-147">不能是：</span><span class="sxs-lookup"><span data-stu-id="e741c-147">It can't be:</span></span>

    * <span data-ttu-id="e741c-148">net</span><span class="sxs-lookup"><span data-stu-id="e741c-148">net</span></span>   

    * <span data-ttu-id="e741c-149">azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="e741c-149">azurewebsites.net</span></span>

    * <span data-ttu-id="e741c-150">p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="e741c-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="e741c-151">&lt;asename&gt;.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="e741c-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="e741c-152">應用程式使用的自訂網域名稱，與您的 ASE 使用的網域名稱不可重疊。</span><span class="sxs-lookup"><span data-stu-id="e741c-152">The custom domain name used for apps and the domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="e741c-153">若 ILB ASE 的網域名稱為 contoso.com，則您的應用程式不能使用像這樣的自訂網域名稱：</span><span class="sxs-lookup"><span data-stu-id="e741c-153">For an ILB ASE with the domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="e741c-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e741c-154">www.contoso.com</span></span>

    * <span data-ttu-id="e741c-155">abcd.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e741c-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="e741c-156">abcd.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e741c-156">abcd.contoso.com</span></span>

   <span data-ttu-id="e741c-157">如果您知道您的應用程式自訂網域名稱，請為 ILB ASE 選擇不會與這些自訂網域名稱相衝突的網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-157">If you know the custom domain names for your apps, choose a domain for the ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="e741c-158">在此範例中，您可以為您的 ASE 使用類似 contoso internal.com 的網域，因為不會與 contoso.com結尾的自訂網域名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="e741c-158">In this example, you can use something like *contoso-internal.com* for the domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="e741c-159">選取 [確定]，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="e741c-159">Select **OK**, and then select **Create**.</span></span>

    ![ASE 建立][1]

<span data-ttu-id="e741c-161">在 [虛擬網路] 刀鋒視窗中，會有一個 [虛擬網路設定] 選項。</span><span class="sxs-lookup"><span data-stu-id="e741c-161">On the **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="e741c-162">您可以用來選擇 [外部 VIP] 或 [內部 VIP]。</span><span class="sxs-lookup"><span data-stu-id="e741c-162">You can use it to select an External VIP or an Internal VIP.</span></span> <span data-ttu-id="e741c-163">預設為「外部」。</span><span class="sxs-lookup"><span data-stu-id="e741c-163">The default is **External**.</span></span> <span data-ttu-id="e741c-164">如果您選取 [外部]，您的 ASE 會使用一個網際網路可存取的 VIP。</span><span class="sxs-lookup"><span data-stu-id="e741c-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="e741c-165">如果您選取 [內部]，您的 ASE 會使用您的 VNet 內 IP 位址搭配 ILB 進行設定。</span><span class="sxs-lookup"><span data-stu-id="e741c-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="e741c-166">選取 [內部] 之後，系統會移除把更多 IP 位址新增至您 ASE 的功能。</span><span class="sxs-lookup"><span data-stu-id="e741c-166">After you select **Internal**, the ability to add more IP addresses to your ASE is removed.</span></span> <span data-ttu-id="e741c-167">取而代之的是您必須提供 ASE 的網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-167">Instead, you need to provide the domain of the ASE.</span></span> <span data-ttu-id="e741c-168">在使用外部 VIP 的 ASE 中，ASE 的名稱會在網域中用於在該 ASE 中建立的 app。</span><span class="sxs-lookup"><span data-stu-id="e741c-168">In an ASE with an External VIP, the name of the ASE is used in the domain for apps created in that ASE.</span></span>

<span data-ttu-id="e741c-169">如果您將 [VIP 類型] 設定為 [內部]，您的 ASE 名稱不會在 ASE 的網域中使用。</span><span class="sxs-lookup"><span data-stu-id="e741c-169">If you set **VIP Type** to **Internal**, your ASE name is not used in the domain for the ASE.</span></span> <span data-ttu-id="e741c-170">您可以明確地指定網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-170">You specify the domain explicitly.</span></span> <span data-ttu-id="e741c-171">如果您的網域是 contoso.corp.net 而您在該 ASE 中建立一個名為 timereporting 的應用程式，該應用程式的 URL 會是 timereporting.contoso.corp.net。</span><span class="sxs-lookup"><span data-stu-id="e741c-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, the URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="e741c-172">在 ILB ASE 中建立應用程式：</span><span class="sxs-lookup"><span data-stu-id="e741c-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="e741c-173">在 ILB ASE 中建立應用程式的做法，與在 ASE 中建立應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="e741c-173">You create an app in an ILB ASE in the same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="e741c-174">在 Azure 入口網站選取 [新增]  >  [Web + 行動]  >  [Web] 或 [行動]，或者 [API 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e741c-174">In the Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="e741c-175">輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="e741c-175">Enter the name of the app.</span></span>

3. <span data-ttu-id="e741c-176">選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e741c-176">Select the subscription.</span></span>

4. <span data-ttu-id="e741c-177">選取或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="e741c-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="e741c-178">選取或建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="e741c-178">Select or create an App Service plan.</span></span> <span data-ttu-id="e741c-179">如果您想建立新的 App Service 方案，請選取您的 ASE 作為位置。</span><span class="sxs-lookup"><span data-stu-id="e741c-179">If you want to create a new App Service plan, select your ASE as the location.</span></span> <span data-ttu-id="e741c-180">選取您想要建立 App Service 方案的背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="e741c-180">Select the worker pool where you want your App Service plan to be created.</span></span> <span data-ttu-id="e741c-181">當您建立 App Service 方案時，選取您的 ASE 作為位置與背景工作角色集區。</span><span class="sxs-lookup"><span data-stu-id="e741c-181">When you create the App Service plan, select your ASE as the location and the worker pool.</span></span> <span data-ttu-id="e741c-182">指定應用程式的名稱時，會看見您的應用程式名稱底下的網域已被您的 ASE 網域取代。</span><span class="sxs-lookup"><span data-stu-id="e741c-182">When you specify the name of the app, the domain under your app name is replaced by the domain for your ASE.</span></span>

6. <span data-ttu-id="e741c-183">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="e741c-183">Select **Create**.</span></span> <span data-ttu-id="e741c-184">如果希望應用程式顯示在儀表板上，選取 [釘選到儀表板] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e741c-184">If you want the app to appear on your dashboard, select the **Pin to dashboard** check box.</span></span>

    ![App Service 方案建立][2]

    <span data-ttu-id="e741c-186">在 [應用程式名稱] 底下，網域名稱會更新，以反映您的 ASE 網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-186">Under **App name**, the domain name is updated to reflect the domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="e741c-187">ILB ASE 建立後驗證</span><span class="sxs-lookup"><span data-stu-id="e741c-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="e741c-188">ILB ASE 與非 ILB ASE 稍微有些不同。</span><span class="sxs-lookup"><span data-stu-id="e741c-188">An ILB ASE is slightly different than the non-ILB ASE.</span></span> <span data-ttu-id="e741c-189">如先前所述，您需要管理自己的 DNS。</span><span class="sxs-lookup"><span data-stu-id="e741c-189">As already noted, you need to manage your own DNS.</span></span> <span data-ttu-id="e741c-190">您也必須提供您自己的 HTTPS 連線憑證。</span><span class="sxs-lookup"><span data-stu-id="e741c-190">You also have to provide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="e741c-191">建立 ASE 之後，網域名稱會顯示您所指定的網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-191">After you create your ASE, the domain name shows the domain you specified.</span></span> <span data-ttu-id="e741c-192">在 [設定] 功能表中會出現新的項目 [ILB 憑證]。</span><span class="sxs-lookup"><span data-stu-id="e741c-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="e741c-193">ASE 使用憑證建立，該憑證未指定 ILB ASE 網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-193">The ASE is created with a certificate that doesn't specify the ILB ASE domain.</span></span> <span data-ttu-id="e741c-194">如果您使用 ASE 與該憑證，您的瀏覽器會告訴您它是無效的。</span><span class="sxs-lookup"><span data-stu-id="e741c-194">If you use the ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="e741c-195">此憑證可讓您更輕鬆地測試 HTTPS，但您必須上傳您自己的繫結至 ILB ASE 網域的憑證。</span><span class="sxs-lookup"><span data-stu-id="e741c-195">This certificate makes it easier to test HTTPS, but you need to upload your own certificate that's tied to your ILB ASE domain.</span></span> <span data-ttu-id="e741c-196">無論您的憑證是自我簽署或是從憑證授權單位取得，這個步驟都是必要的。</span><span class="sxs-lookup"><span data-stu-id="e741c-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![ILB ASE 網域名稱][3]

<span data-ttu-id="e741c-198">您的 ILB ASE 需要有效的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="e741c-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="e741c-199">使用內部憑證授權單位、向外部簽發者購買憑證、或使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="e741c-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="e741c-200">無論 SSL 憑證的來源，都需要正確設定下列憑證屬性︰</span><span class="sxs-lookup"><span data-stu-id="e741c-200">Regardless of the source of the SSL certificate, the following certificate attributes need to be configured properly:</span></span>

* <span data-ttu-id="e741c-201">**Subject**︰此屬性必須設為 *.your-root-domain-here。</span><span class="sxs-lookup"><span data-stu-id="e741c-201">**Subject**: This attribute must be set to *.your-root-domain-here.</span></span>
* <span data-ttu-id="e741c-202">**Subject Alternative Name**︰此屬性必須同時包含 *.your-root-domain-here 和 *.scm.your-root-domain-here。</span><span class="sxs-lookup"><span data-stu-id="e741c-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="e741c-203">系統將使用 your-app-name.scm.your-root-domain-here 形式的位址，進行與每個應用程式相關聯的 SCM/Kudu 網站的 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="e741c-203">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="e741c-204">將 SSL 憑證轉換/儲存為 .pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="e741c-204">Convert/save the SSL certificate as a .pfx file.</span></span> <span data-ttu-id="e741c-205">.pfx 檔案必須包含所有中繼和根憑證。</span><span class="sxs-lookup"><span data-stu-id="e741c-205">The .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="e741c-206">使用密碼保護其安全。</span><span class="sxs-lookup"><span data-stu-id="e741c-206">Secure it with a password.</span></span>

<span data-ttu-id="e741c-207">如果您想要建立自我簽署憑證，可以使用這裡的 PowerShell命令。</span><span class="sxs-lookup"><span data-stu-id="e741c-207">If you want to create a self-signed certificate, you can use the PowerShell commands here.</span></span> <span data-ttu-id="e741c-208">務必使用您的 ILB ASE 網域名稱，而不是 internal.contoso.com：</span><span class="sxs-lookup"><span data-stu-id="e741c-208">Be sure to use your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="e741c-209">這些 PowerShell 命令產生的憑證會被瀏覽器標示，因為憑證不是由瀏覽器信任鏈結中的憑證授權單位建立。</span><span class="sxs-lookup"><span data-stu-id="e741c-209">The certificate that these PowerShell commands generate is flagged by browsers because the certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="e741c-210">若要取得瀏覽器信任的憑證，可向瀏覽器信任鏈結中的商業憑證授權單位購買。</span><span class="sxs-lookup"><span data-stu-id="e741c-210">To get a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![設定 ILB 憑證][4]

<span data-ttu-id="e741c-212">若要上傳您自己的憑證並測試存取：</span><span class="sxs-lookup"><span data-stu-id="e741c-212">To upload your own certificates and test access:</span></span>

1. <span data-ttu-id="e741c-213">建立 ASE 之後，移至 ASE UI。</span><span class="sxs-lookup"><span data-stu-id="e741c-213">After the ASE is created, go to the ASE UI.</span></span> <span data-ttu-id="e741c-214">選取 [ASE]  >  [設定]  >  [ILB 憑證]。</span><span class="sxs-lookup"><span data-stu-id="e741c-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="e741c-215">若要設定 ILB 憑證，選取憑證的 .pfx 檔案並輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="e741c-215">To set the ILB certificate, select the certificate .pfx file and enter the password.</span></span> <span data-ttu-id="e741c-216">這個步驟需要一些處理時間。</span><span class="sxs-lookup"><span data-stu-id="e741c-216">This step takes some time to process.</span></span> <span data-ttu-id="e741c-217">會出現訊息指出上傳作業正在進行中。</span><span class="sxs-lookup"><span data-stu-id="e741c-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="e741c-218">取得 ASE 的 ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="e741c-218">Get the ILB address for your ASE.</span></span> <span data-ttu-id="e741c-219">選取 [ASE]  >  [屬性]  >  [虛擬 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="e741c-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="e741c-220">建立您的 ASE 後，在 ASE 中建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e741c-220">Create a web app in your ASE after the ASE is created.</span></span>

5. <span data-ttu-id="e741c-221">如果您在該 VNet 中還沒有 VM，則建立 VM。</span><span class="sxs-lookup"><span data-stu-id="e741c-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e741c-222">請勿嘗試在與 ASE 相同的子網路中建立此 VM，因為會失敗或造成問題。</span><span class="sxs-lookup"><span data-stu-id="e741c-222">Don't try to create this VM in the same subnet as the ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="e741c-223">設定 ASE 網域的 DNS。</span><span class="sxs-lookup"><span data-stu-id="e741c-223">Set the DNS for your ASE domain.</span></span> <span data-ttu-id="e741c-224">您可以在您的 DNS 中使用萬用字元搭配您的網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="e741c-225">若要執行一些簡單測試，請編輯 VM 上的主機檔案來將 Web 應用程式名稱設定為 VIP IP 位址：</span><span class="sxs-lookup"><span data-stu-id="e741c-225">To do some simple tests, edit the hosts file on your VM to set the web app name to the VIP IP address:</span></span>

    <span data-ttu-id="e741c-226">a.</span><span class="sxs-lookup"><span data-stu-id="e741c-226">a.</span></span> <span data-ttu-id="e741c-227">如果您的 ASE 網域名稱為 .ilbase.com，且您建立名為 mytestapp 的 Web 應用程式，則它將定址為 mytestapp.ilbase.com。然後，您設定 mytestapp.ilbase.com 以解析 ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="e741c-227">If your ASE has the domain name _.ilbase.com_ and you create the web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ to resolve to the ILB address.</span></span> <span data-ttu-id="e741c-228">(在 Windows 上，主機檔案位於 _C:\Windows\System32\drivers\etc\_。)</span><span class="sxs-lookup"><span data-stu-id="e741c-228">(On Windows, the hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="e741c-229">b.</span><span class="sxs-lookup"><span data-stu-id="e741c-229">b.</span></span> <span data-ttu-id="e741c-230">若要測試 Web 部署發佈或存取進階主控台，建立 mytestapp.scm.ilbase.com 的記錄。</span><span class="sxs-lookup"><span data-stu-id="e741c-230">To test web deployment publishing or access to the advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="e741c-231">在該 VM 上使用瀏覽器並移至 http://mytestapp.ilbase.com。(或移至任何名稱含您的網域的 Web 應用程式。)</span><span class="sxs-lookup"><span data-stu-id="e741c-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go to whatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="e741c-232">在該 VM 上使用瀏覽器並移至 https://mytestapp.ilbase.com。如果您使用自我簽署憑證，就必須接受安全性不足。</span><span class="sxs-lookup"><span data-stu-id="e741c-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept the lack of security.</span></span>

    <span data-ttu-id="e741c-233">您的 ILB IP 位址列在 [IP 位址] 底下。</span><span class="sxs-lookup"><span data-stu-id="e741c-233">The IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="e741c-234">此清單中也有外部 VIP 使用的 IP 位址以及用於輸入管理流量的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e741c-234">This list also has the IP addresses used by the external VIP and for inbound management traffic.</span></span>

    ![ILB IP 位址][5]

### <a name="web-jobs-functions-and-the-ilb-ase"></a><span data-ttu-id="e741c-236">Web 工作、函式和 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="e741c-236">Web jobs, Functions and the ILB ASE</span></span>

<span data-ttu-id="e741c-237">ILB ASE 支援函式和 Web 工作，但若要讓入口網站可以使用，您必須具有 SCM 網站的網路存取。</span><span class="sxs-lookup"><span data-stu-id="e741c-237">Both Functions and web jobs are supported on an ILB ASE but for the portal to work with them, you must have network access to the SCM site.</span></span>  <span data-ttu-id="e741c-238">這表示您的瀏覽器必須在主機上，或是在虛擬網路中或已連線到虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e741c-238">This means your browser must either be on a host that is either in or connected to the virtual network.</span></span>  

<span data-ttu-id="e741c-239">當您在 ILB ASE 中使用 Azure Functions 時，可能會遇到錯誤，指出「我們無法立即擷取您的函式。</span><span class="sxs-lookup"><span data-stu-id="e741c-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able to retrieve your functions right now.</span></span> <span data-ttu-id="e741c-240">請稍後再試。」</span><span class="sxs-lookup"><span data-stu-id="e741c-240">Please try again later."</span></span> <span data-ttu-id="e741c-241">由於 Functions UI 透過 HTTPS 利用 SCM 網站，而且根憑證不在瀏覽器信任鏈結中，因此會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e741c-241">This error occurs because the Functions UI leverages the SCM site over HTTPS and the root certificate is not in the browser chain of trust.</span></span> <span data-ttu-id="e741c-242">Web 工作具有類似的問題。</span><span class="sxs-lookup"><span data-stu-id="e741c-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="e741c-243">若要避免此問題，您可以執行下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="e741c-243">To avoid this problem you can do one of the following:</span></span>

- <span data-ttu-id="e741c-244">將憑證新增至您的信任憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="e741c-244">Add the certificate to your trusted certificate store.</span></span> <span data-ttu-id="e741c-245">這會解除封鎖 Edge 及 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="e741c-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="e741c-246">先使用 Chrome 並前往 SCM 網站，接受不受信任的憑證，然後前往入口網站。</span><span class="sxs-lookup"><span data-stu-id="e741c-246">Use Chrome and go to the SCM site first, accept the untrusted certificate and then go to the portal.</span></span>
- <span data-ttu-id="e741c-247">使用瀏覽器信任鏈結中的商業憑證。</span><span class="sxs-lookup"><span data-stu-id="e741c-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="e741c-248">這是最佳選擇。</span><span class="sxs-lookup"><span data-stu-id="e741c-248">This is the best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="e741c-249">DNS 組態</span><span class="sxs-lookup"><span data-stu-id="e741c-249">DNS configuration</span></span> ##

<span data-ttu-id="e741c-250">當您使用外部 VIP，DNS 是由 Azure 管理。</span><span class="sxs-lookup"><span data-stu-id="e741c-250">When you use an External VIP, the DNS is managed by Azure.</span></span> <span data-ttu-id="e741c-251">在您 ASE 中建立的任何 app 都會自動新增至 Azure DNS，這是一個公用 DNS。</span><span class="sxs-lookup"><span data-stu-id="e741c-251">Any app created in your ASE is automatically added to Azure DNS, which is a public DNS.</span></span> <span data-ttu-id="e741c-252">在 ILB ASE 中，您必須管理您自己的 DNS。</span><span class="sxs-lookup"><span data-stu-id="e741c-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="e741c-253">針對指定的網域 (例如 _contoso.net_)，您必須為下列項目，在 DNS 中建立指向您 ILB 位址的 DNS A 記錄︰</span><span class="sxs-lookup"><span data-stu-id="e741c-253">For a given domain such as _contoso.net_, you need to create DNS A records in your DNS that point to your ILB address for:</span></span>

- <span data-ttu-id="e741c-254">*.contoso.net</span><span class="sxs-lookup"><span data-stu-id="e741c-254">*.contoso.net</span></span>
- <span data-ttu-id="e741c-255">*.scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="e741c-255">*.scm.contoso.net</span></span>

<span data-ttu-id="e741c-256">如果 ILB ASE 網域用於此 ASE 之外的多項作業，您可能需要針對每個應用程式名稱進行 DNS 管理。</span><span class="sxs-lookup"><span data-stu-id="e741c-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need to manage DNS on a per-app-name basis.</span></span> <span data-ttu-id="e741c-257">這個做法更有挑戰性，因為每當您建立應用程式時，必須將新的應用程式名稱新增至您的 DNS。</span><span class="sxs-lookup"><span data-stu-id="e741c-257">This method is challenging because you need to add each new app name into your DNS when you create it.</span></span> <span data-ttu-id="e741c-258">基於這個理由，建議使用專用網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="e741c-259">使用 ILB ASE 發佈</span><span class="sxs-lookup"><span data-stu-id="e741c-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="e741c-260">每一個建立的應用程式，都有兩個端點。</span><span class="sxs-lookup"><span data-stu-id="e741c-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="e741c-261">在 ILB ASE 中，您有 &lt;app name>.&lt;ILB ASE Domain> 和 &lt;app name>.scm.&lt;ILB ASE Domain>。</span><span class="sxs-lookup"><span data-stu-id="e741c-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="e741c-262">SCM 網站名稱會帶您前往 Azure 入口網站中的 Kudu 主控台，稱為 [進階入口網站]。</span><span class="sxs-lookup"><span data-stu-id="e741c-262">The SCM site name takes you to the Kudu console, called the **Advanced portal**, within the Azure portal.</span></span> <span data-ttu-id="e741c-263">Kudu 主控台可讓您檢視環境變數、探索磁碟、使用主控台等等。</span><span class="sxs-lookup"><span data-stu-id="e741c-263">The Kudu console lets you view environment variables, explore the disk, use a console, and much more.</span></span> <span data-ttu-id="e741c-264">如需詳細資訊，請參閱 [Azure App Service 的 Kudu 主控台][Kudu]。</span><span class="sxs-lookup"><span data-stu-id="e741c-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="e741c-265">在多租用戶 App Service 和外部 ASE 中，Azure 入口網站與 Kudu 主控台之間有單一登入。</span><span class="sxs-lookup"><span data-stu-id="e741c-265">In the multitenant App Service and in an External ASE, there's single sign-on between the Azure portal and the Kudu console.</span></span> <span data-ttu-id="e741c-266">不過，對於 ILB ASE，您必須使用發佈認證來登入 Kudu 主控台。</span><span class="sxs-lookup"><span data-stu-id="e741c-266">For the ILB ASE, however, you need to use your publishing credentials to sign into the Kudu console.</span></span>

<span data-ttu-id="e741c-267">以網際網路為基礎的 CI 系統 (例如 Github、Visual Studio Team Services) 不能與 ILB ASE 搭配運作，因為發佈端點不是網際網路可存取。</span><span class="sxs-lookup"><span data-stu-id="e741c-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because the publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="e741c-268">相反地，您需要使用會使用提取模型的 CI 系統，例如 Dropbox。</span><span class="sxs-lookup"><span data-stu-id="e741c-268">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="e741c-269">ILB ASE 中應用程式的發佈端點會使用用來建立 ILB ASE 的網域。</span><span class="sxs-lookup"><span data-stu-id="e741c-269">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="e741c-270">在應用程式的發行設定檔中，以及應用程式的入口網站刀鋒視窗中可以看到這個網域 (在 [概觀]  >  [基本資訊] 以及 [屬性] 中)。</span><span class="sxs-lookup"><span data-stu-id="e741c-270">This domain appears in the app's publishing profile and in the app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="e741c-271">如果您的 ILB ASE 具有子網域 contoso.net，且應用程式名為 mytest，則要在 FTP 中使用 mytest.contoso.net，在 Web 部署中使用 mytest.scm.contoso.net。</span><span class="sxs-lookup"><span data-stu-id="e741c-271">If you have an ILB ASE with the subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="e741c-272">將 ILB ASE 與 WAF 裝置耦合</span><span class="sxs-lookup"><span data-stu-id="e741c-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="e741c-273">Azure App Service 提供許多安全性措施來保護您的系統。</span><span class="sxs-lookup"><span data-stu-id="e741c-273">Azure App Service provides many security measures that protect the system.</span></span> <span data-ttu-id="e741c-274">它們也可協助您判斷應用程式是否遭到駭客入侵。</span><span class="sxs-lookup"><span data-stu-id="e741c-274">They also help to determine whether an app was hacked.</span></span> <span data-ttu-id="e741c-275">Web 應用程式的最佳保護是耦合裝載平台，例如 Azure App Service 與 Web 應用程式防火牆 (WAF)。</span><span class="sxs-lookup"><span data-stu-id="e741c-275">The best protection for a web application is to couple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="e741c-276">由於 ILB ASE 具有與網路隔離的應用程式端點，因此適合這樣的使用方式。</span><span class="sxs-lookup"><span data-stu-id="e741c-276">Because the ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="e741c-277">若要深入了解如何設定 ILB ASE 與 WAF 裝置，請參閱[使用 App Service Environment 設定 Web 應用程式防火牆][ASEWAF]。</span><span class="sxs-lookup"><span data-stu-id="e741c-277">To learn more about how to configure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="e741c-278">此文章說明如何搭配使用您的 ASE 與 Barracuda 虛擬應用裝置。</span><span class="sxs-lookup"><span data-stu-id="e741c-278">This article shows how to use a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="e741c-279">另一個選項是使用 Azure 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="e741c-279">Another option is to use Azure Application Gateway.</span></span> <span data-ttu-id="e741c-280">應用程式閘道會使用 OWASP 核心規則來保護後面的任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="e741c-280">Application Gateway uses the OWASP core rules to secure any applications placed behind it.</span></span> <span data-ttu-id="e741c-281">如需有關應用程式閘道的詳細資訊，請參閱 [Azure Web 應用程式防火牆簡介][AppGW]。</span><span class="sxs-lookup"><span data-stu-id="e741c-281">For more information about Application Gateway, see [Introduction to the Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="e741c-282">開始使用</span><span class="sxs-lookup"><span data-stu-id="e741c-282">Get started</span></span> ##

<span data-ttu-id="e741c-283">您可以在 [App Service Environment 的 README][ASEReadme] 中取得 App Service Environment 的所有相關文章與做法。</span><span class="sxs-lookup"><span data-stu-id="e741c-283">All articles and how-to instructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="e741c-284">若要開始使用ASE，請參閱 [App Service Environment 簡介][Intro]。</span><span class="sxs-lookup"><span data-stu-id="e741c-284">To get started with ASEs, see [Introduction to App Service environments][Intro].</span></span>
* <span data-ttu-id="e741c-285">如需有關 Azure App Service 平台的詳細資訊，請參閱 [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/)。</span><span class="sxs-lookup"><span data-stu-id="e741c-285">For more information about the Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
