---
title: "將企業 Web 應用程式移轉至 Azure App Service"
description: "示範如何使用 Web Apps 移轉小幫手，將現有的 IIS 網站快速移轉至 Azure App Service Web Apps"
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
ms.openlocfilehash: 18d6a8da38b42dcf5c1500f7fc26638aea26a809
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-enterprise-web-app-to-azure-app-service"></a><span data-ttu-id="b8a06-103">將企業 Web 應用程式移轉至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b8a06-103">Migrate an enterprise web app to Azure App Service</span></span>
<span data-ttu-id="b8a06-104">您可以輕鬆地將在 Internet Information Service (IIS) 6 或更新版本上執行的現有網站移轉至 [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="b8a06-104">You can easily migrate your existing websites that run on Internet Information Service (IIS) 6 or later to [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b8a06-105">我們已在 2015 年 7 月 14 日終止對 Windows Server 2003 的支援。</span><span class="sxs-lookup"><span data-stu-id="b8a06-105">Windows Server 2003 reached end of support on July 14th 2015.</span></span> <span data-ttu-id="b8a06-106">如果您的網站目前裝載於採用 Windows Server 2003 的 IIS 伺服器上，則 Web Apps 是一種讓您的網站保持連線的低風險、低成本和低摩擦方式，而 Web Apps 移轉小幫手可以協助您自動進行移轉程序。</span><span class="sxs-lookup"><span data-stu-id="b8a06-106">If you are currently hosting your websites on an IIS server that is Windows Server 2003, Web Apps is a low-risk, low-cost, and low-friction way to keep your websites online, and Web Apps Migration Assistant can help automate the migration process for you.</span></span> 
> 
> 

<span data-ttu-id="b8a06-107">[Web Apps 移轉小幫手](https://www.movemetothecloud.net/) 可以分析您的 IIS 伺服器安裝、識別哪些網站可以移轉至 App Service、反白顯示任何無法移轉或平台上不支援的項目，然後將您的網站和相關聯的資料庫移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="b8a06-107">[Web Apps Migration Assistant](https://www.movemetothecloud.net/) can analyze your IIS server installation, identify which sites can be migrated to App Service, highlight any elements that cannot be migrated or are unsupported on the platform, and then migrate your websites and associated databases to Azure.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a><span data-ttu-id="b8a06-108">在相容性分析期間驗證的元素</span><span class="sxs-lookup"><span data-stu-id="b8a06-108">Elements Verified During Compatibility Analysis</span></span>
<span data-ttu-id="b8a06-109">移轉小幫手會建立整備報表，來識別導致無法從內部部署 IIS 成功移轉至 Azure App Service Web Apps 之相關問題或封鎖問題的任何潛在原因。</span><span class="sxs-lookup"><span data-stu-id="b8a06-109">The Migration Assistant creates a readiness report to identify any potential causes for concern or blocking issues which may prevent a successful migration from on-premises IIS to Azure App Service Web Apps.</span></span> <span data-ttu-id="b8a06-110">一些需要留意的重要項目：</span><span class="sxs-lookup"><span data-stu-id="b8a06-110">Some of the key items to be aware of are:</span></span>

* <span data-ttu-id="b8a06-111">連接埠繫結 - Web Apps 僅支援連接埠 80 (適用於 HTTP) 和連接埠 443 (適用於 HTTPS 流量)。</span><span class="sxs-lookup"><span data-stu-id="b8a06-111">Port Bindings – Web Apps only supports Port 80 for HTTP and Port 443 for HTTPS traffic.</span></span> <span data-ttu-id="b8a06-112">系統將會忽略不同的連接埠組態，並將流量路由傳送至 80 或 443。</span><span class="sxs-lookup"><span data-stu-id="b8a06-112">Different port configurations will be ignored and traffic will be routed to 80 or 443.</span></span> 
* <span data-ttu-id="b8a06-113">驗證 - Web Apps 預設支援匿名驗證以及應用程式所指定的表單驗證。</span><span class="sxs-lookup"><span data-stu-id="b8a06-113">Authentication – Web Apps supports Anonymous Authentication by default and Forms Authentication where specified by an application.</span></span> <span data-ttu-id="b8a06-114">只有與 Azure Active Directory 和 ADFS 整合，才能使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="b8a06-114">Windows Authentication can be used by integrating with Azure Active Directory and ADFS only.</span></span> <span data-ttu-id="b8a06-115">目前不支援所有其他形式的驗證 (例如基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="b8a06-115">All other forms of authentication - for example, Basic Authentication - are not currently supported.</span></span> 
* <span data-ttu-id="b8a06-116">全域組件快取 (GAC) - Web Apps 不支援 GAC。</span><span class="sxs-lookup"><span data-stu-id="b8a06-116">Global Assembly Cache (GAC) – The GAC is not supported in Web Apps.</span></span> <span data-ttu-id="b8a06-117">如果您的應用程式會參考您通常部署至 GAC 的組件，就必須部署至 Web Apps 上的應用程式 bin 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b8a06-117">If your application references assemblies which you usually deploy to the GAC, you will need to deploy to the application bin folder in Web Apps.</span></span> 
* <span data-ttu-id="b8a06-118">IIS5 相容性模式 - Web Apps 不支援此模式。</span><span class="sxs-lookup"><span data-stu-id="b8a06-118">IIS5 Compatibility Mode – This is not supported in Web Apps.</span></span> 
* <span data-ttu-id="b8a06-119">應用程式集區 - 在 Web Apps 中，每個網站及其子應用程式都在相同的應用程式集區中執行。</span><span class="sxs-lookup"><span data-stu-id="b8a06-119">Application Pools – In Web Apps, each site and its child applications run in the same application pool.</span></span> <span data-ttu-id="b8a06-120">如果您的網站上有多個利用多個應用程式集區的子應用程式，請將它們彙總到具有通用設定的單一應用程式集區，或將每個應用程式移轉至個別的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b8a06-120">If your site has multiple child applications utilizing multiple application pools, consolidate them to a single application pool with common settings or migrate each application to a separate web app.</span></span>
* <span data-ttu-id="b8a06-121">COM 元件 - Web Apps 不允許在平台上註冊 COM 元件。</span><span class="sxs-lookup"><span data-stu-id="b8a06-121">COM Components – Web Apps does not allow the registration of COM Components on the platform.</span></span> <span data-ttu-id="b8a06-122">如果您的網站或應用程式使用任何 COM 元件，您必須以 Managed 程式碼予以重新撰寫，並與網站或應用程式一起部署這些元件。</span><span class="sxs-lookup"><span data-stu-id="b8a06-122">If your websites or applications make use of any COM Components, you must rewrite them in managed code and deploy them with the website or application.</span></span>
* <span data-ttu-id="b8a06-123">ISAPI 擴充功能 - Web Apps 可支援使用 ISAPI 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b8a06-123">ISAPI Extensions – Web Apps can support the use of ISAPI Extensions.</span></span> <span data-ttu-id="b8a06-124">您需要執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="b8a06-124">You need to do the following:</span></span>
  
  * <span data-ttu-id="b8a06-125">使用您的 Web 應用程式部署 DLL</span><span class="sxs-lookup"><span data-stu-id="b8a06-125">deploy the DLLs with your web app</span></span> 
  * <span data-ttu-id="b8a06-126">使用 [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span><span class="sxs-lookup"><span data-stu-id="b8a06-126">register the DLLs using [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span></span>
  * <span data-ttu-id="b8a06-127">將 applicationHost.xdt 檔案與[這篇文章](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)的 "Allowing arbitrary ISAPI extensions to be loaded" (允許載入任意的 ISAPI 擴充功能) 一節所述的內容一起放在網站根目錄</span><span class="sxs-lookup"><span data-stu-id="b8a06-127">place an applicationHost.xdt file in the site root with the content outlined in "Allowing arbitrart ISAPI extensions to be loaded" [section of this article](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)</span></span> 
    
  
    
    <span data-ttu-id="b8a06-128">如需如何將 XML Document Transformations 使用於您的網站的範例，請參閱 [轉換您的 Microsoft Azure 網站](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b8a06-128">For more examples of how to use XML Document Transformations with your website, see [Transform your Microsoft Azure Web Site](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).</span></span>
* <span data-ttu-id="b8a06-129">不會移轉其他元件，例如 SharePoint、Front Page Server Extensions (FPSE)、FTP、SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="b8a06-129">Other components like SharePoint, front page server extensions (FPSE), FTP, SSL certificates will not be migrated.</span></span>

## <a name="how-to-use-the-web-apps-migration-assistant"></a><span data-ttu-id="b8a06-130">如何使用 Web Apps 移轉小幫手</span><span class="sxs-lookup"><span data-stu-id="b8a06-130">How to use the Web Apps Migration Assistant</span></span>
<span data-ttu-id="b8a06-131">本節將逐步說明如何移轉一些使用 SQL Server 資料庫並在內部部署 Windows Server 2003 R2 (IIS 6.0) 機器上執行之網站的範例：</span><span class="sxs-lookup"><span data-stu-id="b8a06-131">This section steps through an example to to migrate a few websites that use a SQL Server database and running on an on-premises Windows Server 2003 R2 (IIS 6.0) machine:</span></span>

1. <span data-ttu-id="b8a06-132">在 IIS 伺服器或您的用戶端機器上瀏覽至 [https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span><span class="sxs-lookup"><span data-stu-id="b8a06-132">On the IIS server or your client machine navigate to [https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. <span data-ttu-id="b8a06-133">按一下 [專用 IIS 伺服器]  按鈕，以安裝 Web Apps 移轉小幫手。</span><span class="sxs-lookup"><span data-stu-id="b8a06-133">Install Web Apps Migration Assistant by clicking on the **Dedicated IIS Server** button.</span></span> <span data-ttu-id="b8a06-134">在不久的將來會有更多的選項。</span><span class="sxs-lookup"><span data-stu-id="b8a06-134">More options will be options in the near future.</span></span> 
3. <span data-ttu-id="b8a06-135">按一下 [安裝工具]  按鈕，在電腦上安裝 Web Apps 移轉小幫手。</span><span class="sxs-lookup"><span data-stu-id="b8a06-135">Click the **Install Tool** button to install Web Apps Migration Assistant on your machine.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > <span data-ttu-id="b8a06-136">您也可以按一下 [下載以進行離線安裝] 下載 ZIP 檔案，以便在未連線到網際網路的伺服器上安裝。</span><span class="sxs-lookup"><span data-stu-id="b8a06-136">You can also click **Download for offline install** to download a ZIP file for installing on servers not connected to the internet.</span></span> <span data-ttu-id="b8a06-137">或者，您可以按一下 [上傳現有的移轉整備報告] ，這是一個進階選項，可處理您先前產生的現有移轉整備報告 (稍後說明)。</span><span class="sxs-lookup"><span data-stu-id="b8a06-137">Or, you can click **Upload an existing migration readiness report**, which is an advanced option to work with an existing migration readiness report that you previously generated (explained later).</span></span>
   > 
   > 
4. <span data-ttu-id="b8a06-138">在 [應用程式安裝] 畫面中，按一下 [安裝] 即可安裝在電腦上。</span><span class="sxs-lookup"><span data-stu-id="b8a06-138">In the **Application Install** screen, click **Install** to install on your machine.</span></span> <span data-ttu-id="b8a06-139">必要時也會安裝對應的相依項目，如 Web Deploy、DacFX 和 IIS。</span><span class="sxs-lookup"><span data-stu-id="b8a06-139">It will also install corresponding dependencies like Web Deploy, DacFX, and IIS, if needed.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   <span data-ttu-id="b8a06-140">安裝後，Web Apps 移轉小幫手會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="b8a06-140">Once installed, Web Apps Migration Assistant automatically starts.</span></span>
5. <span data-ttu-id="b8a06-141">選擇 [將網站與資料庫從遠端伺服器移轉到 Azure] 。</span><span class="sxs-lookup"><span data-stu-id="b8a06-141">Choose **Migrate sites and databases from a remote server to Azure**.</span></span> <span data-ttu-id="b8a06-142">輸入遠端伺服器的管理認證，並按一下 [繼續] 。</span><span class="sxs-lookup"><span data-stu-id="b8a06-142">Enter the administrative credentials for the remote server and click **Continue**.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   <span data-ttu-id="b8a06-143">您當然可以選擇從本機伺服器移轉。</span><span class="sxs-lookup"><span data-stu-id="b8a06-143">You can of course choose to migrate from the local server.</span></span> <span data-ttu-id="b8a06-144">當您想要從生產 IIS 伺服器移轉網站時，遠端選項很有用。</span><span class="sxs-lookup"><span data-stu-id="b8a06-144">The remote option is useful when you want to migrate websites from a production IIS server.</span></span>
   
   <span data-ttu-id="b8a06-145">此時移轉工具會檢查 IIS 伺服器的組態，例如網站、應用程式、應用程式集區和相依性，以識別可供移轉的候選網站。</span><span class="sxs-lookup"><span data-stu-id="b8a06-145">At this point the migration tool will inspect the your IIS server's configuration, such as Sites, Applications, Application Pools, and dependencies to identify candidate websites for migration.</span></span> 
6. <span data-ttu-id="b8a06-146">以下螢幕擷取畫面顯示三個網站 – **預設的網站**、**TimeTracker** 與 **CommerceNet4**。</span><span class="sxs-lookup"><span data-stu-id="b8a06-146">The screenshot below shows three websites – **Default Web Site**, **TimeTracker**, and **CommerceNet4**.</span></span> <span data-ttu-id="b8a06-147">全部都有我們想要移轉的相關資料庫。</span><span class="sxs-lookup"><span data-stu-id="b8a06-147">All of them have an associated database that we want to migrate.</span></span> <span data-ttu-id="b8a06-148">選取您想評估的所有網站，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b8a06-148">Select all of the sites you would like to assess and then click **Next**.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. <span data-ttu-id="b8a06-149">按一下 [上傳]  以上傳整備報表。</span><span class="sxs-lookup"><span data-stu-id="b8a06-149">Click **Upload** to upload the readiness report.</span></span> <span data-ttu-id="b8a06-150">如果您按一下 [在本機儲存檔案] ，您可以稍後再執行移轉工具，並如先前所述上傳儲存的整備報表。</span><span class="sxs-lookup"><span data-stu-id="b8a06-150">If you click **save file locally**, you can run the migration tool again later and upload the saved readiness report as noted earlier.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   <span data-ttu-id="b8a06-151">一旦上傳整備報表，Azure 就會執行整備分析並顯示結果。</span><span class="sxs-lookup"><span data-stu-id="b8a06-151">Once you upload the readiness report, Azure performs readiness analysis and shows you the results.</span></span> <span data-ttu-id="b8a06-152">讀取每個網站的評估詳細資料，並確定您在您繼續之前已了解或已處理所有的問題。</span><span class="sxs-lookup"><span data-stu-id="b8a06-152">Read the assessment details for each website and make sure that you understand or have addressed all issues before you proceed.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. <span data-ttu-id="b8a06-153">按一下 [開始移轉] 開始進行移轉。您現在會被重新導向至 Azure 來登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8a06-153">Click **Begin Migration** to start the migration.You will now be redirected to Azure to log into your account.</span></span> <span data-ttu-id="b8a06-154">請務必以具有作用中 Azure 訂用帳戶的帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="b8a06-154">It is important that you log in with an account that has an active Azure Subscription.</span></span> <span data-ttu-id="b8a06-155">如果您沒有 Azure 帳戶，可以在[這裡](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_)註冊免費試用。</span><span class="sxs-lookup"><span data-stu-id="b8a06-155">If you do not have an Azure account then you can sign up for a free trial [here](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_).</span></span> 
9. <span data-ttu-id="b8a06-156">選取要針對移轉的 Azure Web 應用程式和資料庫使用的租用戶帳戶、Azure 訂用帳戶和區域，然後按一下 [開始移轉] 。</span><span class="sxs-lookup"><span data-stu-id="b8a06-156">Select the tenant account, Azure subscription and region to use for your migrated Azure web apps and databases, and then click **Start Migration**.</span></span> <span data-ttu-id="b8a06-157">您可以選取稍後要移轉的網站。</span><span class="sxs-lookup"><span data-stu-id="b8a06-157">You can select the websites to migrate later.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. <span data-ttu-id="b8a06-158">在下一個畫面上，您可以變更預設移轉設定，例如：</span><span class="sxs-lookup"><span data-stu-id="b8a06-158">On the next screen you can make changes to the default migration settings, such as:</span></span>
    
    * <span data-ttu-id="b8a06-159">使用現有的 Azure SQL Database 或建立新的 Azure SQL Database，並設定其認證</span><span class="sxs-lookup"><span data-stu-id="b8a06-159">use an existing Azure SQL Database or create a new Azure SQL Database, and configure its credentials</span></span>
    * <span data-ttu-id="b8a06-160">選取要移轉的網站</span><span class="sxs-lookup"><span data-stu-id="b8a06-160">select the websites to migrate</span></span>
    * <span data-ttu-id="b8a06-161">定義 Azure Web 應用程式及其連結的 SQL 資料庫的名稱</span><span class="sxs-lookup"><span data-stu-id="b8a06-161">define names for the Azure web apps and their linked SQL databases</span></span>
    * <span data-ttu-id="b8a06-162">自訂全域設定和網站層級設定</span><span class="sxs-lookup"><span data-stu-id="b8a06-162">customize the global settings and site-level settings</span></span>
    
    <span data-ttu-id="b8a06-163">以下螢幕擷取畫面顯示針對以預設設定移轉而選取的所有網站。</span><span class="sxs-lookup"><span data-stu-id="b8a06-163">The screenshot below shows all the websites selected for migration with the default settings.</span></span>
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > <span data-ttu-id="b8a06-164">自訂設定中的 [啟用 Azure Active Directory] 核取方塊可整合 Azure Web 應用程式與 [Azure Active Directory](../active-directory/active-directory-whatis.md) (預設目錄)。</span><span class="sxs-lookup"><span data-stu-id="b8a06-164">the **Enable Azure Active Directory** checkbox in custom settings integrates the Azure web app with [Azure Active Directory](../active-directory/active-directory-whatis.md) (the **Default Directory**).</span></span> <span data-ttu-id="b8a06-165">如需同步處理 Azure Active Directory 與內部部署 Active Directory 的詳細資訊，請參閱[目錄整合](http://msdn.microsoft.com/library/jj573653)。</span><span class="sxs-lookup"><span data-stu-id="b8a06-165">For more information on syncing Azure Active Directory with your on-premises Active Directory, see [Directory integration](http://msdn.microsoft.com/library/jj573653).</span></span>
    > 
    > 
11. <span data-ttu-id="b8a06-166">進行所有必要的變更後，按一下 [建立]  即可啟動移轉程序。</span><span class="sxs-lookup"><span data-stu-id="b8a06-166">Once you make all the desired changes, click **Create** to start the migration process.</span></span> <span data-ttu-id="b8a06-167">移轉工具會建立 Azure SQL Database 和 Azure Web 應用程式，然後發行網站內容和資料庫。</span><span class="sxs-lookup"><span data-stu-id="b8a06-167">The migration tool will create the Azure SQL Database and Azure web app, and then publish the website content and databases.</span></span> <span data-ttu-id="b8a06-168">移轉進度會清楚地顯示在移轉工具中，而您最後將看到摘要畫面，詳述移轉的網站、移轉是否成功、新建立的 Azure Web 應用程式連結。</span><span class="sxs-lookup"><span data-stu-id="b8a06-168">The migration progress is clearly shown in the migration tool, and you will see a summary screen at the end, which details the sites migrated, whether they were successful, links to the newly-created Azure web apps.</span></span> 
    
    <span data-ttu-id="b8a06-169">如果在移轉期間發生任何錯誤，移轉工具會清楚指出失敗並回復所做的變更。</span><span class="sxs-lookup"><span data-stu-id="b8a06-169">If any error occurs during migration, the migration tool will clearly indicate the failure and rollback the changes.</span></span> <span data-ttu-id="b8a06-170">您也可以按一下 [傳送錯誤報告]  按鈕，將錯誤報告 (包含擷取的失敗的呼叫堆疊和建置訊息內文) 直接傳送給工程小組。</span><span class="sxs-lookup"><span data-stu-id="b8a06-170">You will also be able to send the error report directly to the engineering team by clicking the **Send Error Report** button, with the captured failure call stack and build message body.</span></span> 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    <span data-ttu-id="b8a06-171">如果移轉成功時沒有錯誤，您也可以按一下 [提供意見]  按鈕，直接提供任何意見。</span><span class="sxs-lookup"><span data-stu-id="b8a06-171">If migrate succeeds without errors, you can also click the **Give Feedback** button to provide any feedback directly.</span></span> 
12. <span data-ttu-id="b8a06-172">按一下 Azure Web 應用程式的連結，確認已成功移轉。</span><span class="sxs-lookup"><span data-stu-id="b8a06-172">Click the links to the Azure web apps and verify that the migration has succeeded.</span></span>
13. <span data-ttu-id="b8a06-173">您現在可以管理 Azure App Service 中移轉的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b8a06-173">You can now manage the migrated web apps in Azure App Service.</span></span> <span data-ttu-id="b8a06-174">若要執行這個動作，請登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b8a06-174">To do this, log into the [Azure Portal](https://portal.azure.com).</span></span>
14. <span data-ttu-id="b8a06-175">在 Azure 入口網站中，開啟 Web Apps 分頁，以查看您移轉的網站 (顯示為 Web 應用程式)，然後按一下任一個網站，以便開始管理 Web 應用程式，例如，設定連續發行、建立備份、自動調整，以及監視使用量或效能。</span><span class="sxs-lookup"><span data-stu-id="b8a06-175">In the Azure Portal, open the Web Apps blade to see your migrated websites (shown as web apps), then click on any one of them to start managing the web app, such as configuring continuous publishing, creating backups, autoscaling, and monitoring usage or performance.</span></span>
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> <span data-ttu-id="b8a06-176">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b8a06-176">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b8a06-177">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="b8a06-177">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="b8a06-178">變更的項目</span><span class="sxs-lookup"><span data-stu-id="b8a06-178">What's changed</span></span>
* <span data-ttu-id="b8a06-179">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b8a06-179">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

