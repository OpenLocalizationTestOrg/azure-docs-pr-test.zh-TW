---
title: "aaaCreating 和 App Service 環境中使用內部負載平衡器 |Microsoft 文件"
description: "搭配 ILB 建立及使用 ASE"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="dd279-103">搭配 App Service 環境使用內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="dd279-103">Using an Internal Load Balancer with an App Service Environment</span></span>

> [!NOTE] 
> <span data-ttu-id="dd279-104">這篇文章是關於 hello App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="dd279-104">This article is about hello App Service Environment v1.</span></span> <span data-ttu-id="dd279-105">沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。</span><span class="sxs-lookup"><span data-stu-id="dd279-105">There is a newer version of hello App Service Environment that is easier toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="dd279-106">有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。</span><span class="sxs-lookup"><span data-stu-id="dd279-106">toolearn more about hello new version start with hello [Introduction toohello App Service Environment](../app-service/app-service-environment/intro.md).</span></span>
>

<span data-ttu-id="dd279-107">hello 應用程式服務環境 (ASE) 功能是提供 hello 多租用戶戳記中不提供增強的組態功能的 Azure App Service 的高階服務選項。</span><span class="sxs-lookup"><span data-stu-id="dd279-107">hello App Service Environment (ASE) feature is a Premium service option of Azure App Service that delivers an enhanced configuration capability that is not available in hello multi-tenant stamps.</span></span> <span data-ttu-id="dd279-108">hello ASE 功能基本上部署 Azure 應用程式服務在您的 Azure 虛擬 Network(VNet) hello。</span><span class="sxs-lookup"><span data-stu-id="dd279-108">hello ASE feature essentially deploys hello Azure App Service in your Azure Virtual Network(VNet).</span></span> <span data-ttu-id="dd279-109">應用程式服務環境的 hello 功能更深入瞭解提供的 toogain 讀取 hello[何謂 App Service 環境][ WhatisASE]文件。</span><span class="sxs-lookup"><span data-stu-id="dd279-109">toogain a greater understanding of hello capabilities offered by App Service Environments read hello [What is an App Service Environment][WhatisASE] documentation.</span></span> <span data-ttu-id="dd279-110">如果您不知道的操作在 VNet 中的 hello 優點讀取 hello [Azure 虛擬網路常見問題集][virtualnetwork]。</span><span class="sxs-lookup"><span data-stu-id="dd279-110">If you don't know hello benefits of operating in a VNet read hello [Azure Virtual Network FAQ][virtualnetwork].</span></span> 

## <a name="overview"></a><span data-ttu-id="dd279-111">概觀</span><span class="sxs-lookup"><span data-stu-id="dd279-111">Overview</span></span>
<span data-ttu-id="dd279-112">ASE 可以使用網際網路可存取的端點或您 Vnet 中的 IP 位址加以部署。</span><span class="sxs-lookup"><span data-stu-id="dd279-112">An ASE can be deployed with an internet accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="dd279-113">In 順序 tooset hello IP 位址需要您具有內部的負載 Balancer(ILB) ASE toodeploy tooa VNet 位址。</span><span class="sxs-lookup"><span data-stu-id="dd279-113">In order tooset hello IP address tooa VNet address you need toodeploy your ASE with an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="dd279-114">當您的 ASE 是使用 ILB 設定時，您要提供：</span><span class="sxs-lookup"><span data-stu-id="dd279-114">When your ASE is configured with an ILB you provide:</span></span>

* <span data-ttu-id="dd279-115">您自己的網域或子網域。</span><span class="sxs-lookup"><span data-stu-id="dd279-115">your own domain or subdomain.</span></span> <span data-ttu-id="dd279-116">toomake 它很容易，本文件假設子網域，但您可以設定兩種。</span><span class="sxs-lookup"><span data-stu-id="dd279-116">toomake it easy, this document assumes subdomain but you can configure it either way.</span></span> 
* <span data-ttu-id="dd279-117">使用 HTTPS 的 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="dd279-117">hello certificate used for HTTPS</span></span>
* <span data-ttu-id="dd279-118">您子網域的 DNS 管理。</span><span class="sxs-lookup"><span data-stu-id="dd279-118">DNS management for your subdomain.</span></span> 

<span data-ttu-id="dd279-119">相對的，您可以執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="dd279-119">In return, you can do things such as:</span></span>

* <span data-ttu-id="dd279-120">裝載內部網路應用程式，例如企業營運應用程式，安全地在 hello 雲端您存取透過站台 tooSite 或 ExpressRoute 的 VPN</span><span class="sxs-lookup"><span data-stu-id="dd279-120">host intranet applications, like line of business applications, securely in hello cloud which you access through a Site tooSite or ExpressRoute VPN</span></span>
* <span data-ttu-id="dd279-121">在公用 DNS 伺服器未列出 hello 雲端中的主機應用程式</span><span class="sxs-lookup"><span data-stu-id="dd279-121">host apps in hello cloud that are not listed in public DNS servers</span></span>
* <span data-ttu-id="dd279-122">建立與網際網路隔離，且您的前端 app 可以安全地與之整合的後端應用程式</span><span class="sxs-lookup"><span data-stu-id="dd279-122">create internet isolated backend apps which your front end apps can securely integrate with</span></span>

#### <a name="disabled-functionality"></a><span data-ttu-id="dd279-123">已停用的功能</span><span class="sxs-lookup"><span data-stu-id="dd279-123">Disabled functionality</span></span>
<span data-ttu-id="dd279-124">當您使用 ILB ASE 時，有一些動作您無法執行。</span><span class="sxs-lookup"><span data-stu-id="dd279-124">There are some things that you cannot do when using an ILB ASE.</span></span> <span data-ttu-id="dd279-125">這些動作包括︰</span><span class="sxs-lookup"><span data-stu-id="dd279-125">Those things include:</span></span>

* <span data-ttu-id="dd279-126">使用 IPSSL</span><span class="sxs-lookup"><span data-stu-id="dd279-126">using IPSSL</span></span>
* <span data-ttu-id="dd279-127">指派的 IP 位址 toospecific 應用程式</span><span class="sxs-lookup"><span data-stu-id="dd279-127">assigning IP addresses toospecific apps</span></span>
* <span data-ttu-id="dd279-128">購買並與透過 hello 入口網站應用程式使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="dd279-128">buying and using a certificate with an app through hello portal.</span></span> <span data-ttu-id="dd279-129">您當然仍然可以取得直接與憑證授權單位的憑證，並使用您的應用程式，就不能透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="dd279-129">You can of course still obtain certificates directly with a Certificate Authority and use it with your apps, just not through hello Azure portal.</span></span>

## <a name="creating-an-ilb-ase"></a><span data-ttu-id="dd279-130">建立 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="dd279-130">Creating an ILB ASE</span></span>
<span data-ttu-id="dd279-131">建立 ILB ASE 通常與建立 ASE 沒有太大差異。</span><span class="sxs-lookup"><span data-stu-id="dd279-131">Creating an ILB ASE is not much different from creating an ASE normally.</span></span> <span data-ttu-id="dd279-132">如需建立 ase 中深入討論閱讀[如何 tooCreate App Service 環境][HowtoCreateASE]。</span><span class="sxs-lookup"><span data-stu-id="dd279-132">For a deeper discussion on creating an ASE read [How tooCreate an App Service Environment][HowtoCreateASE].</span></span> <span data-ttu-id="dd279-133">ILB ASE 是 hello 程序 toocreate hello 相同 ASE 建立期間建立 VNet，或選取現有的 VNet 之間。</span><span class="sxs-lookup"><span data-stu-id="dd279-133">hello process toocreate an ILB ASE is hello same between creating a VNet during ASE creation or selecting a pre-existing VNet.</span></span> <span data-ttu-id="dd279-134">toocreate ILB ase 中：</span><span class="sxs-lookup"><span data-stu-id="dd279-134">toocreate an ILB ASE:</span></span> 

1. <span data-ttu-id="dd279-135">在 Azure 入口網站選取 hello**新增]-> [Web + 行動裝置版]-> [App Service 環境**</span><span class="sxs-lookup"><span data-stu-id="dd279-135">In hello Azure portal select **New -> Web + Mobile -> App Service Environment**</span></span>
2. <span data-ttu-id="dd279-136">選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dd279-136">Select your subscription</span></span>
3. <span data-ttu-id="dd279-137">選取或建立資源群組</span><span class="sxs-lookup"><span data-stu-id="dd279-137">Select or create a resource group</span></span>
4. <span data-ttu-id="dd279-138">選取或建立 VNet</span><span class="sxs-lookup"><span data-stu-id="dd279-138">Select or create a VNet</span></span>
5. <span data-ttu-id="dd279-139">建立子網路 (如果選取 VNet)</span><span class="sxs-lookup"><span data-stu-id="dd279-139">Create a subnet if selecting a VNet</span></span>
6. <span data-ttu-id="dd279-140">選取**虛擬的網路位置]-> [VNet 組態**和集 hello VIP 類型 tooInternal</span><span class="sxs-lookup"><span data-stu-id="dd279-140">Select **Virtual Network/Location -> VNet Configuration** and set hello VIP Type tooInternal</span></span>
7. <span data-ttu-id="dd279-141">提供的子網域名稱 （這是用於此 ASE 中建立的應用程式的 hello 子網域）</span><span class="sxs-lookup"><span data-stu-id="dd279-141">Provide subdomain name (this will be hello subdomain used for apps created in this ASE)</span></span>
8. <span data-ttu-id="dd279-142">選取 [確定]，然後選取 [建立]</span><span class="sxs-lookup"><span data-stu-id="dd279-142">Select Ok and then Create</span></span>

![][1]

<span data-ttu-id="dd279-143">Hello 虛擬網路 刀鋒視窗中沒有 VNet 組態選項。</span><span class="sxs-lookup"><span data-stu-id="dd279-143">Within hello Virtual Network blade there is a VNet Configuration option.</span></span> <span data-ttu-id="dd279-144">這個選項可讓您在 [外部 VIP] 或 [內部 VIP] 之間選擇。</span><span class="sxs-lookup"><span data-stu-id="dd279-144">This lets you select between an External VIP or Internal VIP.</span></span> <span data-ttu-id="dd279-145">hello 預設值為外部。</span><span class="sxs-lookup"><span data-stu-id="dd279-145">hello default is External.</span></span> <span data-ttu-id="dd279-146">如果您將它設定 tooExternal 您 ASE 會使用網際網路存取的 VIP。</span><span class="sxs-lookup"><span data-stu-id="dd279-146">If you have it set tooExternal then your ASE will use an internet accessible VIP.</span></span> <span data-ttu-id="dd279-147">如果您選取內部，您的 ASE 會使用您 VNet 內 IP 位址搭配 ILB 進行設定。</span><span class="sxs-lookup"><span data-stu-id="dd279-147">If you select Internal, your ASE will be configured with an ILB on an IP address within your VNet.</span></span> 

<span data-ttu-id="dd279-148">選取內部之後, hello 能力 tooadd 多個 IP 位址的 tooyour ASE 已移除，改為您需要的 hello ASE tooprovide hello 子網域。</span><span class="sxs-lookup"><span data-stu-id="dd279-148">After selecting Internal, hello ability tooadd more IP addresses tooyour ASE is removed and instead you need tooprovide hello subdomain of hello ASE.</span></span> <span data-ttu-id="dd279-149">在以外部 VIP hello ase 中的 hello ASE 名稱用於 hello 子網域該 ASE 中建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dd279-149">In an ASE with an External VIP hello name of hello ASE is used in hello subdomain for apps created in that ASE.</span></span> <span data-ttu-id="dd279-150">如果呼叫您 ASE ***contosotest***和該 ASE 中的應用程式呼叫***mytest***則 hello 子網域會是 hello 格式的***contosotest.p.azurewebsites.net***和hello 針對該應用程式的 URL 會是***mytest.contosotest.p.azurewebsites.net***。</span><span class="sxs-lookup"><span data-stu-id="dd279-150">If your ASE was called ***contosotest*** and your app in that ASE was called ***mytest*** then hello subdomain would be of hello format ***contosotest.p.azurewebsites.net*** and hello URL for that app would be ***mytest.contosotest.p.azurewebsites.net***.</span></span> <span data-ttu-id="dd279-151">如果您設定 hello VIP 類型 tooInternal，ASE 名稱不是 hello 子網域中的 hello ASE。</span><span class="sxs-lookup"><span data-stu-id="dd279-151">If you set hello VIP Type tooInternal, your ASE name is not used in hello subdomain for hello ASE.</span></span> <span data-ttu-id="dd279-152">您可以明確地指定 hello 子網域。</span><span class="sxs-lookup"><span data-stu-id="dd279-152">You specify hello subdomain explicitly.</span></span> <span data-ttu-id="dd279-153">如果您的子網域***contoso.corp.net***並進行應用程式，名為 ASE ***timereporting***然後 hello URL，該應用程式會針對***timereporting.contoso.corp.net***。</span><span class="sxs-lookup"><span data-stu-id="dd279-153">If your subdomain was ***contoso.corp.net*** and you made an app in that ASE named ***timereporting*** then hello URL for that app would be ***timereporting.contoso.corp.net***.</span></span>

## <a name="apps-in-an-ilb-ase"></a><span data-ttu-id="dd279-154">ILB ASE 中的 App</span><span class="sxs-lookup"><span data-stu-id="dd279-154">Apps in an ILB ASE</span></span>
<span data-ttu-id="dd279-155">在 ILB ase 中建立應用程式是 hello 與通常在 ase 中建立應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="dd279-155">Creating an app in an ILB ASE is hello same as creating an app in an ASE normally.</span></span> 

1. <span data-ttu-id="dd279-156">在 Azure 入口網站選取 hello**新增]-> [Web + 行動裝置版]-> [Web**或**行動**或**API 應用程式**</span><span class="sxs-lookup"><span data-stu-id="dd279-156">In hello Azure portal select **New -> Web + Mobile -> Web** or **Mobile** or **API App**</span></span>
2. <span data-ttu-id="dd279-157">輸入 app 的名稱</span><span class="sxs-lookup"><span data-stu-id="dd279-157">Enter name of app</span></span>
3. <span data-ttu-id="dd279-158">選取訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dd279-158">Select subscription</span></span>
4. <span data-ttu-id="dd279-159">選取或建立資源群組</span><span class="sxs-lookup"><span data-stu-id="dd279-159">Select or create resource group</span></span>
5. <span data-ttu-id="dd279-160">選取或建立 App Service 方案 (ASP)。</span><span class="sxs-lookup"><span data-stu-id="dd279-160">Select or create App Service Plan(ASP).</span></span> <span data-ttu-id="dd279-161">如果建立新的 ASP，然後選取您 ASE hello 位置和選取 hello 背景工作集區中建立您 ASP toobe 想。</span><span class="sxs-lookup"><span data-stu-id="dd279-161">If creating a new ASP then select your ASE as hello location and select hello worker pool you want your ASP toobe created in.</span></span> <span data-ttu-id="dd279-162">當您建立 hello ASP 您選取您 ASE hello 位置和 hello 背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="dd279-162">When you create hello ASP you select your ASE as hello location and hello worker pool.</span></span> <span data-ttu-id="dd279-163">當您指定 hello 名稱，您會看到下的該 hello 子網域的 hello 應用程式的應用程式名稱取代 hello 子領域上您 ASE。</span><span class="sxs-lookup"><span data-stu-id="dd279-163">When you specify hello name of hello app you will see that hello subdomain under your app name is replaced by hello subdomain for your ASE.</span></span> 
6. <span data-ttu-id="dd279-164">選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="dd279-164">Select Create.</span></span> <span data-ttu-id="dd279-165">您應該選取 hello **Pin toodashboard**核取方塊，如果您想 hello 應用程式 tooshow 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="dd279-165">You should select hello **Pin toodashboard** checkbox if you want hello app tooshow up on your dashboard.</span></span> 

![][2]

<span data-ttu-id="dd279-166">在 hello 應用程式名稱 hello 子網域名稱會取得您 ASE 更新的 tooreflect hello 子網域。</span><span class="sxs-lookup"><span data-stu-id="dd279-166">Under hello app name hello subdomain name gets updated tooreflect hello subdomain of your ASE.</span></span> 

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="dd279-167">ILB ASE 建立後驗證</span><span class="sxs-lookup"><span data-stu-id="dd279-167">Post ILB ASE creation validation</span></span>
<span data-ttu-id="dd279-168">ILB ase 中有些許不同比 hello 非-ILB ASE。</span><span class="sxs-lookup"><span data-stu-id="dd279-168">An ILB ASE is slightly different than hello non-ILB ASE.</span></span> <span data-ttu-id="dd279-169">如上所述需要 toomanage 自己的 DNS，而且您也可以 tooprovide 供 HTTPS 連線憑證。</span><span class="sxs-lookup"><span data-stu-id="dd279-169">As already noted you need toomanage your own DNS and you also have tooprovide your own certificate for HTTPS connections.</span></span> 

<span data-ttu-id="dd279-170">建立您 ASE 之後您會發現該 hello 子網域會顯示 hello 子網域，您指定，而且新的項目正在 hello**設定**功能表呼叫**ILB 憑證**。</span><span class="sxs-lookup"><span data-stu-id="dd279-170">After you create your ASE you will notice that hello subdomain shows hello subdomain you specified and there is a new item in hello **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="dd279-171">hello ASE 會建立自我簽署憑證，使其更容易 tootest HTTPS。</span><span class="sxs-lookup"><span data-stu-id="dd279-171">hello ASE is created with a self-signed certificate which makes it easier tootest HTTPS.</span></span> <span data-ttu-id="dd279-172">hello 入口網站會告訴您針對 HTTPS 需要 tooprovide 您自己的憑證，但這是 toodrive toohave 亦會隨您的子網域的憑證。</span><span class="sxs-lookup"><span data-stu-id="dd279-172">hello portal will tell you that you need tooprovide your own certificate for HTTPS but this is toodrive you toohave a certificate that goes with your subdomain.</span></span> 

![][3]

<span data-ttu-id="dd279-173">如果您只嘗試項目，並不知道如何 toocreate 憑證，您可以使用 hello IIS MMC 主控台應用程式 toocreate 的自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="dd279-173">If you are simply trying things out and don't know how toocreate a certificate, you can use hello IIS MMC console application toocreate a self signed certificate.</span></span> <span data-ttu-id="dd279-174">一旦建立之後可以將它匯出為.pfx 檔案，並再將它上傳 hello ILB Certificate UI 中。</span><span class="sxs-lookup"><span data-stu-id="dd279-174">Once it is created you can export it as a .pfx file and then upload it in hello ILB Certificate UI.</span></span> <span data-ttu-id="dd279-175">當您存取站台保護使用自我簽署憑證，您的瀏覽器會發出警告 hello 您要存取的網站，並不安全 toohello 無法 toovalidate hello 憑證到期。</span><span class="sxs-lookup"><span data-stu-id="dd279-175">When you access a site secured with a self-signed certificate, your browser will give you a warning that hello site you are accessing is not secure due toohello inability toovalidate hello certificate.</span></span> <span data-ttu-id="dd279-176">如果您想 tooavoid 警告您將需要經過適當簽署的憑證符合您的子網域並具有已辨識您的瀏覽器的信任鏈結。</span><span class="sxs-lookup"><span data-stu-id="dd279-176">If you want tooavoid that warning you need a properly signed certificate that matches your subdomain and has a chain of trust that is recognized by your browser.</span></span>

![][6]

<span data-ttu-id="dd279-177">如果您想 tootry hello 充滿您自己的憑證，並測試 HTTP 和 HTTPS 存取 tooyour ASE:</span><span class="sxs-lookup"><span data-stu-id="dd279-177">If you want tootry hello flow with your own certificates and test both HTTP and HTTPS access tooyour ASE:</span></span>

1. <span data-ttu-id="dd279-178">建立 ASE 後移 tooASE UI **ASE-> 設定-> ILB 憑證**</span><span class="sxs-lookup"><span data-stu-id="dd279-178">Go tooASE UI after ASE is created **ASE -> Settings -> ILB Certificates**</span></span>
2. <span data-ttu-id="dd279-179">選取憑證 .pfx 檔案並提供密碼，來設定 ILB 憑證。</span><span class="sxs-lookup"><span data-stu-id="dd279-179">Set ILB certificate by selecting certificate pfx file and provide password.</span></span> <span data-ttu-id="dd279-180">此步驟需要一些 tooprocess 時，且將顯示調整的作業正在進行中的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="dd279-180">This step takes a little while tooprocess and hello message that a scaling operation is in progress will be shown.</span></span>
3. <span data-ttu-id="dd279-181">Hello ILB 位址取得您 ASE (**ASE]-> [屬性]-> [虛擬 IP 位址**)</span><span class="sxs-lookup"><span data-stu-id="dd279-181">Get hello ILB address for your ASE (**ASE -> Properties -> Virtual IP Address**)</span></span>
4. <span data-ttu-id="dd279-182">建立後，在 ASE 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="dd279-182">Create a web app in ASE after creation</span></span> 
5. <span data-ttu-id="dd279-183">如果您還沒有該 VNET 中建立 VM (不在 hello 相同 hello ASE 或項目中斷與子網路)</span><span class="sxs-lookup"><span data-stu-id="dd279-183">Create a VM if you don't have one in that VNET (Not in hello same subnet as hello ASE or things break)</span></span>
6. <span data-ttu-id="dd279-184">設定您子網域的 DNS。</span><span class="sxs-lookup"><span data-stu-id="dd279-184">Set DNS for your subdomain.</span></span> <span data-ttu-id="dd279-185">您可以使用子網域中的萬用字元，在 DNS 中，或如果您想 toodo 一些簡單的測試中，編輯 hello 您 VM tooset web 應用程式名稱 tooVIP 的 IP 位址上的主機檔案。</span><span class="sxs-lookup"><span data-stu-id="dd279-185">You can use a wildcard with your subdomain in your DNS or if you want toodo some simple tests, edit hello hosts file on your VM tooset web app name tooVIP IP address.</span></span> <span data-ttu-id="dd279-186">如果您 ASE 有 hello 子網域名稱。 ilbase.com 和您所做 hello web 應用程式 mytestapp 使會位於 mytestapp.ilbase.com 然後在主機檔案中進行設定。</span><span class="sxs-lookup"><span data-stu-id="dd279-186">If your ASE had hello subdomain name .ilbase.com and you made hello web app mytestapp so that it would be addressed at mytestapp.ilbase.com then set that in your hosts file.</span></span> <span data-ttu-id="dd279-187">（在 Windows hello 主機檔案位於 C:\Windows\System32\drivers\etc\）</span><span class="sxs-lookup"><span data-stu-id="dd279-187">(On Windows hello hosts file is at C:\Windows\System32\drivers\etc\ )</span></span>
7. <span data-ttu-id="dd279-188">該 VM 上使用瀏覽器並移 toohttp://mytestapp.ilbase.com （或任何 web 應用程式名稱會與您的子網域）</span><span class="sxs-lookup"><span data-stu-id="dd279-188">Use a browser on that VM and go toohttp://mytestapp.ilbase.com (or whatever your web app name is with your subdomain)</span></span>
8. <span data-ttu-id="dd279-189">該 VM 上使用瀏覽器，並移 toohttps://mytestapp.ilbase.com 如果使用自我簽署的憑證，您會有 tooaccept hello 缺乏安全性。</span><span class="sxs-lookup"><span data-stu-id="dd279-189">Use a browser on that VM and go toohttps://mytestapp.ilbase.com You will have tooaccept hello lack of security if using a self-signed certificate.</span></span> 

<span data-ttu-id="dd279-190">hello 您 ILB 的 IP 位址會列為內容中 hello 虛擬 IP 位址</span><span class="sxs-lookup"><span data-stu-id="dd279-190">hello IP address for your ILB is listed in your Properties as hello Virtual IP Address</span></span>

![][4]

## <a name="using-an-ilb-ase"></a><span data-ttu-id="dd279-191">使用 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="dd279-191">Using an ILB ASE</span></span>
#### <a name="network-security-groups"></a><span data-ttu-id="dd279-192">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="dd279-192">Network Security Groups</span></span>
<span data-ttu-id="dd279-193">Hello 應用程式並不是可存取或甚至已知由您的應用程式的 ILB ASE 啟用網路隔離 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="dd279-193">An ILB ASE enables network isolation for your apps as hello apps are not accessible or even known by hello internet.</span></span> <span data-ttu-id="dd279-194">這非常適合用來裝載內部網路網站，例如企業營運應用程式。</span><span class="sxs-lookup"><span data-stu-id="dd279-194">This is excellent for hosting intranet sites such as line of business applications.</span></span> <span data-ttu-id="dd279-195">如果您需要 toorestrict 存取，甚至進一步您仍然可以使用網路安全性 Groups(NSGs) toocontrol 存取在 hello 網路層級。</span><span class="sxs-lookup"><span data-stu-id="dd279-195">When you need toorestrict access even further you can still use Network Security Groups(NSGs) toocontrol access at hello network level.</span></span> 

<span data-ttu-id="dd279-196">如果您想 toouse Nsg toofurther 限制存取，則您需要確定未中斷 hello 通訊 toomake 該 hello ASE 需要順序 toooperate 中。</span><span class="sxs-lookup"><span data-stu-id="dd279-196">If you wish toouse NSGs toofurther restrict access then you need toomake sure you do not break hello communication that hello ASE needs in order toooperate.</span></span> <span data-ttu-id="dd279-197">即使 hello HTTP/HTTPS 存取只能透過 hello ILB 使用 hello ASE hello ASE 仍取決於 hello VNet 外部資源。</span><span class="sxs-lookup"><span data-stu-id="dd279-197">Even though hello HTTP/HTTPS access is only through hello ILB used by hello ASE hello ASE still depends on resource outside of hello VNet.</span></span> <span data-ttu-id="dd279-198">何種網路存取權是的 toosee 仍然需要看 hello 文件中的 hello 資訊上[控制連入流量 tooan App Service 環境][ ControlInbound]和 hello 文件上的[網路透過 ExpressRoute 的 App Service 環境的組態詳細資料][ExpressRoute]。</span><span class="sxs-lookup"><span data-stu-id="dd279-198">toosee what network access is still required look at hello information in hello document on [Controlling Inbound Traffic tooan App Service Environment][ControlInbound] and hello document on [Network Configuration Details for App Service Environments with ExpressRoute][ExpressRoute].</span></span> 

<span data-ttu-id="dd279-199">Azure toomanage 您 ASE 供的 tooconfigure Nsg 需要 tooknow hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dd279-199">tooconfigure your NSGs you need tooknow hello IP address that is used by Azure toomanage your ASE.</span></span> <span data-ttu-id="dd279-200">如果網際網路要求該 IP 位址也是從您 ASE hello 輸出 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dd279-200">That IP address is also hello outbound IP address from your ASE if it makes internet requests.</span></span> <span data-ttu-id="dd279-201">針對您 ASE hello 輸出 IP 位址依然靜態您 ASE hello 存留期間。</span><span class="sxs-lookup"><span data-stu-id="dd279-201">hello outbound IP address for your ASE will remain static for hello life of your ASE.</span></span> <span data-ttu-id="dd279-202">如果您刪除並重建 ASE，您會收到新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dd279-202">If you delete and recreate your ASE, you will get a new IP address.</span></span> <span data-ttu-id="dd279-203">此 IP 位址太移的 toofind**設定]-> [屬性**並尋找 hello**輸出的 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="dd279-203">toofind this IP address go too**Settings -> Properties** and find hello **Outbound IP Address**.</span></span> 

![][5]

#### <a name="general-ilb-ase-management"></a><span data-ttu-id="dd279-204">一般 ILB ASE 管理</span><span class="sxs-lookup"><span data-stu-id="dd279-204">General ILB ASE management</span></span>
<span data-ttu-id="dd279-205">管理 ILB ase 中是主要 hello 與管理 ase 中通常相同。</span><span class="sxs-lookup"><span data-stu-id="dd279-205">Managing an ILB ASE is largely hello same as managing an ASE normally.</span></span> <span data-ttu-id="dd279-206">您需要 tooscale 註冊您的背景工作集區 toohost 詳細的 ASP 執行個體，而且您前端伺服器的 HTTP/HTTPS 流量的增加 toohandle 量向上延展。</span><span class="sxs-lookup"><span data-stu-id="dd279-206">You need tooscale up your worker pools toohost more ASP instances and scale up your Front End servers toohandle increased amounts of HTTP/HTTPS traffic.</span></span> <span data-ttu-id="dd279-207">如需管理 ASE hello 組態的一般資訊，讀取 hello 文件上[設定 App Service 環境][ASEConfig]。</span><span class="sxs-lookup"><span data-stu-id="dd279-207">For general information on managing hello configuration of an ASE, read hello document on [Configuring an App Service Environment][ASEConfig].</span></span> 

<span data-ttu-id="dd279-208">hello 額外的管理項目是管理憑證和 DNS 管理。</span><span class="sxs-lookup"><span data-stu-id="dd279-208">hello additional management items are certificate management and DNS management.</span></span> <span data-ttu-id="dd279-209">您需要 tooobtain ILB ASE 建立之後用於 HTTPS hello 憑證上傳，並在到期之前取代它。</span><span class="sxs-lookup"><span data-stu-id="dd279-209">You need tooobtain and upload hello certificate used for HTTPS after ILB ASE creation and replace it before it expires.</span></span> <span data-ttu-id="dd279-210">由於 Azure 擁有 hello 基底領域我們可以與外部 VIP ASEs 提供憑證。</span><span class="sxs-lookup"><span data-stu-id="dd279-210">Because Azure owns hello base domain we can provide certificates for ASEs with an External VIP.</span></span> <span data-ttu-id="dd279-211">由於 ILB ase 中所使用的 hello 子網域可以是任何項目，您必須 tooprovide 您自己的憑證的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="dd279-211">Since hello subdomain used by an ILB ASE can be anything, you need tooprovide your own certificate for HTTPS.</span></span> 

#### <a name="dns-configuration"></a><span data-ttu-id="dd279-212">DNS 組態</span><span class="sxs-lookup"><span data-stu-id="dd279-212">DNS Configuration</span></span>
<span data-ttu-id="dd279-213">當使用外部 VIP hello DNS 由 Azure 管理。</span><span class="sxs-lookup"><span data-stu-id="dd279-213">When using an External VIP hello DNS is managed by Azure.</span></span> <span data-ttu-id="dd279-214">在您 ASE 中建立任何應用程式會自動加入 tooAzure 即公用 DNS 的 DNS。</span><span class="sxs-lookup"><span data-stu-id="dd279-214">Any app created in your ASE is automatically added tooAzure DNS which is a public DNS.</span></span> <span data-ttu-id="dd279-215">在 ILB ase 中您有 toomanage 自己的 DNS。</span><span class="sxs-lookup"><span data-stu-id="dd279-215">In an ILB ASE you have toomanage your own DNS.</span></span> <span data-ttu-id="dd279-216">指定的子網域，像是 contoso.corp.net 您需要的 toocreate DNS A 記錄該點 tooyour ILB 位址：</span><span class="sxs-lookup"><span data-stu-id="dd279-216">For a given subdomain such as contoso.corp.net you need toocreate DNS A records that point tooyour ILB address for:</span></span>

    * 
    <span data-ttu-id="dd279-217">*.scm ftp 發佈</span><span class="sxs-lookup"><span data-stu-id="dd279-217">*.scm ftp publish</span></span> 


## <a name="getting-started"></a><span data-ttu-id="dd279-218">開始使用</span><span class="sxs-lookup"><span data-stu-id="dd279-218">Getting started</span></span>
<span data-ttu-id="dd279-219">所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="dd279-219">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="dd279-220">tooget 開始使用應用程式服務環境中，請參閱[簡介 tooApp 服務環境][WhatisASE]</span><span class="sxs-lookup"><span data-stu-id="dd279-220">tooget started with App Service Environments, see [Introduction tooApp Service Environments][WhatisASE]</span></span>

<span data-ttu-id="dd279-221">如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="dd279-221">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
