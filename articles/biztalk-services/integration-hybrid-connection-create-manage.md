---
title: "建立和管理混合式連接 | Microsoft Docs"
description: "了解如何建立混合式連線、管理連線和安裝 Hybrid Connection Manager。 MABS，WABS"
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
ms.openlocfilehash: fceb6b0671e0f77c1f8f92bbb49c986fda3660ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-hybrid-connections"></a><span data-ttu-id="f4860-104">建立和管理混合式連線</span><span class="sxs-lookup"><span data-stu-id="f4860-104">Create and Manage Hybrid Connections</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4860-105">BizTalk 混合式連線已停用，並以 App Service 混合式連線取代。</span><span class="sxs-lookup"><span data-stu-id="f4860-105">BizTalk Hybrid Connections is retired, and replaced by App Service Hybrid Connections.</span></span> <span data-ttu-id="f4860-106">如需詳細資訊，包括如何管理您現有的 BizTalk 混合式連線，請參閱 [Azure App Service 混合式連線](../app-service/app-service-hybrid-connections.md)。</span><span class="sxs-lookup"><span data-stu-id="f4860-106">For more information, including how to manage your existing BizTalk Hybrid Connections, see [Azure App Service Hybrid Connections](../app-service/app-service-hybrid-connections.md).</span></span>


## <a name="overview-of-the-steps"></a><span data-ttu-id="f4860-107">步驟概觀</span><span class="sxs-lookup"><span data-stu-id="f4860-107">Overview of the Steps</span></span>
1. <span data-ttu-id="f4860-108">輸入私人網路中內部部署資源的 **host name** 或 **FQDN** of the on-premises resource in your private netw或k.</span><span class="sxs-lookup"><span data-stu-id="f4860-108">Create a Hybrid Connection by entering the **host name** or **FQDN** of the on-premises resource in your private network.</span></span>
2. <span data-ttu-id="f4860-109">將 Azure Web Apps 或 Azure Mobile Apps 連結至混合式連線。</span><span class="sxs-lookup"><span data-stu-id="f4860-109">Link your Azure web apps or Azure mobile apps to the Hybrid Connection.</span></span>
3. <span data-ttu-id="f4860-110">安裝混合式連線管理員在內部部署資源上，並連接至特定的混合式連線。</span><span class="sxs-lookup"><span data-stu-id="f4860-110">Install the Hybrid Connection Manager on your on-premises resource and connect to the specific Hybrid Connection.</span></span> <span data-ttu-id="f4860-111">Azure 入口網站提供按一下即可安裝和連接的體驗。</span><span class="sxs-lookup"><span data-stu-id="f4860-111">The Azure portal provides a single-click experience to install and connect.</span></span>
4. <span data-ttu-id="f4860-112">管理混合式連線及其連接金鑰。</span><span class="sxs-lookup"><span data-stu-id="f4860-112">Manage Hybrid Connections and their connection keys.</span></span>

<span data-ttu-id="f4860-113">本主題將列出這些步驟。</span><span class="sxs-lookup"><span data-stu-id="f4860-113">This topic lists these steps.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f4860-114">可以將「混合式連線」端點設定為 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f4860-114">It is possible to set a Hybrid Connection endpoint to an IP address.</span></span> <span data-ttu-id="f4860-115">如果您使用 IP 位址，視您的用戶端而言，您不一定會觸達內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="f4860-115">If you use an IP address, you may or may not reach the on-premises resource, depending on your client.</span></span> <span data-ttu-id="f4860-116">「混合式連線」取決於執行 DNS 查閱的用戶端。</span><span class="sxs-lookup"><span data-stu-id="f4860-116">The Hybrid Connection depends on the client doing a DNS lookup.</span></span> <span data-ttu-id="f4860-117">在大部分情況下， **用戶端** 是您的應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="f4860-117">In most cases, the **client** is your application code.</span></span> <span data-ttu-id="f4860-118">如果用戶端不執行 DNS 查閱 (不會嘗試解析 IP 位址，彷彿它是網域名稱 (x.x.x.x) 一樣)，則不會透過「混合式連線」傳送流量。</span><span class="sxs-lookup"><span data-stu-id="f4860-118">If the client does not perform a DNS lookup, (it does not try to resolve the IP address as if it were a domain name (x.x.x.x)), then traffic is not sent through the Hybrid Connection.</span></span>
> 
> <span data-ttu-id="f4860-119">例如 (虛擬程式碼)，您會定義 **10.4.5.6** 做為內部部署主機︰</span><span class="sxs-lookup"><span data-stu-id="f4860-119">For example (pseudocode), you define **10.4.5.6** as your on-premises host:</span></span>
> 
> <span data-ttu-id="f4860-120">**下列案例可運作︰**</span><span class="sxs-lookup"><span data-stu-id="f4860-120">**The following scenario works:**</span></span>  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves to 127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> <span data-ttu-id="f4860-121">**下列案例無法運作︰**</span><span class="sxs-lookup"><span data-stu-id="f4860-121">**The following scenario doesn't work:**</span></span>  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route to host`
> 
> 

## <span data-ttu-id="f4860-122"><a name="CreateHybridConnection"></a>建立混合式連線</span><span class="sxs-lookup"><span data-stu-id="f4860-122"><a name="CreateHybridConnection"></a>Create a Hybrid Connection</span></span>
<span data-ttu-id="f4860-123">使用 Web Apps **或** BizTalk 服務可以在 Azure 入口網站中建立「混合式連接」。</span><span class="sxs-lookup"><span data-stu-id="f4860-123">A Hybrid Connection can be created in the Azure portal using Web Apps **or** using BizTalk Services.</span></span> 

<span data-ttu-id="f4860-124">**若要使用 Web Apps 建立「混合式連線」**，請參閱「 [將 Azure Web Apps 連接到內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)」(英文)。</span><span class="sxs-lookup"><span data-stu-id="f4860-124">**To create Hybrid Connections using Web Apps**, see [Connect Azure Web Apps to an On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span> <span data-ttu-id="f4860-125">您也可以從 Web 應用程式安裝混合式連線管理員 (HCM)，這是慣用的方法。</span><span class="sxs-lookup"><span data-stu-id="f4860-125">You can also install the Hybrid Connection Manager (HCM) from your web app, which is the preferred method.</span></span> 

<span data-ttu-id="f4860-126">**若要在 BizTalk 服務中建立「混合式連線」**：</span><span class="sxs-lookup"><span data-stu-id="f4860-126">**To create Hybrid Connections in BizTalk Services**:</span></span>

1. <span data-ttu-id="f4860-127">登入 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="f4860-127">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="f4860-128">在左側瀏覽窗格中，選取 [ **BizTalk 服務** ]，然後選取您的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f4860-128">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
   
    <span data-ttu-id="f4860-129">如果您沒有現有的 BizTalk 服務，您可以 [建立 BizTalk 服務](biztalk-provision-services.md)。</span><span class="sxs-lookup"><span data-stu-id="f4860-129">If you don't have an existing BizTalk Service, you can [Create a BizTalk Service](biztalk-provision-services.md).</span></span>
3. <span data-ttu-id="f4860-130">選取 [混合式連接] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="f4860-130">Select the **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="f4860-131">![混合式連線索引標籤][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="f4860-131">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="f4860-132">選取 [建立混合式連接]，或在工作列中選取 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f4860-132">Select **Create a Hybrid Connection** or select the **ADD** button in the task bar.</span></span> <span data-ttu-id="f4860-133">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="f4860-133">Enter the following:</span></span>
   
   | <span data-ttu-id="f4860-134">屬性</span><span class="sxs-lookup"><span data-stu-id="f4860-134">Property</span></span> | <span data-ttu-id="f4860-135">說明</span><span class="sxs-lookup"><span data-stu-id="f4860-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="f4860-136">名稱</span><span class="sxs-lookup"><span data-stu-id="f4860-136">Name</span></span> |<span data-ttu-id="f4860-137">混合式連線名稱必須是唯一的，且不能與 BizTalk 服務的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="f4860-137">The Hybrid Connection name must be unique and cannot be the same name as the BizTalk Service.</span></span> <span data-ttu-id="f4860-138">您可以輸入任何名稱，但要能夠具體表示用途。</span><span class="sxs-lookup"><span data-stu-id="f4860-138">You can enter any name but be specific with its purpose.</span></span> <span data-ttu-id="f4860-139">範例包括：</span><span class="sxs-lookup"><span data-stu-id="f4860-139">Examples include:</span></span><br/><br/><span data-ttu-id="f4860-140">Payroll*SQLServer*</span><span class="sxs-lookup"><span data-stu-id="f4860-140">Payroll*SQLServer*</span></span><br/><span data-ttu-id="f4860-141">SupplyList*SharepointServer*</span><span class="sxs-lookup"><span data-stu-id="f4860-141">SupplyList*SharepointServer*</span></span><br/><span data-ttu-id="f4860-142">Customers*OracleServer*</span><span class="sxs-lookup"><span data-stu-id="f4860-142">Customers*OracleServer*</span></span> |
   | <span data-ttu-id="f4860-143">主機名稱</span><span class="sxs-lookup"><span data-stu-id="f4860-143">Host Name</span></span> |<span data-ttu-id="f4860-144">輸入內部部署資源的完整主機名稱、僅主機名稱，或 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="f4860-144">Enter the fully qualified host name, only the host name, or the IPv4 address of the on-premises resource.</span></span> <span data-ttu-id="f4860-145">範例包括：</span><span class="sxs-lookup"><span data-stu-id="f4860-145">Examples include:</span></span><br/><br/><span data-ttu-id="f4860-146">mySQLServer</span><span class="sxs-lookup"><span data-stu-id="f4860-146">mySQLServer</span></span><br/><span data-ttu-id="f4860-147">*mySQLServer*.*Domain*.corp.*yourCompany*.com</span><span class="sxs-lookup"><span data-stu-id="f4860-147">*mySQLServer*.*Domain*.corp.*yourCompany*.com</span></span><br/><span data-ttu-id="f4860-148">*myHTTPSharePointServer*</span><span class="sxs-lookup"><span data-stu-id="f4860-148">*myHTTPSharePointServer*</span></span><br/><span data-ttu-id="f4860-149">*myHTTPSharePointServer*.*yourCompany*.com</span><span class="sxs-lookup"><span data-stu-id="f4860-149">*myHTTPSharePointServer*.*yourCompany*.com</span></span><br/><span data-ttu-id="f4860-150">10.100.10.10</span><span class="sxs-lookup"><span data-stu-id="f4860-150">10.100.10.10</span></span><br/><br/><span data-ttu-id="f4860-151">如果您使用 IPv4 位址，請注意，您的用戶端或應用程式程式碼可能不會解析此 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f4860-151">If you use the IPv4 address, note that your client or application code may not resolve the IP address.</span></span> <span data-ttu-id="f4860-152">請參閱本主題最前面的「重要事項」。</span><span class="sxs-lookup"><span data-stu-id="f4860-152">See the Important note at the top of this topic.</span></span> |
   | <span data-ttu-id="f4860-153">連接埠</span><span class="sxs-lookup"><span data-stu-id="f4860-153">Port</span></span> |<span data-ttu-id="f4860-154">輸入內部部署資源的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="f4860-154">Enter the port number of the on-premises resource.</span></span> <span data-ttu-id="f4860-155">例如，如果您使用 Web Apps，請輸入連接埠 80 或 443。</span><span class="sxs-lookup"><span data-stu-id="f4860-155">For example, if you're using Web Apps, enter port 80 or port 443.</span></span> <span data-ttu-id="f4860-156">如果您使用 SQL Server，請輸入連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="f4860-156">If you're using SQL Server, enter port 1433.</span></span> |
5. <span data-ttu-id="f4860-157">選取核取記號以完成設定。</span><span class="sxs-lookup"><span data-stu-id="f4860-157">Select the check mark to complete the setup.</span></span> 

#### <a name="additional"></a><span data-ttu-id="f4860-158">其他</span><span class="sxs-lookup"><span data-stu-id="f4860-158">Additional</span></span>
* <span data-ttu-id="f4860-159">可建立多個混合式連線。</span><span class="sxs-lookup"><span data-stu-id="f4860-159">Multiple Hybrid Connections can be created.</span></span> <span data-ttu-id="f4860-160">請參閱「 [BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md) 」(英文) 瞭解允許的連接數量。</span><span class="sxs-lookup"><span data-stu-id="f4860-160">See the [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) for the number of connections allowed.</span></span> 
* <span data-ttu-id="f4860-161">每個「混合式連線」都是由一對連接字串建立而成：分別是負責「傳送」的應用程式金鑰，以及負責「接聽」的內部部署金鑰。</span><span class="sxs-lookup"><span data-stu-id="f4860-161">Each Hybrid Connection is created with a pair of connection strings: Application keys that SEND and On-premises keys that LISTEN.</span></span> <span data-ttu-id="f4860-162">每一對都有「主要」和「次要」金鑰。</span><span class="sxs-lookup"><span data-stu-id="f4860-162">Each pair has a Primary and a Secondary key.</span></span> 

## <span data-ttu-id="f4860-163"><a name="LinkWebSite"></a>連結 Azure App Service Web 應用程式或行動應用程式</span><span class="sxs-lookup"><span data-stu-id="f4860-163"><a name="LinkWebSite"></a>Link your Azure App Service Web App or Mobile App</span></span>
<span data-ttu-id="f4860-164">若要將 Azure App Service 中的 Web 應用程式或行動應用程式連結至現有的「混合式連線」，請在 [混合式連線] 刀鋒視窗中選取 [使用現有的混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="f4860-164">To link a Web App or Mobile App in Azure App Service to an existing Hybrid Connection, select **use an existing Hybrid Connection** in the Hybrid Connections blade.</span></span> <span data-ttu-id="f4860-165">請參閱[在 Azure App Service 中使用混合式連線存取內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f4860-165">See [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <span data-ttu-id="f4860-166"><a name="InstallHCM"></a>在內部部署安裝混合式連線管理員</span><span class="sxs-lookup"><span data-stu-id="f4860-166"><a name="InstallHCM"></a>Install the Hybrid Connection Manager on-premises</span></span>
<span data-ttu-id="f4860-167">建立混合式連線之後，請在內部部署資源上安裝混合式連線管理員。</span><span class="sxs-lookup"><span data-stu-id="f4860-167">After a Hybrid Connection is created, install the Hybrid Connection Manager on the on-premises resource.</span></span> <span data-ttu-id="f4860-168">可從 Azure Web Apps 或 BizTalk 服務下載此程式。</span><span class="sxs-lookup"><span data-stu-id="f4860-168">It can be downloaded from your Azure web apps or from your BizTalk Service.</span></span> <span data-ttu-id="f4860-169">BizTalk 服務步驟：</span><span class="sxs-lookup"><span data-stu-id="f4860-169">BizTalk Services steps:</span></span> 

1. <span data-ttu-id="f4860-170">登入 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="f4860-170">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="f4860-171">在左側瀏覽窗格中，選取 [ **BizTalk 服務** ]，然後選取您的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f4860-171">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
3. <span data-ttu-id="f4860-172">選取 [混合式連接] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="f4860-172">Select the **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="f4860-173">![混合式連線索引標籤][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="f4860-173">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="f4860-174">在工作列中，選取 [內部部署設定] **內部部署設定**：</span><span class="sxs-lookup"><span data-stu-id="f4860-174">In the task bar, select **On-Premises Setup**:</span></span>  
   <span data-ttu-id="f4860-175">![內部部署設定][HCOnPremSetup]</span><span class="sxs-lookup"><span data-stu-id="f4860-175">![On-Premises Setup][HCOnPremSetup]</span></span>
5. <span data-ttu-id="f4860-176">選取 [ **安裝和設定** ]，在內部部署系統上執行或下載混合式連線管理員。</span><span class="sxs-lookup"><span data-stu-id="f4860-176">Select **Install and Configure** to run or download the Hybrid Connection Manager on the on-premises system.</span></span> 
6. <span data-ttu-id="f4860-177">選取核取記號來開始安裝。</span><span class="sxs-lookup"><span data-stu-id="f4860-177">Select the check mark to start the installation.</span></span> 

<!--
You can also download the Hybrid Connection Manager MSI file and copy the file to your on-premises resource. Specific steps:

1. Copy the on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for the specific steps.
2. Download the Hybrid Connection Manager MSI file. 
3. On the on-premises resource, install the Hybrid Connection Manager from the MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a><span data-ttu-id="f4860-178">其他</span><span class="sxs-lookup"><span data-stu-id="f4860-178">Additional</span></span>
* <span data-ttu-id="f4860-179">混合式連線管理員可以安裝在以下作業系統上︰</span><span class="sxs-lookup"><span data-stu-id="f4860-179">Hybrid Connection Manager can be installed on the following operating systems:</span></span>
  
  * <span data-ttu-id="f4860-180">Windows Server 2008 R2 (須有 .NET Framework 4.5+ 和 Windows Management Framework 4.0+)</span><span class="sxs-lookup"><span data-stu-id="f4860-180">Windows Server 2008 R2 (.NET Framework 4.5+ and Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="f4860-181">Windows Server 2012 (須有 Windows Management Framework 4.0+)</span><span class="sxs-lookup"><span data-stu-id="f4860-181">Windows Server 2012 (Windows Management Framework 4.0+ required)</span></span>
  * <span data-ttu-id="f4860-182">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f4860-182">Windows Server 2012 R2</span></span>
* <span data-ttu-id="f4860-183">安裝混合式連線管理員之後的情況如下：</span><span class="sxs-lookup"><span data-stu-id="f4860-183">After you install the Hybrid Connection Manager, the following occurs:</span></span> 
  
  * <span data-ttu-id="f4860-184">裝載於 Azure 的混合式連線會自動設定為使用「主要應用程式連接字串」。</span><span class="sxs-lookup"><span data-stu-id="f4860-184">The Hybrid Connection hosted on Azure is automatically configured to use the Primary Application Connection String.</span></span> 
  * <span data-ttu-id="f4860-185">內部部署資源會自動設定為使用「主要內部部署連接字串」。</span><span class="sxs-lookup"><span data-stu-id="f4860-185">The On-Premises resource is automatically configured to use the Primary On-Premises Connection String.</span></span>
* <span data-ttu-id="f4860-186">混合式連線管理員必須使用有效的內部部署連接字串，才能進行授權。</span><span class="sxs-lookup"><span data-stu-id="f4860-186">The Hybrid Connection Manager must use a valid on-premises connection string for authorization.</span></span> <span data-ttu-id="f4860-187">Azure Web Apps 或 Azure Mobile Apps 必須使用有效的應用程式連接字串，才能進行授權。</span><span class="sxs-lookup"><span data-stu-id="f4860-187">The Azure Web Apps or Mobile Apps must use a valid application connection string for authorization.</span></span>
* <span data-ttu-id="f4860-188">您可以在另一部伺服器上安裝另一個混合式連線管理員的執行個體，藉此調整混合式連線。</span><span class="sxs-lookup"><span data-stu-id="f4860-188">You can scale Hybrid Connections by installing another instance of the Hybrid Connection Manager on another server.</span></span> <span data-ttu-id="f4860-189">設定內部部署接聽程式，以使用與第一個內部部署接聽程式相同的位址。</span><span class="sxs-lookup"><span data-stu-id="f4860-189">Configure the on-premises listener to use the same address as the first on-premises listener.</span></span> <span data-ttu-id="f4860-190">在此情況下，流量會隨機分散 (循環配置資源) 到作用中的內部部署接聽程式之間。</span><span class="sxs-lookup"><span data-stu-id="f4860-190">In this situation, the traffic is randomly distributed (round robin) between the active on-premises listeners.</span></span> 

## <span data-ttu-id="f4860-191"><a name="ManageHybridConnection"></a>管理混合式連線</span><span class="sxs-lookup"><span data-stu-id="f4860-191"><a name="ManageHybridConnection"></a>Manage Hybrid Connections</span></span>
<span data-ttu-id="f4860-192">若要管理混合式連線，您可以：</span><span class="sxs-lookup"><span data-stu-id="f4860-192">To manage your Hybrid Connections, you can:</span></span>

* <span data-ttu-id="f4860-193">使用 Azure 入口網站並移至您的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f4860-193">Use the Azure portal and go to your BizTalk Service.</span></span> 
* <span data-ttu-id="f4860-194">使用 [REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f4860-194">Use [REST APIs](http://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span>

#### <a name="copyregenerate-the-hybrid-connection-strings"></a><span data-ttu-id="f4860-195">複製/重新產生混合式連線字串</span><span class="sxs-lookup"><span data-stu-id="f4860-195">Copy/regenerate the Hybrid Connection Strings</span></span>
1. <span data-ttu-id="f4860-196">登入 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="f4860-196">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="f4860-197">在左側瀏覽窗格中，選取 [ **BizTalk 服務** ]，然後選取您的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f4860-197">In the left navigation pane, select **BizTalk Services** and then select your BizTalk Service.</span></span> 
3. <span data-ttu-id="f4860-198">選取 [混合式連接] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="f4860-198">Select the **Hybrid Connections** tab:</span></span>  
   <span data-ttu-id="f4860-199">![混合式連線索引標籤][HybridConnectionTab]</span><span class="sxs-lookup"><span data-stu-id="f4860-199">![Hybrid Connections Tab][HybridConnectionTab]</span></span>
4. <span data-ttu-id="f4860-200">選取 [混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="f4860-200">Select the Hybrid Connection.</span></span> <span data-ttu-id="f4860-201">在工作列中，選取 [內部部署設定] ：</span><span class="sxs-lookup"><span data-stu-id="f4860-201">In the task bar, select **Manage Connection**:</span></span>  
   <span data-ttu-id="f4860-202">![管理選項][HCManageConnection]</span><span class="sxs-lookup"><span data-stu-id="f4860-202">![Manage Options][HCManageConnection]</span></span>
   
    <span data-ttu-id="f4860-203"> 會列出應用程式和內部部署連接字串。</span><span class="sxs-lookup"><span data-stu-id="f4860-203">**Manage Connection** lists the Application and On-Premises connection strings.</span></span> <span data-ttu-id="f4860-204">您可以複製連接字串，或重新產生連接字串所使用的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="f4860-204">You can copy the Connection Strings or regenerate the Access Key used in the connection string.</span></span> 
   
    <span data-ttu-id="f4860-205">如果您選取 [重新產生]，連接字串所使用的共用存取金鑰便會變更。</span><span class="sxs-lookup"><span data-stu-id="f4860-205">**If you select Regenerate**, the Shared Access Key used within the Connection String is changed.</span></span> <span data-ttu-id="f4860-206">執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f4860-206">Do the following:</span></span>
   
   * <span data-ttu-id="f4860-207">在 Azure 傳統入口網站中，選取 Azure 應用程式中的 [同步金鑰]  。</span><span class="sxs-lookup"><span data-stu-id="f4860-207">In the Azure classic portal, select **Sync Keys** in the Azure application.</span></span>
   * <span data-ttu-id="f4860-208">重新執行 [ **內部部署設定**]。</span><span class="sxs-lookup"><span data-stu-id="f4860-208">Re-run the **On-Premises Setup**.</span></span> <span data-ttu-id="f4860-209">重新執行內部部署設定時，內部部署資源會自動設定為使用已更新的主要連接字串。</span><span class="sxs-lookup"><span data-stu-id="f4860-209">When you re-run the On-Premises Setup, the on-premises resource is automatically configured to use the updated Primary connection string.</span></span>

#### <a name="use-group-policy-to-control-the-on-premises-resources-used-by-a-hybrid-connection"></a><span data-ttu-id="f4860-210">使用群組原則來控制混合式連線使用的內部部署資源</span><span class="sxs-lookup"><span data-stu-id="f4860-210">Use Group Policy to control the on-premises resources used by a Hybrid Connection</span></span>
1. <span data-ttu-id="f4860-211">下載 [混合式連線管理員的系統管理範本](http://www.microsoft.com/download/details.aspx?id=42963)。</span><span class="sxs-lookup"><span data-stu-id="f4860-211">Download the [Hybrid Connection Manager Administrative Templates](http://www.microsoft.com/download/details.aspx?id=42963).</span></span>
2. <span data-ttu-id="f4860-212">將檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="f4860-212">Extract the files.</span></span>
3. <span data-ttu-id="f4860-213">在修改群組原則的電腦上，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f4860-213">On the computer that modifies group policy, do the following:</span></span>  
   
   * <span data-ttu-id="f4860-214">將 .ADMX 檔案複製到 %WINROOT%\PolicyDefinitions 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f4860-214">Copy the .ADMX files to the *%WINROOT%\PolicyDefinitions* folder.</span></span>
   * <span data-ttu-id="f4860-215">將 .ADML 檔案複製到 %WINROOT%\PolicyDefinitions\en-us 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f4860-215">Copy the .ADML files to the *%WINROOT%\PolicyDefinitions\en-us* folder.</span></span>

<span data-ttu-id="f4860-216">複製之後，您可以使用群組原則編輯器來變更原則。</span><span class="sxs-lookup"><span data-stu-id="f4860-216">Once copied, you can use Group Policy Editor to change the policy.</span></span>

## <a name="next"></a><span data-ttu-id="f4860-217">下一步</span><span class="sxs-lookup"><span data-stu-id="f4860-217">Next</span></span>
[<span data-ttu-id="f4860-218">將 Azure Web Apps 連接到內部部署資源</span><span class="sxs-lookup"><span data-stu-id="f4860-218">Connect Azure Web Apps to an On-Premises Resource</span></span>](../app-service-web/web-sites-hybrid-connection-get-started.md)  
<span data-ttu-id="f4860-219">[從 Azure Web Apps 連接至內部部署 SQL Server](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="f4860-219">[Connect to on-premises SQL Server from Azure Web Apps](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md) </span></span>  
[<span data-ttu-id="f4860-220">混合式連線概觀</span><span class="sxs-lookup"><span data-stu-id="f4860-220">Hybrid Connections Overview</span></span>](integration-hybrid-connection-overview.md)

## <a name="see-also"></a><span data-ttu-id="f4860-221">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f4860-221">See Also</span></span>
[<span data-ttu-id="f4860-222">用於管理 Microsoft Azure 上之 BizTalk 服務的 REST API</span><span class="sxs-lookup"><span data-stu-id="f4860-222">REST API for Managing BizTalk Services on Microsoft Azure</span></span>](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[<span data-ttu-id="f4860-223">BizTalk 服務：版本圖表</span><span class="sxs-lookup"><span data-stu-id="f4860-223">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
[<span data-ttu-id="f4860-224">使用 Azure 傳統入口網站建立「BizTalk 服務」</span><span class="sxs-lookup"><span data-stu-id="f4860-224">Create a BizTalk Service using Azure classic portal</span></span>](biztalk-provision-services.md)  
[<span data-ttu-id="f4860-225">BizTalk 服務：儀表板、監視和調整索引標籤</span><span class="sxs-lookup"><span data-stu-id="f4860-225">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
