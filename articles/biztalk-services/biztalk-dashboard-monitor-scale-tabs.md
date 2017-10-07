---
title: "aaaDashboard 監視器、 小數位數、 設定和 BizTalk 服務的混合式連線 |Microsoft 文件"
description: "深入了解 hello 控制項和監視效能 hello 傳統入口網站 索引標籤上的 BizTalk 服務： 儀表板、 監視器、 小數位數、 設定和混合式連線。 MABS，WABS"
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
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="3fa01-104">檢閱 hello 儀表板、 監視器、 小數位數、 設定和混合式連接索引標籤</span><span class="sxs-lookup"><span data-stu-id="3fa01-104">Review hello Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="3fa01-105">建立 BizTalk 服務和部署您的應用程式之後，您可以變更某些 hello BizTalk 服務設定和監視 hello 應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="3fa01-105">After you create your BizTalk Service and deploy your application, you can change some of hello BizTalk Service settings and monitor hello application performance.</span></span> 

<span data-ttu-id="3fa01-106">當您開啟 hello Azure 傳統入口網站時，系統會自動引導您前往 hello**所有項目** 索引標籤 tooview BizTalk 服務中，選取您的 BizTalk 服務中 hello**所有項目** 索引標籤或選取 hello **BIZTALK 服務**索引標籤上;，然後選取 BizTalk 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa01-106">When you open hello Azure classic portal, you are automatically placed at hello **ALL ITEMS** tab. tooview your BizTalk Service, select your BizTalk Service in hello **ALL ITEMS** tab or select hello **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="3fa01-107">這會開啟新視窗以 hello 下列索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3fa01-107">This opens a new window with hello following tabs.</span></span> <span data-ttu-id="3fa01-108">本主題說明這些索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3fa01-108">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="3fa01-109">快速入門 (</span><span class="sxs-lookup"><span data-stu-id="3fa01-109">Quickstart (</span></span>![快速入門][Quickstart]<span data-ttu-id="3fa01-111">)</span><span class="sxs-lookup"><span data-stu-id="3fa01-111">)</span></span>
<span data-ttu-id="3fa01-112">根據 hello BizTalk 服務版本，可能無法使用所有列出的選項。</span><span class="sxs-lookup"><span data-stu-id="3fa01-112">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="3fa01-113"><strong>取得 hello 工具</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-113"><strong>Get hello tools</strong></span></span></td>
        <td><span data-ttu-id="3fa01-114">下載 hello BizTalk 服務 SDK tooinstall hello Visual Studio 專案範本在內部部署開發電腦上。</span><span class="sxs-lookup"><span data-stu-id="3fa01-114">Download hello BizTalk Services SDK tooinstall hello Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="3fa01-115">這些範本會建立 hello <strong>BizTalk 服務</strong>(bridge) 和 hello <strong>BizTalk 服務成品</strong>部署的 tooyour BizTalk 服務的 （轉換） Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="3fa01-115">These templates create hello <strong>BizTalk Services</strong> (bridge) and hello <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed tooyour BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="3fa01-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">開始使用我該如何 hello Azure BizTalk 服務 SDK</a>和<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">安裝 hello Azure BizTalk 服務 SDK</a>清單 hello 步驟 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="3fa01-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using hello Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing hello Azure BizTalk Services SDK</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fa01-117"><strong>建立夥伴協議</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-117"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="3fa01-118">開啟 hello Azure BizTalk 服務入口網站裝載於 Azure，讓您加入夥伴和建立 X12、 AS2 和 EDIFACT EDI 協議。</span><span class="sxs-lookup"><span data-stu-id="3fa01-118">Opens hello Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="3fa01-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">設定元件的 BizTalk 服務入口網站上的 EDI 傳訊</a>清單 hello 步驟 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="3fa01-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="3fa01-120"><strong>深入了解 BizTalk 服務</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-120"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="3fa01-121">移 toohello<a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">學習中心</a>toolearn 更多關於 Azure BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-121">Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="3fa01-122">在底部 hello hello 工作列，您可以：</span><span class="sxs-lookup"><span data-stu-id="3fa01-122">In hello task bar at hello bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="3fa01-123"><strong>管理</strong>應用程式部署</span><span class="sxs-lookup"><span data-stu-id="3fa01-123"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="3fa01-124">開啟 hello Azure BizTalk 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="3fa01-124">Opens hello Azure BizTalk Services portal.</span></span> <span data-ttu-id="3fa01-125">hello BizTalk 服務入口網站是 hello 進入 tooEDI 的設定，包括加入夥伴和建立 X12、 AS2 和 EDIFACT 協議。</span><span class="sxs-lookup"><span data-stu-id="3fa01-125">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="3fa01-126">這是與相同 hello<strong>建立夥伴協議</strong>上 hello<strong>快速入門</strong> 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3fa01-126">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="3fa01-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">設定元件的 BizTalk 服務入口網站上的 EDI 傳訊</a>hello BizTalk 服務入口網站上提供的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fa01-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="3fa01-128"><strong>連接資訊</strong>的 hello 存取控制命名空間</span><span class="sxs-lookup"><span data-stu-id="3fa01-128"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="3fa01-129">當您選取的連接資訊時，然後 hello 存取控制命名空間、 預設簽發者，並且顯示預設索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-129">When you select Connection Information, then hello Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="3fa01-130">您可以複製這些值。</span><span class="sxs-lookup"><span data-stu-id="3fa01-130">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="3fa01-131">您也可以開啟 hello 存取控制入口網站。</span><span class="sxs-lookup"><span data-stu-id="3fa01-131">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="3fa01-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">建立存取控制命名空間</a>hello 存取控制入口網站上提供的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fa01-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="3fa01-133"><strong>同步索引鍵</strong>hello 儲存體帳戶中</span><span class="sxs-lookup"><span data-stu-id="3fa01-133"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="3fa01-134">當建立儲存體帳戶時，會自動建立主要金鑰和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fa01-134">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="3fa01-135">這些加密金鑰控制存取 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fa01-135">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="3fa01-136">您的 BizTalk 服務會自動使用 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-136">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="3fa01-137"><strong>同步索引鍵</strong>啟用使用者 tooswitch hello 主索引鍵與 hello 次要索引鍵之間，而不會中斷 hello BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-137"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="3fa01-138">例如，您會想 hello BizTalk 服務 toouse hello 儲存體帳戶的新主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-138">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="3fa01-139">toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="3fa01-139">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="3fa01-140">選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="3fa01-140">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="3fa01-141">選取 hello 次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fa01-141">Select hello Secondary Key.</span></span> <span data-ttu-id="3fa01-142">當您這樣做時，hello BizTalk 服務使用啟動 hello 次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fa01-142">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="3fa01-143">在 hello Azure 傳統入口網站，選取儲存體帳戶並重新產生 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-143">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="3fa01-144">請記住，您的 BizTalk 服務使用 hello 次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fa01-144">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="3fa01-145">選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="3fa01-145">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="3fa01-146">現在，選取 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-146">Now, select hello Primary Key.</span></span> <span data-ttu-id="3fa01-147">這是新 hello 您重新產生的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-147">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="3fa01-148">在 hello Azure 傳統入口網站，選取儲存體帳戶，然後重新產生次要金鑰 hello。</span><span class="sxs-lookup"><span data-stu-id="3fa01-148">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="3fa01-149">此程序稱為「換用金鑰」。</span><span class="sxs-lookup"><span data-stu-id="3fa01-149">This process is called "rollover keys".</span></span> <span data-ttu-id="3fa01-150">hello 目的是 tooenable 使用者 tooswitch hello 主索引鍵與 hello 次要索引鍵之間，而不會中斷 hello BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-150">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="3fa01-151"><strong>刪除</strong>應用程式</span><span class="sxs-lookup"><span data-stu-id="3fa01-151"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="3fa01-152">當您選取 刪除 BizTalk 服務和所有部署的項目 tooit 會移除。</span><span class="sxs-lookup"><span data-stu-id="3fa01-152">When you select Delete, your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="3fa01-153">儀表板</span><span class="sxs-lookup"><span data-stu-id="3fa01-153">Dashboard</span></span>
<span data-ttu-id="3fa01-154">根據 hello BizTalk 服務版本，可能無法使用所有列出的選項。</span><span class="sxs-lookup"><span data-stu-id="3fa01-154">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="3fa01-155">當您選取 BizTalk 服務名稱時，則會顯示 hello 儀表板 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3fa01-155">When you select your BizTalk Service name, hello Dashboard tab is displayed.</span></span> <span data-ttu-id="3fa01-156">在 [儀表板] 裡，您可以：</span><span class="sxs-lookup"><span data-stu-id="3fa01-156">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a><span data-ttu-id="3fa01-157">使用量概觀： 會顯示 hello 使用混合式連接的數目</span><span class="sxs-lookup"><span data-stu-id="3fa01-157">Usage Overview: Shows hello number of used Hybrid Connections</span></span>
<span data-ttu-id="3fa01-158">以 gb 為單位，也會顯示 hello 資料使用量。</span><span class="sxs-lookup"><span data-stu-id="3fa01-158">Also displays hello data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="3fa01-159">度量圖：顯示固定的效能度量清單。</span><span class="sxs-lookup"><span data-stu-id="3fa01-159">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="3fa01-160">這些度量會提供有關 hello hello BizTalk 服務健全狀況的即時值。</span><span class="sxs-lookup"><span data-stu-id="3fa01-160">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="3fa01-161">您也可以選擇 hello**相對**或**絕對**值和 hello 時間範圍**間隔**的 hello 圖形中顯示的 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="3fa01-161">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed in hello graph.</span></span> 

<span data-ttu-id="3fa01-162">如需這些效能度量的說明，請移至太[可用的度量](#Metrics)本主題中。</span><span class="sxs-lookup"><span data-stu-id="3fa01-162">For a description of these performance metrics, go too[Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="3fa01-163">快速瀏覽：列出 BizTalk 服務屬性</span><span class="sxs-lookup"><span data-stu-id="3fa01-163">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="3fa01-164"><strong>更新追蹤資料庫認證</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-164"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="3fa01-165">變更 hello 使用者名稱和密碼來 toolog hello 追蹤資料庫。</span><span class="sxs-lookup"><span data-stu-id="3fa01-165">Changes hello user name and password used toolog into hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-166"><strong>更新 SSL 憑證</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-166"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="3fa01-167">可以更新 hello BizTalk 服務 toouse 不同的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="3fa01-167">Can update hello BizTalk Service toouse a different SSL certificate.</span></span> <span data-ttu-id="3fa01-168">自我簽署的 SSL 憑證時，會自動建立您<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">建立 BizTalk 服務的 hello</a>。</span><span class="sxs-lookup"><span data-stu-id="3fa01-168">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create hello BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-169"><strong>下載憑證</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-169"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="3fa01-170">您可以下載 BizTalk 服務 tooa 本機電腦所使用的 hello SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="3fa01-170">You can download hello SSL certificate used by your BizTalk Service tooa local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-171"><strong>狀態</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-171"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="3fa01-172">顯示 hello BizTalk 服務的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="3fa01-172">Displays hello current status of your BizTalk Service.</span></span> <span data-ttu-id="3fa01-173">請參閱 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk 服務：服務狀態圖</a> (英文)。</span><span class="sxs-lookup"><span data-stu-id="3fa01-173">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-174"><strong>服務 URL</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-174"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="3fa01-175">您的 BizTalk 服務的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="3fa01-175">hello URL for your BizTalk Service.</span></span> <span data-ttu-id="3fa01-176">這是為 hello hello 相同<strong>網域 URL</strong>輸入建立 BizTalk 服務時。</span><span class="sxs-lookup"><span data-stu-id="3fa01-176">This is hello same as hello <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-177"><strong>公用虛擬 IP (VIP) 位址</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-177"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="3fa01-178">hello IP 位址指派 tooyour BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-178">hello IP address assigned tooyour BizTalk Service.</span></span> <span data-ttu-id="3fa01-179">它用於所有的輸入端點，而且是 hello 輸出流量的來源位址。</span><span class="sxs-lookup"><span data-stu-id="3fa01-179">It is used for all input endpoints and is hello source address for outbound traffic.</span></span> <span data-ttu-id="3fa01-180">此 IP 位址所屬 tooyour BizTalk 服務，只要它會建立。</span><span class="sxs-lookup"><span data-stu-id="3fa01-180">This IP address belongs tooyour BizTalk Service as long as it is created.</span></span> <span data-ttu-id="3fa01-181">如果您刪除 hello BizTalk 服務，hello IP 位址指派 tooanother BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-181">If you delete hello BizTalk Service, hello IP address is assigned tooanother BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-182"><strong>ACS 命名空間</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-182"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="3fa01-183">向 hello BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-183">Authenticates with hello BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-184"><strong>版本</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-184"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="3fa01-185">列出版本建立 hello BizTalk 服務時所輸入的 hello。</span><span class="sxs-lookup"><span data-stu-id="3fa01-185">Lists hello Edition entered when hello BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-186"><strong>位置</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-186"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="3fa01-187">顯示 hello 主控 BizTalk 服務的地理區域。</span><span class="sxs-lookup"><span data-stu-id="3fa01-187">Displays hello geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-188"><strong>建立時間</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-188"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="3fa01-189">建立 BizTalk 服務顯示 hello 日期和時間 hello。</span><span class="sxs-lookup"><span data-stu-id="3fa01-189">Displays hello date and time hello BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-190"><strong>追蹤資料庫</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-190"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="3fa01-191">儲存追蹤資料表，您的 BizTalk 服務所使用的 hello hello Azure SQL Database 名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa01-191">hello Azure SQL Database name that stores hello tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="3fa01-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">需求說明</a>提供 hello 追蹤資料庫的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fa01-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-193"><strong>監視/封存儲存體</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-193"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="3fa01-194">儲存監視 BizTalk 服務的輸出 hello hello Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="3fa01-194">hello Azure Storage account name that stores hello monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="3fa01-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">需求說明</a>提供 hello 儲存體帳戶的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fa01-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-196"><strong>訂用帳戶名稱</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-196"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="3fa01-197">列出裝載您的 BizTalk 服務的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fa01-197">Lists hello subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="3fa01-198">hello 訂閱控管存取 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="3fa01-198">hello subscription governs access toohello Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-199"><strong>訂用帳戶識別碼</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-199"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="3fa01-200">建立訂用帳戶時，會自動產生訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="3fa01-200">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="3fa01-201">當使用 REST Api，您可能需要 tooenter hello 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="3fa01-201">When using REST APIs, you may need tooenter hello Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="3fa01-202">[BizTalk 服務： 佈建使用 Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=302280)清單 hello 步驟 toocreate BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-202">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists hello steps toocreate a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a><span data-ttu-id="3fa01-203">管理連接資訊，同步金鑰及 hello 工作列中刪除：</span><span class="sxs-lookup"><span data-stu-id="3fa01-203">Manage, Connection Information, Sync Keys, and Delete in hello task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="3fa01-204"><strong>管理</strong>應用程式部署</span><span class="sxs-lookup"><span data-stu-id="3fa01-204"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="3fa01-205">開啟 hello Azure BizTalk 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="3fa01-205">Opens hello Azure BizTalk Services Portal.</span></span> <span data-ttu-id="3fa01-206">hello BizTalk 服務入口網站是 hello 進入 tooEDI 的設定，包括加入夥伴和建立 X12、 AS2 和 EDIFACT 協議。</span><span class="sxs-lookup"><span data-stu-id="3fa01-206">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="3fa01-207">這是與相同 hello<strong>建立夥伴協議</strong>上 hello<strong>快速入門</strong> 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3fa01-207">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="3fa01-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">設定元件的 BizTalk 服務入口網站上的 EDI 傳訊</a>hello BizTalk 服務入口網站上提供的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fa01-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-209"><strong>連接資訊</strong>的 hello 存取控制命名空間</span><span class="sxs-lookup"><span data-stu-id="3fa01-209"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="3fa01-210">顯示 hello 存取控制命名空間、 預設簽發者和預設金鑰值。這可以複製。</span><span class="sxs-lookup"><span data-stu-id="3fa01-210">Displays hello Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="3fa01-211">您也可以開啟 hello 存取控制入口網站。</span><span class="sxs-lookup"><span data-stu-id="3fa01-211">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="3fa01-212">此存取控制入口網站是 hello 與 hello 左側的導覽窗格中使用 hello Active Directory 選項相同。</span><span class="sxs-lookup"><span data-stu-id="3fa01-212">This Access Control Portal is hello same as using hello Active Directory option in hello left navigation pane.</span></span>
<br/><br/><span data-ttu-id="3fa01-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">管理您的 ACS 命名空間</a>hello 存取控制入口網站上提供的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fa01-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-214"><strong>同步索引鍵</strong>hello 儲存體帳戶中</span><span class="sxs-lookup"><span data-stu-id="3fa01-214"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="3fa01-215">當建立儲存體帳戶時，會自動建立主要金鑰和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fa01-215">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="3fa01-216">這些加密金鑰控制存取 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fa01-216">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="3fa01-217">您的 BizTalk 服務會自動使用 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-217">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="3fa01-218"><strong>同步索引鍵</strong>啟用使用者 tooswitch hello 主索引鍵與 hello 次要索引鍵之間，而不會中斷 hello BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-218"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="3fa01-219">例如，您會想 hello BizTalk 服務 toouse hello 儲存體帳戶的新主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-219">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="3fa01-220">toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="3fa01-220">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="3fa01-221">選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="3fa01-221">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="3fa01-222">選取 hello 次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fa01-222">Select hello Secondary Key.</span></span> <span data-ttu-id="3fa01-223">當您這樣做時，hello BizTalk 服務使用啟動 hello 次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fa01-223">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="3fa01-224">在 hello Azure 傳統入口網站，選取儲存體帳戶並重新產生 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-224">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="3fa01-225">請記住，您的 BizTalk 服務使用 hello 次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fa01-225">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="3fa01-226">選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="3fa01-226">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="3fa01-227">現在，選取 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-227">Now, select hello Primary Key.</span></span> <span data-ttu-id="3fa01-228">這是新 hello 您重新產生的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3fa01-228">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="3fa01-229">在 hello Azure 傳統入口網站，選取儲存體帳戶，然後重新產生次要金鑰 hello。</span><span class="sxs-lookup"><span data-stu-id="3fa01-229">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="3fa01-230">此程序稱為「換用金鑰」。</span><span class="sxs-lookup"><span data-stu-id="3fa01-230">This process is called "rollover keys".</span></span> <span data-ttu-id="3fa01-231">hello 目的是 tooenable 使用者 tooswitch hello 主索引鍵與 hello 次要索引鍵之間，而不會中斷 hello BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-231">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="3fa01-232"><strong>刪除</strong>應用程式</span><span class="sxs-lookup"><span data-stu-id="3fa01-232"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="3fa01-233">您的 BizTalk 服務和所有部署的項目 tooit 被移除。</span><span class="sxs-lookup"><span data-stu-id="3fa01-233">Your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="3fa01-234">監視</span><span class="sxs-lookup"><span data-stu-id="3fa01-234">Monitor</span></span>
<span data-ttu-id="3fa01-235">不會套用 toohello 免費版本。</span><span class="sxs-lookup"><span data-stu-id="3fa01-235">Does not apply toohello Free Edition.</span></span>

<span data-ttu-id="3fa01-236">當您選取 BizTalk 服務名稱時，hello 監視 索引標籤使用，並顯示 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="3fa01-236">When you select your BizTalk Service name, hello Monitor tab is available and displays hello following:</span></span>

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a><span data-ttu-id="3fa01-237">顯示 hello 選取效能度量的度量的圖表：</span><span class="sxs-lookup"><span data-stu-id="3fa01-237">Metric Graph: Displays hello selected performance metrics</span></span>
<span data-ttu-id="3fa01-238">這些度量會提供有關 hello hello BizTalk 服務健全狀況的即時值。</span><span class="sxs-lookup"><span data-stu-id="3fa01-238">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="3fa01-239">請選擇要顯示哪些效能度量。</span><span class="sxs-lookup"><span data-stu-id="3fa01-239">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="3fa01-240">一次最多同時顯示六個效能度量。</span><span class="sxs-lookup"><span data-stu-id="3fa01-240">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="3fa01-241">您也可以選擇 hello**相對**或**絕對**值和 hello 時間範圍**間隔**的 hello 度量資訊會顯示。</span><span class="sxs-lookup"><span data-stu-id="3fa01-241">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed.</span></span> 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a><span data-ttu-id="3fa01-242">hello 圖形中 tooremove 或顯示度量：</span><span class="sxs-lookup"><span data-stu-id="3fa01-242">tooremove or display metrics in hello graph:</span></span>
1. <span data-ttu-id="3fa01-243">選取 hello**監視器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3fa01-243">Select hello **Monitor** tab.</span></span>
2. <span data-ttu-id="3fa01-244">選取**加入度量**hello 工作列中：</span><span class="sxs-lookup"><span data-stu-id="3fa01-244">Select **Add Metrics** in hello task bar:</span></span>  
   <span data-ttu-id="3fa01-245">![選取 [新增度量]][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="3fa01-245">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="3fa01-246">請檢查您想要 toodisplay hello 效能度量。</span><span class="sxs-lookup"><span data-stu-id="3fa01-246">Check hello performance metrics you want toodisplay.</span></span>
4. <span data-ttu-id="3fa01-247">選取 hello 核取記號 tooreturn toohello**監視器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3fa01-247">Select hello checkmark tooreturn toohello **Monitor** tab.</span></span>
5. <span data-ttu-id="3fa01-248">選取該度量值 hello 圓形下一步 toohello 度量 toodisplay hello 圖形中。</span><span class="sxs-lookup"><span data-stu-id="3fa01-248">Select hello circle next toohello metric toodisplay that metric's value in hello graph.</span></span>  
   
    <span data-ttu-id="3fa01-249">例如，hello **CPU 使用量**度量呈現灰色，則其輸出不會顯示在 hello 圖形：</span><span class="sxs-lookup"><span data-stu-id="3fa01-249">For example, hello **CPU Usage** metric is grayed out; its output is not displayed in hello graph:</span></span>  
   <span data-ttu-id="3fa01-250">![CPU 使用量度量呈現灰色][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="3fa01-250">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="3fa01-251">選取 hello 灰色圓形 tooenable hello **CPU 使用量**度量 toodisplay hello 圖形中的其輸出：</span><span class="sxs-lookup"><span data-stu-id="3fa01-251">Select hello grayed out circle tooenable hello **CPU Usage** metric toodisplay its output in hello graph:</span></span>  
   <span data-ttu-id="3fa01-252">![CPU 使用量度量已啟用][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="3fa01-252">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="3fa01-253">tooremove hello 顯示圖形與 hello 清單中，度量選取**刪除度量**hello 工作列中。</span><span class="sxs-lookup"><span data-stu-id="3fa01-253">tooremove a metric from hello display graph and hello list, select **Delete Metric** in hello task bar.</span></span> <span data-ttu-id="3fa01-254">tooadd hello 度量後 toohello 清單中，選取**加入度量**在 hello 工作列上，核取 hello 度量，並選取 hello 核取記號 tooreturn toohello**監視器** 索引標籤。選取 hello 圓形 tooenable hello 度量呈現灰色。</span><span class="sxs-lookup"><span data-stu-id="3fa01-254">tooadd hello metric back toohello list, select **Add Metrics** in hello task bar, check hello metric, and select hello checkmark tooreturn toohello **Monitor** tab. Select hello grayed out circle tooenable hello metric.</span></span>

## <span data-ttu-id="3fa01-255"><a name="Metrics"></a>可用的度量</span><span class="sxs-lookup"><span data-stu-id="3fa01-255"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="3fa01-256">下列效能計數器度量的 hello 可用：</span><span class="sxs-lookup"><span data-stu-id="3fa01-256">hello following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="3fa01-257"><strong>往返延遲</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-257"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="3fa01-258">顯示 hello 的平均使用時間 （毫秒） （毫秒） tooprocess 跨所有橋接器 hello BizTalk 服務所完全處理 hello 訊息之前收到來自 hello 時間 hello 訊息的訊息。</span><span class="sxs-lookup"><span data-stu-id="3fa01-258">Displays hello average time taken in milliseconds (ms) tooprocess a message from hello time hello message is received until hello message is fully processed by hello BizTalk Service across all bridges.</span></span> <span data-ttu-id="3fa01-259">只會計算成功處理的訊息。</span><span class="sxs-lookup"><span data-stu-id="3fa01-259">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="3fa01-260">Hello 下列事件發生時，會建立時間戳記：</span><span class="sxs-lookup"><span data-stu-id="3fa01-260">When hello following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="3fa01-261">訊息進入 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="3fa01-261">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="3fa01-262">訊息是路由的 toohello 目的地</span><span class="sxs-lookup"><span data-stu-id="3fa01-262">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="3fa01-263">收到目的地回應</span><span class="sxs-lookup"><span data-stu-id="3fa01-263">Destination response is received</span></span></li>
<li><span data-ttu-id="3fa01-264">目的地通知傳送回應 toohello 閘道</span><span class="sxs-lookup"><span data-stu-id="3fa01-264">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="3fa01-265">此標準會顯示 hello 結果 hello 下列計算：</span><span class="sxs-lookup"><span data-stu-id="3fa01-265">This metric shows hello result of hello following calculation:</span></span>
<br/><br/>
<span data-ttu-id="3fa01-266">[目的地通知傳送回應 toohello gateway]-[訊息進入 hello 閘道]</span><span class="sxs-lookup"><span data-stu-id="3fa01-266">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-267"><strong>來源失敗</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-267"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="3fa01-268">顯示 hello 總數失敗的訊息所 hello 提取從 hello 來源端點的訊息時，BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-268">Displays hello total number of messages that failed by hello BizTalk Service when pulling messages from hello source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-269"><strong>CPU 使用率</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-269"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="3fa01-270">列出 hello 平均處理器時間百分比的所有角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="3fa01-270">Lists hello average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-271"><strong>處理延遲</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-271"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="3fa01-272">顯示 hello 中跨所有橋接器，但不包括 hello 時間 hello BizTalk 服務的訊息目的地所花費的毫秒 (ms) tooprocess 所花費的平均時間。</span><span class="sxs-lookup"><span data-stu-id="3fa01-272">Displays hello average time taken In milliseconds (ms) tooprocess a message by hello BizTalk Service across all bridges, excluding hello time spent in destinations.</span></span> <span data-ttu-id="3fa01-273">只會計算成功處理的訊息。</span><span class="sxs-lookup"><span data-stu-id="3fa01-273">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="3fa01-274">每個 hello 下列事件發生時，會建立時間戳記：</span><span class="sxs-lookup"><span data-stu-id="3fa01-274">When each of hello following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="3fa01-275">訊息進入 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="3fa01-275">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="3fa01-276">訊息是路由的 toohello 目的地</span><span class="sxs-lookup"><span data-stu-id="3fa01-276">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="3fa01-277">收到目的地回應</span><span class="sxs-lookup"><span data-stu-id="3fa01-277">Destination response is received</span></span></li>
<li><span data-ttu-id="3fa01-278">目的地通知傳送回應 toohello 閘道</span><span class="sxs-lookup"><span data-stu-id="3fa01-278">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/><span data-ttu-id="3fa01-279">此標準會顯示 hello 結果 hello 下列計算：</span><span class="sxs-lookup"><span data-stu-id="3fa01-279">This metric shows hello result of hello following calculation:</span></span><br/><br/>
<span data-ttu-id="3fa01-280">[目的地通知傳送回應 toohello gateway]-[訊息進入 hello 閘道]-[目的地未收到回應時] + [訊息是路由的 toohello 目的地]</span><span class="sxs-lookup"><span data-stu-id="3fa01-280">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway] - [Destination response is received] + [Message is routed toohello destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-281"><strong>處理時失敗</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-281"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="3fa01-282">顯示 hello 總數無法在處理期間由跨所有 hello 橋接器 hello BizTalk 服務的時間間隔內的訊息。</span><span class="sxs-lookup"><span data-stu-id="3fa01-282">Displays hello total number of messages that failed during processing by hello BizTalk Service across all hello bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-283"><strong>已傳送的訊息</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-283"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="3fa01-284">顯示 hello 跨所有橋接器 hello BizTalk 服務所傳送的時間間隔內的訊息總數。</span><span class="sxs-lookup"><span data-stu-id="3fa01-284">Displays hello total number of messages sent by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="3fa01-285">此標準會在從管線所傳送的訊息到達 hello 路由目的地時累加。</span><span class="sxs-lookup"><span data-stu-id="3fa01-285">This metric is incremented when a message sent from a pipeline reaches hello route destination.</span></span> <span data-ttu-id="3fa01-286">此度量不表示已成功處理訊息。</span><span class="sxs-lookup"><span data-stu-id="3fa01-286">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="3fa01-287">在要求-回覆案例中，當 hello 路由目的地傳送回條認可後 toohello 管線時，就會遞增 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="3fa01-287">In a Request-Reply scenario, hello metric is incremented when hello route destination sends a receipt acknowledgement back toohello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-288"><strong>已接收的訊息</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-288"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="3fa01-289">顯示 hello 跨所有橋接器 hello BizTalk 服務的時間間隔內接收的訊息總數。</span><span class="sxs-lookup"><span data-stu-id="3fa01-289">Displays hello total number of messages received by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="3fa01-290">Hello 管線收到一封新郵件時，就會遞增此標準。</span><span class="sxs-lookup"><span data-stu-id="3fa01-290">This metric is incremented when a new message is received by hello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-291"><strong>處理中的訊息</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-291"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="3fa01-292">顯示 hello 目前正在處理的 hello BizTalk 服務的時間間隔內的訊息總數。</span><span class="sxs-lookup"><span data-stu-id="3fa01-292">Displays hello total number of messages currently being processed by hello BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3fa01-293"><strong>已處理的訊息</strong></span><span class="sxs-lookup"><span data-stu-id="3fa01-293"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="3fa01-294">顯示 hello 順利處理的時間間隔內跨所有橋接器 hello BizTalk 服務的訊息總數。</span><span class="sxs-lookup"><span data-stu-id="3fa01-294">Displays hello total number of messages successfully processed by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="3fa01-295">訊息已成功收到 hello 管線 」 和 「 已成功路由的 toohello 目的地時，就會遞增此標準。</span><span class="sxs-lookup"><span data-stu-id="3fa01-295">This metric is incremented when a message is successfully received by hello pipeline and successfully routed toohello destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="3fa01-296">調整</span><span class="sxs-lookup"><span data-stu-id="3fa01-296">Scale</span></span>
<span data-ttu-id="3fa01-297">Hello 調整 索引標籤中，您可以加入或減去 hello BizTalk 服務所使用的單位數目。</span><span class="sxs-lookup"><span data-stu-id="3fa01-297">In hello Scale tab, you can add or subtract hello number of units used by your BizTalk Service.</span></span> <span data-ttu-id="3fa01-298">依預設已設定一個單位。</span><span class="sxs-lookup"><span data-stu-id="3fa01-298">By default, there is one Unit configured.</span></span> <span data-ttu-id="3fa01-299">額外的單位可以加入 tooscale BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="3fa01-299">Additional Units can be added tooscale your BizTalk Service.</span></span> <span data-ttu-id="3fa01-300">當您增加 hello 標尺時，您正在提高輸送量。</span><span class="sxs-lookup"><span data-stu-id="3fa01-300">When you increase hello scale, you are increasing throughput.</span></span> <span data-ttu-id="3fa01-301">資源的 hello 數量也會增加，包括已部署的橋接器、 合約、 LOB 連線和處理能力。</span><span class="sxs-lookup"><span data-stu-id="3fa01-301">hello amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="3fa01-302">例如，您會增加 hello 小數位數，從 1 單位 too2 單位。</span><span class="sxs-lookup"><span data-stu-id="3fa01-302">For example, you increase hello scale from 1 Unit too2 Units.</span></span> <span data-ttu-id="3fa01-303">在此情況下，您可以部署雙 hello 橋接器、 double hello 協議，double hello LOB 連接數目，以及雙 hello 的處理能力。</span><span class="sxs-lookup"><span data-stu-id="3fa01-303">In this situation, you can deploy double hello number of bridges, double hello agreements, double hello LOB connections, and double hello processing power.</span></span>

<span data-ttu-id="3fa01-304">有些 BizTalk 版本不提供調整選項。</span><span class="sxs-lookup"><span data-stu-id="3fa01-304">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="3fa01-305">在此情況下，只允許一個單位。</span><span class="sxs-lookup"><span data-stu-id="3fa01-305">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="3fa01-306">toodetermine 多少單位可以調整您的版本，參閱太[BizTalk 服務： 版本圖表](biztalk-editions-feature-chart.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa01-306">toodetermine how many units your edition can be scaled, refer too[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="3fa01-307">增加 hello 單位數目可能會影響定價。</span><span class="sxs-lookup"><span data-stu-id="3fa01-307">Increasing hello number of units may impact pricing.</span></span> <span data-ttu-id="3fa01-308">如果您增加 hello 單位，則選取**儲存**會顯示訊息，告訴您計費會受到影響。</span><span class="sxs-lookup"><span data-stu-id="3fa01-308">If you increase hello Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="3fa01-309">然後，您可以選擇在 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="3fa01-309">You then choose toocontinue.</span></span> <span data-ttu-id="3fa01-310">當您增加 hello 單位數目時，hello BizTalk 服務的狀態會從作用中 tooUpdating 變更。</span><span class="sxs-lookup"><span data-stu-id="3fa01-310">When you increase hello number of Units, hello BizTalk Service status changes from Active tooUpdating.</span></span> <span data-ttu-id="3fa01-311">在 hello 更新狀態，您的 BizTalk 服務會繼續 toorun。</span><span class="sxs-lookup"><span data-stu-id="3fa01-311">In hello Updating state, your BizTalk Service continues toorun.</span></span>

<span data-ttu-id="3fa01-312">[BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md) 定義「單位」。</span><span class="sxs-lookup"><span data-stu-id="3fa01-312">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="3fa01-313">設定</span><span class="sxs-lookup"><span data-stu-id="3fa01-313">Configure</span></span>
<span data-ttu-id="3fa01-314">不適用 tooHybrid 連線。</span><span class="sxs-lookup"><span data-stu-id="3fa01-314">Does not apply tooHybrid Connections.</span></span>

<span data-ttu-id="3fa01-315">Hello 備份狀態 tooNone] 或 [自動設定。</span><span class="sxs-lookup"><span data-stu-id="3fa01-315">Sets hello Backup Status tooNone or Automatic.</span></span> <span data-ttu-id="3fa01-316">當設定 tooNone，備份會自動建立。</span><span class="sxs-lookup"><span data-stu-id="3fa01-316">When set tooNone, no backups are automatically created.</span></span> <span data-ttu-id="3fa01-317">當設定 tooAutomatic，您可以設定 hello 備份位置、 hello 頻率 hello 備份，以及多久 tookeep hello 備份檔案。</span><span class="sxs-lookup"><span data-stu-id="3fa01-317">When set tooAutomatic, you configure hello backup location, hello frequency of hello backup, and how long tookeep hello backup files.</span></span> 

<span data-ttu-id="3fa01-318">[BizTalk 服務： 備份和還原](biztalk-backup-restore.md)提供 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3fa01-318">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides hello details.</span></span> 

## <span data-ttu-id="3fa01-319"><a name="HybridConnections"></a>混合式連線</span><span class="sxs-lookup"><span data-stu-id="3fa01-319"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="3fa01-320">混合式連接連接 Azure 應用程式，例如 Web 應用程式或行動應用程式在 Azure 應用程式服務中，使用靜態 TCP 連接埠，例如 SQL Server、 MySQL、 HTTP 的 Web Api 和最自訂的 Web 服務的 tooan 在內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="3fa01-320">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, tooan on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="3fa01-321">BizTalk 服務的 hello Azure 傳統入口網站中管理混合式連接。</span><span class="sxs-lookup"><span data-stu-id="3fa01-321">Hybrid Connections are managed in  BizTalk Services in hello Azure classic portal.</span></span>

<span data-ttu-id="3fa01-322">toocreate 混合式連線，在 Azure 應用程式服務，請參閱[存取內部部署混合式連線使用 Azure App Service 中的資源](../app-service-web/web-sites-hybrid-connection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa01-322">toocreate Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="3fa01-323">toocreate 或管理在 Azure BizTalk 服務混合式連線，請參閱[混合式連線](integration-hybrid-connection-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa01-323">toocreate or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="3fa01-324">下一步</span><span class="sxs-lookup"><span data-stu-id="3fa01-324">Next</span></span>
<span data-ttu-id="3fa01-325">既然您已熟悉 hello 不同索引標籤，您可以深入了解 hello Azure BizTalk 服務的功能：</span><span class="sxs-lookup"><span data-stu-id="3fa01-325">Now that you're familiar with hello different tabs, you can learn more about hello Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="3fa01-326">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="3fa01-326">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="3fa01-327">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="3fa01-327">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="3fa01-328">BizTalk 服務：備份與還原</span><span class="sxs-lookup"><span data-stu-id="3fa01-328">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="3fa01-329">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3fa01-329">See Also</span></span>
* [<span data-ttu-id="3fa01-330">混合式連線</span><span class="sxs-lookup"><span data-stu-id="3fa01-330">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="3fa01-331">BizTalk 服務：開發人員、基本、標準和高級版本圖表</span><span class="sxs-lookup"><span data-stu-id="3fa01-331">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="3fa01-332">BizTalk 服務：使用 Azure 傳統入口網站進行佈建</span><span class="sxs-lookup"><span data-stu-id="3fa01-332">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="3fa01-333">BizTalk 服務：BizTalk 服務狀態圖</span><span class="sxs-lookup"><span data-stu-id="3fa01-333">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="3fa01-334">開始使用我要如何 hello Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="3fa01-334">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

