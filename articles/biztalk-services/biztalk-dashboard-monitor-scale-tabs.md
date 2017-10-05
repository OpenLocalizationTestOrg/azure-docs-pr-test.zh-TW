---
title: "BizTalk 服務中的儀表板、監視、調整、設定和混合式連接 | Microsoft Docs"
description: "深入了解控制項，以及監視 BizTalk 服務的傳統入口網站索引標籤的效能：儀表板、監視、級別、設定和混合式連接。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 4ec88d9a681a5692b31f7e3990d1c153296b18ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="0e96c-104">檢閱儀表板、監視器、調整、設定和混合式連線索引標籤</span><span class="sxs-lookup"><span data-stu-id="0e96c-104">Review the Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="0e96c-105">在您建立 BizTalk 服務和部署應用程式之後，您可以變更某些 BizTalk 服務設定和監視應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="0e96c-105">After you create your BizTalk Service and deploy your application, you can change some of the BizTalk Service settings and monitor the application performance.</span></span> 

<span data-ttu-id="0e96c-106">當您開啟 Azure 傳統入口網站時，會自動進入 [ **所有項目** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0e96c-106">When you open the Azure classic portal, you are automatically placed at the **ALL ITEMS** tab.</span></span> <span data-ttu-id="0e96c-107">若要檢視 BizTalk 服務，請在 [所有項目] 索引標籤中選取 BizTalk 服務，或選取 [BIZTALK 服務] 索引標籤，然後選取您的 BizTalk 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="0e96c-107">To view your BizTalk Service, select your BizTalk Service in the **ALL ITEMS** tab or select the **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="0e96c-108">這樣會開啟新視窗並顯示下列索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0e96c-108">This opens a new window with the following tabs.</span></span> <span data-ttu-id="0e96c-109">本主題說明這些索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0e96c-109">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="0e96c-110">快速入門 (</span><span class="sxs-lookup"><span data-stu-id="0e96c-110">Quickstart (</span></span>![快速入門][Quickstart]<span data-ttu-id="0e96c-112">)</span><span class="sxs-lookup"><span data-stu-id="0e96c-112">)</span></span>
<span data-ttu-id="0e96c-113">部分 BizTalk 服務版本可能並未提供下列所有選項。</span><span class="sxs-lookup"><span data-stu-id="0e96c-113">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="0e96c-114"><strong>取得工具</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-114"><strong>Get the tools</strong></span></span></td>
        <td><span data-ttu-id="0e96c-115">下載 BizTalk 服務 SDK，將 Visual Studio 專案範本安裝到內部部署開發電腦上。</span><span class="sxs-lookup"><span data-stu-id="0e96c-115">Download the BizTalk Services SDK to install the Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="0e96c-116">這些範本會建立 <strong>BizTalk 服務</strong> (橋接)，以及可部署至 BizTalk 服務的 <strong>BizTalk 服務成品</strong> (轉換) Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="0e96c-116">These templates create the <strong>BizTalk Services</strong> (bridge) and the <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed to your BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="0e96c-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">如何開始使用 Azure BizTalk 服務 SDK</a> 和<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">安裝 Azure BizTalk 服務 SDK</a> 列出開始進行的步驟。</span><span class="sxs-lookup"><span data-stu-id="0e96c-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using the Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing the Azure BizTalk Services SDK</a> lists the steps to get started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="0e96c-118"><strong>建立夥伴協議</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-118"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="0e96c-119">開啟裝載於 Azure 的 Azure BizTalk 服務入口網站，以加入夥伴並建立 X12、AS2 和 EDIFACT EDI 協議。</span><span class="sxs-lookup"><span data-stu-id="0e96c-119">Opens the Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="0e96c-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">在 BizTalk 服務入口網站上設定 EDI 訊息的元件</a>列出開始進行的步驟。</span><span class="sxs-lookup"><span data-stu-id="0e96c-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists the steps to get started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="0e96c-121"><strong>深入了解 BizTalk 服務</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-121"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="0e96c-122">前往<a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">學習中心</a>以深入了解 Azure BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="0e96c-122">Go to the <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> to learn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="0e96c-123">在底部的工作列上，您可以：</span><span class="sxs-lookup"><span data-stu-id="0e96c-123">In the task bar at the bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="0e96c-124"><strong>管理</strong>應用程式部署</span><span class="sxs-lookup"><span data-stu-id="0e96c-124"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="0e96c-125">開啟 Azure BizTalk 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="0e96c-125">Opens the Azure BizTalk Services portal.</span></span> <span data-ttu-id="0e96c-126">BizTalk 服務入口網站是 EDI 組態的入口，包括加入夥伴及建立 X12、AS2 和 EDIFACT 協議。</span><span class="sxs-lookup"><span data-stu-id="0e96c-126">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="0e96c-127">這與 [快速入門]<strong></strong> 索引標籤上的 [建立夥伴合約]<strong></strong> 相同。</span><span class="sxs-lookup"><span data-stu-id="0e96c-127">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="0e96c-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">在 BizTalk 服務入口網站上設定 EDI 訊息的元件</a>提供 BizTalk 服務入口網站的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0e96c-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="0e96c-129">存取控制命名空間的<strong>連線資訊</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-129"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="0e96c-130">選取 [連線資訊] 時會顯示 [存取控制命名空間]、[預設核發者] 和 [預設金鑰]。</span><span class="sxs-lookup"><span data-stu-id="0e96c-130">When you select Connection Information, then the Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="0e96c-131">您可以複製這些值。</span><span class="sxs-lookup"><span data-stu-id="0e96c-131">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="0e96c-132">您也可以開啟存取控制入口網站。</span><span class="sxs-lookup"><span data-stu-id="0e96c-132">You can also open the Access Control Portal.</span></span> <span data-ttu-id="0e96c-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">建立存取控制命名空間</a>提供了存取控制入口網站的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0e96c-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="0e96c-134">儲存體帳戶內的<strong>同步金鑰</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-134"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="0e96c-135">當建立儲存體帳戶時，會自動建立主要金鑰和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-135">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="0e96c-136">這些加密金鑰可控制儲存體帳戶的存取。</span><span class="sxs-lookup"><span data-stu-id="0e96c-136">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="0e96c-137">BizTalk 服務會自動使用主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-137">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="0e96c-138"><strong>同步金鑰</strong>可讓使用者在主要金鑰和次要金鑰之間切換，而不會中斷 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="0e96c-138"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="0e96c-139">例如，您希望 BizTalk 服務對儲存體帳戶使用新的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-139">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="0e96c-140">作法：</span><span class="sxs-lookup"><span data-stu-id="0e96c-140">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="0e96c-141">選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="0e96c-141">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="0e96c-142">選取次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-142">Select the Secondary Key.</span></span> <span data-ttu-id="0e96c-143">這時，BizTalk 服務就會開始使用次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-143">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="0e96c-144">在 Azure 傳統入口網站中，選取您的儲存體帳戶並重新產生主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-144">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="0e96c-145">記住，BizTalk 服務現在使用次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-145">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="0e96c-146">選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="0e96c-146">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="0e96c-147">現在，選取主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-147">Now, select the Primary Key.</span></span> <span data-ttu-id="0e96c-148">這是您重新產生的新主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-148">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="0e96c-149">在 Azure 傳統入口網站中，選取您的儲存體帳戶並重新產生次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-149">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="0e96c-150">此程序稱為「換用金鑰」。</span><span class="sxs-lookup"><span data-stu-id="0e96c-150">This process is called "rollover keys".</span></span> <span data-ttu-id="0e96c-151">目的是讓使用者在主要金鑰和次要金鑰之間切換，而不會中斷 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="0e96c-151">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="0e96c-152"><strong>刪除</strong>應用程式</span><span class="sxs-lookup"><span data-stu-id="0e96c-152"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="0e96c-153">選取 [刪除] 會移除 BizTalk 服務及已部署到它的所有項目。</span><span class="sxs-lookup"><span data-stu-id="0e96c-153">When you select Delete, your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="0e96c-154">儀表板</span><span class="sxs-lookup"><span data-stu-id="0e96c-154">Dashboard</span></span>
<span data-ttu-id="0e96c-155">部分 BizTalk 服務版本可能並未提供下列所有選項。</span><span class="sxs-lookup"><span data-stu-id="0e96c-155">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="0e96c-156">選取 BizTalk 服務名稱時會顯示 [儀表板] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0e96c-156">When you select your BizTalk Service name, the Dashboard tab is displayed.</span></span> <span data-ttu-id="0e96c-157">在 [儀表板] 裡，您可以：</span><span class="sxs-lookup"><span data-stu-id="0e96c-157">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a><span data-ttu-id="0e96c-158">使用量概觀：顯示已使用的混合式連線數量</span><span class="sxs-lookup"><span data-stu-id="0e96c-158">Usage Overview: Shows the number of used Hybrid Connections</span></span>
<span data-ttu-id="0e96c-159">資料使用量 (單位為 GB) 也會顯示。</span><span class="sxs-lookup"><span data-stu-id="0e96c-159">Also displays the data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="0e96c-160">度量圖：顯示固定的效能度量清單。</span><span class="sxs-lookup"><span data-stu-id="0e96c-160">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="0e96c-161">這些度量提供 BizTalk 服務健全狀況的即時值。</span><span class="sxs-lookup"><span data-stu-id="0e96c-161">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="0e96c-162">您也可以選擇 [相對] 值或 [絕對] 值，以及圖表上顯示的度量時間範圍 [間隔]。</span><span class="sxs-lookup"><span data-stu-id="0e96c-162">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed in the graph.</span></span> 

<span data-ttu-id="0e96c-163">如需這些效能度量的說明，請移至本主題的 [可用的度量](#Metrics) 。</span><span class="sxs-lookup"><span data-stu-id="0e96c-163">For a description of these performance metrics, go to [Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="0e96c-164">快速瀏覽：列出 BizTalk 服務屬性</span><span class="sxs-lookup"><span data-stu-id="0e96c-164">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="0e96c-165"><strong>更新追蹤資料庫認證</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-165"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="0e96c-166">變更用於登入追蹤資料庫的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0e96c-166">Changes the user name and password used to log into the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-167"><strong>更新 SSL 憑證</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-167"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="0e96c-168">可更新 BizTalk 服務來使用不同的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="0e96c-168">Can update the BizTalk Service to use a different SSL certificate.</span></span> <span data-ttu-id="0e96c-169">在您<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">建立 BizTalk 服務</a>時，自我簽署 SSL 憑證會自動建立。</span><span class="sxs-lookup"><span data-stu-id="0e96c-169">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create the BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-170"><strong>下載憑證</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-170"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="0e96c-171">您可以將 BizTalk 服務所使用的 SSL 憑證下載到本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="0e96c-171">You can download the SSL certificate used by your BizTalk Service to a local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-172"><strong>狀態</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-172"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="0e96c-173">顯示 BizTalk 服務的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="0e96c-173">Displays the current status of your BizTalk Service.</span></span> <span data-ttu-id="0e96c-174">請參閱 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk 服務：服務狀態圖</a> (英文)。</span><span class="sxs-lookup"><span data-stu-id="0e96c-174">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-175"><strong>服務 URL</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-175"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="0e96c-176">您 BizTalk 服務的 URL。</span><span class="sxs-lookup"><span data-stu-id="0e96c-176">The URL for your BizTalk Service.</span></span> <span data-ttu-id="0e96c-177">這與建立您的 BizTalk 服務時所輸入的<strong>網域 URL</strong> 相同。</span><span class="sxs-lookup"><span data-stu-id="0e96c-177">This is the same as the <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-178"><strong>公用虛擬 IP (VIP) 位址</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-178"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="0e96c-179">此 IP 位址指派給您的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="0e96c-179">The IP address assigned to your BizTalk Service.</span></span> <span data-ttu-id="0e96c-180">它用於所有輸入端點，也是輸出流量的來源位址。</span><span class="sxs-lookup"><span data-stu-id="0e96c-180">It is used for all input endpoints and is the source address for outbound traffic.</span></span> <span data-ttu-id="0e96c-181">此 IP 位址屬於您建立的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="0e96c-181">This IP address belongs to your BizTalk Service as long as it is created.</span></span> <span data-ttu-id="0e96c-182">若您刪除 BizTalk 服務，則此 IP 位址會指派給其他 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="0e96c-182">If you delete the BizTalk Service, the IP address is assigned to another BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-183"><strong>ACS 命名空間</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-183"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="0e96c-184">向 BizTalk 服務驗證。</span><span class="sxs-lookup"><span data-stu-id="0e96c-184">Authenticates with the BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-185"><strong>版本</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-185"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="0e96c-186">列出建立 BizTalk 服務時所輸入的版本。</span><span class="sxs-lookup"><span data-stu-id="0e96c-186">Lists the Edition entered when the BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-187"><strong>位置</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-187"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="0e96c-188">顯示裝載 BizTalk 服務的地理區域。</span><span class="sxs-lookup"><span data-stu-id="0e96c-188">Displays the geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-189"><strong>建立時間</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-189"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="0e96c-190">顯示建立 BizTalk 服務的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="0e96c-190">Displays the date and time the BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-191"><strong>追蹤資料庫</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-191"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="0e96c-192">儲存 BizTalk 服務所使用之追蹤資料表的 Azure SQL Database 名稱。</span><span class="sxs-lookup"><span data-stu-id="0e96c-192">The Azure SQL Database name that stores the tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="0e96c-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">需求說明</a>提供追蹤資料庫的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e96c-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-194"><strong>監視/封存儲存體</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-194"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="0e96c-195">儲存 BizTalk 服務之監視輸出的 Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="0e96c-195">The Azure Storage account name that stores the monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="0e96c-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">需求說明</a>提供儲存體帳戶的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e96c-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-197"><strong>訂用帳戶名稱</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-197"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="0e96c-198">列出裝載 BizTalk 服務的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="0e96c-198">Lists the subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="0e96c-199">訂用帳戶掌管對 Azure 傳統入口網站的存取權。</span><span class="sxs-lookup"><span data-stu-id="0e96c-199">The subscription governs access to the Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-200"><strong>訂用帳戶識別碼</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-200"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="0e96c-201">建立訂用帳戶時，會自動產生訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="0e96c-201">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="0e96c-202">使用 REST API 時，您可能需要輸入訂閱識別碼。</span><span class="sxs-lookup"><span data-stu-id="0e96c-202">When using REST APIs, you may need to enter the Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="0e96c-203">[BizTalk 服務：使用 Azure 傳統入口網站進行佈建](http://go.microsoft.com/fwlink/p/?LinkID=302280) 列出建立 BizTalk 服務的步驟。</span><span class="sxs-lookup"><span data-stu-id="0e96c-203">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists the steps to create a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a><span data-ttu-id="0e96c-204">工作列中的管理、連線資訊、同步金鑰和刪除：</span><span class="sxs-lookup"><span data-stu-id="0e96c-204">Manage, Connection Information, Sync Keys, and Delete in the task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="0e96c-205"><strong>管理</strong>應用程式部署</span><span class="sxs-lookup"><span data-stu-id="0e96c-205"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="0e96c-206">開啟 Azure BizTalk 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="0e96c-206">Opens the Azure BizTalk Services Portal.</span></span> <span data-ttu-id="0e96c-207">BizTalk 服務入口網站是 EDI 組態的入口，包括加入夥伴及建立 X12、AS2 和 EDIFACT 協議。</span><span class="sxs-lookup"><span data-stu-id="0e96c-207">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="0e96c-208">這與 [快速入門]<strong></strong> 索引標籤上的 [建立夥伴合約]<strong></strong> 相同。</span><span class="sxs-lookup"><span data-stu-id="0e96c-208">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="0e96c-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">在 BizTalk 服務入口網站上設定 EDI 訊息的元件</a>提供 BizTalk 服務入口網站的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0e96c-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-210">存取控制命名空間的<strong>連線資訊</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-210"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="0e96c-211">顯示 Access Control 命名空間、預設核發者和預設金鑰值，供您複製。</span><span class="sxs-lookup"><span data-stu-id="0e96c-211">Displays the Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="0e96c-212">您也可以開啟存取控制入口網站。</span><span class="sxs-lookup"><span data-stu-id="0e96c-212">You can also open the Access Control Portal.</span></span> <span data-ttu-id="0e96c-213">此存取控制入口網站的功用就與使用左側導覽窗格中的 [Active Directory] 選項一樣。</span><span class="sxs-lookup"><span data-stu-id="0e96c-213">This Access Control Portal is the same as using the Active Directory option in the left navigation pane.</span></span>
<br/><br/><span data-ttu-id="0e96c-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">管理您的 ACS 命名空間</a>提供存取控制入口網站的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0e96c-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-215">儲存體帳戶內的<strong>同步金鑰</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-215"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="0e96c-216">當建立儲存體帳戶時，會自動建立主要金鑰和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-216">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="0e96c-217">這些加密金鑰可控制儲存體帳戶的存取。</span><span class="sxs-lookup"><span data-stu-id="0e96c-217">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="0e96c-218">BizTalk 服務會自動使用主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-218">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="0e96c-219"><strong>同步金鑰</strong>可讓使用者在主要金鑰和次要金鑰之間切換，而不會中斷 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="0e96c-219"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="0e96c-220">例如，您希望 BizTalk 服務對儲存體帳戶使用新的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-220">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="0e96c-221">作法：</span><span class="sxs-lookup"><span data-stu-id="0e96c-221">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="0e96c-222">選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="0e96c-222">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="0e96c-223">選取次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-223">Select the Secondary Key.</span></span> <span data-ttu-id="0e96c-224">這時，BizTalk 服務就會開始使用次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-224">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="0e96c-225">在 Azure 傳統入口網站中，選取您的儲存體帳戶並重新產生主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-225">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="0e96c-226">記住，BizTalk 服務現在使用次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-226">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="0e96c-227">選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="0e96c-227">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="0e96c-228">現在，選取主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-228">Now, select the Primary Key.</span></span> <span data-ttu-id="0e96c-229">這是您重新產生的新主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-229">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="0e96c-230">在 Azure 傳統入口網站中，選取您的儲存體帳戶並重新產生次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e96c-230">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="0e96c-231">此程序稱為「換用金鑰」。</span><span class="sxs-lookup"><span data-stu-id="0e96c-231">This process is called "rollover keys".</span></span> <span data-ttu-id="0e96c-232">目的是讓使用者在主要金鑰和次要金鑰之間切換，而不會中斷 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="0e96c-232">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="0e96c-233"><strong>刪除</strong>應用程式</span><span class="sxs-lookup"><span data-stu-id="0e96c-233"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="0e96c-234">已移除 BizTalk 服務與部署至服務的所有項目。</span><span class="sxs-lookup"><span data-stu-id="0e96c-234">Your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="0e96c-235">監視</span><span class="sxs-lookup"><span data-stu-id="0e96c-235">Monitor</span></span>
<span data-ttu-id="0e96c-236">不適用於免費版本。</span><span class="sxs-lookup"><span data-stu-id="0e96c-236">Does not apply to the Free Edition.</span></span>

<span data-ttu-id="0e96c-237">選取 BizTalk 服務名稱後，即可使用 [監視] 索引標籤且會顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="0e96c-237">When you select your BizTalk Service name, the Monitor tab is available and displays the following:</span></span>

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a><span data-ttu-id="0e96c-238">度量圖：顯示已選取的效能度量</span><span class="sxs-lookup"><span data-stu-id="0e96c-238">Metric Graph: Displays the selected performance metrics</span></span>
<span data-ttu-id="0e96c-239">這些度量提供 BizTalk 服務健全狀況的即時值。</span><span class="sxs-lookup"><span data-stu-id="0e96c-239">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="0e96c-240">請選擇要顯示哪些效能度量。</span><span class="sxs-lookup"><span data-stu-id="0e96c-240">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="0e96c-241">一次最多同時顯示六個效能度量。</span><span class="sxs-lookup"><span data-stu-id="0e96c-241">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="0e96c-242">您也可以選擇 [相對] 值或 [絕對] 值，以及所顯示的度量時間範圍 [間隔]。</span><span class="sxs-lookup"><span data-stu-id="0e96c-242">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed.</span></span> 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a><span data-ttu-id="0e96c-243">在圖表中移除或顯示度量：</span><span class="sxs-lookup"><span data-stu-id="0e96c-243">To remove or display metrics in the graph:</span></span>
1. <span data-ttu-id="0e96c-244">選取 [ **監視** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0e96c-244">Select the **Monitor** tab.</span></span>
2. <span data-ttu-id="0e96c-245">選取工作列中的 [加入度量]：</span><span class="sxs-lookup"><span data-stu-id="0e96c-245">Select **Add Metrics** in the task bar:</span></span>  
   <span data-ttu-id="0e96c-246">![選取 [新增度量]][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="0e96c-246">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="0e96c-247">勾選您要顯示的效能度量。</span><span class="sxs-lookup"><span data-stu-id="0e96c-247">Check the performance metrics you want to display.</span></span>
4. <span data-ttu-id="0e96c-248">選取勾選記號以回到 [ **監視** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0e96c-248">Select the checkmark to return to the **Monitor** tab.</span></span>
5. <span data-ttu-id="0e96c-249">選取度量旁邊的圓圈，將該度量的值顯示在圖表中。</span><span class="sxs-lookup"><span data-stu-id="0e96c-249">Select the circle next to the metric to display that metric's value in the graph.</span></span>  
   
    <span data-ttu-id="0e96c-250">例如，[CPU 使用率] 度量呈現灰色，其輸出不會出現在圖表中：</span><span class="sxs-lookup"><span data-stu-id="0e96c-250">For example, the **CPU Usage** metric is grayed out; its output is not displayed in the graph:</span></span>  
   <span data-ttu-id="0e96c-251">![CPU 使用量度量呈現灰色][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="0e96c-251">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="0e96c-252">選取灰色的圓圈以啟用 [CPU 使用率] 度量，將其輸出顯示在圖表中：</span><span class="sxs-lookup"><span data-stu-id="0e96c-252">Select the grayed out circle to enable the **CPU Usage** metric to display its output in the graph:</span></span>  
   <span data-ttu-id="0e96c-253">![CPU 使用量度量已啟用][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="0e96c-253">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="0e96c-254">若要從顯示圖表和清單中移除度量，請選取工作列中的 [ **移除度量** ]。</span><span class="sxs-lookup"><span data-stu-id="0e96c-254">To remove a metric from the display graph and the list, select **Delete Metric** in the task bar.</span></span> <span data-ttu-id="0e96c-255">若要將度量加回到清單中，請選取工作列的 [加入度量]，勾選度量，然後選取勾選記號以回到 [監視] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0e96c-255">To add the metric back to the list, select **Add Metrics** in the task bar, check the metric, and select the checkmark to return to the **Monitor** tab.</span></span> <span data-ttu-id="0e96c-256">選取灰色圓圈以啟用度量。</span><span class="sxs-lookup"><span data-stu-id="0e96c-256">Select the grayed out circle to enable the metric.</span></span>

## <span data-ttu-id="0e96c-257"><a name="Metrics"></a>可用的度量</span><span class="sxs-lookup"><span data-stu-id="0e96c-257"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="0e96c-258">以下是可用的效能計數器/度量：</span><span class="sxs-lookup"><span data-stu-id="0e96c-258">The following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="0e96c-259"><strong>往返延遲</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-259"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="0e96c-260">顯示從收到訊息起，到 BizTalk 服務跨所有橋接器完全處理完為止，處理訊息所花費的平均時間，以毫秒為單位 (ms)。</span><span class="sxs-lookup"><span data-stu-id="0e96c-260">Displays the average time taken in milliseconds (ms) to process a message from the time the message is received until the message is fully processed by the BizTalk Service across all bridges.</span></span> <span data-ttu-id="0e96c-261">只會計算成功處理的訊息。</span><span class="sxs-lookup"><span data-stu-id="0e96c-261">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="0e96c-262">發生下列事件時會建立時間戳記：</span><span class="sxs-lookup"><span data-stu-id="0e96c-262">When the following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="0e96c-263">訊息進入閘道</span><span class="sxs-lookup"><span data-stu-id="0e96c-263">Message enters the gateway</span></span></li>
<li><span data-ttu-id="0e96c-264">訊息已路由傳送至目的地</span><span class="sxs-lookup"><span data-stu-id="0e96c-264">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="0e96c-265">收到目的地回應</span><span class="sxs-lookup"><span data-stu-id="0e96c-265">Destination response is received</span></span></li>
<li><span data-ttu-id="0e96c-266">目的地認可回應已傳送至閘道</span><span class="sxs-lookup"><span data-stu-id="0e96c-266">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="0e96c-267">此度量顯示下列計算的結果：</span><span class="sxs-lookup"><span data-stu-id="0e96c-267">This metric shows the result of the following calculation:</span></span>
<br/><br/>
<span data-ttu-id="0e96c-268">[目的地認可回應已傳送至閘道] - [訊息進入閘道]</span><span class="sxs-lookup"><span data-stu-id="0e96c-268">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-269"><strong>來源失敗</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-269"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="0e96c-270">顯示從來源端點提取訊息時，BizTalk 服務無法處理的訊息總數。</span><span class="sxs-lookup"><span data-stu-id="0e96c-270">Displays the total number of messages that failed by the BizTalk Service when pulling messages from the source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-271"><strong>CPU 使用率</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-271"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="0e96c-272">列出所有角色執行個體的平均 % 處理器時間。</span><span class="sxs-lookup"><span data-stu-id="0e96c-272">Lists the average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-273"><strong>處理延遲</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-273"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="0e96c-274">顯示 BizTalk 服務跨所有橋接器來處理某個訊息所花費的平均時間，不包括在目的地所花費的時間，以毫秒為單位 (ms)。</span><span class="sxs-lookup"><span data-stu-id="0e96c-274">Displays the average time taken In milliseconds (ms) to process a message by the BizTalk Service across all bridges, excluding the time spent in destinations.</span></span> <span data-ttu-id="0e96c-275">只會計算成功處理的訊息。</span><span class="sxs-lookup"><span data-stu-id="0e96c-275">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="0e96c-276">發生下列每一個事件時會建立時間戳記：</span><span class="sxs-lookup"><span data-stu-id="0e96c-276">When each of the following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="0e96c-277">訊息進入閘道</span><span class="sxs-lookup"><span data-stu-id="0e96c-277">Message enters the gateway</span></span></li>
<li><span data-ttu-id="0e96c-278">訊息已路由傳送至目的地</span><span class="sxs-lookup"><span data-stu-id="0e96c-278">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="0e96c-279">收到目的地回應</span><span class="sxs-lookup"><span data-stu-id="0e96c-279">Destination response is received</span></span></li>
<li><span data-ttu-id="0e96c-280">目的地認可回應已傳送至閘道</span><span class="sxs-lookup"><span data-stu-id="0e96c-280">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/><span data-ttu-id="0e96c-281">此度量顯示下列計算的結果：</span><span class="sxs-lookup"><span data-stu-id="0e96c-281">This metric shows the result of the following calculation:</span></span><br/><br/>
<span data-ttu-id="0e96c-282">[目的地認可回應已傳送至閘道] - [訊息進入閘道] - [收到目的地回應] + [訊息已路由傳送至目的地]</span><span class="sxs-lookup"><span data-stu-id="0e96c-282">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway] - [Destination response is received] + [Message is routed to the destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-283"><strong>處理時失敗</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-283"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="0e96c-284">顯示在一段時間內，BizTalk 服務跨所有橋接器處理訊息時失敗的訊息總數。</span><span class="sxs-lookup"><span data-stu-id="0e96c-284">Displays the total number of messages that failed during processing by the BizTalk Service across all the bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-285"><strong>已傳送的訊息</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-285"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="0e96c-286">顯示在一段時間內，BizTalk 服務跨所有橋接器傳送的訊息總數。</span><span class="sxs-lookup"><span data-stu-id="0e96c-286">Displays the total number of messages sent by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="0e96c-287">當管線傳送的訊息抵達路由目的地時，此度量會遞增。</span><span class="sxs-lookup"><span data-stu-id="0e96c-287">This metric is incremented when a message sent from a pipeline reaches the route destination.</span></span> <span data-ttu-id="0e96c-288">此度量不表示已成功處理訊息。</span><span class="sxs-lookup"><span data-stu-id="0e96c-288">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="0e96c-289">在要求回覆案例中，當路由目的地將收到認可傳回至管線時，此度量會遞增。</span><span class="sxs-lookup"><span data-stu-id="0e96c-289">In a Request-Reply scenario, the metric is incremented when the route destination sends a receipt acknowledgement back to the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-290"><strong>已接收的訊息</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-290"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="0e96c-291">顯示在一段時間內，BizTalk 服務跨所有橋接器接收的訊息總數。</span><span class="sxs-lookup"><span data-stu-id="0e96c-291">Displays the total number of messages received by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="0e96c-292">當管線收到新的訊息時，此度量會遞增。</span><span class="sxs-lookup"><span data-stu-id="0e96c-292">This metric is incremented when a new message is received by the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-293"><strong>處理中的訊息</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-293"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="0e96c-294">顯示 BizTalk 服務在一段時間內正在處理的訊息總數。</span><span class="sxs-lookup"><span data-stu-id="0e96c-294">Displays the total number of messages currently being processed by the BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0e96c-295"><strong>已處理的訊息</strong></span><span class="sxs-lookup"><span data-stu-id="0e96c-295"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="0e96c-296">顯示在一段時間內，BizTalk 服務跨所有橋接器成功處理的訊息總數。</span><span class="sxs-lookup"><span data-stu-id="0e96c-296">Displays the total number of messages successfully processed by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="0e96c-297">當訊息由管線成功接收且成功地路由傳送至目的地時，此度量會遞增。</span><span class="sxs-lookup"><span data-stu-id="0e96c-297">This metric is incremented when a message is successfully received by the pipeline and successfully routed to the destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="0e96c-298">調整</span><span class="sxs-lookup"><span data-stu-id="0e96c-298">Scale</span></span>
<span data-ttu-id="0e96c-299">在 [調整] 索引標籤中，您可以增加或減少 BizTalk 服務使用的單位數。</span><span class="sxs-lookup"><span data-stu-id="0e96c-299">In the Scale tab, you can add or subtract the number of units used by your BizTalk Service.</span></span> <span data-ttu-id="0e96c-300">依預設已設定一個單位。</span><span class="sxs-lookup"><span data-stu-id="0e96c-300">By default, there is one Unit configured.</span></span> <span data-ttu-id="0e96c-301">您可以將更多單位加入至 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="0e96c-301">Additional Units can be added to scale your BizTalk Service.</span></span> <span data-ttu-id="0e96c-302">增加規模時，也會增量輸送量。</span><span class="sxs-lookup"><span data-stu-id="0e96c-302">When you increase the scale, you are increasing throughput.</span></span> <span data-ttu-id="0e96c-303">資源數量也會增加，包括部署的橋接器、協議、LOB 連接和處理能力。</span><span class="sxs-lookup"><span data-stu-id="0e96c-303">The amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="0e96c-304">例如，將規模從 1 單位增加為 2 單位。</span><span class="sxs-lookup"><span data-stu-id="0e96c-304">For example, you increase the scale from 1 Unit to 2 Units.</span></span> <span data-ttu-id="0e96c-305">在此情況下，您可以部署兩倍的橋接器、兩倍的協議、兩倍的 LOB 連接，以及兩倍的處理能力。</span><span class="sxs-lookup"><span data-stu-id="0e96c-305">In this situation, you can deploy double the number of bridges, double the agreements, double the LOB connections, and double the processing power.</span></span>

<span data-ttu-id="0e96c-306">有些 BizTalk 版本不提供調整選項。</span><span class="sxs-lookup"><span data-stu-id="0e96c-306">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="0e96c-307">在此情況下，只允許一個單位。</span><span class="sxs-lookup"><span data-stu-id="0e96c-307">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="0e96c-308">若要判斷您的版本可調整的單位數，請參閱「 [BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md)」。</span><span class="sxs-lookup"><span data-stu-id="0e96c-308">To determine how many units your edition can be scaled, refer to [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="0e96c-309">增加單位數可能會影響定價。</span><span class="sxs-lookup"><span data-stu-id="0e96c-309">Increasing the number of units may impact pricing.</span></span> <span data-ttu-id="0e96c-310">如果增加單位，選取 **[儲存]** 會出現訊息，告知您計費是否受影響。</span><span class="sxs-lookup"><span data-stu-id="0e96c-310">If you increase the Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="0e96c-311">您可以選擇繼續。</span><span class="sxs-lookup"><span data-stu-id="0e96c-311">You then choose to continue.</span></span> <span data-ttu-id="0e96c-312">增加單位數時，BizTalk 服務狀態會從 [作用中] 變更為 [正在更新]。</span><span class="sxs-lookup"><span data-stu-id="0e96c-312">When you increase the number of Units, the BizTalk Service status changes from Active to Updating.</span></span> <span data-ttu-id="0e96c-313">在更新狀態下，BizTalk 服務會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="0e96c-313">In the Updating state, your BizTalk Service continues to run.</span></span>

<span data-ttu-id="0e96c-314">[BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md) 定義「單位」。</span><span class="sxs-lookup"><span data-stu-id="0e96c-314">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="0e96c-315">設定</span><span class="sxs-lookup"><span data-stu-id="0e96c-315">Configure</span></span>
<span data-ttu-id="0e96c-316">不適用於混合式連線。</span><span class="sxs-lookup"><span data-stu-id="0e96c-316">Does not apply to Hybrid Connections.</span></span>

<span data-ttu-id="0e96c-317">將 [備份狀態] 設為 [無] 或 [自動]。</span><span class="sxs-lookup"><span data-stu-id="0e96c-317">Sets the Backup Status to None or Automatic.</span></span> <span data-ttu-id="0e96c-318">設為 [無] 時不會自動建立備份。</span><span class="sxs-lookup"><span data-stu-id="0e96c-318">When set to None, no backups are automatically created.</span></span> <span data-ttu-id="0e96c-319">設為 [自動] 時需設定備份位置、備份頻率和備份檔案的保留時間。</span><span class="sxs-lookup"><span data-stu-id="0e96c-319">When set to Automatic, you configure the backup location, the frequency of the backup, and how long to keep the backup files.</span></span> 

<span data-ttu-id="0e96c-320">[BizTalk 服務：備份與還原](biztalk-backup-restore.md) 提供詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e96c-320">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides the details.</span></span> 

## <span data-ttu-id="0e96c-321"><a name="HybridConnections"></a>混合式連線</span><span class="sxs-lookup"><span data-stu-id="0e96c-321"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="0e96c-322">混合式連線可將 Azure 應用程式 (例如 Azure App Service 中的 Web Apps 或 Mobile Apps) 連線到使用靜態 TCP 連接埠的內部部署資源，例如 SQL Server、MySQL、HTTP Web API 及大部分的自訂 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="0e96c-322">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, to an on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="0e96c-323">您可以在 Azure 傳統入口網站內的 BizTalk 服務中管理混合式連接。</span><span class="sxs-lookup"><span data-stu-id="0e96c-323">Hybrid Connections are managed in  BizTalk Services in the Azure classic portal.</span></span>

<span data-ttu-id="0e96c-324">若要在 Azure App Service 中建立混合式連線，請參閱[在 Azure App Service 中使用混合式連線存取內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0e96c-324">To create Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="0e96c-325">若要在 Azure BizTalk 服務內建立或管理混合式連線，請參閱 [混合式連線](integration-hybrid-connection-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0e96c-325">To create or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="0e96c-326">下一步</span><span class="sxs-lookup"><span data-stu-id="0e96c-326">Next</span></span>
<span data-ttu-id="0e96c-327">現在，您已熟悉不同的索引標籤，您可以繼續深入了解 Azure BizTalk 服務的功能：</span><span class="sxs-lookup"><span data-stu-id="0e96c-327">Now that you're familiar with the different tabs, you can learn more about the Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="0e96c-328">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="0e96c-328">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="0e96c-329">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="0e96c-329">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="0e96c-330">BizTalk 服務：備份與還原</span><span class="sxs-lookup"><span data-stu-id="0e96c-330">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="0e96c-331">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0e96c-331">See Also</span></span>
* [<span data-ttu-id="0e96c-332">混合式連線</span><span class="sxs-lookup"><span data-stu-id="0e96c-332">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="0e96c-333">BizTalk 服務：開發人員、基本、標準和高級版本圖表</span><span class="sxs-lookup"><span data-stu-id="0e96c-333">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="0e96c-334">BizTalk 服務：使用 Azure 傳統入口網站進行佈建</span><span class="sxs-lookup"><span data-stu-id="0e96c-334">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="0e96c-335">BizTalk 服務：BizTalk 服務狀態圖</span><span class="sxs-lookup"><span data-stu-id="0e96c-335">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="0e96c-336">如何開始使用 Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="0e96c-336">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

