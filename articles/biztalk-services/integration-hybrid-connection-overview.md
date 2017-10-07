---
title: "aaaHybrid 連接概觀 |Microsoft 文件"
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
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a><span data-ttu-id="71c7e-104">混合式連線概觀</span><span class="sxs-lookup"><span data-stu-id="71c7e-104">Hybrid Connections overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71c7e-105">BizTalk 混合式連線已停用，並以 App Service 混合式連線取代。</span><span class="sxs-lookup"><span data-stu-id="71c7e-105">BizTalk Hybrid Connections is retired, and replaced by App Service Hybrid Connections.</span></span> <span data-ttu-id="71c7e-106">如需詳細資訊，包括如何 toomanage 現有 BizTalk 混合式連線，請參閱[Azure 應用程式服務的混合式連線](../app-service/app-service-hybrid-connections.md)。</span><span class="sxs-lookup"><span data-stu-id="71c7e-106">For more information, including how toomanage your existing BizTalk Hybrid Connections, see [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md).</span></span>

<span data-ttu-id="71c7e-107">簡介 tooHybrid 連線，列出支援 hello 組態，並列出 hello 必要的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="71c7e-107">Introduction tooHybrid Connections, lists hello supported configurations, and lists hello required TCP ports.</span></span>

## <a name="what-is-a-hybrid-connection"></a><span data-ttu-id="71c7e-108">什麼是混合式連線</span><span class="sxs-lookup"><span data-stu-id="71c7e-108">What is a hybrid connection</span></span>
<span data-ttu-id="71c7e-109">混合式連線是 Azure BizTalk 服務的功能。</span><span class="sxs-lookup"><span data-stu-id="71c7e-109">Hybrid Connections are a feature of Azure BizTalk Services.</span></span> <span data-ttu-id="71c7e-110">混合式連線可提供 Azure 應用程式服務 （先前稱為網站） 的簡單、 方便的方式 tooconnect hello Web 應用程式功能和防火牆後方的 Azure 應用程式服務 (先前稱為 Mobile Services) tooon 內部部署資源中的 hello 行動應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="71c7e-110">Hybrid Connections provide an easy and convenient way tooconnect hello Web Apps feature in Azure App Service (formerly Websites) and hello Mobile Apps feature in Azure App Service (formerly Mobile Services) tooon-premises resources behind your firewall.</span></span>

![混合式連線][HCImage]

<span data-ttu-id="71c7e-112">混合式連線的優點包括：</span><span class="sxs-lookup"><span data-stu-id="71c7e-112">Hybrid Connections benefits include:</span></span>

* <span data-ttu-id="71c7e-113">Web Apps 和 Mobile Apps 可以安全地存取現有的內部部署資料和服務。</span><span class="sxs-lookup"><span data-stu-id="71c7e-113">Web Apps and Mobile Apps can access existing on-premises data and services securely.</span></span>
* <span data-ttu-id="71c7e-114">多個 Web 應用程式或行動應用程式可以共用的混合式連接 tooaccess 在內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="71c7e-114">Multiple Web Apps or Mobile Apps can share a Hybrid Connection tooaccess an on-premises resource.</span></span>
* <span data-ttu-id="71c7e-115">最小的 TCP 連接埠是必要的 tooaccess 您的網路。</span><span class="sxs-lookup"><span data-stu-id="71c7e-115">Minimal TCP ports are required tooaccess your network.</span></span>
* <span data-ttu-id="71c7e-116">使用混合式連接的應用程式存取只 hello 特定的內部部署資源發行透過 hello 混合式連接。</span><span class="sxs-lookup"><span data-stu-id="71c7e-116">Applications using Hybrid Connections access only hello specific on-premises resource that is published through hello Hybrid Connection.</span></span>
* <span data-ttu-id="71c7e-117">可以使用靜態 TCP 連接埠，例如 SQL Server、 MySQL、 HTTP 的 Web Api，以及大部份的自訂 Web 服務的 tooany 在內部部署資源的連接。</span><span class="sxs-lookup"><span data-stu-id="71c7e-117">Can connect tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="71c7e-118">目前不支援使用動態連接埠的 TCP 服務 (例如 FTP 被動模式或延伸被動模式)。</span><span class="sxs-lookup"><span data-stu-id="71c7e-118">TCP-based services that use dynamic ports (such as FTP Passive Mode or Extended Passive Mode) are currently not supported.</span></span> <span data-ttu-id="71c7e-119">也不支援 LDAP。</span><span class="sxs-lookup"><span data-stu-id="71c7e-119">LDAP is also not supported.</span></span> <span data-ttu-id="71c7e-120">LDAP 使用靜態 TCP 連接埠，但它也可以使用 UDP。</span><span class="sxs-lookup"><span data-stu-id="71c7e-120">LDAP uses a static TCP port but it could also use UDP.</span></span> <span data-ttu-id="71c7e-121">因此不受支援。</span><span class="sxs-lookup"><span data-stu-id="71c7e-121">As a result, it is not supported.</span></span>
  > 
  > 
* <span data-ttu-id="71c7e-122">可以與 Web Apps (.NET、PHP、Java、Python、Node.js) 和 Mobile Apps (Node.js、.NET) 支援的所有架構搭配使用。</span><span class="sxs-lookup"><span data-stu-id="71c7e-122">Can be used with all frameworks supported by Web Apps (.NET, PHP, Java, Python, Node.js) and Mobile Apps (Node.js, .NET).</span></span>
* <span data-ttu-id="71c7e-123">Web 應用程式和行動應用程式可以存取內部資源，完全 hello 中的相同的方式就如同 hello Web 或行動裝置應用程式位於您本機網路上。</span><span class="sxs-lookup"><span data-stu-id="71c7e-123">Web Apps and Mobile Apps can access on-premises resources in exactly hello same way as if hello Web or Mobile App is located on your local network.</span></span> <span data-ttu-id="71c7e-124">例如，hello 相同的連接字串使用內部部署也可用在 Azure。</span><span class="sxs-lookup"><span data-stu-id="71c7e-124">For example, hello same connection string used on-premises can also be used on Azure.</span></span>

<span data-ttu-id="71c7e-125">混合式連線也會提供企業系統管理員控制和可見性 hello 公司資源存取的混合式應用程式，包括：</span><span class="sxs-lookup"><span data-stu-id="71c7e-125">Hybrid Connections also provide enterprise administrators with control and visibility into hello corporate resources accessed by hybrid applications, including:</span></span>

* <span data-ttu-id="71c7e-126">使用 「 群組原則設定，系統管理員可以在 hello 網路上允許混合式連線，並也指定混合式應用程式可以存取的資源。</span><span class="sxs-lookup"><span data-stu-id="71c7e-126">Using Group Policy settings, administrators can allow Hybrid Connections on hello network and also designate resources that can be accessed by hybrid applications.</span></span>
* <span data-ttu-id="71c7e-127">Hello 公司網路上的事件和稽核記錄檔提供存取的混合式連線的 hello 資源可視性。</span><span class="sxs-lookup"><span data-stu-id="71c7e-127">Event and audit logs on hello corporate network provide visibility into hello resources accessed by Hybrid Connections.</span></span>

## <a name="example-scenarios"></a><span data-ttu-id="71c7e-128">範例案例</span><span class="sxs-lookup"><span data-stu-id="71c7e-128">Example scenarios</span></span>
<span data-ttu-id="71c7e-129">混合式連線支援 hello 遵循 framework 和應用程式的組合：</span><span class="sxs-lookup"><span data-stu-id="71c7e-129">Hybrid Connections support hello following framework and application combinations:</span></span>

* <span data-ttu-id="71c7e-130">.NET framework 存取 tooSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="71c7e-130">.NET framework access tooSQL Server</span></span>
* <span data-ttu-id="71c7e-131">.NET framework 存取 tooHTTP/HTTPS 服務使用 WebClient</span><span class="sxs-lookup"><span data-stu-id="71c7e-131">.NET framework access tooHTTP/HTTPS services with WebClient</span></span>
* <span data-ttu-id="71c7e-132">PHP 存取 tooSQL 伺服器 MySQL</span><span class="sxs-lookup"><span data-stu-id="71c7e-132">PHP access tooSQL Server, MySQL</span></span>
* <span data-ttu-id="71c7e-133">Java 存取 tooSQL Server、 MySQL 和 Oracle</span><span class="sxs-lookup"><span data-stu-id="71c7e-133">Java access tooSQL Server, MySQL and Oracle</span></span>
* <span data-ttu-id="71c7e-134">Java 存取 tooHTTP/HTTPS 服務</span><span class="sxs-lookup"><span data-stu-id="71c7e-134">Java access tooHTTP/HTTPS services</span></span>

<span data-ttu-id="71c7e-135">當使用混合式連線 tooaccess 內部部署 SQL Server 時，請考慮下列 hello:</span><span class="sxs-lookup"><span data-stu-id="71c7e-135">When using Hybrid Connections tooaccess on-premises SQL Server, consider hello following:</span></span>

* <span data-ttu-id="71c7e-136">SQL Express 具名執行個體必須設定的 toouse 靜態連接埠。</span><span class="sxs-lookup"><span data-stu-id="71c7e-136">SQL Express Named Instances must be configured toouse static ports.</span></span> <span data-ttu-id="71c7e-137">依預設，SQL Express 具名執行個體是使用動態連接埠。</span><span class="sxs-lookup"><span data-stu-id="71c7e-137">By default, SQL Express named instances use dynamic ports.</span></span>
* <span data-ttu-id="71c7e-138">SQL Express 預設執行個體使用靜態連接埠，但必須啟用 TCP。</span><span class="sxs-lookup"><span data-stu-id="71c7e-138">SQL Express Default Instances use a static port, but TCP must be enabled.</span></span> <span data-ttu-id="71c7e-139">預設不會啟用 TCP。</span><span class="sxs-lookup"><span data-stu-id="71c7e-139">By default, TCP is not enabled.</span></span>
* <span data-ttu-id="71c7e-140">使用群集或可用性群組時，hello`MultiSubnetFailover=true`模式目前不支援。</span><span class="sxs-lookup"><span data-stu-id="71c7e-140">When using Clustering or Availability Groups, hello `MultiSubnetFailover=true` mode is currently not supported.</span></span>
* <span data-ttu-id="71c7e-141">hello`ApplicationIntent=ReadOnly`目前不支援。</span><span class="sxs-lookup"><span data-stu-id="71c7e-141">hello `ApplicationIntent=ReadOnly` is currently not supported.</span></span>
* <span data-ttu-id="71c7e-142">SQL 驗證可能需要為 hello hello Azure 應用程式和 hello 在內部部署 SQL server 所支援的端對端授權方法。</span><span class="sxs-lookup"><span data-stu-id="71c7e-142">SQL Authentication may be required as hello end-to-end authorization method supported by hello Azure application and hello on-premises SQL server.</span></span>

## <a name="security-and-ports"></a><span data-ttu-id="71c7e-143">安全性和連接埠</span><span class="sxs-lookup"><span data-stu-id="71c7e-143">Security and ports</span></span>
<span data-ttu-id="71c7e-144">混合式連線會使用共用存取簽章 (SAS) 授權 toosecure hello 連線從 hello Azure 應用程式和 hello 內部部署混合式連線管理員 toohello 混合式連接。</span><span class="sxs-lookup"><span data-stu-id="71c7e-144">Hybrid Connections use Shared Access Signature (SAS) authorization toosecure hello connections from hello Azure applications and hello on-premises Hybrid Connection Manager toohello Hybrid Connection.</span></span> <span data-ttu-id="71c7e-145">個別連接索引鍵會針對 hello 應用程式和建立 hello 內部部署混合式連線管理員。</span><span class="sxs-lookup"><span data-stu-id="71c7e-145">Separate connection keys are created for hello application and hello on-premises Hybrid Connection Manager.</span></span> <span data-ttu-id="71c7e-146">這些連線金鑰可以個別地更換和撤銷。</span><span class="sxs-lookup"><span data-stu-id="71c7e-146">These connection keys can be rolled over and revoked independently.</span></span>

<span data-ttu-id="71c7e-147">混合式連線提供順暢且安全的分佈的 hello 金鑰 toohello 應用程式，然後 hello 內部部署混合式連線管理員。</span><span class="sxs-lookup"><span data-stu-id="71c7e-147">Hybrid Connections provide for seamless and secure distribution of hello keys toohello applications and hello on-premises Hybrid Connection Manager.</span></span>

<span data-ttu-id="71c7e-148">請參閱 [建立和管理混合式連線](integration-hybrid-connection-create-manage.md)(英文)。</span><span class="sxs-lookup"><span data-stu-id="71c7e-148">See [Create and Manage Hybrid Connections](integration-hybrid-connection-create-manage.md).</span></span>

<span data-ttu-id="71c7e-149">*應用程式的授權是分開 hello 混合式連接*。</span><span class="sxs-lookup"><span data-stu-id="71c7e-149">*Application authorization is separate from hello Hybrid Connection*.</span></span> <span data-ttu-id="71c7e-150">任何適當的授權方法都可使用。</span><span class="sxs-lookup"><span data-stu-id="71c7e-150">Any appropriate authorization method can be used.</span></span> <span data-ttu-id="71c7e-151">hello 授權方法取決於 hello 端對端授權方法，支援跨 hello Azure 雲端和 hello 內部元件。</span><span class="sxs-lookup"><span data-stu-id="71c7e-151">hello authorization method depends on hello end-to-end authorization methods supported across hello Azure cloud and hello on-premises components.</span></span> <span data-ttu-id="71c7e-152">例如，您的 Azure 應用程式存取內部部署 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="71c7e-152">For example, your Azure application accesses an on-premises SQL Server.</span></span> <span data-ttu-id="71c7e-153">在此案例中，SQL 授權可能會支援的端對端的 hello 授權方法。</span><span class="sxs-lookup"><span data-stu-id="71c7e-153">In this scenario, SQL Authorization may be hello authorization method that is supported end-to-end.</span></span>

#### <a name="tcp-ports"></a><span data-ttu-id="71c7e-154">TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="71c7e-154">TCP ports</span></span>
<span data-ttu-id="71c7e-155">混合式連線只需要您私人網路的輸出 TCP 或 HTTP 連線。</span><span class="sxs-lookup"><span data-stu-id="71c7e-155">Hybrid Connections require only outbound TCP or HTTP connectivity from your private network.</span></span> <span data-ttu-id="71c7e-156">您不需要任何防火牆連接埠 tooopen 或變更您的網路周邊組態 tooallow 任何輸入的連線到您的網路。</span><span class="sxs-lookup"><span data-stu-id="71c7e-156">You do not need tooopen any firewall ports or change your network perimeter configuration tooallow any inbound connectivity into your network.</span></span>

<span data-ttu-id="71c7e-157">混合式連線會使用下列 TCP 連接埠的 hello:</span><span class="sxs-lookup"><span data-stu-id="71c7e-157">hello following TCP ports are used by Hybrid Connections:</span></span>

| <span data-ttu-id="71c7e-158">Port</span><span class="sxs-lookup"><span data-stu-id="71c7e-158">Port</span></span> | <span data-ttu-id="71c7e-159">您為何需要它</span><span class="sxs-lookup"><span data-stu-id="71c7e-159">Why you need it</span></span> |
| --- | --- |
| <span data-ttu-id="71c7e-160">9350 - 9354</span><span class="sxs-lookup"><span data-stu-id="71c7e-160">9350 - 9354</span></span> |<span data-ttu-id="71c7e-161">這些連接埠用於資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="71c7e-161">These ports are used for data transmission.</span></span> <span data-ttu-id="71c7e-162">hello Service Bus 轉送管理員探查連接埠 9350 toodetermine TCP 連線是否可用。</span><span class="sxs-lookup"><span data-stu-id="71c7e-162">hello Service Bus relay manager probes port 9350 toodetermine if TCP connectivity is available.</span></span> <span data-ttu-id="71c7e-163">如果可用的話，則會假設連接埠 9352 也是可用。</span><span class="sxs-lookup"><span data-stu-id="71c7e-163">If it is available, then it assumes that port 9352 is also available.</span></span> <span data-ttu-id="71c7e-164">資料流量會經過連接埠 9352。</span><span class="sxs-lookup"><span data-stu-id="71c7e-164">Data traffic goes over port 9352.</span></span> <br/><br/><span data-ttu-id="71c7e-165">允許輸出連線 toothese 連接埠。</span><span class="sxs-lookup"><span data-stu-id="71c7e-165">Allow outbound connections toothese ports.</span></span> |
| <span data-ttu-id="71c7e-166">5671</span><span class="sxs-lookup"><span data-stu-id="71c7e-166">5671</span></span> |<span data-ttu-id="71c7e-167">使用連接埠則為 9352 時的資料流量而言，hello 控制通道為使用連接埠 5671。</span><span class="sxs-lookup"><span data-stu-id="71c7e-167">When port 9352 is used for data traffic, port 5671 is used as hello control channel.</span></span> <br/><br/><span data-ttu-id="71c7e-168">允許輸出連線 toothis 連接埠。</span><span class="sxs-lookup"><span data-stu-id="71c7e-168">Allow outbound connections toothis port.</span></span> |
| <span data-ttu-id="71c7e-169">80、443</span><span class="sxs-lookup"><span data-stu-id="71c7e-169">80, 443</span></span> |<span data-ttu-id="71c7e-170">這些連接埠會用於某些資料要求 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="71c7e-170">These ports are used for some data requests tooAzure.</span></span> <span data-ttu-id="71c7e-171">也，則不會使用連接埠則為 9352 和 5671*然後*的連接埠 80 和 443 會 hello 後援用於資料傳輸和 hello 控制通道。</span><span class="sxs-lookup"><span data-stu-id="71c7e-171">Also, if ports 9352 and 5671 are not usable, *then* ports 80 and 443 are hello fallback ports used for data transmission and hello control channel.</span></span><br/><br/><span data-ttu-id="71c7e-172">允許輸出連線 toothese 連接埠。</span><span class="sxs-lookup"><span data-stu-id="71c7e-172">Allow outbound connections toothese ports.</span></span> <br/><br/><span data-ttu-id="71c7e-173">**請注意**不建議 toouse 這些因為 hello hello 取代後援連接埠的其他 TCP 通訊埠。</span><span class="sxs-lookup"><span data-stu-id="71c7e-173">**Note** It is not recommended toouse these as hello fallback ports in place of hello other TCP ports.</span></span> <span data-ttu-id="71c7e-174">hello HTTP/WebSocket 作為 hello 通訊協定，而不是原生 TCP 資料通道。</span><span class="sxs-lookup"><span data-stu-id="71c7e-174">hello HTTP/WebSocket is used as hello protocol instead of native TCP for data channels.</span></span> <span data-ttu-id="71c7e-175">這可能會導致效能變低。</span><span class="sxs-lookup"><span data-stu-id="71c7e-175">It could result in lower performance.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="71c7e-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71c7e-176">Next steps</span></span>
[<span data-ttu-id="71c7e-177">Create and manage Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="71c7e-177">Create and manage Hybrid Connections</span></span>](integration-hybrid-connection-create-manage.md)<br/><span data-ttu-id="71c7e-178">
[連接 Azure Web Apps tooan 在內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="71c7e-178">
[Connect Azure Web Apps tooan On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md)</span></span><br/><span data-ttu-id="71c7e-179">
[從 Azure web 應用程式連接 tooon 內部部署 SQL Server](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)</span><span class="sxs-lookup"><span data-stu-id="71c7e-179">
[Connect tooon-premises SQL Server from an Azure web app](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)</span></span><br/>

## <a name="see-also"></a><span data-ttu-id="71c7e-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="71c7e-180">See Also</span></span>
<span data-ttu-id="71c7e-181">[用於管理 Microsoft Azure 上之 BizTalk 服務的 REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md)</span><span class="sxs-lookup"><span data-stu-id="71c7e-181">[REST API for Managing BizTalk Services on Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md)</span></span><br/><span data-ttu-id="71c7e-182">
[使用 Azure 入口網站建立 BizTalk 服務](biztalk-provision-services.md)</span><span class="sxs-lookup"><span data-stu-id="71c7e-182">
[Create a BizTalk Service using Azure portal](biztalk-provision-services.md)</span></span><br/><span data-ttu-id="71c7e-183">
[BizTalk 服務：儀表板、監視和調整索引標籤](biztalk-dashboard-monitor-scale-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="71c7e-183">
[BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md)</span></span><br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
