---
title: "在 Azure 入口網站 hello aaaCreate Azure BizTalk 服務 |Microsoft 文件"
description: "深入了解如何 tooprovision 或 hello Azure 入口網站; 中建立 Azure BizTalk 服務MABS WABS"
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
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="f5845-103">建立 BizTalk 服務使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f5845-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="f5845-104">toosign toohello Azure 入口網站中的，您需要 Azure 帳戶和 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5845-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="f5845-105">如果沒有帳戶，您可在幾分鐘內建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5845-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="f5845-106">查看 [Azure 免費試用](http://go.microsoft.com/fwlink/p/?LinkID=239738)。</span><span class="sxs-lookup"><span data-stu-id="f5845-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="f5845-107"><a name="CreateService"></a>建立 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="f5845-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="f5845-108">依據 hello 您選擇的版本，可能提供不是所有的 BizTalk 服務設定。</span><span class="sxs-lookup"><span data-stu-id="f5845-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="f5845-109">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="f5845-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="f5845-110">在 hello 下方瀏覽窗格中，選取**新增**:</span><span class="sxs-lookup"><span data-stu-id="f5845-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="f5845-111">![選取 hello 新按鈕][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="f5845-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="f5845-112">選取 [應用程式服務]  >  [BIZTALK 服務]  >  [自訂建立]：</span><span class="sxs-lookup"><span data-stu-id="f5845-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="f5845-113">![選取 BizTalk 服務] 與選取 [自訂建立]][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="f5845-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="f5845-114">輸入 hello BizTalk 服務設定：</span><span class="sxs-lookup"><span data-stu-id="f5845-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="f5845-115"><strong>BizTalk 服務名稱</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="f5845-116">您可以輸入任何名稱，但請使用特定的名稱。</span><span class="sxs-lookup"><span data-stu-id="f5845-116">You can enter any name but be specific.</span></span> <span data-ttu-id="f5845-117">部分範例包括：</span><span class="sxs-lookup"><span data-stu-id="f5845-117">Some examples include:</span></span><br/><br/><span data-ttu-id="f5845-118">
    <em>mycompany</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="f5845-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="f5845-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="f5845-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="f5845-120">
    <em>myapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="f5845-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="f5845-121">「。 」 會自動新增的 toohello 您所輸入的名稱。</span><span class="sxs-lookup"><span data-stu-id="f5845-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="f5845-122">這會建立您的 BizTalk 服務，例如使用的 tooaccess URL <strong>https://<em>myapplication</em>。</strong>。</span><span class="sxs-lookup"><span data-stu-id="f5845-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="f5845-123"><strong>版本</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="f5845-124">如果您是在 hello 測試/開發階段中，選擇 <strong>開發人員</strong>。</span><span class="sxs-lookup"><span data-stu-id="f5845-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="f5845-125">如果您是在 hello 生產階段中，使用 hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk 服務： 版本圖表</a>toodetermine 如果<strong>Premium</strong>，<strong>標準</strong>，或<strong>Basic</strong>是正確的選擇 hello 的商務案例。</span><span class="sxs-lookup"><span data-stu-id="f5845-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="f5845-126"><strong>區域</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="f5845-127">選取 hello 地理區域 toohost BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="f5845-128"><strong>網域 URL</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="f5845-129"><strong>選用</strong>。</span><span class="sxs-lookup"><span data-stu-id="f5845-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="f5845-130">根據預設，hello 網域 URL 是<em>y</em>。。</span><span class="sxs-lookup"><span data-stu-id="f5845-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="f5845-131">您也可輸入自訂網域。</span><span class="sxs-lookup"><span data-stu-id="f5845-131">A custom domain can also be entered.</span></span> <span data-ttu-id="f5845-132">比方說，如果您的網域為 <em>contoso</em>，則可以輸入：</span><span class="sxs-lookup"><span data-stu-id="f5845-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="f5845-133">
    <em>MyCompany</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="f5845-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="f5845-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="f5845-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="f5845-135">
    <em>MyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="f5845-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="f5845-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="f5845-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="f5845-137">選取 hello 下一步 箭號。</span><span class="sxs-lookup"><span data-stu-id="f5845-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="f5845-138">5.</span><span class="sxs-lookup"><span data-stu-id="f5845-138">5.</span></span> <span data-ttu-id="f5845-139">輸入 hello 儲存體和資料庫設定：</span><span class="sxs-lookup"><span data-stu-id="f5845-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="f5845-140"><strong>監視/封存儲存體帳戶</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="f5845-141">選取現有的儲存體帳戶或建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5845-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="f5845-142">如果您建立新的儲存體帳戶，請輸入 hello<strong>儲存體帳戶名稱</strong>。</span><span class="sxs-lookup"><span data-stu-id="f5845-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="f5845-143"><strong>追蹤資料庫</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="f5845-144">如果您使用現有的 Azure SQL Database，其他 BizTalk 服務將無法使用它。</span><span class="sxs-lookup"><span data-stu-id="f5845-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="f5845-145">您需要輸入時建立的 Azure SQL Database 伺服器 hello 登入名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f5845-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="f5845-146"><strong>提示</strong>建立 hello 追蹤資料庫和監視/封存儲存體帳戶中的 hello 相同的區域為 hello BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="f5845-147">選取 hello 下一步 箭號。</span><span class="sxs-lookup"><span data-stu-id="f5845-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="f5845-148">6.</span><span class="sxs-lookup"><span data-stu-id="f5845-148">6.</span></span> <span data-ttu-id="f5845-149">輸入 hello 資料庫設定：</span><span class="sxs-lookup"><span data-stu-id="f5845-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="f5845-150"><strong>名稱</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="f5845-151">時，才能使用<strong>建立新的 SQL Database 執行個體</strong>hello 上一個畫面中選取。</span><span class="sxs-lookup"><span data-stu-id="f5845-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="f5845-152">輸入 BizTalk 服務所使用的 SQL 資料庫名稱 toobe。</span><span class="sxs-lookup"><span data-stu-id="f5845-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="f5845-153"><strong>伺服器</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="f5845-154">時，才能使用<strong>建立新的 SQL Database 執行個體</strong>hello 上一個畫面中選取。</span><span class="sxs-lookup"><span data-stu-id="f5845-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="f5845-155">選取現有的 SQL Database 伺服器，或是建立全新的 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f5845-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="f5845-156"><strong>伺服器登入名稱</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="f5845-157">輸入 hello 登入使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f5845-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="f5845-158"><strong>伺服器登入密碼</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="f5845-159">輸入 hello 登入密碼。</span><span class="sxs-lookup"><span data-stu-id="f5845-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="f5845-160"><strong>區域</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="f5845-161">可在選取 [建立新的 SQL 資料庫執行個體]<strong></strong> 時使用。</span><span class="sxs-lookup"><span data-stu-id="f5845-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="f5845-162">選取 hello 地理區域 toohost SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f5845-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="f5845-163">選取 hello 核取記號 toocomplete hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="f5845-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="f5845-164">hello 進度圖示會出現：</span><span class="sxs-lookup"><span data-stu-id="f5845-164">hello progress icon appears:</span></span>  
![進度圖示即會顯示][ProgressComplete]

<span data-ttu-id="f5845-166">完成時，hello Azure BizTalk 服務已建立且可供應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5845-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="f5845-167">hello 預設設定，已足夠。</span><span class="sxs-lookup"><span data-stu-id="f5845-167">hello default settings are sufficient.</span></span> <span data-ttu-id="f5845-168">如果您想 toochange hello 預設設定，請選取**BIZTALK 服務**在 hello 左側瀏覽窗格，然後選取 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="f5845-169">其他設定會顯示在 hello[儀表板、 監視器和小數位數的索引標籤](biztalk-dashboard-monitor-scale-tabs.md)hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="f5845-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="f5845-170">根據 hello 的 hello BizTalk 服務的狀態，有一些無法完成的作業。</span><span class="sxs-lookup"><span data-stu-id="f5845-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="f5845-171">如需這些作業的清單，請移至太[BizTalk Services 狀態圖表](biztalk-service-state-chart.md)。</span><span class="sxs-lookup"><span data-stu-id="f5845-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="f5845-172">佈建後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5845-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="f5845-173">在本機電腦上安裝 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="f5845-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="f5845-174">新增實際執行備妥憑證</span><span class="sxs-lookup"><span data-stu-id="f5845-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="f5845-175">取得 hello 存取控制命名空間</span><span class="sxs-lookup"><span data-stu-id="f5845-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="f5845-176"><a name="InstallCert"></a>在本機電腦上安裝 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="f5845-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="f5845-177">自我簽署憑證是 BizTalk 服務佈建的一部分，會在您訂閱 BizTalk 服務時建立並相關聯。</span><span class="sxs-lookup"><span data-stu-id="f5845-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="f5845-178">您必須下載此憑證，並將它安裝在您部署 BizTalk 服務應用程式或傳送訊息 tooa BizTalk 服務端點的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f5845-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="f5845-179">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="f5845-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="f5845-180">選取**BIZTALK 服務**在 hello 左側瀏覽窗格，然後選取您的 BizTalk 服務訂閱。</span><span class="sxs-lookup"><span data-stu-id="f5845-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="f5845-181">選取 hello**儀表板** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f5845-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="f5845-182">選取 [下載 SSL 憑證]：</span><span class="sxs-lookup"><span data-stu-id="f5845-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="f5845-183">![修改 SSL 憑證][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="f5845-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="f5845-184">按兩下 hello 憑證，並透過 hello 精靈 tooinstall hello 認證執行。</span><span class="sxs-lookup"><span data-stu-id="f5845-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="f5845-185">請確定您已安裝 hello hello 憑證**受信任的根憑證授權單位**儲存。</span><span class="sxs-lookup"><span data-stu-id="f5845-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="f5845-186"><a name="AddCert"></a>新增實際執行備妥憑證</span><span class="sxs-lookup"><span data-stu-id="f5845-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="f5845-187">hello 自我簽署的憑證時建立 BizTalk 服務適用於僅限開發環境中自動建立。</span><span class="sxs-lookup"><span data-stu-id="f5845-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="f5845-188">若為生產案例，使用實際執行備妥憑證取代它。</span><span class="sxs-lookup"><span data-stu-id="f5845-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="f5845-189">在 hello**儀表板**索引標籤上，選取**更新 SSL 憑證**。</span><span class="sxs-lookup"><span data-stu-id="f5845-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="f5845-190">瀏覽 tooyour 私用的 SSL 憑證 (*CertificateName*.pfx)，包括您的 BizTalk 服務名稱，輸入 hello 密碼，然後按一下hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="f5845-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="f5845-191"><a name="ACS"></a>取得 hello 存取控制命名空間</span><span class="sxs-lookup"><span data-stu-id="f5845-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="f5845-192">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="f5845-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="f5845-193">選取**BIZTALK 服務**在 hello 左側瀏覽窗格，然後選取 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="f5845-194">在 hello 工作列上，選取 **連接資訊**:</span><span class="sxs-lookup"><span data-stu-id="f5845-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="f5845-195">![選取 [連線資訊]][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="f5845-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="f5845-196">複製 hello 存取控制值。</span><span class="sxs-lookup"><span data-stu-id="f5845-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="f5845-197">從 Visual Studio 部署 BizTalk 服務專案時，您可以輸入此存取控制命名空間。</span><span class="sxs-lookup"><span data-stu-id="f5845-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="f5845-198">hello 存取控制命名空間會自動建立 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="f5845-199">hello 存取控制項的值可以搭配任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5845-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="f5845-200">建立 Azure BizTalk 服務時，此存取控制命名空間會控制與 BizTalk 服務部署的 hello 驗證。</span><span class="sxs-lookup"><span data-stu-id="f5845-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="f5845-201">如果您想 toochange hello 訂用帳戶或管理 hello 命名空間，請選取**ACTIVE DIRECTORY**在 hello 左側的導覽窗格中，然後選取您的命名空間。</span><span class="sxs-lookup"><span data-stu-id="f5845-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="f5845-202">hello 工作列列出您的選項。</span><span class="sxs-lookup"><span data-stu-id="f5845-202">hello task bar lists your options.</span></span>

<span data-ttu-id="f5845-203">按一下**管理**開啟 hello 存取控制管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="f5845-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="f5845-204">在 hello 存取控制管理入口網站，hello BizTalk 服務會使用**服務身分識別**:</span><span class="sxs-lookup"><span data-stu-id="f5845-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="f5845-205">![在 hello 存取控制管理入口網站中 ACS 服務身分識別][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="f5845-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="f5845-206">hello 存取控制服務身分識別是一組認證，讓應用程式或用戶端 tooauthenticate 直接與存取控制，並接收權杖。</span><span class="sxs-lookup"><span data-stu-id="f5845-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5845-207">hello BizTalk 服務使用**擁有者**hello 預設服務身分識別和 hello**密碼**值。</span><span class="sxs-lookup"><span data-stu-id="f5845-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="f5845-208">如果您使用 hello 對稱金鑰值，而不是 hello 密碼值，hello 下列可能發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f5845-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="f5845-209">*無法以指定的 hello 連接 toohello 存取控制管理服務帳戶認證*</span><span class="sxs-lookup"><span data-stu-id="f5845-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="f5845-210">[管理您的 ACS 命名空間](https://msdn.microsoft.com/library/azure/hh674478.aspx) 列出一些指導方針和建議。</span><span class="sxs-lookup"><span data-stu-id="f5845-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="f5845-211">說明各項需求</span><span class="sxs-lookup"><span data-stu-id="f5845-211">Requirements explained</span></span>
<span data-ttu-id="f5845-212">這些需求不會套用 toohello 免費版本。</span><span class="sxs-lookup"><span data-stu-id="f5845-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="f5845-213"><strong>您需要什麼</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="f5845-214"><strong>您為何需要它</strong></span><span class="sxs-lookup"><span data-stu-id="f5845-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f5845-215">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="f5845-215">Azure subscription</span></span></td>
<td><span data-ttu-id="f5845-216">hello 訂用帳戶會決定使用者可以登入 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f5845-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="f5845-217">hello 帳戶持有者會建立在 hello 訂閱<a HREF="https://account.windowsazure.com/Subscriptions">Azure 訂用帳戶</a>。</span><span class="sxs-lookup"><span data-stu-id="f5845-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="f5845-218">hello Azure 帳戶可以有多個訂用帳戶，可以管理允許的任何人。</span><span class="sxs-lookup"><span data-stu-id="f5845-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="f5845-219">例如，您的 Azure 帳戶持有者會建立名為訂用帳戶<em>BizTalkServiceSubscription</em>並可讓您公司內 hello BizTalk 系統管理員 (例如， ContosoBTSAdmins@live.com) 存取 toothis 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5845-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="f5845-220">在此案例中，hello BizTalk 系統管理員登入 toohello Azure 入口網站，並在 hello 訂用帳戶，包括 Azure BizTalk 服務中有完整的系統管理員權限 tooall hello 裝載服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="f5845-221">hello BizTalk 系統管理員不是 hello Azure 帳戶持有者，並因此不需要存取 tooany 帳單資訊。</span><span class="sxs-lookup"><span data-stu-id="f5845-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="f5845-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">在 hello Azure 入口網站中管理訂用帳戶和儲存體帳戶</a>提供詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f5845-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="f5845-223">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f5845-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="f5845-224">儲存 hello 資料表、 檢視和 hello BizTalk 服務，包括 hello 追蹤資料所使用的預存程序。</span><span class="sxs-lookup"><span data-stu-id="f5845-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="f5845-225">在建立 BizTalk 服務時，您可使用現有的 Azure SQL Server、Azure SQL Database，或自動建立新的伺服器或資料庫。</span><span class="sxs-lookup"><span data-stu-id="f5845-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="f5845-226">hello SQL Database 的小數位數會自動設定。</span><span class="sxs-lookup"><span data-stu-id="f5845-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="f5845-227">一般而言，hello 預設小數位數不足，BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="f5845-228">變更 hello 標尺將會影響定價。</span><span class="sxs-lookup"><span data-stu-id="f5845-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="f5845-229">請參閱 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Azure SQL Database 中的帳戶和計費</a>
</span><span class="sxs-lookup"><span data-stu-id="f5845-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="f5845-230">
<strong>注意</strong>
</span><span class="sxs-lookup"><span data-stu-id="f5845-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="f5845-231">當您建立新的 Azure SQL Server 和 Database 時，即會自動啟用 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="f5845-232">hello BizTalk 服務需要 Azure 服務啟用。</span><span class="sxs-lookup"><span data-stu-id="f5845-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="f5845-233">如果您現有的 Azure SQL Server 上建立新的 Azure SQL Database，hello 的 hello 不會變更伺服器的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="f5845-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="f5845-234">如此一來，便可存取 toohello 伺服器的資料庫不允許其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="f5845-235">Azure 存取控制命名空間</span><span class="sxs-lookup"><span data-stu-id="f5845-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="f5845-236">利用 Azure BizTalk 服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f5845-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="f5845-237">從 Visual Studio 部署 BizTalk 服務專案時，您可以輸入此存取控制命名空間。</span><span class="sxs-lookup"><span data-stu-id="f5845-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="f5845-238">當您建立 BizTalk 服務時，會自動建立 hello 存取控制命名空間。</span><span class="sxs-lookup"><span data-stu-id="f5845-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="f5845-239">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f5845-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="f5845-240">提供存取 tootables、 blob 和佇列供您的 BizTalk 服務 toosave hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f5845-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="f5845-241">記錄檔的監視 hello BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="f5845-242">監視輸出的 hello 也會顯示在 hello**監視**hello Azure 入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f5845-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="f5845-243">建立 X12 或合作夥伴之間的 AS2 協議時，您可以啟用 hello 封存功能 toostore 訊息屬性。</span><span class="sxs-lookup"><span data-stu-id="f5845-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="f5845-244">這項資料會儲存在 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5845-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="f5845-245">當建立 BizTalk 服務時，您可以使用現有的儲存體帳戶，或自動建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5845-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="f5845-246">hello 預設儲存體設定已足夠的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="f5845-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="f5845-247">當建立儲存體帳戶時，會自動建立主要金鑰和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="f5845-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="f5845-248">這些金鑰控制存取 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5845-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="f5845-249">hello BizTalk 服務會自動使用 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f5845-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="f5845-250">請參閱<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">儲存體</a>以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="f5845-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="f5845-251">SSL 專用憑證</span><span class="sxs-lookup"><span data-stu-id="f5845-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="f5845-252">當建立 Azure BizTalk 服務時，也會建立一個 HTTPS URL，其中包括 BizTalk 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="f5845-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="f5845-253">此 URL 是自動設定的 toouse 開發階段專用的自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="f5845-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="f5845-254">若為生產案例，您需要私密的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="f5845-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="f5845-255">
<strong>重要 SSL 憑證資訊</strong>


</span><span class="sxs-lookup"><span data-stu-id="f5845-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="f5845-256">hello 憑證到期日必須是少於 5 年。</span><span class="sxs-lookup"><span data-stu-id="f5845-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="f5845-257">所有專用憑證都需要一個密碼。</span><span class="sxs-lookup"><span data-stu-id="f5845-257">All private certificates require a password.</span></span> <span data-ttu-id="f5845-258">知道此密碼，而且最佳作法為與系統管理員分享此密碼。</span><span class="sxs-lookup"><span data-stu-id="f5845-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="f5845-259">自我簽署憑證是在測試/開發環境中使用。</span><span class="sxs-lookup"><span data-stu-id="f5845-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="f5845-260">使用自我簽署的憑證時，匯入 hello 憑證 tooyour 個人憑證存放區和 hello 受信任的根憑證授權單位憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="f5845-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="f5845-261">將傳送嗨生產憑證要求 tooyour 憑證授權單位時，會提供下列憑證屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="f5845-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="f5845-262"><strong>增強金鑰使用方法</strong>：Azure BizTalk 服務至少需要伺服器驗證。</span><span class="sxs-lookup"><span data-stu-id="f5845-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="f5845-263"><strong>一般名稱</strong>： 輸入您的 Azure BizTalk 服務 URL 的 hello 完整的網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="f5845-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="f5845-264">請參閱本文中的<a HREF="#CreateService">建立 BizTalk 服務</a>。</span><span class="sxs-lookup"><span data-stu-id="f5845-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="f5845-265">建立 hello BizTalk 服務之後，可以加入新的或不同的憑證。</span><span class="sxs-lookup"><span data-stu-id="f5845-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="f5845-266">混合式連線</span><span class="sxs-lookup"><span data-stu-id="f5845-266">Hybrid Connections</span></span>
<span data-ttu-id="f5845-267">當您建立 Azure BizTalk 服務時，hello**混合式連線** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="f5845-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![混合式連線索引標籤][HybridConnectionTab]

<span data-ttu-id="f5845-269">混合式連線會使用的 tooconnect Azure 網站或 Azure 行動服務 tooany 內部使用靜態 TCP 連接埠，例如 SQL Server、 MySQL、 HTTP 的 Web Api、 行動服務和大部分的自訂 Web 服務的資源。</span><span class="sxs-lookup"><span data-stu-id="f5845-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="f5845-270">混合式連線及 hello BizTalk 配接器服務會有所不同。</span><span class="sxs-lookup"><span data-stu-id="f5845-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="f5845-271">hello BizTalk Adapter 服務是使用的 tooconnect Azure BizTalk 服務 tooan 在內部部署企業營運 (LOB) 系統。</span><span class="sxs-lookup"><span data-stu-id="f5845-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="f5845-272">請參閱[混合式連線](integration-hybrid-connection-overview.md)toolearn 更多，包括建立和管理混合式連線。</span><span class="sxs-lookup"><span data-stu-id="f5845-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5845-273">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5845-273">Next steps</span></span>
<span data-ttu-id="f5845-274">現在，建立 BizTalk 服務時，讓自己熟悉如何以不同的 hello [BizTalk 服務： 儀表板、 監視器和調整規模 索引標籤](biztalk-dashboard-monitor-scale-tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="f5845-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="f5845-275">您的 BizTalk 服務已準備好可供您的應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="f5845-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="f5845-276">建立應用程式，請跳過 toostart[Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=235197)。</span><span class="sxs-lookup"><span data-stu-id="f5845-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="f5845-277">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f5845-277">See also</span></span>
* [<span data-ttu-id="f5845-278">BizTalk 服務：版本圖表</span><span class="sxs-lookup"><span data-stu-id="f5845-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="f5845-279">BizTalk 服務：狀態圖表</span><span class="sxs-lookup"><span data-stu-id="f5845-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="f5845-280">BizTalk 服務：備份與還原</span><span class="sxs-lookup"><span data-stu-id="f5845-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="f5845-281">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="f5845-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="f5845-282">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="f5845-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="f5845-283">開始使用我要如何 hello Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="f5845-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="f5845-284">VNet</span><span class="sxs-lookup"><span data-stu-id="f5845-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
