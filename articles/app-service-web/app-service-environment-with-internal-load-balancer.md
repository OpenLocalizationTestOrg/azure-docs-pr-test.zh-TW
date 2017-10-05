---
title: "搭配 App Service 環境建立及使用內部負載平衡器 | Microsoft Docs"
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
ms.openlocfilehash: 9e5a40f18eb9eaf60579af21afc6f05c2d87f4c1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="0fb70-103">搭配 App Service 環境使用內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="0fb70-103">Using an Internal Load Balancer with an App Service Environment</span></span>

> [!NOTE] 
> <span data-ttu-id="0fb70-104">這篇文章是關於 App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="0fb70-104">This article is about the App Service Environment v1.</span></span> <span data-ttu-id="0fb70-105">有較新版本的 App Service 環境，更易於使用，並且可以在功能更強大的基礎結構上執行。</span><span class="sxs-lookup"><span data-stu-id="0fb70-105">There is a newer version of the App Service Environment that is easier to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="0fb70-106">若要深入了解新版本，請從 [App Service 環境簡介](../app-service/app-service-environment/intro.md)開始。</span><span class="sxs-lookup"><span data-stu-id="0fb70-106">To learn more about the new version start with the [Introduction to the App Service Environment](../app-service/app-service-environment/intro.md).</span></span>
>

<span data-ttu-id="0fb70-107">App Service 環境 (ASE) 功能是 Azure App Service 的進階服務選項，可提供多租用戶戳記中不提供的增強式設定功能。</span><span class="sxs-lookup"><span data-stu-id="0fb70-107">The App Service Environment (ASE) feature is a Premium service option of Azure App Service that delivers an enhanced configuration capability that is not available in the multi-tenant stamps.</span></span> <span data-ttu-id="0fb70-108">ASE功能基本上會在您的 Azure 虛擬網路 (VNet) 中部署 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="0fb70-108">The ASE feature essentially deploys the Azure App Service in your Azure Virtual Network(VNet).</span></span> <span data-ttu-id="0fb70-109">若要更深入了解 App Service Environment 所提供的功能，請閱讀[什麼是 App Service Environment][WhatisASE] 文件。</span><span class="sxs-lookup"><span data-stu-id="0fb70-109">To gain a greater understanding of the capabilities offered by App Service Environments read the [What is an App Service Environment][WhatisASE] documentation.</span></span> <span data-ttu-id="0fb70-110">如果您不了解在 VNet 中操作的優點，請閱讀 [Azure 虛擬網路常見問題集][virtualnetwork]。</span><span class="sxs-lookup"><span data-stu-id="0fb70-110">If you don't know the benefits of operating in a VNet read the [Azure Virtual Network FAQ][virtualnetwork].</span></span> 

## <a name="overview"></a><span data-ttu-id="0fb70-111">概觀</span><span class="sxs-lookup"><span data-stu-id="0fb70-111">Overview</span></span>
<span data-ttu-id="0fb70-112">ASE 可以使用網際網路可存取的端點或您 Vnet 中的 IP 位址加以部署。</span><span class="sxs-lookup"><span data-stu-id="0fb70-112">An ASE can be deployed with an internet accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="0fb70-113">為了將 IP 位址設定為 VNet 位址，您必須搭配內部負載平衡器 (ILB) 來部署您的 ASE。</span><span class="sxs-lookup"><span data-stu-id="0fb70-113">In order to set the IP address to a VNet address you need to deploy your ASE with an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="0fb70-114">當您的 ASE 是使用 ILB 設定時，您要提供：</span><span class="sxs-lookup"><span data-stu-id="0fb70-114">When your ASE is configured with an ILB you provide:</span></span>

* <span data-ttu-id="0fb70-115">您自己的網域或子網域。</span><span class="sxs-lookup"><span data-stu-id="0fb70-115">your own domain or subdomain.</span></span> <span data-ttu-id="0fb70-116">為了能順利進行，本文件假設是子網域，但是您還是可以設定。</span><span class="sxs-lookup"><span data-stu-id="0fb70-116">To make it easy, this document assumes subdomain but you can configure it either way.</span></span> 
* <span data-ttu-id="0fb70-117">針對 HTTPS 使用的憑證</span><span class="sxs-lookup"><span data-stu-id="0fb70-117">the certificate used for HTTPS</span></span>
* <span data-ttu-id="0fb70-118">您子網域的 DNS 管理。</span><span class="sxs-lookup"><span data-stu-id="0fb70-118">DNS management for your subdomain.</span></span> 

<span data-ttu-id="0fb70-119">相對的，您可以執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="0fb70-119">In return, you can do things such as:</span></span>

* <span data-ttu-id="0fb70-120">在您可以透過「端對端」或 ExpressRoute VPN 存取的雲端，安全地裝載內部網路應用程式 (例如企業營運應用程式)</span><span class="sxs-lookup"><span data-stu-id="0fb70-120">host intranet applications, like line of business applications, securely in the cloud which you access through a Site to Site or ExpressRoute VPN</span></span>
* <span data-ttu-id="0fb70-121">在雲端裝載未在公用 DNS 伺服器中列出的 app</span><span class="sxs-lookup"><span data-stu-id="0fb70-121">host apps in the cloud that are not listed in public DNS servers</span></span>
* <span data-ttu-id="0fb70-122">建立與網際網路隔離，且您的前端 app 可以安全地與之整合的後端應用程式</span><span class="sxs-lookup"><span data-stu-id="0fb70-122">create internet isolated backend apps which your front end apps can securely integrate with</span></span>

#### <a name="disabled-functionality"></a><span data-ttu-id="0fb70-123">已停用的功能</span><span class="sxs-lookup"><span data-stu-id="0fb70-123">Disabled functionality</span></span>
<span data-ttu-id="0fb70-124">當您使用 ILB ASE 時，有一些動作您無法執行。</span><span class="sxs-lookup"><span data-stu-id="0fb70-124">There are some things that you cannot do when using an ILB ASE.</span></span> <span data-ttu-id="0fb70-125">這些動作包括︰</span><span class="sxs-lookup"><span data-stu-id="0fb70-125">Those things include:</span></span>

* <span data-ttu-id="0fb70-126">使用 IPSSL</span><span class="sxs-lookup"><span data-stu-id="0fb70-126">using IPSSL</span></span>
* <span data-ttu-id="0fb70-127">將 IP 位址指派給特定 app</span><span class="sxs-lookup"><span data-stu-id="0fb70-127">assigning IP addresses to specific apps</span></span>
* <span data-ttu-id="0fb70-128">透過入口網站購買憑證並搭配 app 使用。</span><span class="sxs-lookup"><span data-stu-id="0fb70-128">buying and using a certificate with an app through the portal.</span></span> <span data-ttu-id="0fb70-129">您當然也可以直接透過「憑證授權單位」取得憑證並搭配您的 app 使用，只是無法透過 Azure 入口網站這樣做。</span><span class="sxs-lookup"><span data-stu-id="0fb70-129">You can of course still obtain certificates directly with a Certificate Authority and use it with your apps, just not through the Azure portal.</span></span>

## <a name="creating-an-ilb-ase"></a><span data-ttu-id="0fb70-130">建立 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="0fb70-130">Creating an ILB ASE</span></span>
<span data-ttu-id="0fb70-131">建立 ILB ASE 通常與建立 ASE 沒有太大差異。</span><span class="sxs-lookup"><span data-stu-id="0fb70-131">Creating an ILB ASE is not much different from creating an ASE normally.</span></span> <span data-ttu-id="0fb70-132">如需有關建立 ASE 的深入討論，請參閱[如何建立 App Service 環境][HowtoCreateASE]。</span><span class="sxs-lookup"><span data-stu-id="0fb70-132">For a deeper discussion on creating an ASE read [How to Create an App Service Environment][HowtoCreateASE].</span></span> <span data-ttu-id="0fb70-133">在 ASE 建立期間建立 VNet 或選取既存的 VNet 之間，建立 ILB ASE 的程序是相同的。</span><span class="sxs-lookup"><span data-stu-id="0fb70-133">The process to create an ILB ASE is the same between creating a VNet during ASE creation or selecting a pre-existing VNet.</span></span> <span data-ttu-id="0fb70-134">若要建立 ILB ASE：</span><span class="sxs-lookup"><span data-stu-id="0fb70-134">To create an ILB ASE:</span></span> 

1. <span data-ttu-id="0fb70-135">在 Azure 入口網站中選取 [新增] -> [Web + 行動] -> [App Service 環境]</span><span class="sxs-lookup"><span data-stu-id="0fb70-135">In the Azure portal select **New -> Web + Mobile -> App Service Environment**</span></span>
2. <span data-ttu-id="0fb70-136">選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0fb70-136">Select your subscription</span></span>
3. <span data-ttu-id="0fb70-137">選取或建立資源群組</span><span class="sxs-lookup"><span data-stu-id="0fb70-137">Select or create a resource group</span></span>
4. <span data-ttu-id="0fb70-138">選取或建立 VNet</span><span class="sxs-lookup"><span data-stu-id="0fb70-138">Select or create a VNet</span></span>
5. <span data-ttu-id="0fb70-139">建立子網路 (如果選取 VNet)</span><span class="sxs-lookup"><span data-stu-id="0fb70-139">Create a subnet if selecting a VNet</span></span>
6. <span data-ttu-id="0fb70-140">選取 [虛擬網路/位置] -> [VNet 組態]，並將 [VIP 類型] 設定為 [內部]</span><span class="sxs-lookup"><span data-stu-id="0fb70-140">Select **Virtual Network/Location -> VNet Configuration** and set the VIP Type to Internal</span></span>
7. <span data-ttu-id="0fb70-141">提供子網域名稱 (這會成為在此 ASE 中建立的 app 所使用的子網域)</span><span class="sxs-lookup"><span data-stu-id="0fb70-141">Provide subdomain name (this will be the subdomain used for apps created in this ASE)</span></span>
8. <span data-ttu-id="0fb70-142">選取 [確定]，然後選取 [建立]</span><span class="sxs-lookup"><span data-stu-id="0fb70-142">Select Ok and then Create</span></span>

![][1]

<span data-ttu-id="0fb70-143">在 [虛擬網路] 刀鋒視窗中，會有一個 [VNet 組態] 選項。</span><span class="sxs-lookup"><span data-stu-id="0fb70-143">Within the Virtual Network blade there is a VNet Configuration option.</span></span> <span data-ttu-id="0fb70-144">這個選項可讓您在 [外部 VIP] 或 [內部 VIP] 之間選擇。</span><span class="sxs-lookup"><span data-stu-id="0fb70-144">This lets you select between an External VIP or Internal VIP.</span></span> <span data-ttu-id="0fb70-145">預設為「外部」。</span><span class="sxs-lookup"><span data-stu-id="0fb70-145">The default is External.</span></span> <span data-ttu-id="0fb70-146">如果您設定為外部，您的 ASE 會使用一個網際網路可存取的 VIP。</span><span class="sxs-lookup"><span data-stu-id="0fb70-146">If you have it set to External then your ASE will use an internet accessible VIP.</span></span> <span data-ttu-id="0fb70-147">如果您選取內部，您的 ASE 會使用您 VNet 內 IP 位址搭配 ILB 進行設定。</span><span class="sxs-lookup"><span data-stu-id="0fb70-147">If you select Internal, your ASE will be configured with an ILB on an IP address within your VNet.</span></span> 

<span data-ttu-id="0fb70-148">選取內部之後，將會移除把更多 IP 位址新增至您 ASE 的功能，取而代之的是您必須提供 ASE 的子網域。</span><span class="sxs-lookup"><span data-stu-id="0fb70-148">After selecting Internal, the ability to add more IP addresses to your ASE is removed and instead you need to provide the subdomain of the ASE.</span></span> <span data-ttu-id="0fb70-149">在使用外部 VIP 的 ASE 中，ASE 的名稱會在子網域中用於在該 ASE 中建立的 app。</span><span class="sxs-lookup"><span data-stu-id="0fb70-149">In an ASE with an External VIP the name of the ASE is used in the subdomain for apps created in that ASE.</span></span> <span data-ttu-id="0fb70-150">如果您的 ASE 名稱為 ***contosotest***，而您在該 ASE 中的應用程式名稱為 ***mytest***，子網域的格式就會是 ***contosotest.p.azurewebsites.net***，該應用程式的 URL 則會是 ***mytest.contosotest.p.azurewebsites.net***。</span><span class="sxs-lookup"><span data-stu-id="0fb70-150">If your ASE was called ***contosotest*** and your app in that ASE was called ***mytest*** then the subdomain would be of the format ***contosotest.p.azurewebsites.net*** and the URL for that app would be ***mytest.contosotest.p.azurewebsites.net***.</span></span> <span data-ttu-id="0fb70-151">如果您將 VIP 類型設定為 [內部]，您的 ASE 名稱不會在 ASE 的子網域中使用。</span><span class="sxs-lookup"><span data-stu-id="0fb70-151">If you set the VIP Type to Internal, your ASE name is not used in the subdomain for the ASE.</span></span> <span data-ttu-id="0fb70-152">您可以明確地指定子網域。</span><span class="sxs-lookup"><span data-stu-id="0fb70-152">You specify the subdomain explicitly.</span></span> <span data-ttu-id="0fb70-153">如果您的子網域是 ***contoso.corp.net*** 而您在該 ASE 中建立一個名為 ***timereporting*** 的應用程式，該應用程式的 URL 會是 ***timereporting.contoso.corp.net***。</span><span class="sxs-lookup"><span data-stu-id="0fb70-153">If your subdomain was ***contoso.corp.net*** and you made an app in that ASE named ***timereporting*** then the URL for that app would be ***timereporting.contoso.corp.net***.</span></span>

## <a name="apps-in-an-ilb-ase"></a><span data-ttu-id="0fb70-154">ILB ASE 中的 App</span><span class="sxs-lookup"><span data-stu-id="0fb70-154">Apps in an ILB ASE</span></span>
<span data-ttu-id="0fb70-155">在 ILB ASE 中建立 app，通常與在 ASE 中建立 app 相同。</span><span class="sxs-lookup"><span data-stu-id="0fb70-155">Creating an app in an ILB ASE is the same as creating an app in an ASE normally.</span></span> 

1. <span data-ttu-id="0fb70-156">在 Azure 入口網站選取 [新增] -> [Web + 行動] -> [Web] 或 [行動]，或者 [API 應用程式]</span><span class="sxs-lookup"><span data-stu-id="0fb70-156">In the Azure portal select **New -> Web + Mobile -> Web** or **Mobile** or **API App**</span></span>
2. <span data-ttu-id="0fb70-157">輸入 app 的名稱</span><span class="sxs-lookup"><span data-stu-id="0fb70-157">Enter name of app</span></span>
3. <span data-ttu-id="0fb70-158">選取訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0fb70-158">Select subscription</span></span>
4. <span data-ttu-id="0fb70-159">選取或建立資源群組</span><span class="sxs-lookup"><span data-stu-id="0fb70-159">Select or create resource group</span></span>
5. <span data-ttu-id="0fb70-160">選取或建立 App Service 方案 (ASP)。</span><span class="sxs-lookup"><span data-stu-id="0fb70-160">Select or create App Service Plan(ASP).</span></span> <span data-ttu-id="0fb70-161">如果是建立新的 ASP，請選取您的 ASE 作為位置並選取您希望在其中建立 ASP 的背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="0fb70-161">If creating a new ASP then select your ASE as the location and select the worker pool you want your ASP to be created in.</span></span> <span data-ttu-id="0fb70-162">當您建立 ASP 時，可以選取您的 ASE 作為位置與背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="0fb70-162">When you create the ASP you select your ASE as the location and the worker pool.</span></span> <span data-ttu-id="0fb70-163">當您指定 app 的名稱時，您會看見您 app 名稱底下的子網域會由您 ASE 的子網域取代。</span><span class="sxs-lookup"><span data-stu-id="0fb70-163">When you specify the name of the app you will see that the subdomain under your app name is replaced by the subdomain for your ASE.</span></span> 
6. <span data-ttu-id="0fb70-164">選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="0fb70-164">Select Create.</span></span> <span data-ttu-id="0fb70-165">如果您希望 app 顯示在儀表板上，您應該選取 [釘選到儀表板]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0fb70-165">You should select the **Pin to dashboard** checkbox if you want the app to show up on your dashboard.</span></span> 

![][2]

<span data-ttu-id="0fb70-166">在 app 名稱底下，子網域名稱會更新，以反映您的 ASE 子網域。</span><span class="sxs-lookup"><span data-stu-id="0fb70-166">Under the app name the subdomain name gets updated to reflect the subdomain of your ASE.</span></span> 

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="0fb70-167">ILB ASE 建立後驗證</span><span class="sxs-lookup"><span data-stu-id="0fb70-167">Post ILB ASE creation validation</span></span>
<span data-ttu-id="0fb70-168">ILB ASE 與非 ILB ASE 稍微有些不同。</span><span class="sxs-lookup"><span data-stu-id="0fb70-168">An ILB ASE is slightly different than the non-ILB ASE.</span></span> <span data-ttu-id="0fb70-169">如先前所述，您必須管理您自己的 DNS，而且您也必須提供您自己的 HTTPS 連線憑證。</span><span class="sxs-lookup"><span data-stu-id="0fb70-169">As already noted you need to manage your own DNS and you also have to provide your own certificate for HTTPS connections.</span></span> 

<span data-ttu-id="0fb70-170">建立您的 ASE 之後，您會注意到子網域顯示您所指定的子網域，且 [設定] 功能表中會有一個稱為 [ILB 憑證] 的新項目。</span><span class="sxs-lookup"><span data-stu-id="0fb70-170">After you create your ASE you will notice that the subdomain shows the subdomain you specified and there is a new item in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="0fb70-171">ASE 是使用可易於測試 HTTPS 的自我簽署憑證建立。</span><span class="sxs-lookup"><span data-stu-id="0fb70-171">The ASE is created with a self-signed certificate which makes it easier to test HTTPS.</span></span> <span data-ttu-id="0fb70-172">入口網站會讓您知道您需要針對 HTTPS 提供自己的憑證，但這是要促使您擁有子網域附帶的憑證。</span><span class="sxs-lookup"><span data-stu-id="0fb70-172">The portal will tell you that you need to provide your own certificate for HTTPS but this is to drive you to have a certificate that goes with your subdomain.</span></span> 

![][3]

<span data-ttu-id="0fb70-173">如果您只是要測試而且不知道如何建立憑證，您可以使用 IIS MMC 主控台應用程式來建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="0fb70-173">If you are simply trying things out and don't know how to create a certificate, you can use the IIS MMC console application to create a self signed certificate.</span></span> <span data-ttu-id="0fb70-174">建立之後，您可以將它匯出為 .pfx 檔案，然後在 ILB 憑證 UI 中上傳。</span><span class="sxs-lookup"><span data-stu-id="0fb70-174">Once it is created you can export it as a .pfx file and then upload it in the ILB Certificate UI.</span></span> <span data-ttu-id="0fb70-175">當您存取使用自我簽署憑證保護的網站時，您的瀏覽器將發出警告指出您正在存取的網站不安全，因為無法驗證憑證。</span><span class="sxs-lookup"><span data-stu-id="0fb70-175">When you access a site secured with a self-signed certificate, your browser will give you a warning that the site you are accessing is not secure due to the inability to validate the certificate.</span></span> <span data-ttu-id="0fb70-176">如果您想要避免這個警告產生，您需要一個符合您的子網域、具有您的瀏覽器已識別的信任鏈結，並且已經正確簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="0fb70-176">If you want to avoid that warning you need a properly signed certificate that matches your subdomain and has a chain of trust that is recognized by your browser.</span></span>

![][6]

<span data-ttu-id="0fb70-177">如果您想要使用您自己的憑證嘗試流程，並測試對 ASE 的 HTTP 和 HTTPS 存取：</span><span class="sxs-lookup"><span data-stu-id="0fb70-177">If you want to try the flow with your own certificates and test both HTTP and HTTPS access to your ASE:</span></span>

1. <span data-ttu-id="0fb70-178">在建立 ASE 之後移至 ASE UI ([ASE] -> [設定] -> [ILB 憑證])</span><span class="sxs-lookup"><span data-stu-id="0fb70-178">Go to ASE UI after ASE is created **ASE -> Settings -> ILB Certificates**</span></span>
2. <span data-ttu-id="0fb70-179">選取憑證 .pfx 檔案並提供密碼，來設定 ILB 憑證。</span><span class="sxs-lookup"><span data-stu-id="0fb70-179">Set ILB certificate by selecting certificate pfx file and provide password.</span></span> <span data-ttu-id="0fb70-180">這個步驟需要一些時間來處理，且會顯示調整作業正在進行中的訊息。</span><span class="sxs-lookup"><span data-stu-id="0fb70-180">This step takes a little while to process and the message that a scaling operation is in progress will be shown.</span></span>
3. <span data-ttu-id="0fb70-181">取得您 ASE 的 ILB 位址 ([ASE] -> [屬性] -> [虛擬 IP 位址])</span><span class="sxs-lookup"><span data-stu-id="0fb70-181">Get the ILB address for your ASE (**ASE -> Properties -> Virtual IP Address**)</span></span>
4. <span data-ttu-id="0fb70-182">建立後，在 ASE 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0fb70-182">Create a web app in ASE after creation</span></span> 
5. <span data-ttu-id="0fb70-183">如果您在該 VNET 中沒有 VM 的話，請建立一個 (不是在與 ASE 相同的子網路中，否則會無法運作)</span><span class="sxs-lookup"><span data-stu-id="0fb70-183">Create a VM if you don't have one in that VNET (Not in the same subnet as the ASE or things break)</span></span>
6. <span data-ttu-id="0fb70-184">設定您子網域的 DNS。</span><span class="sxs-lookup"><span data-stu-id="0fb70-184">Set DNS for your subdomain.</span></span> <span data-ttu-id="0fb70-185">您可以在您 DNS 中使用萬用字元搭配您的子網域，或者如果您想要執行一些簡單測試，請編輯您 VM 上的主機檔案來將 Web 應用程式名稱設定為 VIP IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0fb70-185">You can use a wildcard with your subdomain in your DNS or if you want to do some simple tests, edit the hosts file on your VM to set web app name to VIP IP address.</span></span> <span data-ttu-id="0fb70-186">如果您的 ASE 具有子網域名稱 .ilbase.com 且 Web 應用程式名稱為 mytestapp，它將會定址為 mytestapp.ilbase.com 並在您的主機檔案中設定。</span><span class="sxs-lookup"><span data-stu-id="0fb70-186">If your ASE had the subdomain name .ilbase.com and you made the web app mytestapp so that it would be addressed at mytestapp.ilbase.com then set that in your hosts file.</span></span> <span data-ttu-id="0fb70-187">(在 Windows 上，主機檔案位於 C:\Windows\System32\drivers\etc\ )</span><span class="sxs-lookup"><span data-stu-id="0fb70-187">(On Windows the hosts file is at C:\Windows\System32\drivers\etc\ )</span></span>
7. <span data-ttu-id="0fb70-188">在該 VM 上使用瀏覽器並移至 http://mytestapp.ilbase.com (或者您的 Web 應用程式名稱與您的子網域)</span><span class="sxs-lookup"><span data-stu-id="0fb70-188">Use a browser on that VM and go to http://mytestapp.ilbase.com (or whatever your web app name is with your subdomain)</span></span>
8. <span data-ttu-id="0fb70-189">在該 VM 上使用瀏覽器並移至 https://mytestapp.ilbase.com，如果使用自我簽署憑證，您將必須接受安全性不足的問題。</span><span class="sxs-lookup"><span data-stu-id="0fb70-189">Use a browser on that VM and go to https://mytestapp.ilbase.com You will have to accept the lack of security if using a self-signed certificate.</span></span> 

<span data-ttu-id="0fb70-190">您 ILB 的 IP 位址會在您的 [屬性] 中列出為 [虛擬 IP 位址]</span><span class="sxs-lookup"><span data-stu-id="0fb70-190">The IP address for your ILB is listed in your Properties as the Virtual IP Address</span></span>

![][4]

## <a name="using-an-ilb-ase"></a><span data-ttu-id="0fb70-191">使用 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="0fb70-191">Using an ILB ASE</span></span>
#### <a name="network-security-groups"></a><span data-ttu-id="0fb70-192">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="0fb70-192">Network Security Groups</span></span>
<span data-ttu-id="0fb70-193">ILB ASE 可針對您的 app 啟用網路隔離，讓 app 無法透過網際網路存取或讓 app 在網際網路中完全找不到。</span><span class="sxs-lookup"><span data-stu-id="0fb70-193">An ILB ASE enables network isolation for your apps as the apps are not accessible or even known by the internet.</span></span> <span data-ttu-id="0fb70-194">這非常適合用來裝載內部網路網站，例如企業營運應用程式。</span><span class="sxs-lookup"><span data-stu-id="0fb70-194">This is excellent for hosting intranet sites such as line of business applications.</span></span> <span data-ttu-id="0fb70-195">當您需要更進一步地限制存取時，您仍然可以使用「網路安全性群組 (NSG)」來控制網路層級的存取。</span><span class="sxs-lookup"><span data-stu-id="0fb70-195">When you need to restrict access even further you can still use Network Security Groups(NSGs) to control access at the network level.</span></span> 

<span data-ttu-id="0fb70-196">如果您想要使用 NSG 來進一步限制存取，您需要確定您不會中斷 ASE 運作所需的通訊。</span><span class="sxs-lookup"><span data-stu-id="0fb70-196">If you wish to use NSGs to further restrict access then you need to make sure you do not break the communication that the ASE needs in order to operate.</span></span> <span data-ttu-id="0fb70-197">即使 HTTP/HTTPS 存取只會透過 ASE 所使用的 ILB 進行，ASE 仍需依賴 VNet 外部資源。</span><span class="sxs-lookup"><span data-stu-id="0fb70-197">Even though the HTTP/HTTPS access is only through the ILB used by the ASE the ASE still depends on resource outside of the VNet.</span></span> <span data-ttu-id="0fb70-198">若要查看仍需要何種網路存取權，請查看[控制 App Service 環境的輸入流量][ControlInbound]和[使用 ExpressRoute 的 App Service 環境的網路組態詳細資料][ExpressRoute]中的文件所提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="0fb70-198">To see what network access is still required look at the information in the document on [Controlling Inbound Traffic to an App Service Environment][ControlInbound] and the document on [Network Configuration Details for App Service Environments with ExpressRoute][ExpressRoute].</span></span> 

<span data-ttu-id="0fb70-199">若要設定您的 NSG，您需要知道 Azure 所使用的 IP 位址，以管理您的 ASE。</span><span class="sxs-lookup"><span data-stu-id="0fb70-199">To configure your NSGs you need to know the IP address that is used by Azure to manage your ASE.</span></span> <span data-ttu-id="0fb70-200">如果該 IP 位址提出網際網路要求，它也會成為您 ASE 的輸出 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0fb70-200">That IP address is also the outbound IP address from your ASE if it makes internet requests.</span></span> <span data-ttu-id="0fb70-201">在 ASE 的存留期內，ASE 的輸出 IP 位址仍維持不變。</span><span class="sxs-lookup"><span data-stu-id="0fb70-201">The outbound IP address for your ASE will remain static for the life of your ASE.</span></span> <span data-ttu-id="0fb70-202">如果您刪除並重建 ASE，您會收到新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0fb70-202">If you delete and recreate your ASE, you will get a new IP address.</span></span> <span data-ttu-id="0fb70-203">若要尋找此 IP 位址，請移至 [設定] -> [屬性] 並尋找 [輸出 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="0fb70-203">To find this IP address go to **Settings -> Properties** and find the **Outbound IP Address**.</span></span> 

![][5]

#### <a name="general-ilb-ase-management"></a><span data-ttu-id="0fb70-204">一般 ILB ASE 管理</span><span class="sxs-lookup"><span data-stu-id="0fb70-204">General ILB ASE management</span></span>
<span data-ttu-id="0fb70-205">管理 ILB ASE 通常大部分與管理 ASE 相同。</span><span class="sxs-lookup"><span data-stu-id="0fb70-205">Managing an ILB ASE is largely the same as managing an ASE normally.</span></span> <span data-ttu-id="0fb70-206">您需要相應增加您的背景工作集區來裝載更多 ASP 執行個體，並相應增加您的前端伺服器，以處理增加的 HTTP/HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="0fb70-206">You need to scale up your worker pools to host more ASP instances and scale up your Front End servers to handle increased amounts of HTTP/HTTPS traffic.</span></span> <span data-ttu-id="0fb70-207">如需管理 ASE 組態的一般資訊，請參閱[設定 App Service 環境][ASEConfig]中的文件。</span><span class="sxs-lookup"><span data-stu-id="0fb70-207">For general information on managing the configuration of an ASE, read the document on [Configuring an App Service Environment][ASEConfig].</span></span> 

<span data-ttu-id="0fb70-208">其他管理項目是憑證管理和 DNS 管理。</span><span class="sxs-lookup"><span data-stu-id="0fb70-208">The additional management items are certificate management and DNS management.</span></span> <span data-ttu-id="0fb70-209">在建立 ILB ASE 之後，您必須取得並上傳針對 HTTPS 使用的憑證，並在它到期之前將它取代。</span><span class="sxs-lookup"><span data-stu-id="0fb70-209">You need to obtain and upload the certificate used for HTTPS after ILB ASE creation and replace it before it expires.</span></span> <span data-ttu-id="0fb70-210">因為 Azure 擁有基底網域，所以我們可以使用外部 VIP 提供 ASE 的憑證。</span><span class="sxs-lookup"><span data-stu-id="0fb70-210">Because Azure owns the base domain we can provide certificates for ASEs with an External VIP.</span></span> <span data-ttu-id="0fb70-211">因為 ILB ASE 所使用的子網域可以是任何項目，所以您必須提供您自己的 HTTPS 憑證。</span><span class="sxs-lookup"><span data-stu-id="0fb70-211">Since the subdomain used by an ILB ASE can be anything, you need to provide your own certificate for HTTPS.</span></span> 

#### <a name="dns-configuration"></a><span data-ttu-id="0fb70-212">DNS 組態</span><span class="sxs-lookup"><span data-stu-id="0fb70-212">DNS Configuration</span></span>
<span data-ttu-id="0fb70-213">使用外部 VIP 時，DNS 是由 Azure 管理。</span><span class="sxs-lookup"><span data-stu-id="0fb70-213">When using an External VIP the DNS is managed by Azure.</span></span> <span data-ttu-id="0fb70-214">在您 ASE 中建立的任何 app 都會自動新增至 Azure DNS，這是一個公用 DNS。</span><span class="sxs-lookup"><span data-stu-id="0fb70-214">Any app created in your ASE is automatically added to Azure DNS which is a public DNS.</span></span> <span data-ttu-id="0fb70-215">在 ILB ASE 中，您必須管理您自己的 DNS。</span><span class="sxs-lookup"><span data-stu-id="0fb70-215">In an ILB ASE you have to manage your own DNS.</span></span> <span data-ttu-id="0fb70-216">針對指定的子網域 (例如 contoso.corp.net)，您必須建立指向您 ILB 位址的 DNS A 記錄，以︰</span><span class="sxs-lookup"><span data-stu-id="0fb70-216">For a given subdomain such as contoso.corp.net you need to create DNS A records that point to your ILB address for:</span></span>

    * 
    <span data-ttu-id="0fb70-217">*.scm ftp 發佈</span><span class="sxs-lookup"><span data-stu-id="0fb70-217">*.scm ftp publish</span></span> 


## <a name="getting-started"></a><span data-ttu-id="0fb70-218">開始使用</span><span class="sxs-lookup"><span data-stu-id="0fb70-218">Getting started</span></span>
<span data-ttu-id="0fb70-219">您可以在 [應用程式服務環境的讀我檔案](../app-service/app-service-app-service-environments-readme.md)中取得 App Service 環境的所有相關文章與做法。</span><span class="sxs-lookup"><span data-stu-id="0fb70-219">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="0fb70-220">若要開始使用 App Service Environment，請參閱 [App Service Environment 簡介][WhatisASE]</span><span class="sxs-lookup"><span data-stu-id="0fb70-220">To get started with App Service Environments, see [Introduction to App Service Environments][WhatisASE]</span></span>

<span data-ttu-id="0fb70-221">如需有關 Azure App Service 平台的詳細資訊，請參閱 [Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="0fb70-221">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
