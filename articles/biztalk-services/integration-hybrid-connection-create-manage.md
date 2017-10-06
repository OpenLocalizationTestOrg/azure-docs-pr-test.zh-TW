---
title: "aaaCreate 和管理混合式連線 |Microsoft 文件"
description: "了解 toocreate 混合連線，管理 hello 連接和安裝 hello 混合式連線管理員的方式。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a><span data-ttu-id="2da33-104">建立和管理混合式連線</span><span class="sxs-lookup"><span data-stu-id="2da33-104">Create and Manage Hybrid Connections</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2da33-105">BizTalk 混合式連線已停用，並以 App Service 混合式連線取代。</span><span class="sxs-lookup"><span data-stu-id="2da33-105">BizTalk Hybrid Connections is retired, and replaced by App Service Hybrid Connections.</span></span> <span data-ttu-id="2da33-106">如需詳細資訊，包括如何 toomanage 現有 BizTalk 混合式連線，請參閱[Azure 應用程式服務的混合式連線](../app-service/app-service-hybrid-connections.md)。</span><span class="sxs-lookup"><span data-stu-id="2da33-106">For more information, including how toomanage your existing BizTalk Hybrid Connections, see [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md).</span></span>


## <a name="overview-of-hello-steps"></a><span data-ttu-id="2da33-107">Hello 步驟的概觀</span><span class="sxs-lookup"><span data-stu-id="2da33-107">Overview of hello Steps</span></span>
1. <span data-ttu-id="2da33-108">建立混合式連接輸入 hello**主機名稱**或**FQDN**的私人網路中的 hello 在內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="2da33-108">Create a Hybrid Connection by entering hello **host name** or **FQDN** of hello on-premises resource in your private network.</span></span>
2. <span data-ttu-id="2da33-109">連結您的 Azure web 應用程式或 Azure 的行動裝置應用程式 toohello 混合式連接。</span><span class="sxs-lookup"><span data-stu-id="2da33-109">Link your Azure web apps or Azure mobile apps toohello Hybrid Connection.</span></span>
3. <span data-ttu-id="2da33-110">在內部部署資源上安裝 hello 混合式連線管理員，而且連接 toohello 特定混合式連接。</span><span class="sxs-lookup"><span data-stu-id="2da33-110">Install hello Hybrid Connection Manager on your on-premises resource and connect toohello specific Hybrid Connection.</span></span> <span data-ttu-id="2da33-111">提供按一下體驗 tooinstall hello Azure 入口網站，並連接。</span><span class="sxs-lookup"><span data-stu-id="2da33-111">hello Azure portal provides a single-click experience tooinstall and connect.</span></span>
4. <span data-ttu-id="2da33-112">管理混合式連線及其連接金鑰。</span><span class="sxs-lookup"><span data-stu-id="2da33-112">Manage Hybrid Connections and their connection keys.</span></span>

<span data-ttu-id="2da33-113">本主題將列出這些步驟。</span><span class="sxs-lookup"><span data-stu-id="2da33-113">This topic lists these steps.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2da33-114">很可能 tooset 混合式連接端點 tooan IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2da33-114">It is possible tooset a Hybrid Connection endpoint tooan IP address.</span></span> <span data-ttu-id="2da33-115">如果您使用的 IP 位址，您可能會或可能無法到達 hello 在內部部署資源，根據您的用戶端。</span><span class="sxs-lookup"><span data-stu-id="2da33-115">If you use an IP address, you may or may not reach hello on-premises resource, depending on your client.</span></span> <span data-ttu-id="2da33-116">hello 混合式連接取決於 hello 用戶端執行 DNS 查閱。</span><span class="sxs-lookup"><span data-stu-id="2da33-116">hello Hybrid Connection depends on hello client doing a DNS lookup.</span></span> <span data-ttu-id="2da33-117">在大部分情況下，hello**用戶端**是應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="2da33-117">In most cases, hello **client** is your application code.</span></span> <span data-ttu-id="2da33-118">如果 hello 用戶端不會執行 DNS 查閱、 （它不會嘗試 tooresolve hello IP 位址就好像是網域名稱 (x.x.x.x)），則流量不會傳送到 hello 混合式連接。</span><span class="sxs-lookup"><span data-stu-id="2da33-118">If hello client does not perform a DNS lookup, (it does not try tooresolve hello IP address as if it were a domain name (x.x.x.x)), then traffic is not sent through hello Hybrid Connection.</span></span>
> 
> <span data-ttu-id="2da33-119">例如 (虛擬程式碼)，您會定義 **10.4.5.6** 做為內部部署主機︰</span><span class="sxs-lookup"><span data-stu-id="2da33-119">For example (pseudocode), you define **10.4.5.6** as your on-premises host:</span></span>
> 
> <span data-ttu-id="2da33-120">**下列案例中運作的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2da33-120">**hello following scenario works:**</span></span>  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> <span data-ttu-id="2da33-121">**不適用於下列案例中的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2da33-121">**hello following scenario doesn't work:**</span></span>  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <span data-ttu-id="2da33-122"><a name="CreateHybridConnection"></a>建立混合式連線</span><span class="sxs-lookup"><span data-stu-id="2da33-122"><a name="CreateHybridConnection"></a>Create a Hybrid Connection</span></span>
<span data-ttu-id="2da33-123">混合式連接中可建立 hello 使用 Web 應用程式的 Azure 入口網站**或**使用 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="2da33-123">A Hybrid Connection can be created in hello Azure portal using Web Apps **or** using BizTalk Services.</span></span> 

<span data-ttu-id="2da33-124">**toocreate 使用 Web 應用程式的混合式連線**，請參閱[連接 Azure Web Apps tooan 在內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="2da33-124">**toocreate Hybrid Connections using Web Apps**, see [Connect Azure Web Apps tooan On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span> <span data-ttu-id="2da33-125">您也可以從您的 web 應用程式，這是慣用的 hello 方法安裝 hello 混合式連線管理員 (HCM)。</span><span class="sxs-lookup"><span data-stu-id="2da33-125">You can also install hello Hybrid Connection Manager (HCM) from your web app, which is hello preferred method.</span></span> 

<span data-ttu-id="2da33-126">**在 BizTalk 服務中的混合式連線 toocreate**:</span><span class="sxs-lookup"><span data-stu-id="2da33-126">**toocreate Hybrid Connections in BizTalk Services**:</span></span>

1. <span data-ttu-id="2da33-127">登入 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="2da33-127">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="2da33-128">在 hello 左側瀏覽窗格中，選取**BizTalk 服務**，然後選取 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="2da33-128">In hello left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
   
    <span data-ttu-id="2da33-129">如果您沒有現有的 BizTalk 服務，您可以 [建立 BizTalk 服務](biztalk-provision-services.md)。</span><span class="sxs-lookup"><span data-stu-id="2da33-129">If you don't have an existing BizTalk Service, you can [Create a BizTalk Service](biztalk-provision-services.md).</span></span>
3. <span data-ttu-id="2da33-130">選取 hello**混合式連線** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="2da33-130">Select hello **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="2da33-131">![混合式連線索引標籤][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="2da33-131">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="2da33-132">選取**建立混合式連接**或選取 hello**新增**hello 工作列中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="2da33-132">Select **Create a Hybrid Connection** or select hello **ADD** button in hello task bar.</span></span> <span data-ttu-id="2da33-133">輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2da33-133">Enter hello following:</span></span>
   
   | <span data-ttu-id="2da33-134">屬性</span><span class="sxs-lookup"><span data-stu-id="2da33-134">Property</span></span> | <span data-ttu-id="2da33-135">說明</span><span class="sxs-lookup"><span data-stu-id="2da33-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="2da33-136">名稱</span><span class="sxs-lookup"><span data-stu-id="2da33-136">Name</span></span> |<span data-ttu-id="2da33-137">hello 混合式連接名稱必須是唯一的而且不能 hello 相同命名為 hello BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="2da33-137">hello Hybrid Connection name must be unique and cannot be hello same name as hello BizTalk Service.</span></span> <span data-ttu-id="2da33-138">您可以輸入任何名稱，但要能夠具體表示用途。</span><span class="sxs-lookup"><span data-stu-id="2da33-138">You can enter any name but be specific with its purpose.</span></span> <span data-ttu-id="2da33-139">範例包括：</span><span class="sxs-lookup"><span data-stu-id="2da33-139">Examples include:</span></span><br/><br/><span data-ttu-id="2da33-140">Payroll*SQLServer*</span><span class="sxs-lookup"><span data-stu-id="2da33-140">Payroll*SQLServer*</span></span><br/><span data-ttu-id="2da33-141">SupplyList*SharepointServer*</span><span class="sxs-lookup"><span data-stu-id="2da33-141">SupplyList*SharepointServer*</span></span><br/><span data-ttu-id="2da33-142">Customers*OracleServer*</span><span class="sxs-lookup"><span data-stu-id="2da33-142">Customers*OracleServer*</span></span> |
   | <span data-ttu-id="2da33-143">主機名稱</span><span class="sxs-lookup"><span data-stu-id="2da33-143">Host Name</span></span> |<span data-ttu-id="2da33-144">輸入 hello 完整的主機名稱，只有 hello 主機名稱，或是 hello hello 在內部部署資源的 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="2da33-144">Enter hello fully qualified host name, only hello host name, or hello IPv4 address of hello on-premises resource.</span></span> <span data-ttu-id="2da33-145">範例包括：</span><span class="sxs-lookup"><span data-stu-id="2da33-145">Examples include:</span></span><br/><br/><span data-ttu-id="2da33-146">mySQLServer</span><span class="sxs-lookup"><span data-stu-id="2da33-146">mySQLServer</span></span><br/><span data-ttu-id="2da33-147">*mySQLServer*.*Domain*.corp.*yourCompany*.com</span><span class="sxs-lookup"><span data-stu-id="2da33-147">*mySQLServer*.*Domain*.corp.*yourCompany*.com</span></span><br/><span data-ttu-id="2da33-148">*myHTTPSharePointServer*</span><span class="sxs-lookup"><span data-stu-id="2da33-148">*myHTTPSharePointServer*</span></span><br/><span data-ttu-id="2da33-149">*myHTTPSharePointServer*.*yourCompany*.com</span><span class="sxs-lookup"><span data-stu-id="2da33-149">*myHTTPSharePointServer*.*yourCompany*.com</span></span><br/><span data-ttu-id="2da33-150">10.100.10.10</span><span class="sxs-lookup"><span data-stu-id="2da33-150">10.100.10.10</span></span><br/><br/><span data-ttu-id="2da33-151">如果您使用 hello IPv4 位址，請注意您的用戶端或應用程式程式碼可能無法解析 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2da33-151">If you use hello IPv4 address, note that your client or application code may not resolve hello IP address.</span></span> <span data-ttu-id="2da33-152">請參閱 hello 重要附註在 hello 本主題的頂端。</span><span class="sxs-lookup"><span data-stu-id="2da33-152">See hello Important note at hello top of this topic.</span></span> |
   | <span data-ttu-id="2da33-153">Port</span><span class="sxs-lookup"><span data-stu-id="2da33-153">Port</span></span> |<span data-ttu-id="2da33-154">輸入 hello hello 在內部部署資源連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="2da33-154">Enter hello port number of hello on-premises resource.</span></span> <span data-ttu-id="2da33-155">例如，如果您使用 Web Apps，請輸入連接埠 80 或 443。</span><span class="sxs-lookup"><span data-stu-id="2da33-155">For example, if you're using Web Apps, enter port 80 or port 443.</span></span> <span data-ttu-id="2da33-156">如果您使用 SQL Server，請輸入連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="2da33-156">If you're using SQL Server, enter port 1433.</span></span> |
5. <span data-ttu-id="2da33-157">選取 hello 核取記號 toocomplete hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="2da33-157">Select hello check mark toocomplete hello setup.</span></span> 

#### <a name="additional"></a><span data-ttu-id="2da33-158">其他</span><span class="sxs-lookup"><span data-stu-id="2da33-158">Additional</span></span>
* <span data-ttu-id="2da33-159">可建立多個混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2da33-159">Multiple Hybrid Connections can be created.</span></span> <span data-ttu-id="2da33-160">請參閱 hello [BizTalk 服務： 版本圖表](biztalk-editions-feature-chart.md)hello 允許連線的數目。</span><span class="sxs-lookup"><span data-stu-id="2da33-160">See hello [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) for hello number of connections allowed.</span></span> 
* <span data-ttu-id="2da33-161">每個「混合式連線」都是由一對連接字串建立而成：分別是負責「傳送」的應用程式金鑰，以及負責「接聽」的內部部署金鑰。</span><span class="sxs-lookup"><span data-stu-id="2da33-161">Each Hybrid Connection is created with a pair of connection strings: Application keys that SEND and On-premises keys that LISTEN.</span></span> <span data-ttu-id="2da33-162">每一對都有「主要」和「次要」金鑰。</span><span class="sxs-lookup"><span data-stu-id="2da33-162">Each pair has a Primary and a Secondary key.</span></span> 

## <span data-ttu-id="2da33-163"><a name="LinkWebSite"></a>連結 Azure App Service Web 應用程式或行動應用程式</span><span class="sxs-lookup"><span data-stu-id="2da33-163"><a name="LinkWebSite"></a>Link your Azure App Service Web App or Mobile App</span></span>
<span data-ttu-id="2da33-164">選取 toolink Web 應用程式或行動裝置應用程式中現有的混合式連接的 Azure App Service tooan**使用現有的混合式連接**hello 混合式連線刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="2da33-164">toolink a Web App or Mobile App in Azure App Service tooan existing Hybrid Connection, select **use an existing Hybrid Connection** in hello Hybrid Connections blade.</span></span> <span data-ttu-id="2da33-165">請參閱[在 Azure App Service 中使用混合式連線存取內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="2da33-165">See [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <span data-ttu-id="2da33-166"><a name="InstallHCM"></a>安裝 hello 混合式連線管理員內部部署</span><span class="sxs-lookup"><span data-stu-id="2da33-166"><a name="InstallHCM"></a>Install hello Hybrid Connection Manager on-premises</span></span>
<span data-ttu-id="2da33-167">建立混合式連接之後，安裝 hello 混合式連線管理員上 hello 在內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="2da33-167">After a Hybrid Connection is created, install hello Hybrid Connection Manager on hello on-premises resource.</span></span> <span data-ttu-id="2da33-168">可從 Azure Web Apps 或 BizTalk 服務下載此程式。</span><span class="sxs-lookup"><span data-stu-id="2da33-168">It can be downloaded from your Azure web apps or from your BizTalk Service.</span></span> <span data-ttu-id="2da33-169">BizTalk 服務步驟：</span><span class="sxs-lookup"><span data-stu-id="2da33-169">BizTalk Services steps:</span></span> 

1. <span data-ttu-id="2da33-170">登入 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="2da33-170">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="2da33-171">在 hello 左側瀏覽窗格中，選取**BizTalk 服務**，然後選取 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="2da33-171">In hello left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
3. <span data-ttu-id="2da33-172">選取 hello**混合式連線** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="2da33-172">Select hello **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="2da33-173">![混合式連線索引標籤][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="2da33-173">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="2da33-174">在 hello 工作列上，選取 **在內部部署安裝**:</span><span class="sxs-lookup"><span data-stu-id="2da33-174">In hello task bar, select **On-Premises Setup**:</span></span>  
   <span data-ttu-id="2da33-175">![內部部署設定][HCOnPremSetup]</span><span class="sxs-lookup"><span data-stu-id="2da33-175">![On-Premises Setup][HCOnPremSetup]</span></span>
5. <span data-ttu-id="2da33-176">選取**安裝及設定**toorun 或下載 hello 混合式連線管理員上 hello 內部部署系統。</span><span class="sxs-lookup"><span data-stu-id="2da33-176">Select **Install and Configure** toorun or download hello Hybrid Connection Manager on hello on-premises system.</span></span> 
6. <span data-ttu-id="2da33-177">選取 hello 核取記號 toostart hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="2da33-177">Select hello check mark toostart hello installation.</span></span> 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a><span data-ttu-id="2da33-178">其他</span><span class="sxs-lookup"><span data-stu-id="2da33-178">Additional</span></span>
* <span data-ttu-id="2da33-179">混合式連線管理員可以安裝在下列作業系統的 hello:</span><span class="sxs-lookup"><span data-stu-id="2da33-179">Hybrid Connection Manager can be installed on hello following operating systems:</span></span>
  
  * <span data-ttu-id="2da33-180">Windows Server 2008 R2 (須有 .NET Framework 4.5+ 和 Windows Management Framework 4.0+)</span><span class="sxs-lookup"><span data-stu-id="2da33-180">Windows Server 2008 R2 (.NET Framework 4.5+ and Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="2da33-181">Windows Server 2012 (須有 Windows Management Framework 4.0+)</span><span class="sxs-lookup"><span data-stu-id="2da33-181">Windows Server 2012 (Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="2da33-182">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2da33-182">Windows Server 2012 R2</span></span>
* <span data-ttu-id="2da33-183">安裝 hello 混合式連接管理員之後，hello 會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="2da33-183">After you install hello Hybrid Connection Manager, hello following occurs:</span></span> 
  
  * <span data-ttu-id="2da33-184">hello 裝載於 Azure 的混合式連線會自動設定的 toouse hello 主應用程式連接字串。</span><span class="sxs-lookup"><span data-stu-id="2da33-184">hello Hybrid Connection hosted on Azure is automatically configured toouse hello Primary Application Connection String.</span></span> 
  * <span data-ttu-id="2da33-185">hello 在內部部署資源為自動設定的 toouse hello 主要內部部署連接字串。</span><span class="sxs-lookup"><span data-stu-id="2da33-185">hello On-Premises resource is automatically configured toouse hello Primary On-Premises Connection String.</span></span>
* <span data-ttu-id="2da33-186">hello 混合式連線管理員必須使用有效的內部部署連接字串進行授權。</span><span class="sxs-lookup"><span data-stu-id="2da33-186">hello Hybrid Connection Manager must use a valid on-premises connection string for authorization.</span></span> <span data-ttu-id="2da33-187">hello Azure Web 應用程式或行動應用程式必須使用有效的應用程式連接字串進行授權。</span><span class="sxs-lookup"><span data-stu-id="2da33-187">hello Azure Web Apps or Mobile Apps must use a valid application connection string for authorization.</span></span>
* <span data-ttu-id="2da33-188">您可以在另一部伺服器上安裝另一個執行個體的 hello 混合式連線管理員調整混合式連線。</span><span class="sxs-lookup"><span data-stu-id="2da33-188">You can scale Hybrid Connections by installing another instance of hello Hybrid Connection Manager on another server.</span></span> <span data-ttu-id="2da33-189">設定 hello 在內部部署接聽程式 toouse hello 相同位址為 hello 第一個在內部部署接聽程式。</span><span class="sxs-lookup"><span data-stu-id="2da33-189">Configure hello on-premises listener toouse hello same address as hello first on-premises listener.</span></span> <span data-ttu-id="2da33-190">在此情況下，hello 已流量隨機分配 （循環配置資源） 之間 hello 作用中的內部部署接聽程式。</span><span class="sxs-lookup"><span data-stu-id="2da33-190">In this situation, hello traffic is randomly distributed (round robin) between hello active on-premises listeners.</span></span> 

## <span data-ttu-id="2da33-191"><a name="ManageHybridConnection"></a>管理混合式連線</span><span class="sxs-lookup"><span data-stu-id="2da33-191"><a name="ManageHybridConnection"></a>Manage Hybrid Connections</span></span>
<span data-ttu-id="2da33-192">toomanage 混合式連線，您可以：</span><span class="sxs-lookup"><span data-stu-id="2da33-192">toomanage your Hybrid Connections, you can:</span></span>

* <span data-ttu-id="2da33-193">使用 hello Azure 入口網站，並移 tooyour BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="2da33-193">Use hello Azure portal and go tooyour BizTalk Service.</span></span> 
* <span data-ttu-id="2da33-194">使用 [REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2da33-194">Use [REST APIs](http://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span>

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a><span data-ttu-id="2da33-195">複製/重新產生 hello 混合式連接字串</span><span class="sxs-lookup"><span data-stu-id="2da33-195">Copy/regenerate hello Hybrid Connection Strings</span></span>
1. <span data-ttu-id="2da33-196">登入 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="2da33-196">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="2da33-197">在 hello 左側瀏覽窗格中，選取**BizTalk 服務**，然後選取 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="2da33-197">In hello left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
3. <span data-ttu-id="2da33-198">選取 hello**混合式連線** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="2da33-198">Select hello **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="2da33-199">![混合式連線索引標籤][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="2da33-199">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="2da33-200">選取 hello 混合式連接。</span><span class="sxs-lookup"><span data-stu-id="2da33-200">Select hello Hybrid Connection.</span></span> <span data-ttu-id="2da33-201">在 hello 工作列上，選取 **管理連接**:</span><span class="sxs-lookup"><span data-stu-id="2da33-201">In hello task bar, select **Manage Connection**:</span></span>  
   <span data-ttu-id="2da33-202">![管理選項][HCManageConnection]</span><span class="sxs-lookup"><span data-stu-id="2da33-202">![Manage Options][HCManageConnection]</span></span>
   
    <span data-ttu-id="2da33-203">**管理連線**清單 hello 應用程式和內部部署連接字串。</span><span class="sxs-lookup"><span data-stu-id="2da33-203">**Manage Connection** lists hello Application and On-Premises connection strings.</span></span> <span data-ttu-id="2da33-204">您可以複製連接字串 hello 或重新產生存取金鑰 hello 連接字串中所使用的 hello。</span><span class="sxs-lookup"><span data-stu-id="2da33-204">You can copy hello Connection Strings or regenerate hello Access Key used in hello connection string.</span></span> 
   
    <span data-ttu-id="2da33-205">**如果您選取重新產生**，hello 的 hello 則變更連接字串內使用共用存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2da33-205">**If you select Regenerate**, hello Shared Access Key used within hello Connection String is changed.</span></span> <span data-ttu-id="2da33-206">請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="2da33-206">Do hello following:</span></span>
   
   * <span data-ttu-id="2da33-207">在 hello Azure 傳統入口網站，選取 **同步金鑰**hello Azure 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="2da33-207">In hello Azure classic portal, select **Sync Keys** in hello Azure application.</span></span>
   * <span data-ttu-id="2da33-208">重新執行 hello**在內部部署安裝**。</span><span class="sxs-lookup"><span data-stu-id="2da33-208">Re-run hello **On-Premises Setup**.</span></span> <span data-ttu-id="2da33-209">當您重新執行 hello 在內部部署安裝程式，在內部部署資源，則會自動 hello 設定 toouse hello 更新主要連接字串。</span><span class="sxs-lookup"><span data-stu-id="2da33-209">When you re-run hello On-Premises Setup, hello on-premises resource is automatically configured toouse hello updated Primary connection string.</span></span>

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a><span data-ttu-id="2da33-210">使用群組原則 toocontrol hello 內部部署混合式連接所使用的資源</span><span class="sxs-lookup"><span data-stu-id="2da33-210">Use Group Policy toocontrol hello on-premises resources used by a Hybrid Connection</span></span>
1. <span data-ttu-id="2da33-211">下載 hello[混合式連線管理員系統管理範本](http://www.microsoft.com/download/details.aspx?id=42963)。</span><span class="sxs-lookup"><span data-stu-id="2da33-211">Download hello [Hybrid Connection Manager Administrative Templates](http://www.microsoft.com/download/details.aspx?id=42963).</span></span>
2. <span data-ttu-id="2da33-212">Hello 檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="2da33-212">Extract hello files.</span></span>
3. <span data-ttu-id="2da33-213">Hello 在電腦上修改群組原則，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="2da33-213">On hello computer that modifies group policy, do hello following:</span></span>  
   
   * <span data-ttu-id="2da33-214">將複製 hello。ADMX 檔案 toohello *%WINROOT%\PolicyDefinitions*資料夾。</span><span class="sxs-lookup"><span data-stu-id="2da33-214">Copy hello .ADMX files toohello *%WINROOT%\PolicyDefinitions* folder.</span></span>
   * <span data-ttu-id="2da33-215">將複製 hello。ADML 檔案 toohello *%WINROOT%\PolicyDefinitions\en-us*資料夾。</span><span class="sxs-lookup"><span data-stu-id="2da33-215">Copy hello .ADML files toohello *%WINROOT%\PolicyDefinitions\en-us* folder.</span></span>

<span data-ttu-id="2da33-216">複製後，您可以使用群組原則編輯器 toochange hello 原則。</span><span class="sxs-lookup"><span data-stu-id="2da33-216">Once copied, you can use Group Policy Editor toochange hello policy.</span></span>

## <a name="next"></a><span data-ttu-id="2da33-217">下一步</span><span class="sxs-lookup"><span data-stu-id="2da33-217">Next</span></span>
[<span data-ttu-id="2da33-218">連接 Azure Web Apps tooan 在內部部署資源</span><span class="sxs-lookup"><span data-stu-id="2da33-218">Connect Azure Web Apps tooan On-Premises Resource</span></span>](../app-service-web/web-sites-hybrid-connection-get-started.md)  
<span data-ttu-id="2da33-219">[從 Azure Web 應用程式連接 tooon 內部部署 SQL Server](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="2da33-219">[Connect tooon-premises SQL Server from Azure Web Apps](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md) </span></span>  
[<span data-ttu-id="2da33-220">混合式連線概觀</span><span class="sxs-lookup"><span data-stu-id="2da33-220">Hybrid Connections Overview</span></span>](integration-hybrid-connection-overview.md)

## <a name="see-also"></a><span data-ttu-id="2da33-221">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2da33-221">See Also</span></span>
[<span data-ttu-id="2da33-222">用於管理 Microsoft Azure 上之 BizTalk 服務的 REST API</span><span class="sxs-lookup"><span data-stu-id="2da33-222">REST API for Managing BizTalk Services on Microsoft Azure</span></span>](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[<span data-ttu-id="2da33-223">BizTalk 服務：版本圖表</span><span class="sxs-lookup"><span data-stu-id="2da33-223">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
[<span data-ttu-id="2da33-224">使用 Azure 傳統入口網站建立「BizTalk 服務」</span><span class="sxs-lookup"><span data-stu-id="2da33-224">Create a BizTalk Service using Azure classic portal</span></span>](biztalk-provision-services.md)  
[<span data-ttu-id="2da33-225">BizTalk 服務：儀表板、監視和調整索引標籤</span><span class="sxs-lookup"><span data-stu-id="2da33-225">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
