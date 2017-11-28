---
title: "aaa\"Azure App Service 混合式連線 |Microsoft 文件 」"
description: "如何在不同的網路中的 toocreate 和使用混合式連線 tooaccess 資源"
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
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a><span data-ttu-id="2d809-103">Azure App Service 混合式連線</span><span class="sxs-lookup"><span data-stu-id="2d809-103">Azure App Service Hybrid Connections</span></span> #

## <a name="overview"></a><span data-ttu-id="2d809-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2d809-104">Overview</span></span> ##

<span data-ttu-id="2d809-105">混合式連線是 Azure 中的服務以及 hello Azure App Service 中的功能。</span><span class="sxs-lookup"><span data-stu-id="2d809-105">Hybrid Connections is both a service in Azure as well as a feature in hello Azure App Service.</span></span>  <span data-ttu-id="2d809-106">為服務，它有使用和之外，可利用 hello Azure App Service 中的功能。</span><span class="sxs-lookup"><span data-stu-id="2d809-106">As a service it has use and capabilities beyond those that are leveraged in hello Azure App Service.</span></span>  <span data-ttu-id="2d809-107">深入了解混合式連線和外部 hello Azure 應用程式服務，您可以從這裡開始，其用法 toolearn [Azure 轉送混合式連線][HCService]</span><span class="sxs-lookup"><span data-stu-id="2d809-107">toolearn more about Hybrid Connections and their usage outside of hello Azure App Service you can start here, [Azure Relay Hybrid Connections][HCService]</span></span>

<span data-ttu-id="2d809-108">Hello Azure 應用程式服務，在混合式連線可以使用的 tooaccess 應用程式的其他網路資源。</span><span class="sxs-lookup"><span data-stu-id="2d809-108">Within hello Azure App Service, hybrid connections can be used tooaccess application resources in other networks.</span></span> <span data-ttu-id="2d809-109">它可從您的應用程式 tooan 應用程式端點的存取。</span><span class="sxs-lookup"><span data-stu-id="2d809-109">It provides access FROM your app tooan application endpoint.</span></span>  <span data-ttu-id="2d809-110">不會啟用其他功能 tooaccess 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d809-110">It does not enable an alternative capability tooaccess your application.</span></span>  <span data-ttu-id="2d809-111">使用 hello App Service 中，每個混合式連接相互關聯 tooa 單一 TCP 主機和連接埠組合。</span><span class="sxs-lookup"><span data-stu-id="2d809-111">As used in hello App Service, each hybrid connection correlates tooa single TCP host and port combination.</span></span>  <span data-ttu-id="2d809-112">這表示該 hello 混合式連接端點可以在任何作業系統和任何應用程式提供到達 TCP 接聽連接埠。</span><span class="sxs-lookup"><span data-stu-id="2d809-112">This means that hello hybrid connection endpoint can be on any operating system and any application provided you are hitting a TCP listening port.</span></span> <span data-ttu-id="2d809-113">混合式連線不知道或在意 hello 應用程式的通訊協定時，或是您要存取。</span><span class="sxs-lookup"><span data-stu-id="2d809-113">Hybrid connections does not know or care what hello application protocol is or what you are accessing.</span></span>  <span data-ttu-id="2d809-114">它只負責提供網路存取。</span><span class="sxs-lookup"><span data-stu-id="2d809-114">It is simply providing network access.</span></span>  


## <a name="how-it-works"></a><span data-ttu-id="2d809-115">運作方式</span><span class="sxs-lookup"><span data-stu-id="2d809-115">How it works</span></span> ##
<span data-ttu-id="2d809-116">hello 混合式連線 」 功能是由兩個輸出呼叫 tooService 匯流排轉送所組成。</span><span class="sxs-lookup"><span data-stu-id="2d809-116">hello hybrid connections feature consists of two outbound calls tooService Bus Relay.</span></span>  <span data-ttu-id="2d809-117">沒有來自其中 hello app service 中執行您的應用程式，而且沒有從 hello 混合式連線 Manager(HCM) tooService 匯流排轉送連線 hello 主機上的程式庫的連接。</span><span class="sxs-lookup"><span data-stu-id="2d809-117">There is a connection from a library on hello host where your app is running in hello app service and then there is a connection from hello Hybrid Connection Manager(HCM) tooService Bus relay.</span></span>  <span data-ttu-id="2d809-118">hello HCM 是您部署內 hello 網路裝載的轉送服務</span><span class="sxs-lookup"><span data-stu-id="2d809-118">hello HCM is a relay service that you deploy within hello network hosting</span></span> 

<span data-ttu-id="2d809-119">Hello 透過兩個聯結的連接，應用程式有 TCP 通道 tooa 固定的主機： 連接埠組合上 hello hello HCM 另一端。</span><span class="sxs-lookup"><span data-stu-id="2d809-119">Through hello two joined connections your app has a TCP tunnel tooa fixed host:port combination on hello other side of hello HCM.</span></span>  <span data-ttu-id="2d809-120">hello 連接使用 TLS 1.2 安全性與驗證/授權的 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2d809-120">hello connection uses TLS 1.2 for security and SAS keys for authentication/authorization.</span></span>    

![][1]

<span data-ttu-id="2d809-121">當您的應用程式發出 DNS 要求符合設定混合式連接端點，然後 hello 輸出 TCP 流量會被重新導向向 hello 混合式連接。</span><span class="sxs-lookup"><span data-stu-id="2d809-121">When your app makes a DNS request that matches a configure Hybrid Connection endpoint, then hello outbound TCP traffic will be redirected down hello hybrid connection.</span></span>  

> [!NOTE]
> <span data-ttu-id="2d809-122">這表示您應該嘗試 tooalways 使用混合式連接的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="2d809-122">This means that you should try tooalways use a DNS name for your Hybrid Connection.</span></span>  <span data-ttu-id="2d809-123">某些用戶端軟體不會進行 DNS 查閱 hello 端點改為使用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2d809-123">Some client software does not do a DNS lookup if hello endpoint uses an IP address instead.</span></span>
>
>

<span data-ttu-id="2d809-124">有兩種類型的混合式連線，hello 新混合式連線會提供給當作 Azure 轉送服務，hello 舊版 BizTalk 混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2d809-124">There are two types of hybrid connections, hello new hybrid connections that are offered as a service under Azure Relay and hello older BizTalk Hybrid Connections.</span></span>  <span data-ttu-id="2d809-125">hello 舊版 BizTalk 混合式連線會在 hello 入口網站的參照的 tooas 傳統的混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2d809-125">hello older BizTalk Hybrid Connections are referred tooas Classic Hybrid Connections in hello portal.</span></span>  <span data-ttu-id="2d809-126">本文稍後會提供這種連線的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2d809-126">There is more information later in this document about them.</span></span>

### <a name="app-service-hybrid-connection-benefits"></a><span data-ttu-id="2d809-127">App Service 混合式連線的好處</span><span class="sxs-lookup"><span data-stu-id="2d809-127">App Service hybrid connection benefits</span></span> ###

<span data-ttu-id="2d809-128">有許多優點 toohello 混合式連線功能，其中包括</span><span class="sxs-lookup"><span data-stu-id="2d809-128">There are a number of benefits toohello hybrid connections capability including</span></span>

- <span data-ttu-id="2d809-129">應用程式可以安全地存取內部部署系統和服務</span><span class="sxs-lookup"><span data-stu-id="2d809-129">Apps can securely access on premises systems and services securely</span></span>
- <span data-ttu-id="2d809-130">hello 功能不需要網際網路存取端點</span><span class="sxs-lookup"><span data-stu-id="2d809-130">hello feature does not require an internet accessible endpoint</span></span>
- <span data-ttu-id="2d809-131">它是快速和輕鬆 tooset 向上</span><span class="sxs-lookup"><span data-stu-id="2d809-131">it is quick and easy tooset up</span></span>  
- <span data-ttu-id="2d809-132">每個混合式連接符合 tooa 單一主機： 連接埠組合，它會是很好的安全性層面</span><span class="sxs-lookup"><span data-stu-id="2d809-132">each hybrid connection matches tooa single host:port combination which is an excellent security aspect</span></span>
- <span data-ttu-id="2d809-133">它通常不需要防火牆漏洞 hello 連線是透過標準的 web 連接埠所有輸出</span><span class="sxs-lookup"><span data-stu-id="2d809-133">it normally does not require firewall holes as hello connections are all outbound over standard web ports</span></span>
- <span data-ttu-id="2d809-134">因為 hello 功能也表示它是由您的應用程式與 hello 技術 hello 端點所使用的無從驗證 toohello 語言的網路層級</span><span class="sxs-lookup"><span data-stu-id="2d809-134">because hello feature is network level that also means that it is agnostic toohello language used by your app and hello technology used by hello endpoint</span></span>
- <span data-ttu-id="2d809-135">它可以從單一應用程式的多個網路中使用 tooprovide 存取</span><span class="sxs-lookup"><span data-stu-id="2d809-135">it can be used tooprovide access in multiple networks from a single app</span></span> 

### <a name="things-you-cannot-do-with-hybrid-connections"></a><span data-ttu-id="2d809-136">混合式連線無法執行的作業</span><span class="sxs-lookup"><span data-stu-id="2d809-136">Things you cannot do with Hybrid Connections</span></span> ###

<span data-ttu-id="2d809-137">您無法透過混合式連線來執行的一些作業如下：</span><span class="sxs-lookup"><span data-stu-id="2d809-137">There are a few things you cannot do with hybrid connections and they include:</span></span>

- <span data-ttu-id="2d809-138">掛接磁碟機</span><span class="sxs-lookup"><span data-stu-id="2d809-138">mounting a drive</span></span>
- <span data-ttu-id="2d809-139">使用 UDP</span><span class="sxs-lookup"><span data-stu-id="2d809-139">using UDP</span></span>
- <span data-ttu-id="2d809-140">存取使用動態連接埠的 TCP 型服務 (例如，FTP 被動模式或延伸被動模式)</span><span class="sxs-lookup"><span data-stu-id="2d809-140">accessing TCP based services that use dynamic ports such as FTP Passive Mode or Extended Passive Mode</span></span>
- <span data-ttu-id="2d809-141">LDAP 支援，因為它有時需要 UDP</span><span class="sxs-lookup"><span data-stu-id="2d809-141">LDAP support, as it sometimes requires UDP</span></span>
- <span data-ttu-id="2d809-142">Active Directory 支援</span><span class="sxs-lookup"><span data-stu-id="2d809-142">Active Directory support</span></span>

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a><span data-ttu-id="2d809-143">在應用程式中新增和建立混合式連線</span><span class="sxs-lookup"><span data-stu-id="2d809-143">Adding and Creating a Hybrid Connection in your App</span></span> ##

<span data-ttu-id="2d809-144">您可以建立混合式連線，透過 hello 應用程式入口網站或從 hello 混合式連接服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="2d809-144">Hybrid Connections can be created through hello app portal or from hello Hybrid Connection service portal.</span></span>  <span data-ttu-id="2d809-145">強烈建議您先使用 hello 應用程式入口網站 toocreate hello 想 toouse 與您的應用程式的混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2d809-145">It is highly recommended that you use hello app portal toocreate hello Hybrid Connections you wish toouse with your app.</span></span>  <span data-ttu-id="2d809-146">toocreate 混合式連接到 toohello [Azure 入口網站][ portal]而進入 hello UI 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d809-146">toocreate a Hybrid Connection go toohello [Azure portal][portal] and go into hello UI for your app.</span></span>  <span data-ttu-id="2d809-147">選取 [網路] > [設定混合式連線端點]。</span><span class="sxs-lookup"><span data-stu-id="2d809-147">Select **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="2d809-148">從這裡您可以看到與您的應用程式設定的 hello 混合式連線</span><span class="sxs-lookup"><span data-stu-id="2d809-148">From here you can see hello Hybrid Connections that are configured with your app</span></span>  

![][2]

<span data-ttu-id="2d809-149">tooadd 新的混合式連接，按一下 新增混合式連接。</span><span class="sxs-lookup"><span data-stu-id="2d809-149">tooadd a new Hybrid Connection, click Add Hybrid Connection.</span></span>  <span data-ttu-id="2d809-150">hello UI 開啟列出您已建立的 hello 混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2d809-150">hello UI that opens up lists hello Hybrid Connections that you have already created.</span></span>  <span data-ttu-id="2d809-151">一或多個這些 tooadd tooyour 應用程式中，按一下 hello 的並叫用**新增選取的混合式連接**。</span><span class="sxs-lookup"><span data-stu-id="2d809-151">tooadd one or more of them tooyour app, click on hello ones you want and hit **Add selected hybrid connection**.</span></span>  

![][3]

<span data-ttu-id="2d809-152">如果您想 toocreate 新的混合式連接，請按一下**建立新的混合式連接**。</span><span class="sxs-lookup"><span data-stu-id="2d809-152">If you want toocreate a new Hybrid Connection, click **Create new hybrid connection**.</span></span>  <span data-ttu-id="2d809-153">您可以在這裡指定：</span><span class="sxs-lookup"><span data-stu-id="2d809-153">From here you specify the:</span></span> 

- <span data-ttu-id="2d809-154">端點名稱</span><span class="sxs-lookup"><span data-stu-id="2d809-154">endpoint name</span></span>
- <span data-ttu-id="2d809-155">端點主機名稱</span><span class="sxs-lookup"><span data-stu-id="2d809-155">endpoint hostname</span></span>
- <span data-ttu-id="2d809-156">端點連接埠</span><span class="sxs-lookup"><span data-stu-id="2d809-156">endpoint port</span></span>
- <span data-ttu-id="2d809-157">您想 toouse 服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="2d809-157">servicebus namespace you wish toouse</span></span>

![][4]

<span data-ttu-id="2d809-158">每個混合式連接繫結的 tooa 服務匯流排命名空間且每個服務匯流排命名空間中的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="2d809-158">Every hybrid connection is tied tooa service bus namespace and each service bus namespace is in an Azure region.</span></span>  <span data-ttu-id="2d809-159">請務必 tootry 和使用服務匯流排命名空間中的 hello 與您的應用程式相同的區域，以 tooavoid 引起的網路延遲。</span><span class="sxs-lookup"><span data-stu-id="2d809-159">It is important tootry and use a service bus namespace in hello same region as your app so as tooavoid network induced latency.</span></span>

<span data-ttu-id="2d809-160">如果您想 tooremove 混合式連線從您的應用程式，以滑鼠右鍵按一下它，然後選取**中斷連線**。</span><span class="sxs-lookup"><span data-stu-id="2d809-160">If you want tooremove your hybrid connection from your app, right click on it and select **Disconnect**.</span></span>  

<span data-ttu-id="2d809-161">一旦混合式連線新增 tooyour web 應用程式，您可以在其上查看詳細資料，只需按一下項目。</span><span class="sxs-lookup"><span data-stu-id="2d809-161">Once a hybrid connection is added tooyour web app, you can see details on it by simply clicking on it.</span></span>  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a><span data-ttu-id="2d809-162">混合式連線和 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="2d809-162">Hybrid Connections and App Service Plans</span></span> ##

<span data-ttu-id="2d809-163">現在您可以做出 hello 唯一的混合式連線會 hello 新混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2d809-163">hello only hybrid connections you can now make are hello new hybrid connections.</span></span>  <span data-ttu-id="2d809-164">基本、標準、進階和隔離的定價 SKU 才能使用混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2d809-164">They are only available in Basic, Standard, Premium and Isolated pricing SKUs.</span></span>  <span data-ttu-id="2d809-165">有繫結限制 toohello 定價計劃。</span><span class="sxs-lookup"><span data-stu-id="2d809-165">There are limits tied toohello pricing plan.</span></span>  

| <span data-ttu-id="2d809-166">定價方案</span><span class="sxs-lookup"><span data-stu-id="2d809-166">Pricing Plan</span></span> | <span data-ttu-id="2d809-167">Hello 計劃中可用的混合式連線的數目</span><span class="sxs-lookup"><span data-stu-id="2d809-167">Number of hybrid connections usable in hello plan</span></span> |
|----|----|
| <span data-ttu-id="2d809-168">基本</span><span class="sxs-lookup"><span data-stu-id="2d809-168">Basic</span></span> | <span data-ttu-id="2d809-169">5</span><span class="sxs-lookup"><span data-stu-id="2d809-169">5</span></span> |
| <span data-ttu-id="2d809-170">標準</span><span class="sxs-lookup"><span data-stu-id="2d809-170">Standard</span></span> | <span data-ttu-id="2d809-171">25</span><span class="sxs-lookup"><span data-stu-id="2d809-171">25</span></span> |
| <span data-ttu-id="2d809-172">進階</span><span class="sxs-lookup"><span data-stu-id="2d809-172">Premium</span></span> | <span data-ttu-id="2d809-173">200</span><span class="sxs-lookup"><span data-stu-id="2d809-173">200</span></span> |
| <span data-ttu-id="2d809-174">隔離</span><span class="sxs-lookup"><span data-stu-id="2d809-174">Isolated</span></span> | <span data-ttu-id="2d809-175">200</span><span class="sxs-lookup"><span data-stu-id="2d809-175">200</span></span> |

<span data-ttu-id="2d809-176">因為有 App Service 方案的限制，另外還有 UI hello App Service 方案，其中顯示您正在使用多少的混合式連線中以及哪些應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d809-176">Since there are App Service Plan restrictions there is also UI in hello App Service Plan that shows you how many hybrid connections are being used and by what apps.</span></span>  

![][6]

<span data-ttu-id="2d809-177">就像 hello 應用程式檢視，您可以看到詳細資料上混合式連接上它即可。</span><span class="sxs-lookup"><span data-stu-id="2d809-177">Just as with hello app view, you can see details on your hybrid connection by clicking on it.</span></span>  <span data-ttu-id="2d809-178">您可以看到您在 hello 應用程式檢視所有 hello 資訊，但也可以都查看在 hello 多少其他應用程式如下所示的 hello 屬性相同應用程式服務方案正在使用該混合式連接。</span><span class="sxs-lookup"><span data-stu-id="2d809-178">In hello properties shown here you can see all hello information you had at hello app view but can also see how many other apps in hello same App Service Plan are using that hybrid connection.</span></span>

![][7]

<span data-ttu-id="2d809-179">Hello 可以用於應用程式服務方案的混合式連接端點數目上限時，可以使用每個混合式連線，跨任意數目的 App Service 方案中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d809-179">While there is a limit on hello number of hybrid connection endpoints that can be used in an App Service Plan, each hybrid connection used can be used across any number of apps in that App Service Plan.</span></span>  <span data-ttu-id="2d809-180">這是 toosay 如果選項 1 我 5 不同的應用程式中使用我的應用程式服務計劃中的混合式連接的是 1 還是混合式連接。</span><span class="sxs-lookup"><span data-stu-id="2d809-180">That is toosay that if I had 1 hybrid connection that I used in 5 separate apps in my App Service Plan, that is still just 1 hybrid connection.</span></span>

<span data-ttu-id="2d809-181">沒有額外的成本 toohybrid 連線正在只可用於 Basic、 Standard、 Premium 或隔離的 SKU。</span><span class="sxs-lookup"><span data-stu-id="2d809-181">There is an additional cost toohybrid connections beyond being only usable in a Basic, Standard, Premium or Isolated SKU.</span></span>  <span data-ttu-id="2d809-182">如需混合式連線定價的詳細資訊，請前往這裡︰[服務匯流排定價][sbpricing]。</span><span class="sxs-lookup"><span data-stu-id="2d809-182">For details on hybrid connection pricing please go here: [Service Bus pricing][sbpricing].</span></span>

## <a name="hybrid-connection-manager"></a><span data-ttu-id="2d809-183">混合式連線管理員</span><span class="sxs-lookup"><span data-stu-id="2d809-183">Hybrid Connection Manager</span></span> ##

<span data-ttu-id="2d809-184">為了讓混合式連線 toowork 必須裝載您的混合式連接端點的 hello 網路中的轉送代理程式。</span><span class="sxs-lookup"><span data-stu-id="2d809-184">In order for hybrid connections toowork you need a relay agent in hello network that hosts your hybrid connection endpoint.</span></span>  <span data-ttu-id="2d809-185">該轉送代理程式稱為 hello 混合式連線管理員 (HCM)。</span><span class="sxs-lookup"><span data-stu-id="2d809-185">That relay agent is called hello Hybrid Connection Manager (HCM).</span></span>  <span data-ttu-id="2d809-186">此工具可以下載從 hello**網路 > 設定您的混合式連接端點**UI 可從您的應用程式在 hello [Azure 入口網站][portal]。</span><span class="sxs-lookup"><span data-stu-id="2d809-186">This tool can be downloaded from hello **Networking > Configure your hybrid connection endpoints** UI available from your app in hello [Azure portal][portal].</span></span>  

<span data-ttu-id="2d809-187">此工具會在 Windows Server 2008 R2 和更新版本的 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="2d809-187">This tool runs on Windows server 2008 R2 and later versions of Windows.</span></span>  <span data-ttu-id="2d809-188">安裝完成後 hello HCM 執行為服務。</span><span class="sxs-lookup"><span data-stu-id="2d809-188">Once installed hello HCM runs as a service.</span></span>  <span data-ttu-id="2d809-189">此服務會連接 tooAzure hello 設定端點為基礎的服務匯流排轉送。</span><span class="sxs-lookup"><span data-stu-id="2d809-189">This service connects tooAzure servicebus relay based on hello configured endpoints.</span></span>  <span data-ttu-id="2d809-190">從 hello HCM hello 連線是輸出 tooports 80 和 443。</span><span class="sxs-lookup"><span data-stu-id="2d809-190">hello connections from hello HCM are outbound tooports 80 and 443.</span></span>    

<span data-ttu-id="2d809-191">hello HCM 具有 UI tooconfigure 它。</span><span class="sxs-lookup"><span data-stu-id="2d809-191">hello HCM has a UI tooconfigure it.</span></span>  <span data-ttu-id="2d809-192">Hello HCM 安裝之後您可以藉由執行 hello HybridConnectionManagerUi.exe 位於 hello 混合式連線管理員的安裝目錄中叫出 hello UI。</span><span class="sxs-lookup"><span data-stu-id="2d809-192">After hello HCM is installed you can bring up hello UI by running hello HybridConnectionManagerUi.exe that sits in hello Hybrid Connection Manager installation directory.</span></span>  <span data-ttu-id="2d809-193">在 Windows 10 上，您也可以在搜尋方塊中輸入「混合式連線管理員 UI」來輕鬆取得該 UI。</span><span class="sxs-lookup"><span data-stu-id="2d809-193">It is also easily reached on Windows 10 by typing *Hybrid Connection Manager UI* in your search box.</span></span>  

<span data-ttu-id="2d809-194">Hello HCM UI 啟動時，首先 hello 您，請參閱時列出的所有設定與這個執行個體的 hello HCM hello 混合式連接的資料表。</span><span class="sxs-lookup"><span data-stu-id="2d809-194">When hello HCM UI is started, hello first thing you see is a table that lists all of hello hybrid connections that are configured with this instance of hello HCM.</span></span>  <span data-ttu-id="2d809-195">如果您想 toomake 您必須使用 Azure tooauthenticate 任何變更。</span><span class="sxs-lookup"><span data-stu-id="2d809-195">If you wish toomake any changes you will need tooauthenticate with Azure.</span></span> 

<span data-ttu-id="2d809-196">tooadd 其中一個或多個混合式連線 tooyour HCM:</span><span class="sxs-lookup"><span data-stu-id="2d809-196">tooadd one or more Hybrid Connections tooyour HCM:</span></span>

1. <span data-ttu-id="2d809-197">啟動 hello HCM UI</span><span class="sxs-lookup"><span data-stu-id="2d809-197">Start hello HCM UI</span></span>
1. <span data-ttu-id="2d809-198">按一下 [設定另一個混合式連線] ![][8]</span><span class="sxs-lookup"><span data-stu-id="2d809-198">Click Configure another hybrid connection ![][8]</span></span>

1. <span data-ttu-id="2d809-199">使用 Azure 帳戶進行登入</span><span class="sxs-lookup"><span data-stu-id="2d809-199">Sign in with your Azure account</span></span>
1. <span data-ttu-id="2d809-200">選擇訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2d809-200">Choose a subscription</span></span>
1. <span data-ttu-id="2d809-201">按一下您要此 HCM toorelay hello 混合式連線![][9]</span><span class="sxs-lookup"><span data-stu-id="2d809-201">Click on hello hybrid connections you want this HCM toorelay ![][9]</span></span>

1. <span data-ttu-id="2d809-202">按一下 [Save] \(儲存)。</span><span class="sxs-lookup"><span data-stu-id="2d809-202">Click Save</span></span>

<span data-ttu-id="2d809-203">此時，您會看到您加入的 hello 混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2d809-203">At this point you will see hello hybrid connections you added.</span></span>  <span data-ttu-id="2d809-204">您也可以按一下 hello 設定混合式連接，然後查看 hello 連線詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2d809-204">You can also click on hello configured hybrid connection and see details about hello connection.</span></span>

![][10]

<span data-ttu-id="2d809-205">HCM toobe 無法 toosupport hello 混合式連線的設定，它需要：</span><span class="sxs-lookup"><span data-stu-id="2d809-205">For your HCM toobe able toosupport hello hybrid connections it is configured with, it needs:</span></span>

- <span data-ttu-id="2d809-206">透過連接埠 80 和 443 TCP 存取 tooAzure</span><span class="sxs-lookup"><span data-stu-id="2d809-206">TCP access tooAzure over ports 80 and 443</span></span>
- <span data-ttu-id="2d809-207">TCP 存取 toohello 混合式連接端點</span><span class="sxs-lookup"><span data-stu-id="2d809-207">TCP access toohello hybrid connection endpoint</span></span>
- <span data-ttu-id="2d809-208">能力 toodo DNS 查詢 ups hello 端點上的裝載和 hello azure 服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="2d809-208">ability toodo DNS look ups on hello endpoint host and hello azure servicebus namespace</span></span>

<span data-ttu-id="2d809-209">hello HCM 支援新的混合式連線以及 hello 舊版 BizTalk 混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2d809-209">hello HCM supports both new hybrid connections as well as hello older BizTalk hybrid connections.</span></span>

### <a name="redundancy"></a><span data-ttu-id="2d809-210">備援性</span><span class="sxs-lookup"><span data-stu-id="2d809-210">Redundancy</span></span> ###

<span data-ttu-id="2d809-211">每個 HCM 都可以支援多個混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2d809-211">Each HCM can support multiple hybrid connections.</span></span>  <span data-ttu-id="2d809-212">此外，任何給定的混合式連線也可由多個 HCM 來支援。</span><span class="sxs-lookup"><span data-stu-id="2d809-212">Also, any given hybrid connection can be supported by multiple HCMs.</span></span>  <span data-ttu-id="2d809-213">hello 預設行為是 tooround 循環配置資源流量，跨 hello HCMs 針對任何指定的端點。</span><span class="sxs-lookup"><span data-stu-id="2d809-213">hello default behavior is tooround robin traffic across hello configured HCMs for any given endpoint.</span></span>  <span data-ttu-id="2d809-214">如果您想讓網路的混合式連線具有高可用性，只需在不同機器上具現化多個 HCM。</span><span class="sxs-lookup"><span data-stu-id="2d809-214">If you want high availability on your hybrid connections from your network, simply instantiate multiple HCMs on separate machines.</span></span> 

### <a name="manually-adding-a-hybrid-connection"></a><span data-ttu-id="2d809-215">手動新增混合式連線</span><span class="sxs-lookup"><span data-stu-id="2d809-215">Manually adding a hybrid connection</span></span> ###

<span data-ttu-id="2d809-216">如果您想有人之外訂用帳戶 toohost HCM 給定的混合式連接的執行個體，您可以在與他們共用 hello hello 混合式連接的閘道連接字串。</span><span class="sxs-lookup"><span data-stu-id="2d809-216">If you wish somebody outside of your subscription toohost an HCM instance for a given hybrid connection, you can share with them hello gateway connection string for hello hybrid connection.</span></span>  <span data-ttu-id="2d809-217">您可以在混合式連線在 hello hello 屬性看到[Azure 入口網站][portal]。</span><span class="sxs-lookup"><span data-stu-id="2d809-217">You can see this in hello properties for a hybrid connection in hello [Azure portal][portal].</span></span> <span data-ttu-id="2d809-218">字串，toouse 按一下 hello**手動設定**hello HCM 按鈕，並貼上 hello 閘道連接字串中。</span><span class="sxs-lookup"><span data-stu-id="2d809-218">toouse that string, click hello **Configure manually** button in hello HCM and paste in hello gateway connection string.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="2d809-219">疑難排解</span><span class="sxs-lookup"><span data-stu-id="2d809-219">Troubleshooting</span></span> ##

<span data-ttu-id="2d809-220">當您混合式連接以執行應用程式設定並沒有至少一個已設定，該混合式連接的 HCM 然後 hello 狀態會顯示**Connected** hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="2d809-220">When your hybrid connection is set up with a running application and there is at least one HCM that has that hybrid connection configured, then hello status will say **Connected** in hello portal.</span></span>  <span data-ttu-id="2d809-221">如果不是顯示**Connected**則表示可能是您的應用程式已關閉，或是您 HCM 無法 out tooAzure 連接埠 80 或 443 連線。</span><span class="sxs-lookup"><span data-stu-id="2d809-221">If it does not say **Connected** then it means that either your app is down or your HCM cannot connect out tooAzure on ports 80 or 443.</span></span>  

<span data-ttu-id="2d809-222">用戶端無法連線 tootheir 端點的 hello 主要原因是因為 hello 端點指定使用的 IP 位址，而不 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="2d809-222">hello primary reason that clients cannot connect tootheir endpoint is because hello endpoint was specified using an IP address instead of a DNS name.</span></span>  <span data-ttu-id="2d809-223">如果您的應用程式無法連線到所需的 hello 端點使用的 IP 位址，切換 toousing hello hello HCM 執行所在的主機有效的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="2d809-223">If your app cannot reach hello desired endpoint and you used an IP address, switch toousing a DNS name that is valid on hello host where hello HCM is running.</span></span>  <span data-ttu-id="2d809-224">其他事項 toocheck 是該 hello DNS 名稱正確解析其中 hello HCM 正在執行，而且沒有從 hello 執行的主控件 hello HCM toohello 混合式連接端點連線的 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="2d809-224">Other things toocheck are that hello DNS name resolves properly on hello host where hello HCM is running and that there is connectivity from hello host where hello HCM is running toohello hybrid connection endpoint.</span></span>  

<span data-ttu-id="2d809-225">Hello 可以叫用呼叫 tcpping hello 主控台從應用程式服務中沒有一項工具。</span><span class="sxs-lookup"><span data-stu-id="2d809-225">There is a tool in hello App Service that can be invoked from hello console called tcpping.</span></span>  <span data-ttu-id="2d809-226">此工具可以告訴您，是否您具有存取 tooa TCP 端點，但不會告訴您是否您有存取 tooa 混合式連接端點。</span><span class="sxs-lookup"><span data-stu-id="2d809-226">This tool can tell you if you have access tooa TCP endpoint but does not tell you if you have access tooa hybrid connection endpoint.</span></span>  <span data-ttu-id="2d809-227">針對混合式連接端點的 hello 主控台中使用時，成功 ping 會只告訴您有混合式連線為使用該主機： port 組合的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="2d809-227">When used in hello console against a hybrid connection endpoint, a successful ping will only tell you that you have a hybrid connection configured for your app that uses that host:port combination.</span></span>  

## <a name="biztalk-hybrid-connections"></a><span data-ttu-id="2d809-228">BizTalk 混合式連線</span><span class="sxs-lookup"><span data-stu-id="2d809-228">BizTalk Hybrid Connections</span></span> ##

<span data-ttu-id="2d809-229">關閉 toofurther BizTalk 混合式連接建立 hello 舊版 BizTalk 混合式連線功能已關閉。</span><span class="sxs-lookup"><span data-stu-id="2d809-229">hello older BizTalk Hybrid Connections capability has been closed off toofurther BizTalk Hybrid Connection creations.</span></span>  <span data-ttu-id="2d809-230">您可以繼續使用您預先存在的 BizTalk 混合式連線您的應用程式，但應該移轉 toohello 新的服務。</span><span class="sxs-lookup"><span data-stu-id="2d809-230">You can continue using your preexisting BizTalk Hybrid Connections with your apps but should migrate toohello new service.</span></span>  <span data-ttu-id="2d809-231">Hello hello hello BizTalk 版本透過新的服務中的優點包括：</span><span class="sxs-lookup"><span data-stu-id="2d809-231">Among hello benefits in hello new service over hello BizTalk version are:</span></span>

- <span data-ttu-id="2d809-232">不需要其他 BizTalk 帳戶</span><span class="sxs-lookup"><span data-stu-id="2d809-232">no additional BizTalk account is required</span></span>
- <span data-ttu-id="2d809-233">TLS 是 1.2，而非 BizTalk 混合式連線所使用的 1.0</span><span class="sxs-lookup"><span data-stu-id="2d809-233">TLS is 1.2 instead of 1.0 as in BizTalk Hybrid Connections</span></span>
- <span data-ttu-id="2d809-234">通訊是透過連接埠 80 和 443 使用 DNS 名稱 tooreach Azure 而不是 IP 位址和其他各種其他連接埠。</span><span class="sxs-lookup"><span data-stu-id="2d809-234">Communication is over ports 80 and 443 using a DNS name tooreach Azure instead of IP addresses and a range of additional other ports.</span></span>  

<span data-ttu-id="2d809-235">tooadd BizTalk 混合式連線 tooyour 應用程式，應用程式移 tooyour hello [Azure 入口網站][ portal]按一下**網路 > 設定您的混合式連接端點**。</span><span class="sxs-lookup"><span data-stu-id="2d809-235">tooadd a BizTalk hybrid connection tooyour app, go tooyour app in hello [Azure portal][portal] and click **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="2d809-236">Hello 傳統混合式連接的資料表中按一下**加入傳統的混合式連接**。</span><span class="sxs-lookup"><span data-stu-id="2d809-236">In hello Classic hybrid connections table click **Add classic hybrid connection**.</span></span>  <span data-ttu-id="2d809-237">您可以在這裡看到 BizTalk 混合式連線的清單。</span><span class="sxs-lookup"><span data-stu-id="2d809-237">From here you will see a list of your BizTalk hybrid connections.</span></span>  


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

