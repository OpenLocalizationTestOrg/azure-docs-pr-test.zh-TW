---
title: "aaaCreate 基本 Azure web 應用程式使用的 Eclipse |Microsoft 文件"
description: "本教學課程會示範如何 toouse hello Azure Toolkit for Eclipse toocreate Azure Hello World 網頁應用程式。"
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="fe5fc-103">使用 Eclipse 建立基本的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fe5fc-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="fe5fc-104">本教學課程示範如何 toocreate 並將基本的 Hello World 應用程式 tooAzure 部署為 Web 應用程式中，使用 hello [Azure Toolkit for Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="fe5fc-105">以下所示的基本 JSP 範例乃力求簡潔，不過只要與 Azure 部署相關，類似的步驟皆適用於 Java servlet。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="fe5fc-106">當您完成本教學課程時，您的應用程式看起來類似 toohello 您網頁瀏覽器中檢視時，下列實例：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Hello World 應用程式預覽][01]

## <a name="prerequisites"></a><span data-ttu-id="fe5fc-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="fe5fc-108">Prerequisites</span></span>
* <span data-ttu-id="fe5fc-109">Java Developer Kit (JDK) 1.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="fe5fc-110">Eclipse IDE for Java EE Developers (Luna 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="fe5fc-111">這可透過 <http://www.eclipse.org/downloads/> 下載。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="fe5fc-112">Java 型 Web 伺服器或應用程式伺服器的散發套件，例如 [Apache Tomcat] 或 [Jetty]。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="fe5fc-113">Azure 訂用帳戶，可以透過 <https://azure.microsoft.com/free/> 或 <http://azure.microsoft.com/pricing/purchase-options/> 取得。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="fe5fc-114">hello [Azure Toolkit for Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-114">hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="fe5fc-115">如需安裝 Azure Toolkit hello 資訊，請參閱[安裝 hello Azure Toolkit for Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for Eclipse].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="fe5fc-116">toocreate Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="fe5fc-116">toocreate a Hello World application</span></span>
<span data-ttu-id="fe5fc-117">首先，我們將從建立 Java 專案開始。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="fe5fc-118">啟動 Eclipse 中，並在 hello 功能表按一下**檔案**，按一下 **新增**，然後按一下**動態 Web 專案**。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-118">Start Eclipse, and at hello menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="fe5fc-119">(如果您沒有看到**動態 Web 專案**列為可用的專案，按一下後**檔案**和**新增**，請勿然後 hello 遵循： 按一下**檔案**，按一下 **新增**，按一下 **專案...**，依序展開**Web**，按一下 **動態 Web 專案**，然後按一下**下一步**。)</span><span class="sxs-lookup"><span data-stu-id="fe5fc-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do hello following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="fe5fc-120">本教學課程的目的而言，專案的名稱，hello **MyWebApp**。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-120">For purposes of this tutorial, name hello project **MyWebApp**.</span></span> <span data-ttu-id="fe5fc-121">您的畫面會出現類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-121">Your screen will appear similar toohello following:</span></span>
   
    ![建立新的動態 Web 專案][02]
3. <span data-ttu-id="fe5fc-123">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-123">Click **Finish**.</span></span>
4. <span data-ttu-id="fe5fc-124">在 Eclipse 的 [專案總管] 檢視中，展開 [MyWebApp]。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="fe5fc-125">在 WebContent 上按一下滑鼠右鍵、按一下 新增，然後按一下JSP 檔案。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="fe5fc-126">在 hello**新增 JSP 檔案**對話方塊中，名稱 hello 檔**index.jsp**，保留 hello 父資料夾為**MyWebApp/WebContent**，然後按一下**下一步**.</span><span class="sxs-lookup"><span data-stu-id="fe5fc-126">In hello **New JSP File** dialog box, name hello file **index.jsp**, keep hello parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="fe5fc-127">在 hello**選取 JSP 範本**對話方塊中的，基於這個教學課程，請選取**新增 JSP 檔案 (html)**，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-127">In hello **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="fe5fc-128">當 Eclipse 中開啟 index.jsp 檔案時，加入在文字 toodynamically 顯示**Hello World ！**</span><span class="sxs-lookup"><span data-stu-id="fe5fc-128">When your index.jsp file opens in Eclipse, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="fe5fc-129">在現有的 hello`<body>`項目。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-129">within hello existing `<body>` element.</span></span> <span data-ttu-id="fe5fc-130">您已更新`<body>`內容應該類似下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe5fc-130">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="fe5fc-131">儲存 index.jsp。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-131">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="fe5fc-132">toodeploy 您應用程式 tooan Azure Web 應用程式容器</span><span class="sxs-lookup"><span data-stu-id="fe5fc-132">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="fe5fc-133">有幾種的方式可以部署 Java web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-133">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="fe5fc-134">本教學課程說明 hello 最簡單的其中一個： 您的應用程式將會部署的 tooan Azure Web 應用程式的容器-沒有特殊專案類型和其他工具所需。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-134">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="fe5fc-135">hello JDK 和 hello web 容器軟體將會提供給您的 Azure 中，所以不需要 tooupload 自己;您只需要為您的 Java Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-135">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="fe5fc-136">如此一來，hello 發行程序，您的應用程式需要秒，不是分鐘。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-136">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="fe5fc-137">在 Eclipse 的專案總管中，以滑鼠右鍵按一下 [MyWebApp] 。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="fe5fc-138">在 hello 內容功能表選取**Azure**，然後按一下 **發行為 Azure Web 應用程式...**</span><span class="sxs-lookup"><span data-stu-id="fe5fc-138">In hello context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![發佈為 Azure Web 應用程式][03]
   
    <span data-ttu-id="fe5fc-140">或者，在 hello [專案總管] 中選取您的 web 應用程式專案時，您可以按一下 hello**發行**hello 工具列，然後選取的下拉式按鈕**發佈 Azure Web 應用程式為**從該處：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-140">Alternatively, while your web application project is selected in hello Project Explorer, you can click hello **Publish** dropdown button on hello toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![發佈為 Azure Web 應用程式][14]
3. <span data-ttu-id="fe5fc-142">如果您有沒有登入 Azure 從 Eclipse，您將會提示的 toosign 到您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-142">If you have not already signed into Azure from Eclipse, you will be prompted toosign into your Azure account:</span></span>
   
    ![[Azure 登入] 對話方塊][04]
   
    <span data-ttu-id="fe5fc-144">如果您有多個 Azure 帳戶，一些期間 hello hello 提示登入程序可能會顯示一次以上，即使看起來 toobe hello 相同。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-144">If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="fe5fc-145">當發生這種情況時，繼續遵循 hello 登入指示。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-145">When this happens, continue following hello sign in instructions.</span></span>
4. <span data-ttu-id="fe5fc-146">您已成功登入您的 Azure 帳戶之後，hello**管理訂用帳戶**對話方塊會顯示您的認證與相關聯的訂用帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-146">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="fe5fc-147">如果有多個列出的訂閱，而且您想 toowork 特定子集合的它們，您可能會選擇性地取消核取 hello 想 toouse 的。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-147">If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello ones you do want toouse.</span></span> <span data-ttu-id="fe5fc-148">當您選取訂用帳戶之後，按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![[管理訂用帳戶] 對話方塊][05]
5. <span data-ttu-id="fe5fc-150">當 hello**部署 Web 應用程式容器 tooAzure**  對話方塊隨即出現，它會顯示您先前已經建立任何 Web 應用程式容器; 如果您尚未建立任何容器，hello 清單將會是空的。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-150">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![部署 tooAzure Web 應用程式容器 對話方塊][06]
6. <span data-ttu-id="fe5fc-152">如果您尚未建立 Azure Web 應用程式容器之前，或如果您想要 toopublish 應用程式 tooa 的新容器，，使用下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-152">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="fe5fc-153">否則，請選取現有的 Web 應用程式容器，並略過 toostep 7。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-153">Otherwise, select an existing Web App Container and skip toostep 7 below.</span></span>
   
   1. <span data-ttu-id="fe5fc-154">按一下 [完成] </span><span class="sxs-lookup"><span data-stu-id="fe5fc-154">Click **New...**</span></span>
      
       ![部署 tooAzure Web 應用程式容器 對話方塊][15]
   2. <span data-ttu-id="fe5fc-156">hello**新的 Web 應用程式容器**對話方塊會顯示：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-156">hello **New Web App Container** dialog box will be displayed:</span></span>
      
       ![[新增 Web 應用程式容器] 對話方塊][07a]
   3. <span data-ttu-id="fe5fc-158">輸入**DNS 標籤**Web 應用程式容器; 這將會形成 hello 分葉 DNS 標籤 hello 主機 URL，web 應用程式在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-158">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="fe5fc-159">（請注意該 hello 名稱必須可供使用且符合 tooAzure Web 應用程式命名需求）。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-159">(Note that hello name must be available and conform tooAzure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="fe5fc-160">在 hello**網頁容器**下拉式功能表、 選取 hello 適當的軟體應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-160">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="fe5fc-161">目前，您可以從 Tomcat 8、Tomcat 7 或 Jetty 9 選擇。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="fe5fc-162">最近的 hello 選取軟體發佈將會由 Azure 中，提供，且可以在建立 Oracle 和 Azure 所提供的 JDK 8 最近發佈。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-162">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="fe5fc-163">在 hello**訂用帳戶**下拉式選單中，您想要此部署 toouse 選取 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-163">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="fe5fc-164">在 hello**資源群組**下拉式功能表，選取 hello 與您想 tooassociate 您 Web 應用程式的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-164">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="fe5fc-165">（azure 資源群組允許您 toogroup 相關資源在一起，以便將，比方說，您可以先刪除這些一起）。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-165">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="fe5fc-166">（如果有），您可以選取現有的資源群組，並略過 toostep g 以下或使用 hello 遵循這些步驟 toocreate 新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-166">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following these steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="fe5fc-167">按一下 [完成] </span><span class="sxs-lookup"><span data-stu-id="fe5fc-167">Click **New...**</span></span>
      * <span data-ttu-id="fe5fc-168">hello**新資源群組**對話方塊會顯示：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-168">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![[新增資源群組] 對話方塊][08]
      * <span data-ttu-id="fe5fc-170">在 hello hello**名稱**文字方塊中，指定新的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-170">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="fe5fc-171">在 hello hello**區域**下拉式選單選取 hello 適當的 Azure 資料中心資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-171">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="fe5fc-172">選擇性： 根據預設，新的 Java 8 分配會部署 Azure 自動為您的 JVM tooyour web 應用程式的容器。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically tooyour web app container as your JVM.</span></span> <span data-ttu-id="fe5fc-173">不過，您可以指定不同的版本和發佈的 hello JVM 如果 Web 應用程式需要它。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-173">However, you can specify a different version and distribution of hello JVM if your Web App requires it.</span></span> <span data-ttu-id="fe5fc-174">toospecify hello JDK 您 Web 應用程式中，按一下 hello **JDK**索引標籤，然後選取其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-174">toospecify hello JDK for your Web App, click hello **JDK** tab, and select one of hello following options:</span></span>
        
        * <span data-ttu-id="fe5fc-175">**部署 hello 預設 Azure Web 應用程式服務所提供的 JDK**： 此選項會將 Java 8 最近發佈的部署。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-175">**Deploy hello default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="fe5fc-176">**部署第 3 個合作對象在 Azure 上可用的 JDK**： 此選項可讓您從 Microsoft Azure 所提供的 Jdk hello 清單 toochoose。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-176">**Deploy a 3rd party JDK available on Azure**: This option allows you toochoose from hello list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="fe5fc-177">**部署我自己的 JDK，從這個下載位置**： 此選項可讓您 toospecify 自己 JDK 散發，這必須為 ZIP 檔案封裝並上傳的 tooeither 公開可用的下載位置或 Azure 儲存體帳戶，您存取權。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-177">**Deploy my own JDK from this download location**: This option allows you toospecify your own JDK distribution, which must be packaged as a ZIP file and uploaded tooeither a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![[新增 Web 應用程式容器] 對話方塊][07b]
   7. <span data-ttu-id="fe5fc-179">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-179">Click **OK**.</span></span>
   8. <span data-ttu-id="fe5fc-180">hello **App Service 方案**下拉式功能表列出 hello 與 hello 您選取的資源群組相關聯的應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-180">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="fe5fc-181">（應用程式服務計劃指定 Web 應用程式，hello 定價層和 hello 運算執行個體大小的 hello 位置等資訊。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-181">(App Service Plans specify information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="fe5fc-182">單一 App Service 方案可用於多個 Web Apps，這也就是要與特定 Web 應用程式部署分開維護的原因。)</span><span class="sxs-lookup"><span data-stu-id="fe5fc-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="fe5fc-183">您可以選取現有的 App Service 方案 （如果有），並略過 toostep h，或使用下列這些新的 App Service 方案的步驟 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="fe5fc-183">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following these steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="fe5fc-184">按一下 [完成] </span><span class="sxs-lookup"><span data-stu-id="fe5fc-184">Click **New...**</span></span>
      * <span data-ttu-id="fe5fc-185">hello**新應用程式服務方案**對話方塊會顯示：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-185">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![[新增 App Service 方案] 對話方塊][09]
      * <span data-ttu-id="fe5fc-187">在 hello hello**名稱**文字方塊中，指定您新的 App Service 方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-187">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="fe5fc-188">在 hello hello**位置**下拉式選單選取 hello 適當的 Azure 資料中心 hello 計劃的位置。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-188">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="fe5fc-189">在 hello hello**定價層**下拉式功能表，選取 hello 適當定價 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-189">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="fe5fc-190">針對測試用途，您可以選擇 [免費] 。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="fe5fc-191">在 hello hello**執行個體大小**下拉式功能表、 選取 hello hello 計劃的適當的執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-191">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="fe5fc-192">針對測試用途，您可以選擇 [小型] 。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="fe5fc-193">當您完成所有 hello 上述步驟時，hello 新的 Web 應用程式容器 對話方塊應該類似下列圖中的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe5fc-193">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![[新增 Web 應用程式容器] 對話方塊][10]
   10. <span data-ttu-id="fe5fc-195">按一下**確定**toocomplete hello 建立新的 Web 應用程式容器。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-195">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="fe5fc-196">等候數秒鐘，讓 hello Web 應用程式容器 toobe hello 清單重新整理，現在應 hello 清單中選取您新建立的 web 應用程式的容器。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-196">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
7. <span data-ttu-id="fe5fc-197">現在您已經準備就緒 toocomplete hello 初始部署 Web 應用程式 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="fe5fc-197">You are now ready toocomplete hello initial deployment of your Web App tooAzure:</span></span>
   
    ![部署 tooAzure Web 應用程式容器 對話方塊][11]
   
    <span data-ttu-id="fe5fc-199">按一下**確定**toodeploy 您的 Java 應用程式 toohello 選取 Web 應用程式的容器。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-199">Click **OK** toodeploy your Java application toohello selected Web App container.</span></span>
   
    <span data-ttu-id="fe5fc-200">根據預設，您的應用程式將會部署為 hello 應用程式伺服器的子目錄。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-200">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="fe5fc-201">如果您想 toobe 部署為 hello 根應用程式，請檢查 hello**部署 tooroot**核取方塊後，再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-201">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="fe5fc-202">接下來，您應該會看見 hello **Azure 活動記錄檔**檢視，其中將指出 hello Web 應用程式的部署狀態。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-202">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Azure 活動記錄檔][12]
   
    <span data-ttu-id="fe5fc-204">部署 Web 應用程式 tooAzure 的 hello 程序應該採取只有幾秒鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-204">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="fe5fc-205">當您的應用程式已備妥，您會看到名為的連結**發佈**在 hello**狀態**資料行。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-205">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="fe5fc-206">當您按一下 hello 連結時，它會帶您 tooyour 部署 Web 應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-206">When you click hello link, it will take you tooyour deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="fe5fc-207">更新 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fe5fc-207">Updating your web app</span></span>
<span data-ttu-id="fe5fc-208">更新現有執行中的 Azure Web 應用程式是一項快速又簡單的程序，而且您有兩個更新選項：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="fe5fc-209">您可以更新 hello 部署現有的 Java Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-209">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="fe5fc-210">您可以將額外的 Java 應用程式 toohello 發行相同的 Web 應用程式容器。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-210">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="fe5fc-211">在任一情況下，hello 程序相同，並需要只有幾秒鐘的時間：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-211">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="fe5fc-212">Hello Eclipse [專案總管] 中以滑鼠右鍵按一下您想要 tooupdate 或加入現有的 Web 應用程式容器 tooan 的 hello Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-212">In hello Eclipse project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="fe5fc-213">Hello 操作功能表出現時，選取**Azure**然後**發行為 Azure Web 應用程式...**</span><span class="sxs-lookup"><span data-stu-id="fe5fc-213">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="fe5fc-214">由於您之前已經登入，因此會看到您現有 Web 應用程式容器的清單。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="fe5fc-215">選取 hello 一您想要 toopublish 或重新發佈您的 Java 應用程式 tooand 按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-215">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="fe5fc-216">在幾秒鐘後，hello **Azure 活動記錄檔**檢視會顯示為您更新的部署**已發佈**而且您將會無法 tooverify 網頁瀏覽器應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-216">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="fe5fc-217">啟動、停止或重新啟動現有的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fe5fc-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="fe5fc-218">toostart 或停止現有的 Azure Web 應用程式容器，（包括所有部署的 hello Java 應用程式中），您可以使用 hello **Azure 總管**檢視。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-218">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="fe5fc-219">如果 hello **Azure 總管**檢視尚未開啟，您可以再按一下來開啟**視窗**功能表在 Eclipse 中，然後按一下**顯示檢視**，然後**其他...**，然後**Azure**，然後按一下 **Azure 總管**。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-219">If hello **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="fe5fc-220">如果您先前尚未登入，則會提示您 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-220">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="fe5fc-221">當 hello **Azure 總管**檢視隨即顯示，請遵循這些步驟 toostart 使用，或停止 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="fe5fc-221">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="fe5fc-222">展開 hello **Azure**節點。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-222">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="fe5fc-223">展開 hello **Web 應用程式**節點。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-223">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="fe5fc-224">以滑鼠右鍵按一下 hello 所需的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-224">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="fe5fc-225">Hello 操作功能表出現時，按一下**啟動**，**停止**，或**重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-225">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="fe5fc-226">請注意，hello 功能表選項內容感知，所以您只可以停止正在執行的 web 應用程式或啟動 web 應用程式目前未執行的。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-226">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![停止現有的 Web 應用程式][13]

## <a name="next-steps"></a><span data-ttu-id="fe5fc-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe5fc-228">Next Steps</span></span>
<span data-ttu-id="fe5fc-229">針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="fe5fc-229">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="fe5fc-230">[Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fe5fc-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="fe5fc-231">[安裝 hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fe5fc-231">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="fe5fc-232">*在 Eclipse 中建立 Azure Hello World Web 應用程式 (本文)*</span><span class="sxs-lookup"><span data-stu-id="fe5fc-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="fe5fc-233">[功能 hello Azure Toolkit for Eclipse 中的新功能]</span><span class="sxs-lookup"><span data-stu-id="fe5fc-233">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="fe5fc-234">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="fe5fc-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="fe5fc-235">[安裝 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="fe5fc-235">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="fe5fc-236">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="fe5fc-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="fe5fc-237">[新功能 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="fe5fc-237">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="fe5fc-238">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-238">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="fe5fc-239">如需有關建立 Azure Web 應用程式的詳細資訊，請參閱 hello [Web 應用程式的概觀]。</span><span class="sxs-lookup"><span data-stu-id="fe5fc-239">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web-intellij-create-hello-world-web-app.md
[安裝 hello Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[功能 hello Azure Toolkit for Eclipse 中的新功能]: ../azure-toolkit-for-eclipse-whats-new.md
[新功能 hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Web 應用程式的概觀]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
