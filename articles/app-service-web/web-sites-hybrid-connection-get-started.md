---
title: "在 Azure App Service 中使用混合式連線存取內部部署資源"
description: "在 Azure App Service 中的 Web 應用程式和使用靜態 TCP 連接埠的內部部署資源之間建立連線"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: fbd22e6e285c5ddaef2a473671d4a06a97384b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="1807c-103">在 Azure App Service 中使用混合式連線存取內部部署資源</span><span class="sxs-lookup"><span data-stu-id="1807c-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="1807c-104">您可以將 Azure App Service 應用程式連接到任何使用靜態 TCP 連接埠 (例如 SQL Server、MySQL、HTTP Web API 和大部分自訂 Web 服務) 的內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="1807c-104">You can connect an Azure App Service app to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="1807c-105">本文章示範如何在 App Service 和內部部署的 SQL Server 資料庫之間建立混合式連線。</span><span class="sxs-lookup"><span data-stu-id="1807c-105">This article shows you how to create a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="1807c-106">「混合式連線」功能的 Web Apps 部分僅適用於 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1807c-106">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="1807c-107">若要在 BizTalk 服務中建立連線，請參閱 [混合式連線](http://go.microsoft.com/fwlink/p/?LinkID=397274)。</span><span class="sxs-lookup"><span data-stu-id="1807c-107">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="1807c-108">此內容也適用於 Azure App Service 中的 Mobile Apps。</span><span class="sxs-lookup"><span data-stu-id="1807c-108">This content also applies to Mobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1807c-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="1807c-109">Prerequisites</span></span>
* <span data-ttu-id="1807c-110">Azure 訂閱。</span><span class="sxs-lookup"><span data-stu-id="1807c-110">An Azure subscription.</span></span> <span data-ttu-id="1807c-111">若要取得免費訂閱，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1807c-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="1807c-112">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1807c-112">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1807c-113">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="1807c-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="1807c-114">若要透過混合式連線使用內部部署 SQL Server 或 SQL Server Express 資料庫，必須在靜態連接埠上啟用 TCP/IP。</span><span class="sxs-lookup"><span data-stu-id="1807c-114">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="1807c-115">建議在 SQL Server 上使用預設執行個體，因為其使用靜態連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="1807c-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="1807c-116">如需安裝及設定 SQL Server Express 以搭配混合式連線使用的相關資訊，請參閱 [使用混合式連線從 Azure 網站連線到內部部署 SQL Server](http://go.microsoft.com/fwlink/?LinkID=397979)。</span><span class="sxs-lookup"><span data-stu-id="1807c-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="1807c-117">本文稍後將會針對安裝內部部署混合式連線管理員代理程式的電腦加以說明：</span><span class="sxs-lookup"><span data-stu-id="1807c-117">The computer on which you install the on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="1807c-118">必須能夠透過連接埠 5671 連線到 Azure</span><span class="sxs-lookup"><span data-stu-id="1807c-118">Must be able to connect to Azure over port 5671</span></span>
  * <span data-ttu-id="1807c-119">必須能夠連繫內部部署資源的 *hostname*上：*portnumber* 。</span><span class="sxs-lookup"><span data-stu-id="1807c-119">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="1807c-120">本文中的步驟假設您使用將主控內部部署混合式連線代理程式之電腦中的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1807c-120">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="1807c-121">在 Azure 入口網站中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1807c-121">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="1807c-122">如果您已在 Azure 入口網站中建立本教學課程要使用的 Web 應用程式或行動應用程式後端，則您可以直接跳到 [建立混合式連線和 BizTalk 服務](#CreateHC) ，並從那裡開始操作。</span><span class="sxs-lookup"><span data-stu-id="1807c-122">If you have already created a web app or Mobile App backend in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="1807c-123">在 [Azure 入口網站](https://portal.azure.com)左上角，依序按一下 [新增] > [Web + 行動] > [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1807c-123">In the upper left corner of the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![新 Web 應用程式][NewWebsite]
2. <span data-ttu-id="1807c-125">在 [Web 應用程式] 刀鋒視窗上，提供 URL，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1807c-125">On the **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="1807c-127">經過一段時間之後，Web 應用程式會建立，並顯示它的 Web 應用程式分頁。</span><span class="sxs-lookup"><span data-stu-id="1807c-127">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="1807c-128">此分頁是垂直捲動的儀表板，可供您管理網站。</span><span class="sxs-lookup"><span data-stu-id="1807c-128">The blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website running][WebSiteRunningBlade]
4. <span data-ttu-id="1807c-130">若要確認網站是否已上線啟用，您可以按一下 [瀏覽]  圖示以顯示預設頁面。</span><span class="sxs-lookup"><span data-stu-id="1807c-130">To verify the site is live, you can click the **Browse** icon to display the default page.</span></span>
   
    ![按一下 [瀏覽] 以查看您的 Web 應用程式][Browse]
   
    ![預設 Web 應用程式頁面][DefaultWebSitePage]

<span data-ttu-id="1807c-133">接著，您將為 Web 應用程式建立混合式連線和 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="1807c-133">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="1807c-134">建立混合式連線和 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="1807c-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="1807c-135">在您的 [Web 應用程式] 刀鋒視窗中按一下 [所有設定] > [網路] > [設定混合式連接端點]。</span><span class="sxs-lookup"><span data-stu-id="1807c-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![混合式連線][CreateHCHCIcon]
2. <span data-ttu-id="1807c-137">在 [混合式連線] 分頁上，按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="1807c-137">On the Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="1807c-138">[新增混合式連線]  分頁隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="1807c-138">The **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="1807c-139">由於這是您的第一個混合式連線，因此會預先選取 [新增混合式連線] 選項，並為您開啟 [建立混合式連線] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1807c-139">Since this is your first hybrid connection, the **New hybrid connection** option is preselected, and the **Create hybrid connection** blade opens for you.</span></span>
   
    ![Create a hybrid connection][TwinCreateHCBlades]
   
    <span data-ttu-id="1807c-141">在 [建立混合式連線分頁] 上：</span><span class="sxs-lookup"><span data-stu-id="1807c-141">On the **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="1807c-142">在 [名稱] 中，提供連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="1807c-142">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="1807c-143">在 [主機名稱] 中，輸入主控資源的內部部署電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="1807c-143">For **Hostname**, enter the name of the on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="1807c-144">在 [連接埠] 中，輸入內部部署資源使用的連接埠號碼 (若是 SQL Server 預設執行個體，請輸入 1433)。</span><span class="sxs-lookup"><span data-stu-id="1807c-144">For **Port**, enter the port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="1807c-145">按一下 [Biz Talk 服務] </span><span class="sxs-lookup"><span data-stu-id="1807c-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="1807c-146">[建立 BizTalk 服務]  分頁隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="1807c-146">The **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="1807c-147">輸入 BizTalk 服務的名稱，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1807c-147">Enter a name for the BizTalk service, and then click **OK**.</span></span>
   
    ![Create BizTalk service][CreateHCCreateBTS]
   
    <span data-ttu-id="1807c-149">[建立 BizTalk 服務] 刀鋒視窗隨即關閉，而您會回到 [建立混合式連線] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1807c-149">The **Create BizTalk Service** blade closes and you are returned to the **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="1807c-150">在 [建立混合式連線] 分頁上，按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1807c-150">On the Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Click OK][CreateBTScomplete]
6. <span data-ttu-id="1807c-152">當程序完成時，入口網站中的通知區域會通知您已成功建立連線。</span><span class="sxs-lookup"><span data-stu-id="1807c-152">When the process completes, the notifications area in the Portal informs you that the connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="1807c-153">在 Web 應用程式的刀鋒視窗上，[混合式連線]  圖示現在會顯示已建立 1 個混合式連線。</span><span class="sxs-lookup"><span data-stu-id="1807c-153">On the web app's blade, the **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="1807c-155">至此，您已完成雲端混合式連線基礎結構的重要部分。</span><span class="sxs-lookup"><span data-stu-id="1807c-155">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="1807c-156">接下來，您將建立對應的內部部署部分。</span><span class="sxs-lookup"><span data-stu-id="1807c-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="1807c-157">安裝內部部署混合式連線管理員以完成連線</span><span class="sxs-lookup"><span data-stu-id="1807c-157">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
1. <span data-ttu-id="1807c-158">在 [Web 應用程式] 刀鋒視窗中按一下 [所有設定] > [網路] > [設定混合式連接端點]。</span><span class="sxs-lookup"><span data-stu-id="1807c-158">On the web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Hybrid connections icon][HCIcon]
2. <span data-ttu-id="1807c-160">在 [混合式連線] 刀鋒視窗上，最近新增之端點的 [狀態] 欄會顯示為 [未連線]。</span><span class="sxs-lookup"><span data-stu-id="1807c-160">On the **Hybrid connections** blade, the **Status** column for the recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="1807c-161">請按一下連線加以設定。</span><span class="sxs-lookup"><span data-stu-id="1807c-161">Click the connection to configure it.</span></span>
   
    ![Not connected][NotConnected]
   
    <span data-ttu-id="1807c-163">[混合式連線] 分頁隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="1807c-163">The Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="1807c-165">在此分頁上，按一下 [Listener Setup] 。</span><span class="sxs-lookup"><span data-stu-id="1807c-165">On the blade, click **Listener Setup**.</span></span>
   
    ![Click Listener Setup][ClickListenerSetup]
4. <span data-ttu-id="1807c-167">[混合式連線屬性]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="1807c-167">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="1807c-168">在 [內部部署混合式連線管理員] 下，選擇 [按一下此處進行安裝]。</span><span class="sxs-lookup"><span data-stu-id="1807c-168">Under **On-premises Hybrid Connection Manager**, choose **Click here to install**.</span></span>
   
    ![Click here to install][ClickToInstallHCM]
5. <span data-ttu-id="1807c-170">在 [應用程式執行] 安全性警告對話方塊中，選擇 [執行]  以繼續作業。</span><span class="sxs-lookup"><span data-stu-id="1807c-170">In the Application Run security warning dialog, choose **Run** to continue.</span></span>
   
    ![Choose Run to continue][ApplicationRunWarning]
6. <span data-ttu-id="1807c-172">在 [使用者帳戶控制] 對話方塊中，選擇 [是]。</span><span class="sxs-lookup"><span data-stu-id="1807c-172">In the **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Choose Yes][UAC]
7. <span data-ttu-id="1807c-174">系統會為您下載並安裝混合式連線管理員。</span><span class="sxs-lookup"><span data-stu-id="1807c-174">The Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![安裝][HCMInstalling]
8. <span data-ttu-id="1807c-176">安裝完成後，請按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="1807c-176">When the install completes, click **Close**.</span></span>
   
    ![Click Close][HCMInstallComplete]
   
    <span data-ttu-id="1807c-178">在 [混合式連線] 刀鋒視窗上，[狀態] 欄此時會顯示為 [未連線]。</span><span class="sxs-lookup"><span data-stu-id="1807c-178">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status][HCStatusConnected]

<span data-ttu-id="1807c-180">現在，您已完成混合式連線基礎結構，您可以使用它來建立混合式應用程式。</span><span class="sxs-lookup"><span data-stu-id="1807c-180">Now that the hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="1807c-181">下列各節示範如何搭配 Mobile Apps .NET 後端專案使用混合式連線。</span><span class="sxs-lookup"><span data-stu-id="1807c-181">The following sections show you how to use a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a><span data-ttu-id="1807c-182">設定行動應用程式 .NET 後端專案以連線到 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="1807c-182">Configure the Mobile App .NET backend project to connect to the SQL Server database</span></span>
<span data-ttu-id="1807c-183">在 App Service 中，Mobile Apps .NET 後端專案只是一個已安裝並初始化其他 Mobile Apps SDK 的 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1807c-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="1807c-184">若要使用 Web 應用程式做為 Mobile Apps 後端，您必須 [下載並初始化 Mobile Apps .NET 後端 SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk)。</span><span class="sxs-lookup"><span data-stu-id="1807c-184">To use your web app as a Mobile Apps backend, you must [download and initialize the Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="1807c-185">針對 Mobile Apps，您也需要定義內部部署資料庫的連接字串與修改後端，以使用此連線。</span><span class="sxs-lookup"><span data-stu-id="1807c-185">For Mobile Apps, you also need to define a connection string for the on-premises database and modify the backend to use this connection.</span></span> 

1. <span data-ttu-id="1807c-186">在 [Visual Studio 方案總管] 中開啟您的行動應用程式 .NET 後端的 Web.config 檔案，並找出 **connectionStrings** 區段，然後新增會指向內部部署 SQL Server 資料庫的 SqlClient 項目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1807c-186">In Solution Explorer in Visual Studio, open the Web.config file for your Mobile App .NET backend, locate the **connectionStrings** section, add a new SqlClient entry like the following, which points to the on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="1807c-187">請記得將此字串中的 `<**secure_password**>` 取代為您為 HybridConnectionLogin 建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="1807c-187">Remember to replace `<**secure_password**>` in this string with the password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="1807c-188">在 Visual Studio 中按一下 [儲存]  ，以儲存 Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="1807c-188">Click **Save** in Visual Studio to save the Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1807c-189">在本機電腦上執行時，會使用此連線設定。</span><span class="sxs-lookup"><span data-stu-id="1807c-189">This connection setting is used when running on the local computer.</span></span> <span data-ttu-id="1807c-190">在 Azure 中執行時，則會以入口網站中所定義的連線設定覆寫這個設定。</span><span class="sxs-lookup"><span data-stu-id="1807c-190">When running in Azure, this setting is overriden by the connection setting defined in the portal.</span></span>
   > 
   > 
3. <span data-ttu-id="1807c-191">展開 **Models** 資料夾，然後開啟以 *Context.cs*結尾的資料模型檔案。</span><span class="sxs-lookup"><span data-stu-id="1807c-191">Expand the **Models** folder and open the data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="1807c-192">修改 **DbContext** 執行個體建構函式，以將 `OnPremisesDBConnection` 值傳遞至類似下列程式碼片段的基底 **DbContext** 建構函式：</span><span class="sxs-lookup"><span data-stu-id="1807c-192">Modify the **DbContext** instance constructor to pass the value `OnPremisesDBConnection` to the base **DbContext** constructor, similar to the following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="1807c-193">現在，服務將會使用新的 SQL Server 資料庫連線。</span><span class="sxs-lookup"><span data-stu-id="1807c-193">The service will now use the new connection to the SQL Server database.</span></span>

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a><span data-ttu-id="1807c-194">更新行動應用程式後端，以使用內部部署連接字串</span><span class="sxs-lookup"><span data-stu-id="1807c-194">Update the Mobile App backend to use the on-premises connection string</span></span>
<span data-ttu-id="1807c-195">接下來，您必須為這個新的連接字串新增應用程式設定，以便能夠從 Azure 使用。</span><span class="sxs-lookup"><span data-stu-id="1807c-195">Next, you need to add an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="1807c-196">回到 [Azure 入口網站](https://portal.azure.com)，在行動應用程式的 Web 應用程式後端程式碼中，按一下 [所有設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="1807c-196">Back in the [Azure portal](https://portal.azure.com) in the web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="1807c-197">在 [Web 應用程式設定] 刀鋒視窗中，向下捲動至 [連接字串]，然後以 `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>` 之類的值新增名稱為 `OnPremisesDBConnection` 的新 **SQL Server** 連接字串。</span><span class="sxs-lookup"><span data-stu-id="1807c-197">In the **Web app settings** blade, scroll down to **Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="1807c-198">將 `<**secure_password**>` 替換為您內部部署資料庫的安全密碼。</span><span class="sxs-lookup"><span data-stu-id="1807c-198">Replace `<**secure_password**>` with the secure password for your on-premises database.</span></span>
   
    ![Connection string for on-premises database](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="1807c-200">按下 [ **儲存** ]，以儲存您剛剛建立的混合式連線和連接字串。</span><span class="sxs-lookup"><span data-stu-id="1807c-200">Press **Save** to save the hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="1807c-201">現在可以重新發佈伺服器專案，並測試與現有的 Mobile Apps 用戶端之間的新連線。</span><span class="sxs-lookup"><span data-stu-id="1807c-201">At this point you can republish the server project and test the new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="1807c-202">將會使用混合式連線，讀取內部部署資料庫中的資料並寫入。</span><span class="sxs-lookup"><span data-stu-id="1807c-202">Data will be read from and written to the on-premises database using the hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="1807c-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1807c-203">Next Steps</span></span>
* <span data-ttu-id="1807c-204">如需建立使用混合式連線的 ASP.NET Web 應用程式相關資訊，請參閱 [使用混合式連線從 Azure 網站連線到內部部署 SQL Server](http://go.microsoft.com/fwlink/?LinkID=397979)。</span><span class="sxs-lookup"><span data-stu-id="1807c-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="1807c-205">其他資源</span><span class="sxs-lookup"><span data-stu-id="1807c-205">Additional Resources</span></span>
[<span data-ttu-id="1807c-206">混合式連線概觀</span><span class="sxs-lookup"><span data-stu-id="1807c-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="1807c-207">Josh Twist 介紹混合式連線 (第 9 頻道視訊)</span><span class="sxs-lookup"><span data-stu-id="1807c-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="1807c-208">混合式連線網站</span><span class="sxs-lookup"><span data-stu-id="1807c-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="1807c-209">BizTalk 服務：儀表板、監視器、調整、設定和混合式連線索引標籤</span><span class="sxs-lookup"><span data-stu-id="1807c-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="1807c-210">透過絕佳的應用程式可攜性建置真實的混合式雲端 (第 9 頻道視訊)</span><span class="sxs-lookup"><span data-stu-id="1807c-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="1807c-211">使用混合式連線從 Azure 行動服務連線到內部部署 SQL Server (第 9 頻道視訊)</span><span class="sxs-lookup"><span data-stu-id="1807c-211">Connect to an on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="1807c-212">變更的項目</span><span class="sxs-lookup"><span data-stu-id="1807c-212">What's changed</span></span>
* <span data-ttu-id="1807c-213">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="1807c-213">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
