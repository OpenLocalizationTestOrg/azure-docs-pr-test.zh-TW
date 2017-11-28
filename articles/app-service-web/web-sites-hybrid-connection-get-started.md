---
title: "使用 Azure App Service 中的混合式連線的 aaaAccess 在內部部署資源"
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
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="24c42-103">在 Azure App Service 中使用混合式連線存取內部部署資源</span><span class="sxs-lookup"><span data-stu-id="24c42-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="24c42-104">您可以連接會使用靜態 TCP 連接埠，例如 SQL Server、 MySQL、 HTTP 的 Web Api 和大部分的自訂 Web 服務的 Azure App Service 應用程式 tooany 在內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="24c42-104">You can connect an Azure App Service app tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="24c42-105">本文章將示範如何 toocreate 應用程式服務與內部部署 SQL Server 資料庫之間的混合式連接。</span><span class="sxs-lookup"><span data-stu-id="24c42-105">This article shows you how toocreate a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="24c42-106">hello 混合式連線功能 hello Web 應用程式部分是只用於 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="24c42-106">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="24c42-107">請參閱 toocreate BizTalk 服務中的連接[混合式連線](http://go.microsoft.com/fwlink/p/?LinkID=397274)。</span><span class="sxs-lookup"><span data-stu-id="24c42-107">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="24c42-108">此內容也適用於 Azure App Service 中的 tooMobile 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24c42-108">This content also applies tooMobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="24c42-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="24c42-109">Prerequisites</span></span>
* <span data-ttu-id="24c42-110">Azure 訂閱。</span><span class="sxs-lookup"><span data-stu-id="24c42-110">An Azure subscription.</span></span> <span data-ttu-id="24c42-111">若要取得免費訂閱，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="24c42-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="24c42-112">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="24c42-112">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="24c42-113">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="24c42-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="24c42-114">toouse 在內部部署 SQL Server 或 SQL Server Express 的混合式連接的資料庫，TCP/IP 需要 toobe 靜態連接埠上啟用。</span><span class="sxs-lookup"><span data-stu-id="24c42-114">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="24c42-115">建議在 SQL Server 上使用預設執行個體，因為其使用靜態連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="24c42-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="24c42-116">如需安裝及設定 SQL Server Express 用於混合式連接的資訊，請參閱[連接 tooan 內部部署 SQL Server 從使用混合式連線的 Azure 網站](http://go.microsoft.com/fwlink/?LinkID=397979)。</span><span class="sxs-lookup"><span data-stu-id="24c42-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="24c42-117">您安裝 hello 在內部部署混合式連線管理員說明的代理程式 」 在本文稍後的 hello 電腦：</span><span class="sxs-lookup"><span data-stu-id="24c42-117">hello computer on which you install hello on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="24c42-118">透過連接埠 5671 必須能夠 tooconnect tooAzure</span><span class="sxs-lookup"><span data-stu-id="24c42-118">Must be able tooconnect tooAzure over port 5671</span></span>
  * <span data-ttu-id="24c42-119">必須是能夠 tooreach hello *hostname*:*portnumber*的內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="24c42-119">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="24c42-120">本文章中的 hello 步驟假設您使用 hello 瀏覽器從 hello 主控 hello 在內部部署混合式連接的代理程式的電腦。</span><span class="sxs-lookup"><span data-stu-id="24c42-120">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="24c42-121">在 hello Azure 入口網站中建立 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="24c42-121">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="24c42-122">如果您已經在 hello 的 toouse 本教學課程中的 Azure 入口網站中建立的 web 應用程式或行動裝置應用程式後端，您可以向前跳過[建立混合式連接和 BizTalk 服務](#CreateHC)並從該處開始。</span><span class="sxs-lookup"><span data-stu-id="24c42-122">If you have already created a web app or Mobile App backend in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="24c42-123">Hello 左上角的 hello [Azure 入口網站](https://portal.azure.com)，按一下 **新增** > **Web + 行動** > **Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="24c42-123">In hello upper left corner of hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![新 Web 應用程式][NewWebsite]
2. <span data-ttu-id="24c42-125">在 hello **Web 應用程式**刀鋒視窗中，提供 URL，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="24c42-125">On hello **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="24c42-127">在幾分鐘之後, 建立 hello web 應用程式和其 web 應用程式 刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="24c42-127">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="24c42-128">hello 刀鋒視窗中是可垂直捲動的儀表板可讓您管理您的網站。</span><span class="sxs-lookup"><span data-stu-id="24c42-128">hello blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website running][WebSiteRunningBlade]
4. <span data-ttu-id="24c42-130">是即時的 tooverify hello 站台，您可以按一下 hello**瀏覽**圖示 toodisplay hello 預設頁面。</span><span class="sxs-lookup"><span data-stu-id="24c42-130">tooverify hello site is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>
   
    ![按一下瀏覽 toosee 您 web 應用程式][Browse]
   
    ![預設 Web 應用程式頁面][DefaultWebSitePage]

<span data-ttu-id="24c42-133">接下來，您將建立混合式連接和 hello web 應用程式的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="24c42-133">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="24c42-134">建立混合式連線和 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="24c42-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="24c42-135">在您的 [Web 應用程式] 刀鋒視窗中按一下 [所有設定] > [網路] > [設定混合式連接端點]。</span><span class="sxs-lookup"><span data-stu-id="24c42-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![混合式連線][CreateHCHCIcon]
2. <span data-ttu-id="24c42-137">在 hello 混合式連線刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="24c42-137">On hello Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="24c42-138">hello**新增混合式連接**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="24c42-138">hello **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="24c42-139">由於這是您第一次的混合式連線，hello**新混合式連接**選項預設選取與 hello**建立混合式連接**刀鋒視窗會為您開啟。</span><span class="sxs-lookup"><span data-stu-id="24c42-139">Since this is your first hybrid connection, hello **New hybrid connection** option is preselected, and hello **Create hybrid connection** blade opens for you.</span></span>
   
    ![Create a hybrid connection][TwinCreateHCBlades]
   
    <span data-ttu-id="24c42-141">在 hello**建立混合式連線刀鋒視窗**:</span><span class="sxs-lookup"><span data-stu-id="24c42-141">On hello **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="24c42-142">如**名稱**，提供 hello 連接的名稱。</span><span class="sxs-lookup"><span data-stu-id="24c42-142">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="24c42-143">如**Hostname**，輸入 hello hello 在內部部署電腦裝載您的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="24c42-143">For **Hostname**, enter hello name of hello on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="24c42-144">如**連接埠**，輸入您在內部部署的資源使用 (SQL Server 預設執行個體 1433) 的 hello 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="24c42-144">For **Port**, enter hello port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="24c42-145">按一下 [Biz Talk 服務] </span><span class="sxs-lookup"><span data-stu-id="24c42-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="24c42-146">hello**建立 BizTalk 服務**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="24c42-146">hello **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="24c42-147">輸入 hello BizTalk 服務的名稱，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="24c42-147">Enter a name for hello BizTalk service, and then click **OK**.</span></span>
   
    ![Create BizTalk service][CreateHCCreateBTS]
   
    <span data-ttu-id="24c42-149">hello**建立 BizTalk 服務**關閉刀鋒視窗中，您將返回 toohello**建立混合式連接**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="24c42-149">hello **Create BizTalk Service** blade closes and you are returned toohello **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="24c42-150">在 hello 建立混合式連線刀鋒視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="24c42-150">On hello Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Click OK][CreateBTScomplete]
6. <span data-ttu-id="24c42-152">Hello 程序完成時，hello 入口網站中的 hello 通知區域會通知您已成功建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="24c42-152">When hello process completes, hello notifications area in hello Portal informs you that hello connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="24c42-153">Hello web 應用程式的刀鋒視窗中，在 hello**混合式連線**圖示現在會顯示已建立 1 的混合式連接。</span><span class="sxs-lookup"><span data-stu-id="24c42-153">On hello web app's blade, hello **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="24c42-155">此時，您已完成 hello 雲端混合式連接的基礎結構的重要部分。</span><span class="sxs-lookup"><span data-stu-id="24c42-155">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="24c42-156">接下來，您將建立對應的內部部署部分。</span><span class="sxs-lookup"><span data-stu-id="24c42-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="24c42-157">安裝 hello 在內部部署混合式連線管理員 toocomplete hello 連線</span><span class="sxs-lookup"><span data-stu-id="24c42-157">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
1. <span data-ttu-id="24c42-158">在 hello web 應用程式的刀鋒視窗中，按一下 **所有設定** > **網路** > **設定您的混合式連接端點**。</span><span class="sxs-lookup"><span data-stu-id="24c42-158">On hello web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Hybrid connections icon][HCIcon]
2. <span data-ttu-id="24c42-160">在 hello**混合式連線**刀鋒視窗，hello**狀態**hello 的資料行最近新增端點顯示**未連接**。</span><span class="sxs-lookup"><span data-stu-id="24c42-160">On hello **Hybrid connections** blade, hello **Status** column for hello recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="24c42-161">按一下 hello 連接 tooconfigure 它。</span><span class="sxs-lookup"><span data-stu-id="24c42-161">Click hello connection tooconfigure it.</span></span>
   
    ![Not connected][NotConnected]
   
    <span data-ttu-id="24c42-163">hello 混合式連線刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="24c42-163">hello Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="24c42-165">在 hello 刀鋒視窗中，按一下 **接聽程式的安裝程式**。</span><span class="sxs-lookup"><span data-stu-id="24c42-165">On hello blade, click **Listener Setup**.</span></span>
   
    ![Click Listener Setup][ClickListenerSetup]
4. <span data-ttu-id="24c42-167">hello**混合式連接屬性**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="24c42-167">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="24c42-168">在下**在內部部署混合式連線管理員**，選擇**按一下這裡 tooinstall**。</span><span class="sxs-lookup"><span data-stu-id="24c42-168">Under **On-premises Hybrid Connection Manager**, choose **Click here tooinstall**.</span></span>
   
    ![按一下這裡 tooinstall][ClickToInstallHCM]
5. <span data-ttu-id="24c42-170">在 hello 應用程式執行安全性警告對話方塊中，選擇 **執行**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="24c42-170">In hello Application Run security warning dialog, choose **Run** toocontinue.</span></span>
   
    ![選擇執行 toocontinue][ApplicationRunWarning]
6. <span data-ttu-id="24c42-172">在 [hello**使用者帳戶控制**] 對話方塊中，選擇**是**。</span><span class="sxs-lookup"><span data-stu-id="24c42-172">In hello **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Choose Yes][UAC]
7. <span data-ttu-id="24c42-174">下載並安裝您 hello 混合式連線管理員時。</span><span class="sxs-lookup"><span data-stu-id="24c42-174">hello Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![安裝][HCMInstalling]
8. <span data-ttu-id="24c42-176">Hello 安裝完成時，按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="24c42-176">When hello install completes, click **Close**.</span></span>
   
    ![Click Close][HCMInstallComplete]
   
    <span data-ttu-id="24c42-178">在 hello**混合式連線**刀鋒視窗，hello**狀態**資料行現在會顯示**已連接**。</span><span class="sxs-lookup"><span data-stu-id="24c42-178">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status][HCStatusConnected]

<span data-ttu-id="24c42-180">現在該 hello 混合式連接基礎結構已完成，您可以建立混合式應用程式使用它。</span><span class="sxs-lookup"><span data-stu-id="24c42-180">Now that hello hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="24c42-181">hello 下列各節說明您如何 toouse 與行動應用程式的.NET 後端專案的混合式連接。</span><span class="sxs-lookup"><span data-stu-id="24c42-181">hello following sections show you how toouse a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a><span data-ttu-id="24c42-182">設定 hello 行動應用程式的.NET 後端專案 tooconnect toohello SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="24c42-182">Configure hello Mobile App .NET backend project tooconnect toohello SQL Server database</span></span>
<span data-ttu-id="24c42-183">在 App Service 中，Mobile Apps .NET 後端專案只是一個已安裝並初始化其他 Mobile Apps SDK 的 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24c42-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="24c42-184">toouse 的行動應用程式後端 web 應用程式，您必須[下載，並初始化 hello 行動應用程式的.NET 後端 SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk)。</span><span class="sxs-lookup"><span data-stu-id="24c42-184">toouse your web app as a Mobile Apps backend, you must [download and initialize hello Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="24c42-185">針對行動裝置應用程式，您也需要 toodefine 連接字串 hello 在內部部署資料庫，並修改 hello 後端 toouse 此連線。</span><span class="sxs-lookup"><span data-stu-id="24c42-185">For Mobile Apps, you also need toodefine a connection string for hello on-premises database and modify hello backend toouse this connection.</span></span> 

1. <span data-ttu-id="24c42-186">在 Visual Studio 中，您的行動應用程式的.NET 後端開啟 hello Web.config 檔案中的 [方案總管] 中找出 hello **connectionStrings**區段中，新增類似 hello 下列，哪一個點 toohello 內部部署 SQL SqlClient 項目伺服器資料庫：</span><span class="sxs-lookup"><span data-stu-id="24c42-186">In Solution Explorer in Visual Studio, open hello Web.config file for your Mobile App .NET backend, locate hello **connectionStrings** section, add a new SqlClient entry like hello following, which points toohello on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="24c42-187">請記住 tooreplace `<**secure_password**>` hello 密碼為您建立與這個字串中*HybridConnectionLogin*。</span><span class="sxs-lookup"><span data-stu-id="24c42-187">Remember tooreplace `<**secure_password**>` in this string with hello password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="24c42-188">按一下**儲存**Visual Studio toosave hello Web.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="24c42-188">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="24c42-189">Hello 本機電腦上執行時，會使用此連線設定。</span><span class="sxs-lookup"><span data-stu-id="24c42-189">This connection setting is used when running on hello local computer.</span></span> <span data-ttu-id="24c42-190">Azure 中執行時，這個設定會定義在 hello 入口網站中的 hello 連接設定所覆寫。</span><span class="sxs-lookup"><span data-stu-id="24c42-190">When running in Azure, this setting is overriden by hello connection setting defined in hello portal.</span></span>
   > 
   > 
3. <span data-ttu-id="24c42-191">展開 hello**模型**資料夾和開啟 hello 資料模型檔案，在為結束*Context.cs*。</span><span class="sxs-lookup"><span data-stu-id="24c42-191">Expand hello **Models** folder and open hello data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="24c42-192">修改 hello **DbContext**執行個體建構函式 toopass hello 值`OnPremisesDBConnection`toohello 基底**DbContext**建構函式，類似下列程式碼片段的 toohello:</span><span class="sxs-lookup"><span data-stu-id="24c42-192">Modify hello **DbContext** instance constructor toopass hello value `OnPremisesDBConnection` toohello base **DbContext** constructor, similar toohello following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="24c42-193">hello 服務現在將使用 hello 新連線 toohello SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="24c42-193">hello service will now use hello new connection toohello SQL Server database.</span></span>

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a><span data-ttu-id="24c42-194">更新 hello 行動裝置應用程式後端 toouse hello 在內部部署連接字串</span><span class="sxs-lookup"><span data-stu-id="24c42-194">Update hello Mobile App backend toouse hello on-premises connection string</span></span>
<span data-ttu-id="24c42-195">接下來，您需要 tooadd 應用程式設定這個新的連接字串，使其可以從 Azure 用。</span><span class="sxs-lookup"><span data-stu-id="24c42-195">Next, you need tooadd an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="24c42-196">在 hello [Azure 入口網站](https://portal.azure.com)hello web 應用程式後端程式碼中您的行動裝置應用程式，按一下 **所有設定**，然後**應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="24c42-196">Back in hello [Azure portal](https://portal.azure.com) in hello web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="24c42-197">在 hello **Web 應用程式設定**刀鋒視窗中，向下捲動太**連接字串**並加入新**SQL Server**名為連接字串`OnPremisesDBConnection`值會類似`Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="24c42-197">In hello **Web app settings** blade, scroll down too**Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="24c42-198">取代`<**secure_password**>`hello 安全密碼在內部部署資料庫。</span><span class="sxs-lookup"><span data-stu-id="24c42-198">Replace `<**secure_password**>` with hello secure password for your on-premises database.</span></span>
   
    ![Connection string for on-premises database](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="24c42-200">按**儲存**toosave hello 混合式連接和連接字串您剛建立。</span><span class="sxs-lookup"><span data-stu-id="24c42-200">Press **Save** toosave hello hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="24c42-201">此時，您可以重新發佈 hello 伺服器專案，並與現有的行動應用程式用戶端測試 hello 新的連接。</span><span class="sxs-lookup"><span data-stu-id="24c42-201">At this point you can republish hello server project and test hello new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="24c42-202">資料會讀取並寫入 toohello 在內部部署資料庫使用 hello 混合式連接。</span><span class="sxs-lookup"><span data-stu-id="24c42-202">Data will be read from and written toohello on-premises database using hello hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="24c42-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="24c42-203">Next Steps</span></span>
* <span data-ttu-id="24c42-204">如需建立 ASP.NET web 應用程式使用混合式連接的資訊，請參閱[連接 tooan 內部部署 SQL Server 從使用混合式連線的 Azure 網站](http://go.microsoft.com/fwlink/?LinkID=397979)。</span><span class="sxs-lookup"><span data-stu-id="24c42-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="24c42-205">其他資源</span><span class="sxs-lookup"><span data-stu-id="24c42-205">Additional Resources</span></span>
[<span data-ttu-id="24c42-206">混合式連線概觀</span><span class="sxs-lookup"><span data-stu-id="24c42-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="24c42-207">Josh Twist 介紹混合式連線 (第 9 頻道視訊)</span><span class="sxs-lookup"><span data-stu-id="24c42-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="24c42-208">混合式連線網站</span><span class="sxs-lookup"><span data-stu-id="24c42-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="24c42-209">BizTalk 服務：儀表板、監視器、調整、設定和混合式連線索引標籤</span><span class="sxs-lookup"><span data-stu-id="24c42-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="24c42-210">透過絕佳的應用程式可攜性建置真實的混合式雲端 (第 9 頻道視訊)</span><span class="sxs-lookup"><span data-stu-id="24c42-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="24c42-211">連接 tooan 內部部署 SQL Server 與 Azure 行動服務使用混合式連線 （Channel 9 影片）</span><span class="sxs-lookup"><span data-stu-id="24c42-211">Connect tooan on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="24c42-212">變更的項目</span><span class="sxs-lookup"><span data-stu-id="24c42-212">What's changed</span></span>
* <span data-ttu-id="24c42-213">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="24c42-213">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
