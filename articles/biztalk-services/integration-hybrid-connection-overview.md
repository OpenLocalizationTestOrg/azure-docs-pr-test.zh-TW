---
title: "混合式連線概觀 | Microsoft Docs"
description: "了解混合式連線、安全性、TCP 連接埠和支援的組態。 MABS，WABS。"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 9367d6f57e694c8a438781004ef29a09de77aaa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="hybrid-connections-overview"></a><span data-ttu-id="42b83-104">混合式連線概觀</span><span class="sxs-lookup"><span data-stu-id="42b83-104">Hybrid Connections overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42b83-105">BizTalk 混合式連線已停用，並以 App Service 混合式連線取代。</span><span class="sxs-lookup"><span data-stu-id="42b83-105">BizTalk Hybrid Connections is retired, and replaced by App Service Hybrid Connections.</span></span> <span data-ttu-id="42b83-106">如需詳細資訊，包括如何管理您現有的 BizTalk 混合式連線，請參閱 [Azure App Service 混合式連線](../app-service/app-service-hybrid-connections.md)。</span><span class="sxs-lookup"><span data-stu-id="42b83-106">For more information, including how to manage your existing BizTalk Hybrid Connections, see [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md).</span></span>

<span data-ttu-id="42b83-107">簡介混合式連線、列出支援的組態，並列出需要的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="42b83-107">Introduction to Hybrid Connections, lists the supported configurations, and lists the required TCP ports.</span></span>

## <a name="what-is-a-hybrid-connection"></a><span data-ttu-id="42b83-108">什麼是混合式連線</span><span class="sxs-lookup"><span data-stu-id="42b83-108">What is a hybrid connection</span></span>
<span data-ttu-id="42b83-109">混合式連線是 Azure BizTalk 服務的功能。</span><span class="sxs-lookup"><span data-stu-id="42b83-109">Hybrid Connections are a feature of Azure BizTalk Services.</span></span> <span data-ttu-id="42b83-110">混合式連線可讓您簡單又方便地將 Azure App Service 中的 Web Apps 功能 (前身為網站) 和 Azure App Service 中的 Mobile Apps 功能 (前身為行動服務)，連線到防火牆後的內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="42b83-110">Hybrid Connections provide an easy and convenient way to connect the Web Apps feature in Azure App Service (formerly Websites) and the Mobile Apps feature in Azure App Service (formerly Mobile Services) to on-premises resources behind your firewall.</span></span>

![混合式連線][HCImage]

<span data-ttu-id="42b83-112">混合式連線的優點包括：</span><span class="sxs-lookup"><span data-stu-id="42b83-112">Hybrid Connections benefits include:</span></span>

* <span data-ttu-id="42b83-113">Web Apps 和 Mobile Apps 可以安全地存取現有的內部部署資料和服務。</span><span class="sxs-lookup"><span data-stu-id="42b83-113">Web Apps and Mobile Apps can access existing on-premises data and services securely.</span></span>
* <span data-ttu-id="42b83-114">多個 Web Apps 或 Mobile Apps 可共用一個混合式連線存取內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="42b83-114">Multiple Web Apps or Mobile Apps can share a Hybrid Connection to access an on-premises resource.</span></span>
* <span data-ttu-id="42b83-115">只需要最少的 TCP 連接埠就能存取您的網路。</span><span class="sxs-lookup"><span data-stu-id="42b83-115">Minimal TCP ports are required to access your network.</span></span>
* <span data-ttu-id="42b83-116">使用混合式連線的應用程式只存取透過混合式連線發佈的特定內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="42b83-116">Applications using Hybrid Connections access only the specific on-premises resource that is published through the Hybrid Connection.</span></span>
* <span data-ttu-id="42b83-117">可以連接到任何使用靜態 TCP 連接埠的內部部署資源，例如 SQL Server、MySQL、HTTP Web API 和大部分的自訂 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="42b83-117">Can connect to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="42b83-118">目前不支援使用動態連接埠的 TCP 服務 (例如 FTP 被動模式或延伸被動模式)。</span><span class="sxs-lookup"><span data-stu-id="42b83-118">TCP-based services that use dynamic ports (such as FTP Passive Mode or Extended Passive Mode) are currently not supported.</span></span> <span data-ttu-id="42b83-119">也不支援 LDAP。</span><span class="sxs-lookup"><span data-stu-id="42b83-119">LDAP is also not supported.</span></span> <span data-ttu-id="42b83-120">LDAP 使用靜態 TCP 連接埠，但它也可以使用 UDP。</span><span class="sxs-lookup"><span data-stu-id="42b83-120">LDAP uses a static TCP port but it could also use UDP.</span></span> <span data-ttu-id="42b83-121">因此不受支援。</span><span class="sxs-lookup"><span data-stu-id="42b83-121">As a result, it is not supported.</span></span>
  > 
  > 
* <span data-ttu-id="42b83-122">可以與 Web Apps (.NET、PHP、Java、Python、Node.js) 和 Mobile Apps (Node.js、.NET) 支援的所有架構搭配使用。</span><span class="sxs-lookup"><span data-stu-id="42b83-122">Can be used with all frameworks supported by Web Apps (.NET, PHP, Java, Python, Node.js) and Mobile Apps (Node.js, .NET).</span></span>
* <span data-ttu-id="42b83-123">Web Apps 和 Mobile Apps 能夠以完全相同的方式存取內部部署資源，就像是該 Web 或 Mobile Apps 位於本機網路一樣。</span><span class="sxs-lookup"><span data-stu-id="42b83-123">Web Apps and Mobile Apps can access on-premises resources in exactly the same way as if the Web or Mobile App is located on your local network.</span></span> <span data-ttu-id="42b83-124">例如，內部部署使用的相同連接字串也可以在 Azure 上使用。</span><span class="sxs-lookup"><span data-stu-id="42b83-124">For example, the same connection string used on-premises can also be used on Azure.</span></span>

<span data-ttu-id="42b83-125">混合式連線也可讓企業系統管理員控制和檢視混合式應用程式所存取的公司資源，包括：</span><span class="sxs-lookup"><span data-stu-id="42b83-125">Hybrid Connections also provide enterprise administrators with control and visibility into the corporate resources accessed by hybrid applications, including:</span></span>

* <span data-ttu-id="42b83-126">系統管理員可以使用群組原則設定，以允許在網站上使用混合式連線，也能指定混合式應用程式可存取的資源。</span><span class="sxs-lookup"><span data-stu-id="42b83-126">Using Group Policy settings, administrators can allow Hybrid Connections on the network and also designate resources that can be accessed by hybrid applications.</span></span>
* <span data-ttu-id="42b83-127">公司網路上的事件和稽核記錄可讓您查看混合式連線所存取的資源。</span><span class="sxs-lookup"><span data-stu-id="42b83-127">Event and audit logs on the corporate network provide visibility into the resources accessed by Hybrid Connections.</span></span>

## <a name="example-scenarios"></a><span data-ttu-id="42b83-128">範例案例</span><span class="sxs-lookup"><span data-stu-id="42b83-128">Example scenarios</span></span>
<span data-ttu-id="42b83-129">混合式連線支援下列架構和應用程式的組合：</span><span class="sxs-lookup"><span data-stu-id="42b83-129">Hybrid Connections support the following framework and application combinations:</span></span>

* <span data-ttu-id="42b83-130">.NET 架構存取 SQL Server</span><span class="sxs-lookup"><span data-stu-id="42b83-130">.NET framework access to SQL Server</span></span>
* <span data-ttu-id="42b83-131">.NET 架構搭配 WebClient 存取 HTTP/HTTPS 服務</span><span class="sxs-lookup"><span data-stu-id="42b83-131">.NET framework access to HTTP/HTTPS services with WebClient</span></span>
* <span data-ttu-id="42b83-132">PHP 存取 SQL Server、MySQL</span><span class="sxs-lookup"><span data-stu-id="42b83-132">PHP access to SQL Server, MySQL</span></span>
* <span data-ttu-id="42b83-133">Java 存取 SQL Server、MySQL 和 Oracle</span><span class="sxs-lookup"><span data-stu-id="42b83-133">Java access to SQL Server, MySQL and Oracle</span></span>
* <span data-ttu-id="42b83-134">Java 存取 HTTP/HTTPS 服務</span><span class="sxs-lookup"><span data-stu-id="42b83-134">Java access to HTTP/HTTPS services</span></span>

<span data-ttu-id="42b83-135">使用混合式連線來存取內部部署 SQL Server 時，請注意下列事項：</span><span class="sxs-lookup"><span data-stu-id="42b83-135">When using Hybrid Connections to access on-premises SQL Server, consider the following:</span></span>

* <span data-ttu-id="42b83-136">SQL Express 具名執行個體必須設定為使用靜態連接埠。</span><span class="sxs-lookup"><span data-stu-id="42b83-136">SQL Express Named Instances must be configured to use static ports.</span></span> <span data-ttu-id="42b83-137">依預設，SQL Express 具名執行個體是使用動態連接埠。</span><span class="sxs-lookup"><span data-stu-id="42b83-137">By default, SQL Express named instances use dynamic ports.</span></span>
* <span data-ttu-id="42b83-138">SQL Express 預設執行個體使用靜態連接埠，但必須啟用 TCP。</span><span class="sxs-lookup"><span data-stu-id="42b83-138">SQL Express Default Instances use a static port, but TCP must be enabled.</span></span> <span data-ttu-id="42b83-139">預設不會啟用 TCP。</span><span class="sxs-lookup"><span data-stu-id="42b83-139">By default, TCP is not enabled.</span></span>
* <span data-ttu-id="42b83-140">使用叢集或可用性群組時，暫不支援 `MultiSubnetFailover=true` 模式。</span><span class="sxs-lookup"><span data-stu-id="42b83-140">When using Clustering or Availability Groups, the `MultiSubnetFailover=true` mode is currently not supported.</span></span>
* <span data-ttu-id="42b83-141">目前不支援 `ApplicationIntent=ReadOnly` 。</span><span class="sxs-lookup"><span data-stu-id="42b83-141">The `ApplicationIntent=ReadOnly` is currently not supported.</span></span>
* <span data-ttu-id="42b83-142">可能需要 SQL 驗證當做 Azure 應用程式和內部部署 SQL Server 所支援的端對端授權方法。</span><span class="sxs-lookup"><span data-stu-id="42b83-142">SQL Authentication may be required as the end-to-end authorization method supported by the Azure application and the on-premises SQL server.</span></span>

## <a name="security-and-ports"></a><span data-ttu-id="42b83-143">安全性和連接埠</span><span class="sxs-lookup"><span data-stu-id="42b83-143">Security and ports</span></span>
<span data-ttu-id="42b83-144">混合式連線採用共用存取簽章 (SAS) 授權，保護從 Azure 應用程式和內部部署混合式連線管理員至混合式連線的連接安全。</span><span class="sxs-lookup"><span data-stu-id="42b83-144">Hybrid Connections use Shared Access Signature (SAS) authorization to secure the connections from the Azure applications and the on-premises Hybrid Connection Manager to the Hybrid Connection.</span></span> <span data-ttu-id="42b83-145">針對應用程式和內部部署混合式連線管理員，系統會建立個別的連線金鑰。</span><span class="sxs-lookup"><span data-stu-id="42b83-145">Separate connection keys are created for the application and the on-premises Hybrid Connection Manager.</span></span> <span data-ttu-id="42b83-146">這些連線金鑰可以個別地更換和撤銷。</span><span class="sxs-lookup"><span data-stu-id="42b83-146">These connection keys can be rolled over and revoked independently.</span></span>

<span data-ttu-id="42b83-147">混合式連線能夠以順暢且安全的方式，將金鑰發佈給應用程式和內部部署混合式連線管理員。</span><span class="sxs-lookup"><span data-stu-id="42b83-147">Hybrid Connections provide for seamless and secure distribution of the keys to the applications and the on-premises Hybrid Connection Manager.</span></span>

<span data-ttu-id="42b83-148">請參閱 [建立和管理混合式連線](integration-hybrid-connection-create-manage.md)(英文)。</span><span class="sxs-lookup"><span data-stu-id="42b83-148">See [Create and Manage Hybrid Connections](integration-hybrid-connection-create-manage.md).</span></span>

<span data-ttu-id="42b83-149">*應用程式授權與混合式連線分開*。</span><span class="sxs-lookup"><span data-stu-id="42b83-149">*Application authorization is separate from the Hybrid Connection*.</span></span> <span data-ttu-id="42b83-150">任何適當的授權方法都可使用。</span><span class="sxs-lookup"><span data-stu-id="42b83-150">Any appropriate authorization method can be used.</span></span> <span data-ttu-id="42b83-151">授權方法視 Azure 雲端和內部部署元件之間支援的端對端授權方法而定。</span><span class="sxs-lookup"><span data-stu-id="42b83-151">The authorization method depends on the end-to-end authorization methods supported across the Azure cloud and the on-premises components.</span></span> <span data-ttu-id="42b83-152">例如，您的 Azure 應用程式存取內部部署 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="42b83-152">For example, your Azure application accesses an on-premises SQL Server.</span></span> <span data-ttu-id="42b83-153">在此情況下，SQL 授權可能是端對端支援的授權方法。</span><span class="sxs-lookup"><span data-stu-id="42b83-153">In this scenario, SQL Authorization may be the authorization method that is supported end-to-end.</span></span>

#### <a name="tcp-ports"></a><span data-ttu-id="42b83-154">TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="42b83-154">TCP ports</span></span>
<span data-ttu-id="42b83-155">混合式連線只需要您私人網路的輸出 TCP 或 HTTP 連線。</span><span class="sxs-lookup"><span data-stu-id="42b83-155">Hybrid Connections require only outbound TCP or HTTP connectivity from your private network.</span></span> <span data-ttu-id="42b83-156">您不需要開啟任何防火牆連接埠，或變更您的網路周邊組態，即可允許任何輸入連線進入您的網路。</span><span class="sxs-lookup"><span data-stu-id="42b83-156">You do not need to open any firewall ports or change your network perimeter configuration to allow any inbound connectivity into your network.</span></span>

<span data-ttu-id="42b83-157">混合式連線會使用下列 TCP 通訊埠：</span><span class="sxs-lookup"><span data-stu-id="42b83-157">The following TCP ports are used by Hybrid Connections:</span></span>

| <span data-ttu-id="42b83-158">連接埠</span><span class="sxs-lookup"><span data-stu-id="42b83-158">Port</span></span> | <span data-ttu-id="42b83-159">您為何需要它</span><span class="sxs-lookup"><span data-stu-id="42b83-159">Why you need it</span></span> |
| --- | --- |
| <span data-ttu-id="42b83-160">9350 - 9354</span><span class="sxs-lookup"><span data-stu-id="42b83-160">9350 - 9354</span></span> |<span data-ttu-id="42b83-161">這些連接埠用於資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="42b83-161">These ports are used for data transmission.</span></span> <span data-ttu-id="42b83-162">服務匯流排轉送管理員會探查連接埠 9350，以判斷 TCP 連線是否可用。</span><span class="sxs-lookup"><span data-stu-id="42b83-162">The Service Bus relay manager probes port 9350 to determine if TCP connectivity is available.</span></span> <span data-ttu-id="42b83-163">如果可用的話，則會假設連接埠 9352 也是可用。</span><span class="sxs-lookup"><span data-stu-id="42b83-163">If it is available, then it assumes that port 9352 is also available.</span></span> <span data-ttu-id="42b83-164">資料流量會經過連接埠 9352。</span><span class="sxs-lookup"><span data-stu-id="42b83-164">Data traffic goes over port 9352.</span></span> <br/><br/><span data-ttu-id="42b83-165">允許對這些連接埠的輸出連線。</span><span class="sxs-lookup"><span data-stu-id="42b83-165">Allow outbound connections to these ports.</span></span> |
| <span data-ttu-id="42b83-166">5671</span><span class="sxs-lookup"><span data-stu-id="42b83-166">5671</span></span> |<span data-ttu-id="42b83-167">當連接埠 9352 用於資料流量時，連接埠 5671 就做為控制通道。</span><span class="sxs-lookup"><span data-stu-id="42b83-167">When port 9352 is used for data traffic, port 5671 is used as the control channel.</span></span> <br/><br/><span data-ttu-id="42b83-168">允許對此連接埠的輸出連線。</span><span class="sxs-lookup"><span data-stu-id="42b83-168">Allow outbound connections to this port.</span></span> |
| <span data-ttu-id="42b83-169">80、443</span><span class="sxs-lookup"><span data-stu-id="42b83-169">80, 443</span></span> |<span data-ttu-id="42b83-170">這些連接埠用於傳送部分資料要求給 Azure。</span><span class="sxs-lookup"><span data-stu-id="42b83-170">These ports are used for some data requests to Azure.</span></span> <span data-ttu-id="42b83-171">而且，如果連接埠 9352 和 5671 無法使用，則連接埠 80 和 443 是用於資料傳輸和控制通道的後援連接埠。允許對這些連接埠的輸出連線。</span><span class="sxs-lookup"><span data-stu-id="42b83-171">Also, if ports 9352 and 5671 are not usable, *then* ports 80 and 443 are the fallback ports used for data transmission and the control channel.</span></span><br/><br/><span data-ttu-id="42b83-172">允許對這些連接埠的輸出連線。</span><span class="sxs-lookup"><span data-stu-id="42b83-172">Allow outbound connections to these ports.</span></span> <br/><br/><span data-ttu-id="42b83-173">**注意** 不建議使用這些做為後援連接埠來代替其他 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="42b83-173">**Note** It is not recommended to use these as the fallback ports in place of the other TCP ports.</span></span> <span data-ttu-id="42b83-174">HTTP/WebSocket 是做為通訊協定使用，而非資料通道的原生 TCP。</span><span class="sxs-lookup"><span data-stu-id="42b83-174">The HTTP/WebSocket is used as the protocol instead of native TCP for data channels.</span></span> <span data-ttu-id="42b83-175">這可能會導致效能變低。</span><span class="sxs-lookup"><span data-stu-id="42b83-175">It could result in lower performance.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="42b83-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42b83-176">Next steps</span></span>
[<span data-ttu-id="42b83-177">Create and manage Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="42b83-177">Create and manage Hybrid Connections</span></span>](integration-hybrid-connection-create-manage.md)<br/><span data-ttu-id="42b83-178">
[將 Azure Web Apps 連接到內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="42b83-178">
[Connect Azure Web Apps to an On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md)</span></span><br/><span data-ttu-id="42b83-179">
[從 Azure Web 應用程式連接至內部部署 SQL Server](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)</span><span class="sxs-lookup"><span data-stu-id="42b83-179">
[Connect to on-premises SQL Server from an Azure web app](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)</span></span><br/>

## <a name="see-also"></a><span data-ttu-id="42b83-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="42b83-180">See Also</span></span>
<span data-ttu-id="42b83-181">[用於管理 Microsoft Azure 上之 BizTalk 服務的 REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md)</span><span class="sxs-lookup"><span data-stu-id="42b83-181">[REST API for Managing BizTalk Services on Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md)</span></span><br/><span data-ttu-id="42b83-182">
[使用 Azure 入口網站建立 BizTalk 服務](biztalk-provision-services.md)</span><span class="sxs-lookup"><span data-stu-id="42b83-182">
[Create a BizTalk Service using Azure portal](biztalk-provision-services.md)</span></span><br/><span data-ttu-id="42b83-183">
[BizTalk 服務：儀表板、監視和調整索引標籤](biztalk-dashboard-monitor-scale-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="42b83-183">
[BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md)</span></span><br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
