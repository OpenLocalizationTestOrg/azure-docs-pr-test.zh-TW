---
title: "在 Azure 入口網站中建立 Azure BizTalk 服務 | Microsoft Docs"
description: "了解如何在 Azure 入口網站中佈建或建立 BizTalk 服務；MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: eca77b4a82eb67e1755717bb4429f8d450a64dc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-biztalk-services-using-the-azure-portal"></a><span data-ttu-id="d5f45-103">使用 Azure 入口網站建立 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="d5f45-103">Create BizTalk Services using the Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="d5f45-104">若要登入 Azure 入口網站，您需要 Azure 帳戶和 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5f45-104">To sign in to the Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="d5f45-105">如果沒有帳戶，您可在幾分鐘內建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5f45-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="d5f45-106">查看 [Azure 免費試用](http://go.microsoft.com/fwlink/p/?LinkID=239738)。</span><span class="sxs-lookup"><span data-stu-id="d5f45-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="d5f45-107"><a name="CreateService"></a>建立 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="d5f45-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="d5f45-108">視您所選的版本而定，部分 BizTalk 服務設定可能無法使用。</span><span class="sxs-lookup"><span data-stu-id="d5f45-108">Depending on the Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="d5f45-109">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="d5f45-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d5f45-110">在底端的導覽窗格中，選取 [新增]：</span><span class="sxs-lookup"><span data-stu-id="d5f45-110">In the bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="d5f45-111">![選取 [新增] 按鈕。][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="d5f45-111">![Select the New button][NEWButton]</span></span>
3. <span data-ttu-id="d5f45-112">選取 [應用程式服務]  >  [BIZTALK 服務]  >  [自訂建立]：</span><span class="sxs-lookup"><span data-stu-id="d5f45-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="d5f45-113">![選取 [BizTalk 服務] 與選取 [自訂建立]][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="d5f45-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="d5f45-114">輸入 BizTalk 服務設定：</span><span class="sxs-lookup"><span data-stu-id="d5f45-114">Enter the BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="d5f45-115"><strong>BizTalk 服務名稱</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="d5f45-116">您可以輸入任何名稱，但請使用特定的名稱。</span><span class="sxs-lookup"><span data-stu-id="d5f45-116">You can enter any name but be specific.</span></span> <span data-ttu-id="d5f45-117">部分範例包括：</span><span class="sxs-lookup"><span data-stu-id="d5f45-117">Some examples include:</span></span><br/><br/><span data-ttu-id="d5f45-118">
    <em>mycompany</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="d5f45-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="d5f45-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="d5f45-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="d5f45-120">
    <em>myapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="d5f45-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="d5f45-121">".biztalk.windows.net" 會自動新增至您輸入的名稱。</span><span class="sxs-lookup"><span data-stu-id="d5f45-121">".biztalk.windows.net" is automatically added to the name you enter.</span></span> <span data-ttu-id="d5f45-122">這會建立一個用來存取 BizTalk 服務的 URL，例如 <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>。</span><span class="sxs-lookup"><span data-stu-id="d5f45-122">This creates a URL that is used to access your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="d5f45-123"><strong>版本</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="d5f45-124">如果您是處於測試/開發階段，請選擇 [開發人員]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="d5f45-124">If you are in the testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="d5f45-125">如果您處於實際執行階段，請使用 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk 服務：版本圖表</a>來判定<strong>進階</strong>、<strong>標準</strong>，還是<strong>基本</strong>才是您的商業案例的正確選擇。</span><span class="sxs-lookup"><span data-stu-id="d5f45-125">If you are in the production phase, use the <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> to determine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is the correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="d5f45-126"><strong>區域</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="d5f45-127">選取地理區域來主控您的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="d5f45-127">Select the geographic region to host your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d5f45-128"><strong>網域 URL</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="d5f45-129"><strong>選擇性</strong>。</span><span class="sxs-lookup"><span data-stu-id="d5f45-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="d5f45-130">依預設，網域 URL 為 <em>YourBizTalkServiceName</em>.biztalk.windows.net。</span><span class="sxs-lookup"><span data-stu-id="d5f45-130">By default, the domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="d5f45-131">您也可輸入自訂網域。</span><span class="sxs-lookup"><span data-stu-id="d5f45-131">A custom domain can also be entered.</span></span> <span data-ttu-id="d5f45-132">比方說，如果您的網域為 <em>contoso</em>，則可以輸入：</span><span class="sxs-lookup"><span data-stu-id="d5f45-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="d5f45-133">
    <em>MyCompany</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d5f45-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="d5f45-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d5f45-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="d5f45-135">
    <em>MyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d5f45-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="d5f45-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d5f45-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="d5f45-137">選取下一個箭頭。</span><span class="sxs-lookup"><span data-stu-id="d5f45-137">Select the NEXT arrow.</span></span>
<span data-ttu-id="d5f45-138">5.</span><span class="sxs-lookup"><span data-stu-id="d5f45-138">5.</span></span> <span data-ttu-id="d5f45-139">輸入儲存體和資料庫設定：</span><span class="sxs-lookup"><span data-stu-id="d5f45-139">Enter the Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="d5f45-140"><strong>監視/封存儲存體帳戶</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="d5f45-141">選取現有的儲存體帳戶或建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5f45-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="d5f45-142">如果您建立新的儲存體帳戶，請輸入 [儲存體帳戶名稱]<strong></strong>。</span><span class="sxs-lookup"><span data-stu-id="d5f45-142">If you create a new Storage account, enter the <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d5f45-143"><strong>追蹤資料庫</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="d5f45-144">如果您使用現有的 Azure SQL Database，其他 BizTalk 服務將無法使用它。</span><span class="sxs-lookup"><span data-stu-id="d5f45-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="d5f45-145">您需要建立 Azure SQL Database 伺服器時輸入的登入名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d5f45-145">You need the login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="d5f45-146"><strong>秘訣</strong> 在與 BizTalk 服務相同的區域中，建立追蹤資料庫和監視/封存儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5f45-146"><strong>TIP</strong> Create the Tracking database and Monitoring/Archiving storage account in the same region as the BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="d5f45-147">選取下一個箭頭。</span><span class="sxs-lookup"><span data-stu-id="d5f45-147">Select the NEXT arrow.</span></span>
<span data-ttu-id="d5f45-148">6.</span><span class="sxs-lookup"><span data-stu-id="d5f45-148">6.</span></span> <span data-ttu-id="d5f45-149">輸入資料庫設定：</span><span class="sxs-lookup"><span data-stu-id="d5f45-149">Enter the Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="d5f45-150"><strong>名稱</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="d5f45-151">可在前一個畫面中選取 [建立新的 SQL 資料庫執行個體]<strong></strong> 時使用。</span><span class="sxs-lookup"><span data-stu-id="d5f45-151">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="d5f45-152">輸入 BizTalk 服務要使用的 SQL Database 名稱。</span><span class="sxs-lookup"><span data-stu-id="d5f45-152">Enter a SQL Database name to be used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d5f45-153"><strong>伺服器</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="d5f45-154">可在前一個畫面中選取 [建立新的 SQL 資料庫執行個體]<strong></strong> 時使用。</span><span class="sxs-lookup"><span data-stu-id="d5f45-154">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="d5f45-155">選取現有的 SQL Database 伺服器，或是建立全新的 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d5f45-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d5f45-156"><strong>伺服器登入名稱</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="d5f45-157">輸入登入使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d5f45-157">Enter the login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d5f45-158"><strong>伺服器登入密碼</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="d5f45-159">輸入登入密碼。</span><span class="sxs-lookup"><span data-stu-id="d5f45-159">Enter the login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d5f45-160"><strong>區域</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="d5f45-161">可在選取 [建立新的 SQL 資料庫執行個體]<strong></strong> 時使用。</span><span class="sxs-lookup"><span data-stu-id="d5f45-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="d5f45-162">選取地理區域來主控您的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="d5f45-162">Select the geographic region to host your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="d5f45-163">選取核取記號來完成精靈。</span><span class="sxs-lookup"><span data-stu-id="d5f45-163">Select the check mark to complete the wizard.</span></span> <span data-ttu-id="d5f45-164">進度圖示隨即顯示：</span><span class="sxs-lookup"><span data-stu-id="d5f45-164">The progress icon appears:</span></span>  
![進度圖示即會顯示][ProgressComplete]

<span data-ttu-id="d5f45-166">完成時，會建立 Azure BizTalk 服務，並備妥供應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="d5f45-166">When complete, the Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="d5f45-167">預設設定已夠用。</span><span class="sxs-lookup"><span data-stu-id="d5f45-167">The default settings are sufficient.</span></span> <span data-ttu-id="d5f45-168">如果想要變更預設設定，請在左導覽窗格中選取 [BIZTALK 服務]  ，然後選取您的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="d5f45-168">If you want to change the default settings, select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="d5f45-169">其他設定會顯示在 [[儀表板]、[監視器] 和 [調整]](biztalk-dashboard-monitor-scale-tabs.md) 索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="d5f45-169">Additional settings are displayed in the [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at the top.</span></span>

<span data-ttu-id="d5f45-170">有一些無法完成的作業，視 BizTalk 服務的狀態而定。</span><span class="sxs-lookup"><span data-stu-id="d5f45-170">Depending on the state of the BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="d5f45-171">如需這些作業的清單，請參閱 [BizTalk 服務狀態圖](biztalk-service-state-chart.md)。</span><span class="sxs-lookup"><span data-stu-id="d5f45-171">For a list of these operations, go to [BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="d5f45-172">佈建後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5f45-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="d5f45-173">在本機電腦上安裝憑證</span><span class="sxs-lookup"><span data-stu-id="d5f45-173">Install the certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="d5f45-174">新增實際執行備妥憑證</span><span class="sxs-lookup"><span data-stu-id="d5f45-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="d5f45-175">取得存取控制命名空間</span><span class="sxs-lookup"><span data-stu-id="d5f45-175">Get the Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="d5f45-176"><a name="InstallCert"></a>在本機電腦上安裝憑證</span><span class="sxs-lookup"><span data-stu-id="d5f45-176"><a name="InstallCert"></a>Install the certificate on a local computer</span></span>
<span data-ttu-id="d5f45-177">自我簽署憑證是 BizTalk 服務佈建的一部分，會在您訂閱 BizTalk 服務時建立並相關聯。</span><span class="sxs-lookup"><span data-stu-id="d5f45-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="d5f45-178">您必須下載此憑證，並將它安裝於您部署 BizTalk 服務應用程式、或向 BizTalk 服務端點傳送訊息的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d5f45-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages to a BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="d5f45-179">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="d5f45-179">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d5f45-180">選取左導覽窗格中的 [BIZTALK 服務]  ，然後選取您的 BizTalk 服務訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5f45-180">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="d5f45-181">選取 [ **儀表板** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d5f45-181">Select the **Dashboard** tab.</span></span>
4. <span data-ttu-id="d5f45-182">選取 [下載 SSL 憑證]：</span><span class="sxs-lookup"><span data-stu-id="d5f45-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="d5f45-183">![修改 SSL 憑證][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="d5f45-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="d5f45-184">按兩下此憑證，然後完成執行精靈，即可安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="d5f45-184">Double-click the certificate and run through the wizard to install the certificate.</span></span> <span data-ttu-id="d5f45-185">確定您已在 **受信任的根授權單位** 存放區之中安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="d5f45-185">Make sure you install the certificate under the **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="d5f45-186"><a name="AddCert"></a>新增實際執行備妥憑證</span><span class="sxs-lookup"><span data-stu-id="d5f45-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="d5f45-187">在建立 BizTalk 服務時自動建立的自我簽署憑證僅限用於開發環境。</span><span class="sxs-lookup"><span data-stu-id="d5f45-187">The self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="d5f45-188">若為生產案例，使用實際執行備妥憑證取代它。</span><span class="sxs-lookup"><span data-stu-id="d5f45-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="d5f45-189">在 [儀表板] 索引標籤上，選取 [更新 SSL 憑證]。</span><span class="sxs-lookup"><span data-stu-id="d5f45-189">On the **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="d5f45-190">瀏覽至包括 BizTalk 服務名稱的私人 SSL 憑證 (*CertificateName*.pfx)，輸入密碼，然後選取核取記號。</span><span class="sxs-lookup"><span data-stu-id="d5f45-190">Browse to your private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter the password, and then click the check mark.</span></span>

#### <span data-ttu-id="d5f45-191"><a name="ACS"></a>取得存取控制命名空間</span><span class="sxs-lookup"><span data-stu-id="d5f45-191"><a name="ACS"></a>Get the Access Control namespace</span></span>
1. <span data-ttu-id="d5f45-192">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="d5f45-192">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d5f45-193">在左導覽窗格中選取 [BIZTALK 服務]  ，然後選取您的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="d5f45-193">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="d5f45-194">在工作列中，選取 [連線資訊]：</span><span class="sxs-lookup"><span data-stu-id="d5f45-194">In the task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="d5f45-195">![選取 [連線資訊]][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="d5f45-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="d5f45-196">複製存取控制值。</span><span class="sxs-lookup"><span data-stu-id="d5f45-196">Copy the Access Control values.</span></span>

<span data-ttu-id="d5f45-197">從 Visual Studio 部署 BizTalk 服務專案時，您可以輸入此存取控制命名空間。</span><span class="sxs-lookup"><span data-stu-id="d5f45-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="d5f45-198">為 BizTalk 服務自動建立存取控制命名空間。</span><span class="sxs-lookup"><span data-stu-id="d5f45-198">The Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="d5f45-199">存取控制值可用於任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5f45-199">The Access Control values can be used with any application.</span></span> <span data-ttu-id="d5f45-200">當建立 Azure BizTalk 服務時，此存取控制命名空間會利用 BizTalk 服務部署來控制驗證。</span><span class="sxs-lookup"><span data-stu-id="d5f45-200">When Azure BizTalk Services is created, this Access Control namespace controls the authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="d5f45-201">如果想要變更訂閱或管理命名空間，請在左導覽窗格中選取 [ACTIVE DIRECTORY]  ，然後選取您的命名空間。</span><span class="sxs-lookup"><span data-stu-id="d5f45-201">If you want to change the subscription or manage the namespace, select **ACTIVE DIRECTORY** in the left navigation pane and then select your namespace.</span></span> <span data-ttu-id="d5f45-202">工作列會列出您的選項。</span><span class="sxs-lookup"><span data-stu-id="d5f45-202">The task bar lists your options.</span></span>

<span data-ttu-id="d5f45-203">按一下 [ **管理** ]，即可開啟存取控制管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="d5f45-203">Clicking **Manage** opens the Access Control Management Portal.</span></span> <span data-ttu-id="d5f45-204">在存取控制管理入口網站中，BizTalk 服務會使用 [服務身分識別]：</span><span class="sxs-lookup"><span data-stu-id="d5f45-204">In the Access Control Management Portal, the BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="d5f45-205">![存取控制管理入口網站中的 ACS 服務身分識別][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="d5f45-205">![ACS Service Identities in the Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="d5f45-206">存取控制服務身分識別是一組認證，可讓應用程式或用戶端直接使用 Azure AD 存取控制進行驗證，並接收權杖。</span><span class="sxs-lookup"><span data-stu-id="d5f45-206">The Access Control service identity is a set of credentials that allow applications or clients to authenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5f45-207">BizTalk 服務會使用 [擁有者] 做為預設服務識別，並使用 [密碼] 值。</span><span class="sxs-lookup"><span data-stu-id="d5f45-207">The BizTalk Service uses **Owner** for the default service identity and the **Password** value.</span></span> <span data-ttu-id="d5f45-208">如果您使用對稱金鑰值而不是密碼值，則可能發生下列錯誤。</span><span class="sxs-lookup"><span data-stu-id="d5f45-208">If you use the Symmetric Key value instead of the Password value, the following error may occur.</span></span><br/><br/><span data-ttu-id="d5f45-209">*無法利用指定的認證連接至存取控制管理服務帳戶*</span><span class="sxs-lookup"><span data-stu-id="d5f45-209">*Could not connect to the Access Control Management Service account with the specified credentials*</span></span>
> 
> 

<span data-ttu-id="d5f45-210">[管理您的 ACS 命名空間](https://msdn.microsoft.com/library/azure/hh674478.aspx) 列出一些指導方針和建議。</span><span class="sxs-lookup"><span data-stu-id="d5f45-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="d5f45-211">說明各項需求</span><span class="sxs-lookup"><span data-stu-id="d5f45-211">Requirements explained</span></span>
<span data-ttu-id="d5f45-212">這些需求並不適用於免費版本。</span><span class="sxs-lookup"><span data-stu-id="d5f45-212">These requirements do not apply to the Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="d5f45-213"><strong>您需要什麼</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="d5f45-214"><strong>您為何需要它</strong></span><span class="sxs-lookup"><span data-stu-id="d5f45-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d5f45-215">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="d5f45-215">Azure subscription</span></span></td>
<td><span data-ttu-id="d5f45-216">訂用帳戶可判定誰能夠登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d5f45-216">The subscription determines who can sign in to the Azure portal.</span></span> <span data-ttu-id="d5f45-217">帳戶持有者可在 <a HREF="https://account.windowsazure.com/Subscriptions">Azure 訂用帳戶</a>中建立訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5f45-217">The Account holder creates the subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="d5f45-218">Azure 帳戶可擁有多個訂用帳戶，只要使用者取得允許皆可管理這些帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5f45-218">The Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="d5f45-219">例如，您的 Azure 帳戶持有者建立一個名稱為 <em>BizTalkServiceSubscription</em> 的訂用帳戶，並給與您公司內的 BizTalk 系統管理員 (例如 ContosoBTSAdmins@live.com) 存取此訂閱的權限。</span><span class="sxs-lookup"><span data-stu-id="d5f45-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives the BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access to this subscription.</span></span> <span data-ttu-id="d5f45-220">在此案例中，BizTalk 系統管理員可以登入 Azure 入口網站，並對訂用帳戶中的所有代管服務 (包括 Azure BizTalk 服務) 具有完整系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="d5f45-220">In this scenario, the BizTalk Administrators sign in to the Azure portal and have full Administrator rights to all the hosted services in the subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="d5f45-221">BizTalk 系統管理員不是 Azure 帳戶持有者，因此無權存取任何任何計費資訊。</span><span class="sxs-lookup"><span data-stu-id="d5f45-221">The BizTalk Administrators are not the Azure account holders and therefore don't have access to any billing information.</span></span>
<br/><br/><span data-ttu-id="d5f45-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">管理 Azure 入口網站中的訂用帳戶和儲存體帳戶</a>提供更多相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d5f45-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in the Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="d5f45-223">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d5f45-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="d5f45-224">儲存 Azure BizTalk 服務所使用的資料表、檢視和預存程序，包括追蹤資料。</span><span class="sxs-lookup"><span data-stu-id="d5f45-224">Stores the tables, views, and stored procedures used by the BizTalk Service, including the Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="d5f45-225">在建立 BizTalk 服務時，您可使用現有的 Azure SQL Server、Azure SQL Database，或自動建立新的伺服器或資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5f45-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="d5f45-226">系統會自動設定 SQL Database 調整。</span><span class="sxs-lookup"><span data-stu-id="d5f45-226">The SQL Database scale is automatically configured.</span></span> <span data-ttu-id="d5f45-227">一般來說，預設的調整對 BizTalk 服務已夠用。</span><span class="sxs-lookup"><span data-stu-id="d5f45-227">Typically, the default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="d5f45-228">修改調整會影響定價。</span><span class="sxs-lookup"><span data-stu-id="d5f45-228">Changing the scale impacts pricing.</span></span> <span data-ttu-id="d5f45-229">請參閱 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Azure SQL Database 中的帳戶和計費</a>
</span><span class="sxs-lookup"><span data-stu-id="d5f45-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="d5f45-230">
<strong>注意</strong>
</span><span class="sxs-lookup"><span data-stu-id="d5f45-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="d5f45-231">當您建立新的 Azure SQL Server 和 Database 時，即會自動啟用 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="d5f45-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="d5f45-232">BizTalk 服務需要啟用 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="d5f45-232">The BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="d5f45-233">如果在現有的 Azure SQL Server 上建立新的 Azure SQL Database，則不會變更伺服器的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="d5f45-233">If you create a new Azure SQL Database on an existing Azure SQL Server, the firewall rules of the Server are not changed.</span></span> <span data-ttu-id="d5f45-234">因此，可能不允許其他 Azure 服務存取伺服器的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5f45-234">As a result, it's possible other Azure Services are not allowed access to the Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="d5f45-235">Azure 存取控制命名空間</span><span class="sxs-lookup"><span data-stu-id="d5f45-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="d5f45-236">利用 Azure BizTalk 服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d5f45-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="d5f45-237">從 Visual Studio 部署 BizTalk 服務專案時，您可以輸入此存取控制命名空間。</span><span class="sxs-lookup"><span data-stu-id="d5f45-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="d5f45-238">當您建立 BizTalk 服務時，存取控制命名空間會自動建立。</span><span class="sxs-lookup"><span data-stu-id="d5f45-238">When you create a BizTalk Service, the Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="d5f45-239">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d5f45-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="d5f45-240">允許使用 BizTalk 服務所用的資料表、Blob 和佇列，以儲存下列檔案：</span><span class="sxs-lookup"><span data-stu-id="d5f45-240">Gives access to tables, blobs, and queues used by your BizTalk Service to save the following:</span></span>

<ul>
<li><span data-ttu-id="d5f45-241">監視 BizTalk 服務的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d5f45-241">Log files that monitor the BizTalk Service.</span></span> <span data-ttu-id="d5f45-242">監視輸出也會顯示在 Azure 入口網站的 [監視] 索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="d5f45-242">The monitoring output is also displayed in the **Monitoring** tab in the Azure portal.</span></span></li>
<li><span data-ttu-id="d5f45-243">在夥伴之間建立 X12 或 AS2 協定時，您可以啟用封存功能來儲存訊息內容。</span><span class="sxs-lookup"><span data-stu-id="d5f45-243">When creating an X12 or AS2 agreement between partners, you can enable the Archiving feature to store message properties.</span></span> <span data-ttu-id="d5f45-244">此資料儲存在此儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d5f45-244">This data is saved in the Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="d5f45-245">當建立 BizTalk 服務時，您可以使用現有的儲存體帳戶，或自動建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5f45-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="d5f45-246">預設儲存體設定對 BizTalk 服務已夠用。</span><span class="sxs-lookup"><span data-stu-id="d5f45-246">The default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="d5f45-247">當建立儲存體帳戶時，會自動建立主要金鑰和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="d5f45-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="d5f45-248">這些金鑰可控制儲存體帳戶的存取。</span><span class="sxs-lookup"><span data-stu-id="d5f45-248">These Keys control access to your Storage account.</span></span> <span data-ttu-id="d5f45-249">BizTalk 服務會自動使用主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="d5f45-249">The BizTalk Service automatically uses the Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="d5f45-250">請參閱<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">儲存體</a>以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="d5f45-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="d5f45-251">SSL 專用憑證</span><span class="sxs-lookup"><span data-stu-id="d5f45-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="d5f45-252">當建立 Azure BizTalk 服務時，也會建立一個 HTTPS URL，其中包括 BizTalk 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="d5f45-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="d5f45-253">此 URL 會自動設定為使用自我簽署的開發專用憑證。</span><span class="sxs-lookup"><span data-stu-id="d5f45-253">This URL is automatically configured to use a self-signed development-only certificate.</span></span> <span data-ttu-id="d5f45-254">若為生產案例，您需要私密的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="d5f45-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="d5f45-255">
<strong>重要 SSL 憑證資訊</strong>


</span><span class="sxs-lookup"><span data-stu-id="d5f45-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="d5f45-256">憑證到期日必須少於 5 年。</span><span class="sxs-lookup"><span data-stu-id="d5f45-256">The certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="d5f45-257">所有專用憑證都需要一個密碼。</span><span class="sxs-lookup"><span data-stu-id="d5f45-257">All private certificates require a password.</span></span> <span data-ttu-id="d5f45-258">知道此密碼，而且最佳作法為與系統管理員分享此密碼。</span><span class="sxs-lookup"><span data-stu-id="d5f45-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="d5f45-259">自我簽署憑證是在測試/開發環境中使用。</span><span class="sxs-lookup"><span data-stu-id="d5f45-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="d5f45-260">當使用自我簽署憑證時，請將憑證匯入至您的個人憑證存放區和受信任的根授權單位憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="d5f45-260">When using self-signed certificates, import the certificate to your Personal certificate store and the Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="d5f45-261">將實際執行憑證要求傳送至您的憑證授權單位時，請提供下列憑證內容：</span><span class="sxs-lookup"><span data-stu-id="d5f45-261">When sending the production certificate request to your certification authority, give the following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="d5f45-262"><strong>增強金鑰使用方法</strong>：Azure BizTalk 服務至少需要伺服器驗證。</span><span class="sxs-lookup"><span data-stu-id="d5f45-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="d5f45-263"><strong>一般名稱</strong>：輸入 Azure BizTalk 服務 URL 的完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="d5f45-263"><strong>Common Name</strong>: Enter the fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="d5f45-264">請參閱本文中的<a HREF="#CreateService">建立 BizTalk 服務</a>。</span><span class="sxs-lookup"><span data-stu-id="d5f45-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="d5f45-265">在建立 BizTalk 服務後，可以加入新的或不同的憑證。</span><span class="sxs-lookup"><span data-stu-id="d5f45-265">A new or different certificate can be added after the BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting to any location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="d5f45-266">混合式連線</span><span class="sxs-lookup"><span data-stu-id="d5f45-266">Hybrid Connections</span></span>
<span data-ttu-id="d5f45-267">當您建立 Azure BizTalk 服務時，[ **混合式連線** ] 索引標籤可供使用：</span><span class="sxs-lookup"><span data-stu-id="d5f45-267">When you create an Azure BizTalk Service, the **Hybrid Connections** tab is available:</span></span>

![混合式連線索引標籤][HybridConnectionTab]

<span data-ttu-id="d5f45-269">混合式連線可將 Azure 網站或 Azure 行動服務連線到使用靜態 TCP 連接埠的任何內部部署資源，例如 SQL Server、MySQL、HTTP Web API、行動服務及大多數的自訂 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="d5f45-269">Hybrid Connections are used to connect an Azure website or Azure mobile service to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="d5f45-270">混合式連線和 BizTalk 配接器服務不同。</span><span class="sxs-lookup"><span data-stu-id="d5f45-270">Hybrid Connections and the BizTalk Adapter Service are different.</span></span> <span data-ttu-id="d5f45-271">BizTalk 配接器服務是用於將 Azure BizTalk 服務連線至內部部署企業營運 (LOB) 系統。</span><span class="sxs-lookup"><span data-stu-id="d5f45-271">The BizTalk Adapter Service is used to connect Azure BizTalk Services to an on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="d5f45-272">查閱 [混合式連線](integration-hybrid-connection-overview.md) 以深入了解，其中包含建立和管理混合式連線。</span><span class="sxs-lookup"><span data-stu-id="d5f45-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) to learn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5f45-273">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5f45-273">Next steps</span></span>
<span data-ttu-id="d5f45-274">現在，既然已建立 BizTalk 服務，請讓自己熟悉一下各種不同的 [BizTalk 服務：儀表板、監視和調整索引標籤](biztalk-dashboard-monitor-scale-tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="d5f45-274">Now that a BizTalk Service is created, familiarize yourself with the different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="d5f45-275">您的 BizTalk 服務已準備好可供您的應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="d5f45-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="d5f45-276">若要開始建立應用程式，請移至 [Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=235197)(英文)。</span><span class="sxs-lookup"><span data-stu-id="d5f45-276">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="d5f45-277">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d5f45-277">See also</span></span>
* [<span data-ttu-id="d5f45-278">BizTalk 服務：版本圖表</span><span class="sxs-lookup"><span data-stu-id="d5f45-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="d5f45-279">BizTalk 服務：狀態圖表</span><span class="sxs-lookup"><span data-stu-id="d5f45-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="d5f45-280">BizTalk 服務：備份與還原</span><span class="sxs-lookup"><span data-stu-id="d5f45-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="d5f45-281">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="d5f45-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="d5f45-282">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="d5f45-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="d5f45-283">如何開始使用 Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="d5f45-283">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="d5f45-284">混合式連線</span><span class="sxs-lookup"><span data-stu-id="d5f45-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
