---
title: "aaaMigrate 企業 web 應用程式 tooAzure 應用程式服務"
description: "顯示 toouse Web 應用程式移轉小幫手 tooquickly 要如何移轉現有的 IIS 網站 tooAzure App Service Web 應用程式"
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a><span data-ttu-id="ffad0-103">移轉企業 web 應用程式 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="ffad0-103">Migrate an enterprise web app tooAzure App Service</span></span>
<span data-ttu-id="ffad0-104">您可以輕鬆地移轉您現有的網站，執行在網際網路資訊服務 (IIS) 6 或更新版本太[App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="ffad0-104">You can easily migrate your existing websites that run on Internet Information Service (IIS) 6 or later too[App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ffad0-105">我們已在 2015 年 7 月 14 日終止對 Windows Server 2003 的支援。</span><span class="sxs-lookup"><span data-stu-id="ffad0-105">Windows Server 2003 reached end of support on July 14th 2015.</span></span> <span data-ttu-id="ffad0-106">如果您目前裝載您為 Windows Server 2003 的 IIS 伺服器上的網站，Web 應用程式就會是的 tookeep 上線，網站和 Web 應用程式移轉小幫手可協助您自動化 hello 移轉程序的低風險、 低成本和低人事方法。</span><span class="sxs-lookup"><span data-stu-id="ffad0-106">If you are currently hosting your websites on an IIS server that is Windows Server 2003, Web Apps is a low-risk, low-cost, and low-friction way tookeep your websites online, and Web Apps Migration Assistant can help automate hello migration process for you.</span></span> 
> 
> 

<span data-ttu-id="ffad0-107">[Web 應用程式移轉小幫手](https://www.movemetothecloud.net/)可以分析 IIS 伺服器安裝，請找出哪些站台可以是移轉的 tooApp 服務、 反白顯示無法移轉或 hello 平台上，不支援的任何項目，然後再移轉您的網站，並相關聯的資料庫 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="ffad0-107">[Web Apps Migration Assistant](https://www.movemetothecloud.net/) can analyze your IIS server installation, identify which sites can be migrated tooApp Service, highlight any elements that cannot be migrated or are unsupported on hello platform, and then migrate your websites and associated databases tooAzure.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a><span data-ttu-id="ffad0-108">在相容性分析期間驗證的元素</span><span class="sxs-lookup"><span data-stu-id="ffad0-108">Elements Verified During Compatibility Analysis</span></span>
<span data-ttu-id="ffad0-109">移轉小幫手 hello 建立任何可能會造成的問題或封鎖的問題可能導致無法成功從內部部署 IIS tooAzure App Service Web 應用程式移轉整備報表 tooidentify。</span><span class="sxs-lookup"><span data-stu-id="ffad0-109">hello Migration Assistant creates a readiness report tooidentify any potential causes for concern or blocking issues which may prevent a successful migration from on-premises IIS tooAzure App Service Web Apps.</span></span> <span data-ttu-id="ffad0-110">某些 hello 索引鍵的項目 toobe 注意的是：</span><span class="sxs-lookup"><span data-stu-id="ffad0-110">Some of hello key items toobe aware of are:</span></span>

* <span data-ttu-id="ffad0-111">連接埠繫結 - Web Apps 僅支援連接埠 80 (適用於 HTTP) 和連接埠 443 (適用於 HTTPS 流量)。</span><span class="sxs-lookup"><span data-stu-id="ffad0-111">Port Bindings – Web Apps only supports Port 80 for HTTP and Port 443 for HTTPS traffic.</span></span> <span data-ttu-id="ffad0-112">會忽略不同的通訊埠設定，而流量會路由的 too80 或 443。</span><span class="sxs-lookup"><span data-stu-id="ffad0-112">Different port configurations will be ignored and traffic will be routed too80 or 443.</span></span> 
* <span data-ttu-id="ffad0-113">驗證 - Web Apps 預設支援匿名驗證以及應用程式所指定的表單驗證。</span><span class="sxs-lookup"><span data-stu-id="ffad0-113">Authentication – Web Apps supports Anonymous Authentication by default and Forms Authentication where specified by an application.</span></span> <span data-ttu-id="ffad0-114">只有與 Azure Active Directory 和 ADFS 整合，才能使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="ffad0-114">Windows Authentication can be used by integrating with Azure Active Directory and ADFS only.</span></span> <span data-ttu-id="ffad0-115">目前不支援所有其他形式的驗證 (例如基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="ffad0-115">All other forms of authentication - for example, Basic Authentication - are not currently supported.</span></span> 
* <span data-ttu-id="ffad0-116">全域組件快取 (GAC) – GAC 不支援在 Web 應用程式中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ffad0-116">Global Assembly Cache (GAC) – hello GAC is not supported in Web Apps.</span></span> <span data-ttu-id="ffad0-117">如果您的應用程式參考組件的通常是部署 toohello GAC，您就需要 toodeploy toohello 應用程式在 Web 應用程式的 bin 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ffad0-117">If your application references assemblies which you usually deploy toohello GAC, you will need toodeploy toohello application bin folder in Web Apps.</span></span> 
* <span data-ttu-id="ffad0-118">IIS5 相容性模式 - Web Apps 不支援此模式。</span><span class="sxs-lookup"><span data-stu-id="ffad0-118">IIS5 Compatibility Mode – This is not supported in Web Apps.</span></span> 
* <span data-ttu-id="ffad0-119">在 hello 中執行的應用程式集區-Web 應用程式中的，每個站台及其子應用程式相同的應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="ffad0-119">Application Pools – In Web Apps, each site and its child applications run in hello same application pool.</span></span> <span data-ttu-id="ffad0-120">如果您的網站有多個子應用程式利用多個應用程式集區，將其合併 tooa 單一應用程式集區使用通用的設定，或移轉每個應用程式 tooa 個別 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffad0-120">If your site has multiple child applications utilizing multiple application pools, consolidate them tooa single application pool with common settings or migrate each application tooa separate web app.</span></span>
* <span data-ttu-id="ffad0-121">COM 元件： Web 應用程式不允許在 hello 平台上的 hello 註冊的 COM 元件。</span><span class="sxs-lookup"><span data-stu-id="ffad0-121">COM Components – Web Apps does not allow hello registration of COM Components on hello platform.</span></span> <span data-ttu-id="ffad0-122">如果您的網站或應用程式使用的任何 COM 元件，您必須重新撰寫它們在 managed 程式碼，並將其部署與 hello 網站或應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffad0-122">If your websites or applications make use of any COM Components, you must rewrite them in managed code and deploy them with hello website or application.</span></span>
* <span data-ttu-id="ffad0-123">ISAPI 擴充程式 – Web 應用程式可以支援 hello 使用 ISAPI 擴充程式。</span><span class="sxs-lookup"><span data-stu-id="ffad0-123">ISAPI Extensions – Web Apps can support hello use of ISAPI Extensions.</span></span> <span data-ttu-id="ffad0-124">您需要 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ffad0-124">You need toodo hello following:</span></span>
  
  * <span data-ttu-id="ffad0-125">部署 web 應用程式的 hello Dll</span><span class="sxs-lookup"><span data-stu-id="ffad0-125">deploy hello DLLs with your web app</span></span> 
  * <span data-ttu-id="ffad0-126">註冊使用 hello Dll [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span><span class="sxs-lookup"><span data-stu-id="ffad0-126">register hello DLLs using [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span></span>
  * <span data-ttu-id="ffad0-127">applicationHost.xdt 檔案置於 hello 網站根目錄，以 「 允許 arbitrart ISAPI 延伸模組 toobe 載入 」 所述的 hello 內容[本文一節](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)</span><span class="sxs-lookup"><span data-stu-id="ffad0-127">place an applicationHost.xdt file in hello site root with hello content outlined in "Allowing arbitrart ISAPI extensions toobe loaded" [section of this article](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)</span></span> 
    
  
    
    <span data-ttu-id="ffad0-128">如需如何的範例 toouse XML 文件轉換到您的網站，請參閱[轉換您的 Microsoft Azure 網站](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ffad0-128">For more examples of how toouse XML Document Transformations with your website, see [Transform your Microsoft Azure Web Site](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).</span></span>
* <span data-ttu-id="ffad0-129">不會移轉其他元件，例如 SharePoint、Front Page Server Extensions (FPSE)、FTP、SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="ffad0-129">Other components like SharePoint, front page server extensions (FPSE), FTP, SSL certificates will not be migrated.</span></span>

## <a name="how-toouse-hello-web-apps-migration-assistant"></a><span data-ttu-id="ffad0-130">如何 toouse hello Web 應用程式移轉小幫手</span><span class="sxs-lookup"><span data-stu-id="ffad0-130">How toouse hello Web Apps Migration Assistant</span></span>
<span data-ttu-id="ffad0-131">本節逐步說明範例 tootoomigrate 幾個網站使用 SQL Server 資料庫，並在內部部署 Windows Server 2003 R2 (IIS 6.0) 電腦上執行：</span><span class="sxs-lookup"><span data-stu-id="ffad0-131">This section steps through an example tootoomigrate a few websites that use a SQL Server database and running on an on-premises Windows Server 2003 R2 (IIS 6.0) machine:</span></span>

1. <span data-ttu-id="ffad0-132">在 hello IIS 伺服器或用戶端電腦瀏覽過[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span><span class="sxs-lookup"><span data-stu-id="ffad0-132">On hello IIS server or your client machine navigate too[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. <span data-ttu-id="ffad0-133">安裝 Web 應用程式移轉小幫手按一下 hello**專用 IIS 伺服器** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ffad0-133">Install Web Apps Migration Assistant by clicking on hello **Dedicated IIS Server** button.</span></span> <span data-ttu-id="ffad0-134">更多選項將會在未來附近的 hello 的選項。</span><span class="sxs-lookup"><span data-stu-id="ffad0-134">More options will be options in hello near future.</span></span> 
3. <span data-ttu-id="ffad0-135">按一下 hello **Install Tool**按鈕在電腦上的 Web 應用程式移轉小幫手 tooinstall。</span><span class="sxs-lookup"><span data-stu-id="ffad0-135">Click hello **Install Tool** button tooinstall Web Apps Migration Assistant on your machine.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > <span data-ttu-id="ffad0-136">您也可以按一下**下載離線安裝**toodownload ZIP 檔案不在伺服器上安裝連線 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="ffad0-136">You can also click **Download for offline install** toodownload a ZIP file for installing on servers not connected toohello internet.</span></span> <span data-ttu-id="ffad0-137">或者，您可以按一下**上傳現有的移轉整備報表**，這是進階的選項 toowork，與現有移轉整備報表先前產生 （稍後說明）。</span><span class="sxs-lookup"><span data-stu-id="ffad0-137">Or, you can click **Upload an existing migration readiness report**, which is an advanced option toowork with an existing migration readiness report that you previously generated (explained later).</span></span>
   > 
   > 
4. <span data-ttu-id="ffad0-138">在 hello**應用程式安裝**畫面上，按一下**安裝**tooinstall 您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ffad0-138">In hello **Application Install** screen, click **Install** tooinstall on your machine.</span></span> <span data-ttu-id="ffad0-139">必要時也會安裝對應的相依項目，如 Web Deploy、DacFX 和 IIS。</span><span class="sxs-lookup"><span data-stu-id="ffad0-139">It will also install corresponding dependencies like Web Deploy, DacFX, and IIS, if needed.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   <span data-ttu-id="ffad0-140">安裝後，Web Apps 移轉小幫手會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="ffad0-140">Once installed, Web Apps Migration Assistant automatically starts.</span></span>
5. <span data-ttu-id="ffad0-141">選擇**將站台和資料庫移轉從遠端伺服器 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="ffad0-141">Choose **Migrate sites and databases from a remote server tooAzure**.</span></span> <span data-ttu-id="ffad0-142">輸入 hello 遠端伺服器 hello 系統管理認證，然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="ffad0-142">Enter hello administrative credentials for hello remote server and click **Continue**.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   <span data-ttu-id="ffad0-143">您當然可以選擇 toomigrate hello 的本機伺服器。</span><span class="sxs-lookup"><span data-stu-id="ffad0-143">You can of course choose toomigrate from hello local server.</span></span> <span data-ttu-id="ffad0-144">當您想從實際執行的 IIS 伺服器 toomigrate 網站時，則 hello 遠端選項會很有用。</span><span class="sxs-lookup"><span data-stu-id="ffad0-144">hello remote option is useful when you want toomigrate websites from a production IIS server.</span></span>
   
   <span data-ttu-id="ffad0-145">Hello 移轉工具會檢查在此時 hello IIS 伺服器的組態，例如網站、 應用程式、 應用程式集區，以及相依性 tooidentify 候選的網站進行移轉。</span><span class="sxs-lookup"><span data-stu-id="ffad0-145">At this point hello migration tool will inspect hello your IIS server's configuration, such as Sites, Applications, Application Pools, and dependencies tooidentify candidate websites for migration.</span></span> 
6. <span data-ttu-id="ffad0-146">hello 以下螢幕擷取畫面顯示三個網站 – **Default Web Site**， **TimeTracker**，和**CommerceNet4**。</span><span class="sxs-lookup"><span data-stu-id="ffad0-146">hello screenshot below shows three websites – **Default Web Site**, **TimeTracker**, and **CommerceNet4**.</span></span> <span data-ttu-id="ffad0-147">全部都有相關聯的資料庫，我們想要 toomigrate。</span><span class="sxs-lookup"><span data-stu-id="ffad0-147">All of them have an associated database that we want toomigrate.</span></span> <span data-ttu-id="ffad0-148">選取所有 hello 站台，tooassess 然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="ffad0-148">Select all of hello sites you would like tooassess and then click **Next**.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. <span data-ttu-id="ffad0-149">按一下**上傳**tooupload hello 整備報表。</span><span class="sxs-lookup"><span data-stu-id="ffad0-149">Click **Upload** tooupload hello readiness report.</span></span> <span data-ttu-id="ffad0-150">如果您按一下**檔案儲存在本機儲存**，您可以稍後再執行 hello 移轉工具，並且上傳 hello 儲存整備報表，如前文所述。</span><span class="sxs-lookup"><span data-stu-id="ffad0-150">If you click **save file locally**, you can run hello migration tool again later and upload hello saved readiness report as noted earlier.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   <span data-ttu-id="ffad0-151">一旦您上傳 hello 整備報表時，Azure 會在執行整備分析和顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ffad0-151">Once you upload hello readiness report, Azure performs readiness analysis and shows you hello results.</span></span> <span data-ttu-id="ffad0-152">讀取 hello 評估每個網站的詳細資料，並確定您了解，或是解決所有問題後再繼續。</span><span class="sxs-lookup"><span data-stu-id="ffad0-152">Read hello assessment details for each website and make sure that you understand or have addressed all issues before you proceed.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. <span data-ttu-id="ffad0-153">按一下**開始移轉**toostart hello 移轉。您現在將會重新導向的 tooAzure toolog 入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="ffad0-153">Click **Begin Migration** toostart hello migration.You will now be redirected tooAzure toolog into your account.</span></span> <span data-ttu-id="ffad0-154">請務必以具有作用中 Azure 訂用帳戶的帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="ffad0-154">It is important that you log in with an account that has an active Azure Subscription.</span></span> <span data-ttu-id="ffad0-155">如果您沒有 Azure 帳戶，可以在[這裡](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_)註冊免費試用。</span><span class="sxs-lookup"><span data-stu-id="ffad0-155">If you do not have an Azure account then you can sign up for a free trial [here](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_).</span></span> 
9. <span data-ttu-id="ffad0-156">選取 hello 租用戶帳戶、 Azure 訂用帳戶和地區 toouse 已移轉的 Azure web 應用程式和資料庫，然後按一下**開始移轉**。</span><span class="sxs-lookup"><span data-stu-id="ffad0-156">Select hello tenant account, Azure subscription and region toouse for your migrated Azure web apps and databases, and then click **Start Migration**.</span></span> <span data-ttu-id="ffad0-157">您可以稍後再選取 hello 網站 toomigrate。</span><span class="sxs-lookup"><span data-stu-id="ffad0-157">You can select hello websites toomigrate later.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. <span data-ttu-id="ffad0-158">Hello 下一個畫面中您可以變更 toohello 預設移轉設定，例如：</span><span class="sxs-lookup"><span data-stu-id="ffad0-158">On hello next screen you can make changes toohello default migration settings, such as:</span></span>
    
    * <span data-ttu-id="ffad0-159">使用現有的 Azure SQL Database 或建立新的 Azure SQL Database，並設定其認證</span><span class="sxs-lookup"><span data-stu-id="ffad0-159">use an existing Azure SQL Database or create a new Azure SQL Database, and configure its credentials</span></span>
    * <span data-ttu-id="ffad0-160">選取 hello 網站 toomigrate</span><span class="sxs-lookup"><span data-stu-id="ffad0-160">select hello websites toomigrate</span></span>
    * <span data-ttu-id="ffad0-161">定義 hello Azure web 應用程式並將其連結的 SQL 資料庫的名稱</span><span class="sxs-lookup"><span data-stu-id="ffad0-161">define names for hello Azure web apps and their linked SQL databases</span></span>
    * <span data-ttu-id="ffad0-162">hello 通用及自訂設定網站層級設定</span><span class="sxs-lookup"><span data-stu-id="ffad0-162">customize hello global settings and site-level settings</span></span>
    
    <span data-ttu-id="ffad0-163">hello 以下螢幕擷取畫面顯示以 hello 預設設定的移轉選取的所有 hello 網站。</span><span class="sxs-lookup"><span data-stu-id="ffad0-163">hello screenshot below shows all hello websites selected for migration with hello default settings.</span></span>
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > <span data-ttu-id="ffad0-164">hello**啟用 Azure Active Directory**核取方塊，在自訂設定整合 hello Azure web 應用程式與[Azure Active Directory](../active-directory/active-directory-whatis.md) (hello**預設目錄**)。</span><span class="sxs-lookup"><span data-stu-id="ffad0-164">hello **Enable Azure Active Directory** checkbox in custom settings integrates hello Azure web app with [Azure Active Directory](../active-directory/active-directory-whatis.md) (hello **Default Directory**).</span></span> <span data-ttu-id="ffad0-165">如需同步處理 Azure Active Directory 與內部部署 Active Directory 的詳細資訊，請參閱[目錄整合](http://msdn.microsoft.com/library/jj573653)。</span><span class="sxs-lookup"><span data-stu-id="ffad0-165">For more information on syncing Azure Active Directory with your on-premises Active Directory, see [Directory integration](http://msdn.microsoft.com/library/jj573653).</span></span>
    > 
    > 
11. <span data-ttu-id="ffad0-166">一旦您進行 hello 所需的所有變更，按一下 **建立**toostart hello 移轉程序。</span><span class="sxs-lookup"><span data-stu-id="ffad0-166">Once you make all hello desired changes, click **Create** toostart hello migration process.</span></span> <span data-ttu-id="ffad0-167">hello 移轉工具會建立 hello Azure SQL Database 和 Azure web 應用程式，並再發行 hello 網站內容和資料庫。</span><span class="sxs-lookup"><span data-stu-id="ffad0-167">hello migration tool will create hello Azure SQL Database and Azure web app, and then publish hello website content and databases.</span></span> <span data-ttu-id="ffad0-168">hello 移轉工具，清楚地顯示 hello 移轉進度，且您會看到在 hello 結束時，哪些詳細資料 hello 站台移轉、 他們是否成功、 連結 toohello 新建的 Azure web 應用程式的摘要畫面。</span><span class="sxs-lookup"><span data-stu-id="ffad0-168">hello migration progress is clearly shown in hello migration tool, and you will see a summary screen at hello end, which details hello sites migrated, whether they were successful, links toohello newly-created Azure web apps.</span></span> 
    
    <span data-ttu-id="ffad0-169">如果任何錯誤，就會發生在移轉期間，hello 移轉工具 會清楚指出 hello 失敗和回復 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="ffad0-169">If any error occurs during migration, hello migration tool will clearly indicate hello failure and rollback hello changes.</span></span> <span data-ttu-id="ffad0-170">您也會無法 toosend hello 錯誤報告直接 toohello 工程小組，網址為按一下 hello**傳送錯誤報表**按鈕，與 hello 擷取的失敗的呼叫堆疊，並建立訊息本文。</span><span class="sxs-lookup"><span data-stu-id="ffad0-170">You will also be able toosend hello error report directly toohello engineering team by clicking hello **Send Error Report** button, with hello captured failure call stack and build message body.</span></span> 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    <span data-ttu-id="ffad0-171">如果移轉成功且沒有錯誤，您也可以按一下 hello**提供意見反應**直接按鈕 tooprovide 任何意見反應。</span><span class="sxs-lookup"><span data-stu-id="ffad0-171">If migrate succeeds without errors, you can also click hello **Give Feedback** button tooprovide any feedback directly.</span></span> 
12. <span data-ttu-id="ffad0-172">按一下 hello 連結 toohello Azure web 應用程式並確認已成功 hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="ffad0-172">Click hello links toohello Azure web apps and verify that hello migration has succeeded.</span></span>
13. <span data-ttu-id="ffad0-173">您現在可以管理 hello 移轉 Azure App Service 中的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffad0-173">You can now manage hello migrated web apps in Azure App Service.</span></span> <span data-ttu-id="ffad0-174">toodo，登入 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ffad0-174">toodo this, log into hello [Azure Portal](https://portal.azure.com).</span></span>
14. <span data-ttu-id="ffad0-175">在 [hello Azure 入口網站，開啟 hello Web 應用程式] 刀鋒視窗 toosee 移轉網站 （顯示為 web 應用程式），然後按一下其中任何一個 toostart 管理 hello web 應用程式，例如設定連續發行、 建立備份，自動調整，以及監視使用量或效能。</span><span class="sxs-lookup"><span data-stu-id="ffad0-175">In hello Azure Portal, open hello Web Apps blade toosee your migrated websites (shown as web apps), then click on any one of them toostart managing hello web app, such as configuring continuous publishing, creating backups, autoscaling, and monitoring usage or performance.</span></span>
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> <span data-ttu-id="ffad0-176">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="ffad0-176">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ffad0-177">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="ffad0-177">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="ffad0-178">變更的項目</span><span class="sxs-lookup"><span data-stu-id="ffad0-178">What's changed</span></span>
* <span data-ttu-id="ffad0-179">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ffad0-179">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

