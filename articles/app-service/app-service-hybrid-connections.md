---
title: "Azure App Service 混合式連線 | Microsoft Docs"
description: "如何建立和使用混合式連線以存取不同網路的資源"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: fef9e7b280387934cb093f51b4c8aa134a3b87e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-hybrid-connections"></a><span data-ttu-id="0e24f-103">Azure App Service 混合式連線</span><span class="sxs-lookup"><span data-stu-id="0e24f-103">Azure App Service Hybrid Connections</span></span> #

## <a name="overview"></a><span data-ttu-id="0e24f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0e24f-104">Overview</span></span> ##

<span data-ttu-id="0e24f-105">混合式連線既是 Azure 服務，也是 Azure App Service 功能。</span><span class="sxs-lookup"><span data-stu-id="0e24f-105">Hybrid Connections is both a service in Azure as well as a feature in the Azure App Service.</span></span>  <span data-ttu-id="0e24f-106">作為服務時，它具有 Azure App Service 所利用之用途和功能以外的用途和功能。</span><span class="sxs-lookup"><span data-stu-id="0e24f-106">As a service it has use and capabilities beyond those that are leveraged in the Azure App Service.</span></span>  <span data-ttu-id="0e24f-107">若要深入了解混合式連線以及其在 Azure App Service 之外的使用方式，您可以從 [Azure 轉送混合式連線][HCService]來開始</span><span class="sxs-lookup"><span data-stu-id="0e24f-107">To learn more about Hybrid Connections and their usage outside of the Azure App Service you can start here, [Azure Relay Hybrid Connections][HCService]</span></span>

<span data-ttu-id="0e24f-108">在 Azure App Service 中，混合式連線可用來存取其他網路的應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="0e24f-108">Within the Azure App Service, hybrid connections can be used to access application resources in other networks.</span></span> <span data-ttu-id="0e24f-109">它可讓您從應用程式存取應用程式端點。</span><span class="sxs-lookup"><span data-stu-id="0e24f-109">It provides access FROM your app TO an application endpoint.</span></span>  <span data-ttu-id="0e24f-110">它無法讓您以其他功能來存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e24f-110">It does not enable an alternative capability to access your application.</span></span>  <span data-ttu-id="0e24f-111">和在 App Service 中使用時相同，每個混合式連線都會與單一 TCP 主機和連接埠的組合相互關聯。</span><span class="sxs-lookup"><span data-stu-id="0e24f-111">As used in the App Service, each hybrid connection correlates to a single TCP host and port combination.</span></span>  <span data-ttu-id="0e24f-112">這表示混合式連線端點可以位於任何作業系統和任何應用程式上，只要您有叫用 TCP 接聽連接埠就行。</span><span class="sxs-lookup"><span data-stu-id="0e24f-112">This means that the hybrid connection endpoint can be on any operating system and any application provided you are hitting a TCP listening port.</span></span> <span data-ttu-id="0e24f-113">混合式連線不知道 (或不在意) 應用程式通訊協定為何或您要存取什麼資源。</span><span class="sxs-lookup"><span data-stu-id="0e24f-113">Hybrid connections does not know or care what the application protocol is or what you are accessing.</span></span>  <span data-ttu-id="0e24f-114">它只負責提供網路存取。</span><span class="sxs-lookup"><span data-stu-id="0e24f-114">It is simply providing network access.</span></span>  


## <a name="how-it-works"></a><span data-ttu-id="0e24f-115">運作方式</span><span class="sxs-lookup"><span data-stu-id="0e24f-115">How it works</span></span> ##
<span data-ttu-id="0e24f-116">混合式連線功能是由服務匯流排轉送的兩個輸出呼叫所組成。</span><span class="sxs-lookup"><span data-stu-id="0e24f-116">The hybrid connections feature consists of two outbound calls to Service Bus Relay.</span></span>  <span data-ttu-id="0e24f-117">系統會從應用程式在應用程式服務中執行所在之主機上的程式庫進行連線，然後再從混合式連線管理員 (HCM) 連線到服務匯流排轉送。</span><span class="sxs-lookup"><span data-stu-id="0e24f-117">There is a connection from a library on the host where your app is running in the app service and then there is a connection from the Hybrid Connection Manager(HCM) to Service Bus relay.</span></span>  <span data-ttu-id="0e24f-118">HCM 是轉送服務，您會將它部署在網路裝載內</span><span class="sxs-lookup"><span data-stu-id="0e24f-118">The HCM is a relay service that you deploy within the network hosting</span></span> 

<span data-ttu-id="0e24f-119">透過兩個聯結的連線，應用程式會對 HCM 另一端的固定「主機:連接埠」組合建立 TCP 通道。</span><span class="sxs-lookup"><span data-stu-id="0e24f-119">Through the two joined connections your app has a TCP tunnel to a fixed host:port combination on the other side of the HCM.</span></span>  <span data-ttu-id="0e24f-120">連線會使用 TLS 1.2 來獲得安全性，並使用 SAS 金鑰來進行驗證/授權。</span><span class="sxs-lookup"><span data-stu-id="0e24f-120">The connection uses TLS 1.2 for security and SAS keys for authentication/authorization.</span></span>    

![][1]

<span data-ttu-id="0e24f-121">當應用程式所提出的 DNS 要求符合所設定的混合式連線端點時，系統就會將輸出 TCP 流量往下朝混合式連線進行重新導向。</span><span class="sxs-lookup"><span data-stu-id="0e24f-121">When your app makes a DNS request that matches a configure Hybrid Connection endpoint, then the outbound TCP traffic will be redirected down the hybrid connection.</span></span>  

> [!NOTE]
> <span data-ttu-id="0e24f-122">這表示您應該嘗試一律對混合式連線使用 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="0e24f-122">This means that you should try to always use a DNS name for your Hybrid Connection.</span></span>  <span data-ttu-id="0e24f-123">如果端點改為使用 IP 位址，某些用戶端軟體不會執行 DNS 查閱。</span><span class="sxs-lookup"><span data-stu-id="0e24f-123">Some client software does not do a DNS lookup if the endpoint uses an IP address instead.</span></span>
>
>

<span data-ttu-id="0e24f-124">混合式連線有兩種，分別是在 Azure 轉送底下以服務形式來提供的新式混合式連線，以及舊式的 BizTalk 混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-124">There are two types of hybrid connections, the new hybrid connections that are offered as a service under Azure Relay and the older BizTalk Hybrid Connections.</span></span>  <span data-ttu-id="0e24f-125">在入口網站中，舊式的 BizTalk 混合式連線稱為傳統混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-125">The older BizTalk Hybrid Connections are referred to as Classic Hybrid Connections in the portal.</span></span>  <span data-ttu-id="0e24f-126">本文稍後會提供這種連線的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0e24f-126">There is more information later in this document about them.</span></span>

### <a name="app-service-hybrid-connection-benefits"></a><span data-ttu-id="0e24f-127">App Service 混合式連線的好處</span><span class="sxs-lookup"><span data-stu-id="0e24f-127">App Service hybrid connection benefits</span></span> ###

<span data-ttu-id="0e24f-128">混合式連線功能的諸多好處如下</span><span class="sxs-lookup"><span data-stu-id="0e24f-128">There are a number of benefits to the hybrid connections capability including</span></span>

- <span data-ttu-id="0e24f-129">應用程式可以安全地存取內部部署系統和服務</span><span class="sxs-lookup"><span data-stu-id="0e24f-129">Apps can securely access on premises systems and services securely</span></span>
- <span data-ttu-id="0e24f-130">此功能不需要可從網際網路存取的端點</span><span class="sxs-lookup"><span data-stu-id="0e24f-130">the feature does not require an internet accessible endpoint</span></span>
- <span data-ttu-id="0e24f-131">安裝速度快且過程簡單</span><span class="sxs-lookup"><span data-stu-id="0e24f-131">it is quick and easy to set up</span></span>  
- <span data-ttu-id="0e24f-132">每個混合式連線都會與單一的「主機:連接埠」組合匹配，因此具有良好的安全性</span><span class="sxs-lookup"><span data-stu-id="0e24f-132">each hybrid connection matches to a single host:port combination which is an excellent security aspect</span></span>
- <span data-ttu-id="0e24f-133">它通常不需要防火牆漏洞，因為所有連線都是透過標準的 Web 連接埠來輸出</span><span class="sxs-lookup"><span data-stu-id="0e24f-133">it normally does not require firewall holes as the connections are all outbound over standard web ports</span></span>
- <span data-ttu-id="0e24f-134">因為這是網路層級的功能，因此也表示此功能不會因為應用程式所使用的語言以及端點所使用的技術而受到影響</span><span class="sxs-lookup"><span data-stu-id="0e24f-134">because the feature is network level that also means that it is agnostic to the language used by your app and the technology used by the endpoint</span></span>
- <span data-ttu-id="0e24f-135">它可用來讓您從單一應用程式存取多個網路</span><span class="sxs-lookup"><span data-stu-id="0e24f-135">it can be used to provide access in multiple networks from a single app</span></span> 

### <a name="things-you-cannot-do-with-hybrid-connections"></a><span data-ttu-id="0e24f-136">混合式連線無法執行的作業</span><span class="sxs-lookup"><span data-stu-id="0e24f-136">Things you cannot do with Hybrid Connections</span></span> ###

<span data-ttu-id="0e24f-137">您無法透過混合式連線來執行的一些作業如下：</span><span class="sxs-lookup"><span data-stu-id="0e24f-137">There are a few things you cannot do with hybrid connections and they include:</span></span>

- <span data-ttu-id="0e24f-138">掛接磁碟機</span><span class="sxs-lookup"><span data-stu-id="0e24f-138">mounting a drive</span></span>
- <span data-ttu-id="0e24f-139">使用 UDP</span><span class="sxs-lookup"><span data-stu-id="0e24f-139">using UDP</span></span>
- <span data-ttu-id="0e24f-140">存取使用動態連接埠的 TCP 型服務 (例如，FTP 被動模式或延伸被動模式)</span><span class="sxs-lookup"><span data-stu-id="0e24f-140">accessing TCP based services that use dynamic ports such as FTP Passive Mode or Extended Passive Mode</span></span>
- <span data-ttu-id="0e24f-141">LDAP 支援，因為它有時需要 UDP</span><span class="sxs-lookup"><span data-stu-id="0e24f-141">LDAP support, as it sometimes requires UDP</span></span>
- <span data-ttu-id="0e24f-142">Active Directory 支援</span><span class="sxs-lookup"><span data-stu-id="0e24f-142">Active Directory support</span></span>

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a><span data-ttu-id="0e24f-143">在應用程式中新增和建立混合式連線</span><span class="sxs-lookup"><span data-stu-id="0e24f-143">Adding and Creating a Hybrid Connection in your App</span></span> ##

<span data-ttu-id="0e24f-144">您可以透過應用程式入口網站或從混合式連線服務入口網站，來建立混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-144">Hybrid Connections can be created through the app portal or from the Hybrid Connection service portal.</span></span>  <span data-ttu-id="0e24f-145">強烈建議您使用應用程式入口網站來建立要用於應用程式的混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-145">It is highly recommended that you use the app portal to create the Hybrid Connections you wish to use with your app.</span></span>  <span data-ttu-id="0e24f-146">若要建立混合式連線，請移至 [Azure 入口網站][portal]，然後進到應用程式的 UI。</span><span class="sxs-lookup"><span data-stu-id="0e24f-146">To create a Hybrid Connection go to the [Azure portal][portal] and go into the UI for your app.</span></span>  <span data-ttu-id="0e24f-147">選取 [網路] > [設定混合式連線端點]。</span><span class="sxs-lookup"><span data-stu-id="0e24f-147">Select **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="0e24f-148">您可以在這裡看到應用程式所設定的混合式連線</span><span class="sxs-lookup"><span data-stu-id="0e24f-148">From here you can see the Hybrid Connections that are configured with your app</span></span>  

![][2]

<span data-ttu-id="0e24f-149">若要新增混合式連線，請按一下 [新增混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="0e24f-149">To add a new Hybrid Connection, click Add Hybrid Connection.</span></span>  <span data-ttu-id="0e24f-150">所開啟的 UI 會列出您已建立的混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-150">The UI that opens up lists the Hybrid Connections that you have already created.</span></span>  <span data-ttu-id="0e24f-151">若要在應用程式中新增其中的一或多個混合式連線，請按一下您想要的混合式連線，並按下 [新增選取的混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="0e24f-151">To add one or more of them to your app, click on the ones you want and hit **Add selected hybrid connection**.</span></span>  

![][3]

<span data-ttu-id="0e24f-152">如果您想要建立新的混合式連線，請按一下 [建立新的混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="0e24f-152">If you want to create a new Hybrid Connection, click **Create new hybrid connection**.</span></span>  <span data-ttu-id="0e24f-153">您可以在這裡指定：</span><span class="sxs-lookup"><span data-stu-id="0e24f-153">From here you specify the:</span></span> 

- <span data-ttu-id="0e24f-154">端點名稱</span><span class="sxs-lookup"><span data-stu-id="0e24f-154">endpoint name</span></span>
- <span data-ttu-id="0e24f-155">端點主機名稱</span><span class="sxs-lookup"><span data-stu-id="0e24f-155">endpoint hostname</span></span>
- <span data-ttu-id="0e24f-156">端點連接埠</span><span class="sxs-lookup"><span data-stu-id="0e24f-156">endpoint port</span></span>
- <span data-ttu-id="0e24f-157">您想要使用的服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="0e24f-157">servicebus namespace you wish to use</span></span>

![][4]

<span data-ttu-id="0e24f-158">每個混合式連線都會繫結至一個服務匯流排命名空間，而且每個服務匯流排命名空間都位於 Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="0e24f-158">Every hybrid connection is tied to a service bus namespace and each service bus namespace is in an Azure region.</span></span>  <span data-ttu-id="0e24f-159">請務必嘗試並使用和應用程式位於相同區域的服務匯流排命名空間，以避免網路所引發的延遲。</span><span class="sxs-lookup"><span data-stu-id="0e24f-159">It is important to try and use a service bus namespace in the same region as your app so as to avoid network induced latency.</span></span>

<span data-ttu-id="0e24f-160">如果您想要移除應用程式中的混合式連線，請對它按一下滑鼠右鍵，然後選取 [中斷連線]。</span><span class="sxs-lookup"><span data-stu-id="0e24f-160">If you want to remove your hybrid connection from your app, right click on it and select **Disconnect**.</span></span>  

<span data-ttu-id="0e24f-161">在將混合式連線新增至 Web 應用程式後，您只要對它按一下就可以查看其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e24f-161">Once a hybrid connection is added to your web app, you can see details on it by simply clicking on it.</span></span>  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a><span data-ttu-id="0e24f-162">混合式連線和 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="0e24f-162">Hybrid Connections and App Service Plans</span></span> ##

<span data-ttu-id="0e24f-163">您現在只能建立新的混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-163">The only hybrid connections you can now make are the new hybrid connections.</span></span>  <span data-ttu-id="0e24f-164">基本、標準、進階和隔離的定價 SKU 才能使用混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-164">They are only available in Basic, Standard, Premium and Isolated pricing SKUs.</span></span>  <span data-ttu-id="0e24f-165">定價方案會有相關聯的限制。</span><span class="sxs-lookup"><span data-stu-id="0e24f-165">There are limits tied to the pricing plan.</span></span>  

| <span data-ttu-id="0e24f-166">定價方案</span><span class="sxs-lookup"><span data-stu-id="0e24f-166">Pricing Plan</span></span> | <span data-ttu-id="0e24f-167">方案中可用的混合式連線數目</span><span class="sxs-lookup"><span data-stu-id="0e24f-167">Number of hybrid connections usable in the plan</span></span> |
|----|----|
| <span data-ttu-id="0e24f-168">基本</span><span class="sxs-lookup"><span data-stu-id="0e24f-168">Basic</span></span> | <span data-ttu-id="0e24f-169">5</span><span class="sxs-lookup"><span data-stu-id="0e24f-169">5</span></span> |
| <span data-ttu-id="0e24f-170">標準</span><span class="sxs-lookup"><span data-stu-id="0e24f-170">Standard</span></span> | <span data-ttu-id="0e24f-171">25</span><span class="sxs-lookup"><span data-stu-id="0e24f-171">25</span></span> |
| <span data-ttu-id="0e24f-172">進階</span><span class="sxs-lookup"><span data-stu-id="0e24f-172">Premium</span></span> | <span data-ttu-id="0e24f-173">200</span><span class="sxs-lookup"><span data-stu-id="0e24f-173">200</span></span> |
| <span data-ttu-id="0e24f-174">隔離</span><span class="sxs-lookup"><span data-stu-id="0e24f-174">Isolated</span></span> | <span data-ttu-id="0e24f-175">200</span><span class="sxs-lookup"><span data-stu-id="0e24f-175">200</span></span> |

<span data-ttu-id="0e24f-176">因為 App Service 方案有相關限制，因此 App Service 方案會提供 UI，來顯示應用程式所使用的混合式連線數目，以及是哪些應用程式在使用。</span><span class="sxs-lookup"><span data-stu-id="0e24f-176">Since there are App Service Plan restrictions there is also UI in the App Service Plan that shows you how many hybrid connections are being used and by what apps.</span></span>  

![][6]

<span data-ttu-id="0e24f-177">和應用程式檢視一樣，您也可以按一下混合式連線來查看其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e24f-177">Just as with the app view, you can see details on your hybrid connection by clicking on it.</span></span>  <span data-ttu-id="0e24f-178">在這裡所顯示的屬性中，您可以查看您在應用程式檢視中擁有的所有資訊，但也可以查看相同的 App Service 方案內有多少其他應用程式正在使用該混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-178">In the properties shown here you can see all the information you had at the app view but can also see how many other apps in the same App Service Plan are using that hybrid connection.</span></span>

![][7]

<span data-ttu-id="0e24f-179">雖然 App Service 方案中可以使用的混合式連線端點數目有所限制，但所使用的每個混合式連線都可以用於該 App Service 方案中任意數目的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="0e24f-179">While there is a limit on the number of hybrid connection endpoints that can be used in an App Service Plan, each hybrid connection used can be used across any number of apps in that App Service Plan.</span></span>  <span data-ttu-id="0e24f-180">也就是說，如果我將 1 個混合式連線用在 App Service 方案的 5 個不同應用程式中，仍只算 1 個混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-180">That is to say that if I had 1 hybrid connection that I used in 5 separate apps in my App Service Plan, that is still just 1 hybrid connection.</span></span>

<span data-ttu-id="0e24f-181">除了只能用於基本、標準、進階或隔離的 SKU 外，混合式連線還有額外成本。</span><span class="sxs-lookup"><span data-stu-id="0e24f-181">There is an additional cost to hybrid connections beyond being only usable in a Basic, Standard, Premium or Isolated SKU.</span></span>  <span data-ttu-id="0e24f-182">如需混合式連線定價的詳細資訊，請前往這裡︰[服務匯流排定價][sbpricing]。</span><span class="sxs-lookup"><span data-stu-id="0e24f-182">For details on hybrid connection pricing please go here: [Service Bus pricing][sbpricing].</span></span>

## <a name="hybrid-connection-manager"></a><span data-ttu-id="0e24f-183">混合式連線管理員</span><span class="sxs-lookup"><span data-stu-id="0e24f-183">Hybrid Connection Manager</span></span> ##

<span data-ttu-id="0e24f-184">為了讓混合式連線運作，裝載混合式連線端點的網路中必須有轉送代理程式。</span><span class="sxs-lookup"><span data-stu-id="0e24f-184">In order for hybrid connections to work you need a relay agent in the network that hosts your hybrid connection endpoint.</span></span>  <span data-ttu-id="0e24f-185">該轉送代理程式稱為混合式連線管理員 (HCM)。</span><span class="sxs-lookup"><span data-stu-id="0e24f-185">That relay agent is called the Hybrid Connection Manager (HCM).</span></span>  <span data-ttu-id="0e24f-186">您可以在 [Azure 入口網站][portal]中，從應用程式所提供的 UI ([網路] > [設定混合式連線端點]) 下載這項工具。</span><span class="sxs-lookup"><span data-stu-id="0e24f-186">This tool can be downloaded from the **Networking > Configure your hybrid connection endpoints** UI available from your app in the [Azure portal][portal].</span></span>  

<span data-ttu-id="0e24f-187">此工具會在 Windows Server 2008 R2 和更新版本的 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="0e24f-187">This tool runs on Windows server 2008 R2 and later versions of Windows.</span></span>  <span data-ttu-id="0e24f-188">安裝完成後，HCM 會以服務形式來執行。</span><span class="sxs-lookup"><span data-stu-id="0e24f-188">Once installed the HCM runs as a service.</span></span>  <span data-ttu-id="0e24f-189">此服務會根據所設定的端點來連線到 Azure 服務匯流排轉送。</span><span class="sxs-lookup"><span data-stu-id="0e24f-189">This service connects to Azure servicebus relay based on the configured endpoints.</span></span>  <span data-ttu-id="0e24f-190">來自 HCM 的連線會輸出到連接埠 80 和 443。</span><span class="sxs-lookup"><span data-stu-id="0e24f-190">The connections from the HCM are outbound to ports 80 and 443.</span></span>    

<span data-ttu-id="0e24f-191">HCM 有提供 UI 來供您進行設定。</span><span class="sxs-lookup"><span data-stu-id="0e24f-191">The HCM has a UI to configure it.</span></span>  <span data-ttu-id="0e24f-192">HCM 安裝完成後，您可以執行混合式連線管理員安裝目錄中的 HybridConnectionManagerUi.exe 來顯示 UI。</span><span class="sxs-lookup"><span data-stu-id="0e24f-192">After the HCM is installed you can bring up the UI by running the HybridConnectionManagerUi.exe that sits in the Hybrid Connection Manager installation directory.</span></span>  <span data-ttu-id="0e24f-193">在 Windows 10 上，您也可以在搜尋方塊中輸入「混合式連線管理員 UI」來輕鬆取得該 UI。</span><span class="sxs-lookup"><span data-stu-id="0e24f-193">It is also easily reached on Windows 10 by typing *Hybrid Connection Manager UI* in your search box.</span></span>  

<span data-ttu-id="0e24f-194">當 HCM UI 啟動時，您會先看到一個資料表，裡面會列出這個 HCM 執行個體所設定的所有混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-194">When the HCM UI is started, the first thing you see is a table that lists all of the hybrid connections that are configured with this instance of the HCM.</span></span>  <span data-ttu-id="0e24f-195">如果您想要進行變更，您必須對 Azure 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0e24f-195">If you wish to make any changes you will need to authenticate with Azure.</span></span> 

<span data-ttu-id="0e24f-196">若要在 HCM 中新增一或多個混合式連線︰</span><span class="sxs-lookup"><span data-stu-id="0e24f-196">To add one or more Hybrid Connections to your HCM:</span></span>

1. <span data-ttu-id="0e24f-197">啟動 HCM UI</span><span class="sxs-lookup"><span data-stu-id="0e24f-197">Start the HCM UI</span></span>
1. <span data-ttu-id="0e24f-198">按一下 [設定另一個混合式連線] ![][8]</span><span class="sxs-lookup"><span data-stu-id="0e24f-198">Click Configure another hybrid connection ![][8]</span></span>

1. <span data-ttu-id="0e24f-199">使用 Azure 帳戶進行登入</span><span class="sxs-lookup"><span data-stu-id="0e24f-199">Sign in with your Azure account</span></span>
1. <span data-ttu-id="0e24f-200">選擇訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0e24f-200">Choose a subscription</span></span>
1. <span data-ttu-id="0e24f-201">按一下您要讓這個 HCM 轉送的混合式連線 ![][9]</span><span class="sxs-lookup"><span data-stu-id="0e24f-201">Click on the hybrid connections you want this HCM to relay ![][9]</span></span>

1. <span data-ttu-id="0e24f-202">按一下 [Save] \(儲存)。</span><span class="sxs-lookup"><span data-stu-id="0e24f-202">Click Save</span></span>

<span data-ttu-id="0e24f-203">此時，您會看到您新增的混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-203">At this point you will see the hybrid connections you added.</span></span>  <span data-ttu-id="0e24f-204">您也可以按一下所設定的混合式連線，然後查看該連線的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0e24f-204">You can also click on the configured hybrid connection and see details about the connection.</span></span>

![][10]

<span data-ttu-id="0e24f-205">若要讓 HCM 能夠支援其所設定要使用的混合式連線，它需要︰</span><span class="sxs-lookup"><span data-stu-id="0e24f-205">For your HCM to be able to support the hybrid connections it is configured with, it needs:</span></span>

- <span data-ttu-id="0e24f-206">對 Azure 的 TCP 存取權 (透過連接埠 80 和 443)</span><span class="sxs-lookup"><span data-stu-id="0e24f-206">TCP access to Azure over ports 80 and 443</span></span>
- <span data-ttu-id="0e24f-207">對混合式連線端點的 TCP 存取權</span><span class="sxs-lookup"><span data-stu-id="0e24f-207">TCP access to the hybrid connection endpoint</span></span>
- <span data-ttu-id="0e24f-208">可以對端點主機和 Azure 服務匯流排命名空間執行 DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="0e24f-208">ability to do DNS look ups on the endpoint host and the azure servicebus namespace</span></span>

<span data-ttu-id="0e24f-209">HCM 同時支援新式混合式連線以及舊式的 BizTalk 混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-209">The HCM supports both new hybrid connections as well as the older BizTalk hybrid connections.</span></span>

### <a name="redundancy"></a><span data-ttu-id="0e24f-210">備援性</span><span class="sxs-lookup"><span data-stu-id="0e24f-210">Redundancy</span></span> ###

<span data-ttu-id="0e24f-211">每個 HCM 都可以支援多個混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e24f-211">Each HCM can support multiple hybrid connections.</span></span>  <span data-ttu-id="0e24f-212">此外，任何給定的混合式連線也可由多個 HCM 來支援。</span><span class="sxs-lookup"><span data-stu-id="0e24f-212">Also, any given hybrid connection can be supported by multiple HCMs.</span></span>  <span data-ttu-id="0e24f-213">預設行為是在給定端點所設定的 HCM 之間循環配置流量。</span><span class="sxs-lookup"><span data-stu-id="0e24f-213">The default behavior is to round robin traffic across the configured HCMs for any given endpoint.</span></span>  <span data-ttu-id="0e24f-214">如果您想讓網路的混合式連線具有高可用性，只需在不同機器上具現化多個 HCM。</span><span class="sxs-lookup"><span data-stu-id="0e24f-214">If you want high availability on your hybrid connections from your network, simply instantiate multiple HCMs on separate machines.</span></span> 

### <a name="manually-adding-a-hybrid-connection"></a><span data-ttu-id="0e24f-215">手動新增混合式連線</span><span class="sxs-lookup"><span data-stu-id="0e24f-215">Manually adding a hybrid connection</span></span> ###

<span data-ttu-id="0e24f-216">如果您想讓訂用帳戶以外的人員裝載給定混合式連線的 HCM 執行個體，您可以與他們共用混合式連線的閘道連接字串。</span><span class="sxs-lookup"><span data-stu-id="0e24f-216">If you wish somebody outside of your subscription to host an HCM instance for a given hybrid connection, you can share with them the gateway connection string for the hybrid connection.</span></span>  <span data-ttu-id="0e24f-217">在 [Azure 入口網站][portal]中，您可以在混合式連線的屬性中看到此字串。</span><span class="sxs-lookup"><span data-stu-id="0e24f-217">You can see this in the properties for a hybrid connection in the [Azure portal][portal].</span></span> <span data-ttu-id="0e24f-218">若要使用該字串，請在 HCM 中按一下 [手動設定] 按鈕，然後貼入閘道連接字串。</span><span class="sxs-lookup"><span data-stu-id="0e24f-218">To use that string, click the **Configure manually** button in the HCM and paste in the gateway connection string.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="0e24f-219">疑難排解</span><span class="sxs-lookup"><span data-stu-id="0e24f-219">Troubleshooting</span></span> ##

<span data-ttu-id="0e24f-220">當您的混合式連線已設定用於執行中的應用程式，且至少有一個 HCM 已設定混合式連線時，入口網站中的狀態會顯示為**已連線**。</span><span class="sxs-lookup"><span data-stu-id="0e24f-220">When your hybrid connection is set up with a running application and there is at least one HCM that has that hybrid connection configured, then the status will say **Connected** in the portal.</span></span>  <span data-ttu-id="0e24f-221">如果狀態未顯示為**已連線**，則表示您的應用程式已關閉，或是您的 HCM 無法在連接埠 80 或 443 上向外連線到 Azure。</span><span class="sxs-lookup"><span data-stu-id="0e24f-221">If it does not say **Connected** then it means that either your app is down or your HCM cannot connect out to Azure on ports 80 or 443.</span></span>  

<span data-ttu-id="0e24f-222">用戶端無法連線至其端點的主要原因是，端點在指定時所使用的是 IP 位址而非 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="0e24f-222">The primary reason that clients cannot connect to their endpoint is because the endpoint was specified using an IP address instead of a DNS name.</span></span>  <span data-ttu-id="0e24f-223">如果您的應用程式無法連線到所要的端點，且您使用的是 IP 位址，請改為使用對 HCM 執行所在之主機有效的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="0e24f-223">If your app cannot reach the desired endpoint and you used an IP address, switch to using a DNS name that is valid on the host where the HCM is running.</span></span>  <span data-ttu-id="0e24f-224">另外則要檢查 HCM 執行所在的主機上是否已正確解析 DNS 名稱，以及 HCM 執行所在的主機是否可以連線到混合式連線端點。</span><span class="sxs-lookup"><span data-stu-id="0e24f-224">Other things to check are that the DNS name resolves properly on the host where the HCM is running and that there is connectivity from the host where the HCM is running to the hybrid connection endpoint.</span></span>  

<span data-ttu-id="0e24f-225">App Service 中有一個稱為 tcpping 的工具，您可以從主控台叫用這個工具。</span><span class="sxs-lookup"><span data-stu-id="0e24f-225">There is a tool in the App Service that can be invoked from the console called tcpping.</span></span>  <span data-ttu-id="0e24f-226">這個工具可以指出您是否有 TCP 端點的存取權，但不會指出您是否有混合式連線端點的存取權。</span><span class="sxs-lookup"><span data-stu-id="0e24f-226">This tool can tell you if you have access to a TCP endpoint but does not tell you if you have access to a hybrid connection endpoint.</span></span>  <span data-ttu-id="0e24f-227">當您在主控台中對混合式連線端點使用此工具時，成功的 ping 只表示您已為應用程式設定了混合式連線，且此連線使用「主機:連接埠」組合。</span><span class="sxs-lookup"><span data-stu-id="0e24f-227">When used in the console against a hybrid connection endpoint, a successful ping will only tell you that you have a hybrid connection configured for your app that uses that host:port combination.</span></span>  

## <a name="biztalk-hybrid-connections"></a><span data-ttu-id="0e24f-228">BizTalk 混合式連線</span><span class="sxs-lookup"><span data-stu-id="0e24f-228">BizTalk Hybrid Connections</span></span> ##

<span data-ttu-id="0e24f-229">舊式的 BizTalk 混合式連線功能已關閉，以促進 BizTalk 混合式連線的建立。</span><span class="sxs-lookup"><span data-stu-id="0e24f-229">The older BizTalk Hybrid Connections capability has been closed off to further BizTalk Hybrid Connection creations.</span></span>  <span data-ttu-id="0e24f-230">您可以繼續對應用程式使用既有的 BizTalk 混合式連線，但請將其移轉至新服務。</span><span class="sxs-lookup"><span data-stu-id="0e24f-230">You can continue using your preexisting BizTalk Hybrid Connections with your apps but should migrate to the new service.</span></span>  <span data-ttu-id="0e24f-231">相較於 BizTalk 版本，新服務的好處包括︰</span><span class="sxs-lookup"><span data-stu-id="0e24f-231">Among the benefits in the new service over the BizTalk version are:</span></span>

- <span data-ttu-id="0e24f-232">不需要其他 BizTalk 帳戶</span><span class="sxs-lookup"><span data-stu-id="0e24f-232">no additional BizTalk account is required</span></span>
- <span data-ttu-id="0e24f-233">TLS 是 1.2，而非 BizTalk 混合式連線所使用的 1.0</span><span class="sxs-lookup"><span data-stu-id="0e24f-233">TLS is 1.2 instead of 1.0 as in BizTalk Hybrid Connections</span></span>
- <span data-ttu-id="0e24f-234">通訊是使用 DNS 名稱透過連接埠 80 和 443 來連線到 Azure，而非使用 IP 位址和其他連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="0e24f-234">Communication is over ports 80 and 443 using a DNS name to reach Azure instead of IP addresses and a range of additional other ports.</span></span>  

<span data-ttu-id="0e24f-235">若要在您的應用程式中新增 BizTalk 混合式連線，請在 [Azure 入口網站][portal] 中移至您的應用程式，然後按一下 [網路] > [設定混合式連線端點]。</span><span class="sxs-lookup"><span data-stu-id="0e24f-235">To add a BizTalk hybrid connection to your app, go to your app in the [Azure portal][portal] and click **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="0e24f-236">在傳統的混合式連線資料表中，按一下 [新增傳統混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="0e24f-236">In the Classic hybrid connections table click **Add classic hybrid connection**.</span></span>  <span data-ttu-id="0e24f-237">您可以在這裡看到 BizTalk 混合式連線的清單。</span><span class="sxs-lookup"><span data-stu-id="0e24f-237">From here you will see a list of your BizTalk hybrid connections.</span></span>  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/

