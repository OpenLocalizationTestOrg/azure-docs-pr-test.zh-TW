---
title: "aaaCreate 與使用 Azure App Service 環境的內部負載平衡器"
description: "有關如何 toocreate 和使用網際網路隔離的 Azure App Service 環境"
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
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="db114-103">建立及使用內部負載平衡器與 App Service Environment</span><span class="sxs-lookup"><span data-stu-id="db114-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="db114-104">Azure App Service Environment (ASE) 是將 Azure App Service 部署到客戶 Azure 虛擬網路 (VNet) 中子網路的一種部署。</span><span class="sxs-lookup"><span data-stu-id="db114-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="db114-105">有兩種方式 toodeploy App Service 環境 (ASE):</span><span class="sxs-lookup"><span data-stu-id="db114-105">There are two ways toodeploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="db114-106">使用外部 IP 位址上的 VIP，通常稱為「外部 ASE」。</span><span class="sxs-lookup"><span data-stu-id="db114-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="db114-107">與內部 IP 位址上 VIP，通常稱為 ILB ASE 因為 hello 內部端點的內部負載平衡器 (ILB)。</span><span class="sxs-lookup"><span data-stu-id="db114-107">With a VIP on an internal IP address, often called an ILB ASE because hello internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="db114-108">本文章將示範如何 toocreate ILB ase。</span><span class="sxs-lookup"><span data-stu-id="db114-108">This article shows you how toocreate an ILB ASE.</span></span> <span data-ttu-id="db114-109">如需 hello ASE 的概觀，請參閱[簡介 tooApp 服務環境][Intro]。</span><span class="sxs-lookup"><span data-stu-id="db114-109">For an overview on hello ASE, see [Introduction tooApp Service environments][Intro].</span></span> <span data-ttu-id="db114-110">如何 toocreate 外部 ase 中，請參閱的 toolearn[建立外部 ASE][MakeExternalASE]。</span><span class="sxs-lookup"><span data-stu-id="db114-110">toolearn how toocreate an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="db114-111">概觀</span><span class="sxs-lookup"><span data-stu-id="db114-111">Overview</span></span> ##

<span data-ttu-id="db114-112">您可以使用網際網路可存取端點或是您的 VNet 中的 IP 位址來部署 ASE。</span><span class="sxs-lookup"><span data-stu-id="db114-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="db114-113">tooset hello IP 位址 tooa VNet 位址，hello ASE 必須部署搭配 ILB 一起運作。</span><span class="sxs-lookup"><span data-stu-id="db114-113">tooset hello IP address tooa VNet address, hello ASE must be deployed with an ILB.</span></span> <span data-ttu-id="db114-114">在部署 ASE 與 ILB 時，必須提供：</span><span class="sxs-lookup"><span data-stu-id="db114-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="db114-115">當您建立您的應用程式時，所使用的您自己的網域。</span><span class="sxs-lookup"><span data-stu-id="db114-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="db114-116">hello HTTPS 所用的憑證。</span><span class="sxs-lookup"><span data-stu-id="db114-116">hello certificate used for HTTPS.</span></span>
-   <span data-ttu-id="db114-117">您的網域的 DNS 管理。</span><span class="sxs-lookup"><span data-stu-id="db114-117">DNS management for your domain.</span></span>

<span data-ttu-id="db114-118">相對的，您可以執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="db114-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="db114-119">安全地在 hello 雲端，您可以透過站對站或 Azure ExpressRoute VPN 存取主機內部網路應用程式。</span><span class="sxs-lookup"><span data-stu-id="db114-119">Host intranet applications securely in hello cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="db114-120">主機的應用程式 hello 雲端中未列出的公用 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="db114-120">Host apps in hello cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="db114-121">建立與網際網路隔離，且您的前端 app 可以安全地與之整合的後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="db114-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="db114-122">已停用的功能</span><span class="sxs-lookup"><span data-stu-id="db114-122">Disabled functionality</span></span> ###

<span data-ttu-id="db114-123">使用 ILB ASE 時，有一些動作您無法執行：</span><span class="sxs-lookup"><span data-stu-id="db114-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="db114-124">使用以 IP 為主的 SSL。</span><span class="sxs-lookup"><span data-stu-id="db114-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="db114-125">指派 IP 位址 toospecific 應用程式。</span><span class="sxs-lookup"><span data-stu-id="db114-125">Assign IP addresses toospecific apps.</span></span>
-   <span data-ttu-id="db114-126">購買和使用憑證與透過 hello Azure 入口網站應用程式。</span><span class="sxs-lookup"><span data-stu-id="db114-126">Buy and use a certificate with an app through hello Azure portal.</span></span> <span data-ttu-id="db114-127">您可以直接透過「憑證授權單位」取得憑證並搭配您的應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="db114-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="db114-128">您無法透過 hello Azure 入口網站來取得它們。</span><span class="sxs-lookup"><span data-stu-id="db114-128">You can't obtain them through hello Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="db114-129">建立 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="db114-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="db114-130">toocreate ILB ase 中：</span><span class="sxs-lookup"><span data-stu-id="db114-130">toocreate an ILB ASE:</span></span>

1. <span data-ttu-id="db114-131">在 hello Azure 入口網站，選取 **新增** > **Web + 行動** > **App Service 環境**。</span><span class="sxs-lookup"><span data-stu-id="db114-131">In hello Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="db114-132">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="db114-132">Select your subscription.</span></span>

3. <span data-ttu-id="db114-133">選取或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="db114-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="db114-134">選取或建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="db114-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="db114-135">如果您選取現有的 VNet，您需要的子網路 toohold hello ASE toocreate。</span><span class="sxs-lookup"><span data-stu-id="db114-135">If you select an existing VNet, you need toocreate a subnet toohold hello ASE.</span></span> <span data-ttu-id="db114-136">請確定 tooset 子網路的大小夠大 tooaccommodate 未來成長的您 ASE。</span><span class="sxs-lookup"><span data-stu-id="db114-136">Make sure tooset a subnet size large enough tooaccommodate any future growth of your ASE.</span></span> <span data-ttu-id="db114-137">建議的大小是 `/25`，具有 128 個位址，而且可以處理最大大小的 ASE。</span><span class="sxs-lookup"><span data-stu-id="db114-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="db114-138">hello 最小的大小，您可以選取`/28`。</span><span class="sxs-lookup"><span data-stu-id="db114-138">hello minimum size you can select is a `/28`.</span></span> <span data-ttu-id="db114-139">需要基礎結構之後，這個大小可能會縮放的 tooa 最大值為 11 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="db114-139">After infrastructure needs, this size can be scaled tooa maximum of 11 instances.</span></span>

    * <span data-ttu-id="db114-140">在您的應用程式服務計劃超越 hello 的 100 個執行個體的預設最大值。</span><span class="sxs-lookup"><span data-stu-id="db114-140">Go beyond hello default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="db114-141">調整至接近 100，但其中較多快速前端調整。</span><span class="sxs-lookup"><span data-stu-id="db114-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="db114-142">選取 [虛擬網路/位置]  >  [虛擬網路設定]，</span><span class="sxs-lookup"><span data-stu-id="db114-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="db114-143">設定 hello **VIP 類型**太**內部**。</span><span class="sxs-lookup"><span data-stu-id="db114-143">Set hello **VIP Type** too**Internal**.</span></span>

7. <span data-ttu-id="db114-144">輸入網域名稱。</span><span class="sxs-lookup"><span data-stu-id="db114-144">Enter a domain name.</span></span> <span data-ttu-id="db114-145">此網域為 hello 用於此 ASE 中建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="db114-145">This domain is hello one used for apps created in this ASE.</span></span> <span data-ttu-id="db114-146">有某些限制。</span><span class="sxs-lookup"><span data-stu-id="db114-146">There are some restrictions.</span></span> <span data-ttu-id="db114-147">不能是：</span><span class="sxs-lookup"><span data-stu-id="db114-147">It can't be:</span></span>

    * <span data-ttu-id="db114-148">net</span><span class="sxs-lookup"><span data-stu-id="db114-148">net</span></span>   

    * <span data-ttu-id="db114-149">azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="db114-149">azurewebsites.net</span></span>

    * <span data-ttu-id="db114-150">p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="db114-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="db114-151">&lt;asename&gt;.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="db114-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="db114-152">hello 自訂網域名稱用於應用程式，供您 ASE hello 網域名稱不能重疊。</span><span class="sxs-lookup"><span data-stu-id="db114-152">hello custom domain name used for apps and hello domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="db114-153">針對 ILB ase 中 hello 網域名稱與_contoso.com_，您無法使用您的應用程式，類似的自訂網域名稱：</span><span class="sxs-lookup"><span data-stu-id="db114-153">For an ILB ASE with hello domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="db114-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="db114-154">www.contoso.com</span></span>

    * <span data-ttu-id="db114-155">abcd.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="db114-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="db114-156">abcd.contoso.com</span><span class="sxs-lookup"><span data-stu-id="db114-156">abcd.contoso.com</span></span>

   <span data-ttu-id="db114-157">如果您知道您的應用程式的 hello 自訂網域名稱，選擇 不需要使用這些自訂網域名稱衝突的 ILB ASE hello 的網域。</span><span class="sxs-lookup"><span data-stu-id="db114-157">If you know hello custom domain names for your apps, choose a domain for hello ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="db114-158">在此範例中，您可以使用類似*contoso internal.com* hello 網域的 ASE 您因為不會衝突的自訂網域名稱結尾*。 contoso.com*。</span><span class="sxs-lookup"><span data-stu-id="db114-158">In this example, you can use something like *contoso-internal.com* for hello domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="db114-159">選取 [確定]，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="db114-159">Select **OK**, and then select **Create**.</span></span>

    ![ASE 建立][1]

<span data-ttu-id="db114-161">在 hello**虛擬網路**刀鋒視窗中，有**虛擬網路組態**選項。</span><span class="sxs-lookup"><span data-stu-id="db114-161">On hello **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="db114-162">您可以使用 tooselect 外部 VIP 或 VIP 內部。</span><span class="sxs-lookup"><span data-stu-id="db114-162">You can use it tooselect an External VIP or an Internal VIP.</span></span> <span data-ttu-id="db114-163">hello 預設值是**外部**。</span><span class="sxs-lookup"><span data-stu-id="db114-163">hello default is **External**.</span></span> <span data-ttu-id="db114-164">如果您選取 [外部]，您的 ASE 會使用一個網際網路可存取的 VIP。</span><span class="sxs-lookup"><span data-stu-id="db114-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="db114-165">如果您選取 [內部]，您的 ASE 會使用您的 VNet 內 IP 位址搭配 ILB 進行設定。</span><span class="sxs-lookup"><span data-stu-id="db114-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="db114-166">選取後**內部**，hello 能力 tooadd 多個 IP 位址的 tooyour ASE 已移除。</span><span class="sxs-lookup"><span data-stu-id="db114-166">After you select **Internal**, hello ability tooadd more IP addresses tooyour ASE is removed.</span></span> <span data-ttu-id="db114-167">相反地，您需要 hello ASE tooprovide hello 的網域。</span><span class="sxs-lookup"><span data-stu-id="db114-167">Instead, you need tooprovide hello domain of hello ASE.</span></span> <span data-ttu-id="db114-168">在 ase 中與外部 VIP，hello hello ASE 在 hello 網域用於該 ASE 中建立的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="db114-168">In an ASE with an External VIP, hello name of hello ASE is used in hello domain for apps created in that ASE.</span></span>

<span data-ttu-id="db114-169">如果您設定**VIP 類型**太**內部**，ASE 名稱不是 hello 網域中的 hello ASE。</span><span class="sxs-lookup"><span data-stu-id="db114-169">If you set **VIP Type** too**Internal**, your ASE name is not used in hello domain for hello ASE.</span></span> <span data-ttu-id="db114-170">您可以明確地指定 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="db114-170">You specify hello domain explicitly.</span></span> <span data-ttu-id="db114-171">如果您的網域是*contoso.corp.net*和您建立的應用程式，名為 ASE *timereporting*，該應用程式是 timereporting.contoso.corp.net hello URL。</span><span class="sxs-lookup"><span data-stu-id="db114-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, hello URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="db114-172">在 ILB ASE 中建立應用程式：</span><span class="sxs-lookup"><span data-stu-id="db114-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="db114-173">您在中 hello ILB ase 中建立的應用程式，您建立應用程式在 ase 中正常的方式相同。</span><span class="sxs-lookup"><span data-stu-id="db114-173">You create an app in an ILB ASE in hello same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="db114-174">在 hello Azure 入口網站，選取 **新增** > **Web + 行動** > **Web**或**行動**或**API 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="db114-174">In hello Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="db114-175">輸入 hello hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="db114-175">Enter hello name of hello app.</span></span>

3. <span data-ttu-id="db114-176">選取 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="db114-176">Select hello subscription.</span></span>

4. <span data-ttu-id="db114-177">選取或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="db114-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="db114-178">選取或建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="db114-178">Select or create an App Service plan.</span></span> <span data-ttu-id="db114-179">如果您想 toocreate 新的 App Service 方案，請選取您 ASE 做為 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="db114-179">If you want toocreate a new App Service plan, select your ASE as hello location.</span></span> <span data-ttu-id="db114-180">選取您想要建立您的應用程式服務計劃 toobe hello 背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="db114-180">Select hello worker pool where you want your App Service plan toobe created.</span></span> <span data-ttu-id="db114-181">當您建立 hello 應用程式服務方案時，選取您 ASE hello 位置和 hello 背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="db114-181">When you create hello App Service plan, select your ASE as hello location and hello worker pool.</span></span> <span data-ttu-id="db114-182">當您指定 hello hello 應用程式名稱時，在您的應用程式名稱的 hello 定義域已取代 hello 網域您 ASE。</span><span class="sxs-lookup"><span data-stu-id="db114-182">When you specify hello name of hello app, hello domain under your app name is replaced by hello domain for your ASE.</span></span>

6. <span data-ttu-id="db114-183">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="db114-183">Select **Create**.</span></span> <span data-ttu-id="db114-184">如果您想 hello 應用程式 tooappear 儀表板上，選取**Pin toodashboard**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="db114-184">If you want hello app tooappear on your dashboard, select the **Pin toodashboard** check box.</span></span>

    ![App Service 方案建立][2]

    <span data-ttu-id="db114-186">在下**應用程式名稱**，hello 網域名稱是您 ASE 更新的 tooreflect hello 網域。</span><span class="sxs-lookup"><span data-stu-id="db114-186">Under **App name**, hello domain name is updated tooreflect hello domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="db114-187">ILB ASE 建立後驗證</span><span class="sxs-lookup"><span data-stu-id="db114-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="db114-188">ILB ase 中有些許不同比 hello 非-ILB ASE。</span><span class="sxs-lookup"><span data-stu-id="db114-188">An ILB ASE is slightly different than hello non-ILB ASE.</span></span> <span data-ttu-id="db114-189">如先前所述，您需要 toomanage 自己的 DNS。</span><span class="sxs-lookup"><span data-stu-id="db114-189">As already noted, you need toomanage your own DNS.</span></span> <span data-ttu-id="db114-190">您也可以 tooprovide 供 HTTPS 連線憑證。</span><span class="sxs-lookup"><span data-stu-id="db114-190">You also have tooprovide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="db114-191">建立您 ASE 之後，hello 網域名稱會顯示您所指定的 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="db114-191">After you create your ASE, hello domain name shows hello domain you specified.</span></span> <span data-ttu-id="db114-192">在 [設定] 功能表中會出現新的項目 [ILB 憑證]。</span><span class="sxs-lookup"><span data-stu-id="db114-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="db114-193">hello ASE 會建立未指定 hello ILB ASE 網域的憑證。</span><span class="sxs-lookup"><span data-stu-id="db114-193">hello ASE is created with a certificate that doesn't specify hello ILB ASE domain.</span></span> <span data-ttu-id="db114-194">如果您使用 hello ASE 與該憑證時，您的瀏覽器會告訴您它無效。</span><span class="sxs-lookup"><span data-stu-id="db114-194">If you use hello ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="db114-195">此憑證可讓您更輕鬆 tootest HTTPS，但您需要 tooupload 自己是繫結的 tooyour ILB ASE 網域的憑證。</span><span class="sxs-lookup"><span data-stu-id="db114-195">This certificate makes it easier tootest HTTPS, but you need tooupload your own certificate that's tied tooyour ILB ASE domain.</span></span> <span data-ttu-id="db114-196">無論您的憑證是自我簽署或是從憑證授權單位取得，這個步驟都是必要的。</span><span class="sxs-lookup"><span data-stu-id="db114-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![ILB ASE 網域名稱][3]

<span data-ttu-id="db114-198">您的 ILB ASE 需要有效的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="db114-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="db114-199">使用內部憑證授權單位、向外部簽發者購買憑證、或使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="db114-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="db114-200">Hello hello SSL 憑證的來源，不論 hello 下列憑證的屬性皆需要 toobe 正確設定：</span><span class="sxs-lookup"><span data-stu-id="db114-200">Regardless of hello source of hello SSL certificate, hello following certificate attributes need toobe configured properly:</span></span>

* <span data-ttu-id="db114-201">**主旨**: too*.your 根網域-這裡必須設定這個屬性。</span><span class="sxs-lookup"><span data-stu-id="db114-201">**Subject**: This attribute must be set too*.your-root-domain-here.</span></span>
* <span data-ttu-id="db114-202">**Subject Alternative Name**︰此屬性必須同時包含 *.your-root-domain-here 和 *.scm.your-root-domain-here。</span><span class="sxs-lookup"><span data-stu-id="db114-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="db114-203">與每個應用程式關聯的 SCM/Kudu 站台的 SSL 連線 toohello 使用 hello 表單的位址*your-app-name.scm.your-root-domain-here*。</span><span class="sxs-lookup"><span data-stu-id="db114-203">SSL connections toohello SCM/Kudu site associated with each app use an address of hello form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="db114-204">轉換/儲存為.pfx 檔案 hello SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="db114-204">Convert/save hello SSL certificate as a .pfx file.</span></span> <span data-ttu-id="db114-205">hello.pfx 檔案必須包含所有中繼和根憑證。</span><span class="sxs-lookup"><span data-stu-id="db114-205">hello .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="db114-206">使用密碼保護其安全。</span><span class="sxs-lookup"><span data-stu-id="db114-206">Secure it with a password.</span></span>

<span data-ttu-id="db114-207">如果您想 toocreate 自我簽署憑證，您可以在這裡使用 hello PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="db114-207">If you want toocreate a self-signed certificate, you can use hello PowerShell commands here.</span></span> <span data-ttu-id="db114-208">ILB ASE 網域名稱，而不是要確定 toouse *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="db114-208">Be sure toouse your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="db114-209">下列 PowerShell 命令產生的 hello 憑證會標示瀏覽器，因為 hello 憑證不建立您的瀏覽器信任鏈結中的憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="db114-209">hello certificate that these PowerShell commands generate is flagged by browsers because hello certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="db114-210">tooget 的憑證，您的瀏覽器信任，採購它從您的瀏覽器信任鏈結中的商業憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="db114-210">tooget a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![設定 ILB 憑證][4]

<span data-ttu-id="db114-212">tooupload 您自己的憑證及測試存取：</span><span class="sxs-lookup"><span data-stu-id="db114-212">tooupload your own certificates and test access:</span></span>

1. <span data-ttu-id="db114-213">建立 hello ASE 之後，請移 toohello ASE UI。</span><span class="sxs-lookup"><span data-stu-id="db114-213">After hello ASE is created, go toohello ASE UI.</span></span> <span data-ttu-id="db114-214">選取 [ASE]  >  [設定]  >  [ILB 憑證]。</span><span class="sxs-lookup"><span data-stu-id="db114-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="db114-215">tooset hello ILB 憑證，請選取 hello 憑證.pfx 檔案，然後輸入 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="db114-215">tooset hello ILB certificate, select hello certificate .pfx file and enter hello password.</span></span> <span data-ttu-id="db114-216">這個步驟需要一些時間 tooprocess。</span><span class="sxs-lookup"><span data-stu-id="db114-216">This step takes some time tooprocess.</span></span> <span data-ttu-id="db114-217">會出現訊息指出上傳作業正在進行中。</span><span class="sxs-lookup"><span data-stu-id="db114-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="db114-218">取得您 ASE hello ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="db114-218">Get hello ILB address for your ASE.</span></span> <span data-ttu-id="db114-219">選取 [ASE]  >  [屬性]  >  [虛擬 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="db114-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="db114-220">建立 hello ASE 之後，請在您 ASE 中建立 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="db114-220">Create a web app in your ASE after hello ASE is created.</span></span>

5. <span data-ttu-id="db114-221">如果您在該 VNet 中還沒有 VM，則建立 VM。</span><span class="sxs-lookup"><span data-stu-id="db114-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="db114-222">不在此 VM 試 toocreate hello 相同子網路，如 hello ASE，因為它將會失敗，或是會造成問題。</span><span class="sxs-lookup"><span data-stu-id="db114-222">Don't try toocreate this VM in hello same subnet as hello ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="db114-223">設定 hello DNS ASE 網域。</span><span class="sxs-lookup"><span data-stu-id="db114-223">Set hello DNS for your ASE domain.</span></span> <span data-ttu-id="db114-224">您可以在您的 DNS 中使用萬用字元搭配您的網域。</span><span class="sxs-lookup"><span data-stu-id="db114-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="db114-225">toodo 一些簡單的測試，請編輯您 VM tooset hello web 應用程式名稱 toohello VIP 的 IP 位址上 hello 主機檔案：</span><span class="sxs-lookup"><span data-stu-id="db114-225">toodo some simple tests, edit hello hosts file on your VM tooset hello web app name toohello VIP IP address:</span></span>

    <span data-ttu-id="db114-226">a.</span><span class="sxs-lookup"><span data-stu-id="db114-226">a.</span></span> <span data-ttu-id="db114-227">如果您 ASE 擁有 hello 網域名稱_。 ilbase.com_並建立名為 hello web 應用程式_mytestapp_，同時解決_mytestapp.ilbase.com_。然後，您設定_mytestapp.ilbase.com_ tooresolve toohello ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="db114-227">If your ASE has hello domain name _.ilbase.com_ and you create hello web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ tooresolve toohello ILB address.</span></span> <span data-ttu-id="db114-228">(在 Windows 中，hello 主機檔案位於 _C:\Windows\System32\drivers\etc\_。)</span><span class="sxs-lookup"><span data-stu-id="db114-228">(On Windows, hello hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="db114-229">b.</span><span class="sxs-lookup"><span data-stu-id="db114-229">b.</span></span> <span data-ttu-id="db114-230">tootest web 部署發行或存取 toohello 進階主控台中，建立的記錄_mytestapp.scm.ilbase.com_。</span><span class="sxs-lookup"><span data-stu-id="db114-230">tootest web deployment publishing or access toohello advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="db114-231">在該 VM 上使用瀏覽器並移至 http://mytestapp.ilbase.com 。（或移的 toowhatever web 應用程式名稱會與您的網域）。</span><span class="sxs-lookup"><span data-stu-id="db114-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go toowhatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="db114-232">在該 VM 上使用瀏覽器並移至 https://mytestapp.ilbase.com 。如果您使用自我簽署的憑證，請接受 hello 缺乏安全性。</span><span class="sxs-lookup"><span data-stu-id="db114-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept hello lack of security.</span></span>

    <span data-ttu-id="db114-233">hello 對於您 ILB 的 IP 位址會列示在下**IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="db114-233">hello IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="db114-234">這份清單也會有 hello hello 外部 VIP、 輸入的管理流量使用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="db114-234">This list also has hello IP addresses used by hello external VIP and for inbound management traffic.</span></span>

    ![ILB IP 位址][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a><span data-ttu-id="db114-236">Web 工作，函式和 hello ILB ASE</span><span class="sxs-lookup"><span data-stu-id="db114-236">Web jobs, Functions and hello ILB ASE</span></span>

<span data-ttu-id="db114-237">ILB ASE 支援函式和 web 工作，但 hello 入口 toowork 它們，您必須擁有網路存取 toohello SCM 站台。</span><span class="sxs-lookup"><span data-stu-id="db114-237">Both Functions and web jobs are supported on an ILB ASE but for hello portal toowork with them, you must have network access toohello SCM site.</span></span>  <span data-ttu-id="db114-238">這表示您的瀏覽器必須處於或連接 toohello 虛擬網路的主機上。</span><span class="sxs-lookup"><span data-stu-id="db114-238">This means your browser must either be on a host that is either in or connected toohello virtual network.</span></span>  

<span data-ttu-id="db114-239">當您使用 ILB ASE Azure 函式時，您可能會收到錯誤訊息表示 「 我們無法函式現在能夠 tooretrieve。</span><span class="sxs-lookup"><span data-stu-id="db114-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able tooretrieve your functions right now.</span></span> <span data-ttu-id="db114-240">請稍後再試。」</span><span class="sxs-lookup"><span data-stu-id="db114-240">Please try again later."</span></span> <span data-ttu-id="db114-241">Hello 函式 UI 會透過 HTTPS 運用 hello SCM 站台和 hello 根憑證不在 hello 瀏覽器信任鏈結，就會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="db114-241">This error occurs because hello Functions UI leverages hello SCM site over HTTPS and hello root certificate is not in hello browser chain of trust.</span></span> <span data-ttu-id="db114-242">Web 工作具有類似的問題。</span><span class="sxs-lookup"><span data-stu-id="db114-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="db114-243">tooavoid 這個問題，您可以執行 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="db114-243">tooavoid this problem you can do one of hello following:</span></span>

- <span data-ttu-id="db114-244">新增 hello 憑證 tooyour 受信任的憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="db114-244">Add hello certificate tooyour trusted certificate store.</span></span> <span data-ttu-id="db114-245">這會解除封鎖 Edge 及 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="db114-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="db114-246">使用 Chrome 第一次移 toohello SCM 站台、 接受 hello 受信任的憑證並前往 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="db114-246">Use Chrome and go toohello SCM site first, accept hello untrusted certificate and then go toohello portal.</span></span>
- <span data-ttu-id="db114-247">使用瀏覽器信任鏈結中的商業憑證。</span><span class="sxs-lookup"><span data-stu-id="db114-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="db114-248">這是 hello 最佳選項。</span><span class="sxs-lookup"><span data-stu-id="db114-248">This is hello best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="db114-249">DNS 組態</span><span class="sxs-lookup"><span data-stu-id="db114-249">DNS configuration</span></span> ##

<span data-ttu-id="db114-250">當您使用外部 VIP 時，hello DNS 是由 Azure 中管理。</span><span class="sxs-lookup"><span data-stu-id="db114-250">When you use an External VIP, hello DNS is managed by Azure.</span></span> <span data-ttu-id="db114-251">在您 ASE 中建立任何應用程式會自動加入 tooAzure DNS，這是公用的 DNS。</span><span class="sxs-lookup"><span data-stu-id="db114-251">Any app created in your ASE is automatically added tooAzure DNS, which is a public DNS.</span></span> <span data-ttu-id="db114-252">在 ILB ASE 中，您必須管理您自己的 DNS。</span><span class="sxs-lookup"><span data-stu-id="db114-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="db114-253">針對指定的網域，例如_contoso.net_，您需要的 toocreate DNS A 記錄在 DNS 中針對該點 tooyour ILB 位址：</span><span class="sxs-lookup"><span data-stu-id="db114-253">For a given domain such as _contoso.net_, you need toocreate DNS A records in your DNS that point tooyour ILB address for:</span></span>

- <span data-ttu-id="db114-254">*.contoso.net</span><span class="sxs-lookup"><span data-stu-id="db114-254">*.contoso.net</span></span>
- <span data-ttu-id="db114-255">*.scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="db114-255">*.scm.contoso.net</span></span>

<span data-ttu-id="db114-256">如果 ILB ASE 網域來進行多項功能，此 ASE 之外，您可能需要 toomanage DNS 以每個應用程式名稱為基礎。</span><span class="sxs-lookup"><span data-stu-id="db114-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need toomanage DNS on a per-app-name basis.</span></span> <span data-ttu-id="db114-257">這個方法很困難，因為時，您需要 tooadd 每個新的應用程式名稱在您的 DNS 中建立它。</span><span class="sxs-lookup"><span data-stu-id="db114-257">This method is challenging because you need tooadd each new app name into your DNS when you create it.</span></span> <span data-ttu-id="db114-258">基於這個理由，建議使用專用網域。</span><span class="sxs-lookup"><span data-stu-id="db114-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="db114-259">使用 ILB ASE 發佈</span><span class="sxs-lookup"><span data-stu-id="db114-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="db114-260">每一個建立的應用程式，都有兩個端點。</span><span class="sxs-lookup"><span data-stu-id="db114-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="db114-261">在 ILB ASE 中，您有 &lt;app name>.&lt;ILB ASE Domain> 和 &lt;app name>.scm.&lt;ILB ASE Domain>。</span><span class="sxs-lookup"><span data-stu-id="db114-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="db114-262">hello SCM 網站名稱會採用您 toohello Kudu 主控台中，稱為 hello**進階入口網站**內 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="db114-262">hello SCM site name takes you toohello Kudu console, called hello **Advanced portal**, within hello Azure portal.</span></span> <span data-ttu-id="db114-263">hello Kudu 主控台可讓您檢視環境變數中，瀏覽 hello 磁碟，請使用主控台，以及執行更多。</span><span class="sxs-lookup"><span data-stu-id="db114-263">hello Kudu console lets you view environment variables, explore hello disk, use a console, and much more.</span></span> <span data-ttu-id="db114-264">如需詳細資訊，請參閱 [Azure App Service 的 Kudu 主控台][Kudu]。</span><span class="sxs-lookup"><span data-stu-id="db114-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="db114-265">在 hello 多租用戶應用程式服務和外部 ase 中，沒有單一登入 Azure 入口網站的 hello 與 hello Kudu 主控台之間的功能。</span><span class="sxs-lookup"><span data-stu-id="db114-265">In hello multitenant App Service and in an External ASE, there's single sign-on between hello Azure portal and hello Kudu console.</span></span> <span data-ttu-id="db114-266">Hello ILB ASE，不過，您需要 toouse 發行的憑證 toosign hello Kudu 主控台。</span><span class="sxs-lookup"><span data-stu-id="db114-266">For hello ILB ASE, however, you need toouse your publishing credentials toosign into hello Kudu console.</span></span>

<span data-ttu-id="db114-267">以網際網路為基礎 CI 系統，例如 GitHub 和 Visual Studio Team Services，不使用 ILB ASE 因為 hello 發行端點無法存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="db114-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because hello publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="db114-268">相反地，您需要 toouse 使用提取模型，例如 Dropbox 的 CI 系統。</span><span class="sxs-lookup"><span data-stu-id="db114-268">Instead, you need toouse a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="db114-269">hello ILB ASE 中的應用程式的發行端點會使用 ILB ASE 建立與該 hello hello 網域。</span><span class="sxs-lookup"><span data-stu-id="db114-269">hello publishing endpoints for apps in an ILB ASE use hello domain that hello ILB ASE was created with.</span></span> <span data-ttu-id="db114-270">此網域會出現在 hello 應用程式發行設定檔和 hello 應用程式的入口網站的刀鋒視窗 (**概觀** > **Essentials**以及**屬性**)。</span><span class="sxs-lookup"><span data-stu-id="db114-270">This domain appears in hello app's publishing profile and in hello app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="db114-271">如果您有與 hello 子網域 ILB ASE *contoso.net*和應用程式命名*mytest*，使用*mytest.contoso.net* ftp 和*mytest.scm.contoso.net*用於 web 部署。</span><span class="sxs-lookup"><span data-stu-id="db114-271">If you have an ILB ASE with hello subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="db114-272">將 ILB ASE 與 WAF 裝置耦合</span><span class="sxs-lookup"><span data-stu-id="db114-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="db114-273">Azure App Service 提供許多保護 hello 系統的安全性措施。</span><span class="sxs-lookup"><span data-stu-id="db114-273">Azure App Service provides many security measures that protect hello system.</span></span> <span data-ttu-id="db114-274">它們也可以協助 toodetermine 是否已遭竊取應用程式。</span><span class="sxs-lookup"><span data-stu-id="db114-274">They also help toodetermine whether an app was hacked.</span></span> <span data-ttu-id="db114-275">hello 最佳保護 web 應用程式是 toocouple 裝載平台，Azure 應用程式服務，例如 web 應用程式防火牆 (WAF)。</span><span class="sxs-lookup"><span data-stu-id="db114-275">hello best protection for a web application is toocouple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="db114-276">因為 hello ILB ASE 的網路隔離的應用程式端點，所以很適合這樣的使用。</span><span class="sxs-lookup"><span data-stu-id="db114-276">Because hello ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="db114-277">深入了解如何 tooconfigure 程式的 ILB ASE WAF 裝置，請參閱 toolearn[使用 App Service 環境設定 web 應用程式防火牆][ASEWAF]。</span><span class="sxs-lookup"><span data-stu-id="db114-277">toolearn more about how tooconfigure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="db114-278">本文將說明如何 toouse Barracuda 虛擬應用裝置與您 ASE。</span><span class="sxs-lookup"><span data-stu-id="db114-278">This article shows how toouse a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="db114-279">另一個選項是 toouse Azure 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="db114-279">Another option is toouse Azure Application Gateway.</span></span> <span data-ttu-id="db114-280">應用程式閘道會使用任何應用程式放在它後面的 hello OWASP 核心規則 toosecure。</span><span class="sxs-lookup"><span data-stu-id="db114-280">Application Gateway uses hello OWASP core rules toosecure any applications placed behind it.</span></span> <span data-ttu-id="db114-281">如需應用程式閘道的詳細資訊，請參閱[簡介 toohello Azure web 應用程式防火牆][AppGW]。</span><span class="sxs-lookup"><span data-stu-id="db114-281">For more information about Application Gateway, see [Introduction toohello Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="db114-282">開始使用</span><span class="sxs-lookup"><span data-stu-id="db114-282">Get started</span></span> ##

<span data-ttu-id="db114-283">中都提供所有發行項和 ASEs 的方式-tooinstructions [App Service 環境的讀我檔案][ASEReadme]。</span><span class="sxs-lookup"><span data-stu-id="db114-283">All articles and how-tooinstructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="db114-284">tooget 入門 ASEs，請參閱[簡介 tooApp 服務環境][Intro]。</span><span class="sxs-lookup"><span data-stu-id="db114-284">tooget started with ASEs, see [Introduction tooApp Service environments][Intro].</span></span>
* <span data-ttu-id="db114-285">如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/)。</span><span class="sxs-lookup"><span data-stu-id="db114-285">For more information about hello Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
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
