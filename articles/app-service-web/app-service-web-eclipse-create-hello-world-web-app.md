---
title: "使用 Eclipse 建立基本的 Azure Web 應用程式 | Microsoft Docs"
description: "本教學課程將示範如何使用適用於 Eclipse 的 Azure 工具組來建立 Azure Hello World Web 應用程式。"
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
ms.openlocfilehash: 683d6828546995a4dc60d8cac0669f356501c723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="1ac01-103">使用 Eclipse 建立基本的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ac01-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="1ac01-104">本教學課程示範如何使用 [適用於 Eclipse 的 Azure 工具組]，建立基本的 Hello World 應用程式，並部署到 Azure 做為 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ac01-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="1ac01-105">以下所示的基本 JSP 範例乃力求簡潔，不過只要與 Azure 部署相關，類似的步驟皆適用於 Java servlet。</span><span class="sxs-lookup"><span data-stu-id="1ac01-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="1ac01-106">當您完成本教學課程，在網頁瀏覽器中檢視您的應用程式時，看起來會如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="1ac01-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Hello World 應用程式預覽][01]

## <a name="prerequisites"></a><span data-ttu-id="1ac01-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="1ac01-108">Prerequisites</span></span>
* <span data-ttu-id="1ac01-109">Java Developer Kit (JDK) 1.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1ac01-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="1ac01-110">Eclipse IDE for Java EE Developers (Luna 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="1ac01-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="1ac01-111">這可透過 <http://www.eclipse.org/downloads/> 下載。</span><span class="sxs-lookup"><span data-stu-id="1ac01-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="1ac01-112">Java 型 Web 伺服器或應用程式伺服器的散發套件，例如 [Apache Tomcat] 或 [Jetty]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="1ac01-113">Azure 訂用帳戶，可以透過 <https://azure.microsoft.com/free/> 或 <http://azure.microsoft.com/pricing/purchase-options/> 取得。</span><span class="sxs-lookup"><span data-stu-id="1ac01-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="1ac01-114">[適用於 Eclipse 的 Azure 工具組]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-114">The [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="1ac01-115">如需安裝 Azure 工具組的相關資訊，請參閱[安裝 Azure Toolkit for Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for Eclipse].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="1ac01-116">建立 Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ac01-116">To create a Hello World application</span></span>
<span data-ttu-id="1ac01-117">首先，我們將從建立 Java 專案開始。</span><span class="sxs-lookup"><span data-stu-id="1ac01-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="1ac01-118">啟動 Eclipse，於功能表上依序按一下 [檔案]、[新增] 及 [動態 Web 專案]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-118">Start Eclipse, and at the menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="1ac01-119">(如果在按一下 [檔案] 和 [新增] 後沒有看到 [動態 Web 專案] 列為可用的專案，請執行下列動作：依序按一下 [檔案]、[新增]、[專案...]，展開 [Web]，按一下 [動態 Web 專案]，然後按 [下一步]。)</span><span class="sxs-lookup"><span data-stu-id="1ac01-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="1ac01-120">基於本教學課程的目的，將專案命名為 **MyWebApp**。</span><span class="sxs-lookup"><span data-stu-id="1ac01-120">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="1ac01-121">您的畫面將出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ac01-121">Your screen will appear similar to the following:</span></span>
   
    ![建立新的動態 Web 專案][02]
3. <span data-ttu-id="1ac01-123">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="1ac01-123">Click **Finish**.</span></span>
4. <span data-ttu-id="1ac01-124">在 Eclipse 的 [專案總管] 檢視中，展開 [MyWebApp]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="1ac01-125">在 [WebContent] 上按一下滑鼠右鍵、按一下 [新增]，然後按一下 [JSP 檔案]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="1ac01-126">在 [新增 JSP 檔案] 對話方塊中，將檔案命名為 **index.jsp**、將父資料夾保留為 **MyWebApp/WebContent**，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-126">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="1ac01-127">在 [選取 JSP 範本] 對話方塊中，基於本教學課程的目的，選取 [新增 JSP 檔案 (html)]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-127">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="1ac01-128">當 index.jsp 檔案在 Eclipse 中開啟時，新增文字以動態顯示 **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="1ac01-128">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="1ac01-129">(在現有 `<body>` 元素內)。</span><span class="sxs-lookup"><span data-stu-id="1ac01-129">within the existing `<body>` element.</span></span> <span data-ttu-id="1ac01-130">您已更新的 `<body>` 內容看起來應該與下列範例類似：</span><span class="sxs-lookup"><span data-stu-id="1ac01-130">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="1ac01-131">儲存 index.jsp。</span><span class="sxs-lookup"><span data-stu-id="1ac01-131">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="1ac01-132">將應用程式部署至 Azure Web 應用程式容器</span><span class="sxs-lookup"><span data-stu-id="1ac01-132">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="1ac01-133">您有數種方式可以將 Java Web 應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="1ac01-133">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="1ac01-134">本教學課程說明其中一個最簡單的方式：將您的應用程式部署至 Azure Web 應用程式容器，無需特殊的專案類型或額外的工具。</span><span class="sxs-lookup"><span data-stu-id="1ac01-134">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="1ac01-135">Azure 會為您提供 JDK 及 Web 容器軟體，因此您不需要自己上傳；只需要您的 Java Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ac01-135">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="1ac01-136">如此一來，您的應用程式發行程序只需數秒，連一分鐘都不用。</span><span class="sxs-lookup"><span data-stu-id="1ac01-136">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="1ac01-137">在 Eclipse 的專案總管中，以滑鼠右鍵按一下 [MyWebApp] 。</span><span class="sxs-lookup"><span data-stu-id="1ac01-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="1ac01-138">在操作功能表中，選取 [Azure]，然後按一下 [發佈為 Azure Web 應用程式...]</span><span class="sxs-lookup"><span data-stu-id="1ac01-138">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![發佈為 Azure Web 應用程式][03]
   
    <span data-ttu-id="1ac01-140">或者，您也可以在專案總管中選取 Web 應用程式專案時，按一下工具列的 [發佈] 下拉式按鈕，然後從這裡選取 [發佈為 Azure Web 應用程式]：</span><span class="sxs-lookup"><span data-stu-id="1ac01-140">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![發佈為 Azure Web 應用程式][14]
3. <span data-ttu-id="1ac01-142">如果尚未從 Eclipse 登入 Azure，系統會提示您登入 Azure 帳戶︰</span><span class="sxs-lookup"><span data-stu-id="1ac01-142">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
    ![[Azure 登入] 對話方塊][04]
   
    <span data-ttu-id="1ac01-144">如果您有多個 Azure 帳戶，登入程序期間的某些提示即使內容相同也可能會出現多次。</span><span class="sxs-lookup"><span data-stu-id="1ac01-144">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="1ac01-145">發生此情況時，請遵循登入指示繼續。</span><span class="sxs-lookup"><span data-stu-id="1ac01-145">When this happens, continue following the sign in instructions.</span></span>
4. <span data-ttu-id="1ac01-146">在您成功登入 Azure 帳戶後，[管理訂用帳戶]  對話方塊將會顯示與您的認證相關聯的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="1ac01-146">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="1ac01-147">如果列出多個訂用帳戶，而您只想使用其中幾個帳戶，您可以選擇取消選取要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ac01-147">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="1ac01-148">當您選取訂用帳戶之後，按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="1ac01-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![[管理訂用帳戶] 對話方塊][05]
5. <span data-ttu-id="1ac01-150">當 [部署至 Azure Web 應用程式容器]  對話方塊出現時，它會顯示您先前建立的所有 Web 應用程式容器；如果您尚未建立任何容器，清單將會是空白的。</span><span class="sxs-lookup"><span data-stu-id="1ac01-150">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![[部署至 Azure Web 應用程式容器] 對話方塊][06]
6. <span data-ttu-id="1ac01-152">如果您之前尚未建立 Azure Web 應用程式容器，或您想要將應用程式發佈到新的容器中，請使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="1ac01-152">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="1ac01-153">否則，請選取現有的 Web 應用程式容器，並跳至以下的步驟 7。</span><span class="sxs-lookup"><span data-stu-id="1ac01-153">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   1. <span data-ttu-id="1ac01-154">按一下 [完成] </span><span class="sxs-lookup"><span data-stu-id="1ac01-154">Click **New...**</span></span>
      
       ![[部署至 Azure Web 應用程式容器] 對話方塊][15]
   2. <span data-ttu-id="1ac01-156">[新增 Web 應用程式容器]  對話方塊會隨即顯示：</span><span class="sxs-lookup"><span data-stu-id="1ac01-156">The **New Web App Container** dialog box will be displayed:</span></span>
      
       ![[新增 Web 應用程式容器] 對話方塊][07a]
   3. <span data-ttu-id="1ac01-158">為您的 Web 應用程式容器輸入 **DNS 標籤** ，這會為您在 Azure 中的 Web 應用程式構成主機 URL 的分葉 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="1ac01-158">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="1ac01-159">(請注意，名稱必須可用，且符合 Azure Web 應用程式命名需求。)</span><span class="sxs-lookup"><span data-stu-id="1ac01-159">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="1ac01-160">在 [Web 容器]  下拉式功能表中，為您的應用程式選取適當的軟體。</span><span class="sxs-lookup"><span data-stu-id="1ac01-160">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="1ac01-161">目前，您可以從 Tomcat 8、Tomcat 7 或 Jetty 9 選擇。</span><span class="sxs-lookup"><span data-stu-id="1ac01-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="1ac01-162">所選軟體最新發行的版本由 Azure 提供，會在最新發行的 JDK 8 (由 Oracle 建立並由 Azure 提供) 中運作。</span><span class="sxs-lookup"><span data-stu-id="1ac01-162">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="1ac01-163">在 [訂用帳戶]  下拉式選單中，選取您希望此部署使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ac01-163">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="1ac01-164">在 [資源群組]  下拉式功能表中，選取您要與 Web 應用程式相關聯的資源群組。</span><span class="sxs-lookup"><span data-stu-id="1ac01-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="1ac01-165">(Azure 資源群組可讓您將相關的資源分在同一組，方便一次刪除。)</span><span class="sxs-lookup"><span data-stu-id="1ac01-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="1ac01-166">您可以選取現有的資源群組 (如果有)，並略過下方步驟 g，或使用以下步驟建立新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="1ac01-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="1ac01-167">按一下 [完成] </span><span class="sxs-lookup"><span data-stu-id="1ac01-167">Click **New...**</span></span>
      * <span data-ttu-id="1ac01-168">[新增資源群組]  對話方塊會隨即顯示：</span><span class="sxs-lookup"><span data-stu-id="1ac01-168">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![[新增資源群組] 對話方塊][08]
      * <span data-ttu-id="1ac01-170">在 [名稱]  文字方塊中，為新的資源群組指定名稱。</span><span class="sxs-lookup"><span data-stu-id="1ac01-170">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="1ac01-171">在 [區域]  下拉式功能表中，為資源群組選取適當的 Azure 資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="1ac01-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="1ac01-172">選擇性︰根據預設，Azure 會自動將最新的 Java 8 散發套件部署到 Web 應用程式容器，成為 JVM。</span><span class="sxs-lookup"><span data-stu-id="1ac01-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="1ac01-173">不過，如果 Web 應用程式需要的話，您也可以指定 JVM 的其他版本和散發套件。</span><span class="sxs-lookup"><span data-stu-id="1ac01-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="1ac01-174">若要指定 Web 應用程式的 JDK，請按一下 [JDK]  索引標籤，然後選取下列選項之一︰</span><span class="sxs-lookup"><span data-stu-id="1ac01-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
        
        * <span data-ttu-id="1ac01-175">**部署 Azure Web Apps 服務提供的預設 JDK**︰這個選項會部署最新的 Java 8 散發套件。</span><span class="sxs-lookup"><span data-stu-id="1ac01-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="1ac01-176">**部署 Azure 提供的第三方 JDK**：這個選項可讓您從 Microsoft Azure 提供的 JDK 清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="1ac01-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="1ac01-177">**從這個下載位置部署自己的 JDK：**這個選項可讓您指定自己的 JDK 散發套件。您必須將它封裝為 ZIP 檔案，再上傳到公開使用的下載位置，或您擁有存取權限的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ac01-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![[新增 Web 應用程式容器] 對話方塊][07b]
   7. <span data-ttu-id="1ac01-179">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1ac01-179">Click **OK**.</span></span>
   8. <span data-ttu-id="1ac01-180">[App Service 方案]  下拉式功能表會列出與您選取之資源群組相關聯的應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="1ac01-180">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="1ac01-181">(App Service 方案會指定如 Web 應用程式的位置、定價層及計算執行個體大小等資訊。</span><span class="sxs-lookup"><span data-stu-id="1ac01-181">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="1ac01-182">單一 App Service 方案可用於多個 Web Apps，這也就是要與特定 Web 應用程式部署分開維護的原因。)</span><span class="sxs-lookup"><span data-stu-id="1ac01-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="1ac01-183">您可以選取現有的 App Service 方案 (如果有)，並略過下方步驟 h，或使用以下步驟建立新的 App Service 方案：</span><span class="sxs-lookup"><span data-stu-id="1ac01-183">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="1ac01-184">按一下 [完成] </span><span class="sxs-lookup"><span data-stu-id="1ac01-184">Click **New...**</span></span>
      * <span data-ttu-id="1ac01-185">[新增 App Service 方案]  對話方塊會隨即顯示：</span><span class="sxs-lookup"><span data-stu-id="1ac01-185">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![[新增 App Service 方案] 對話方塊][09]
      * <span data-ttu-id="1ac01-187">在 [名稱]  文字方塊中，為新的 App Service 方案指定名稱。</span><span class="sxs-lookup"><span data-stu-id="1ac01-187">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="1ac01-188">在 [位置]  下拉式功能表中，為該方案選取適當的 Azure 資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="1ac01-188">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="1ac01-189">在 [定價層]  下拉式功能表中，為方案選取適當的價格。</span><span class="sxs-lookup"><span data-stu-id="1ac01-189">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="1ac01-190">針對測試用途，您可以選擇 [免費] 。</span><span class="sxs-lookup"><span data-stu-id="1ac01-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="1ac01-191">在 [執行個體大小]  下拉式功能表中，為方案選取適當的執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="1ac01-191">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="1ac01-192">針對測試用途，您可以選擇 [小型] 。</span><span class="sxs-lookup"><span data-stu-id="1ac01-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="1ac01-193">一旦您完成所有上述步驟之後，[New Web App Container] \(新增 Web 應用程式容器) 對話方塊看起來應該如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="1ac01-193">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![[新增 Web 應用程式容器] 對話方塊][10]
   10. <span data-ttu-id="1ac01-195">按一下 [確定]  來完成建立新的 Web 應用程式容器。</span><span class="sxs-lookup"><span data-stu-id="1ac01-195">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="1ac01-196">等待數秒鐘，讓 Web 應用程式容器清單重新整理；接著，您應該會在清單中看到新建立的 Web 應用程式容器已被選取。</span><span class="sxs-lookup"><span data-stu-id="1ac01-196">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
7. <span data-ttu-id="1ac01-197">您現在已經準備好，可以完成將 Web 應用程式部署至 Azure 的初始部署：</span><span class="sxs-lookup"><span data-stu-id="1ac01-197">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
    ![[部署至 Azure Web 應用程式容器] 對話方塊][11]
   
    <span data-ttu-id="1ac01-199">按一下 [確定]  來將您的 Java 應用程式部署至選取的 Web 應用程式容器。</span><span class="sxs-lookup"><span data-stu-id="1ac01-199">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
    <span data-ttu-id="1ac01-200">根據預設，您的應用程式將會部署為應用程式伺服器的子目錄。</span><span class="sxs-lookup"><span data-stu-id="1ac01-200">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="1ac01-201">如果您想要部署為根應用程式，請選取 [部署到根目錄] 核取方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-201">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="1ac01-202">接下來，您應該會看到 [Azure 活動記錄檔]  檢視，它會指出 Web 應用程式的部署狀態。</span><span class="sxs-lookup"><span data-stu-id="1ac01-202">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Azure 活動記錄檔][12]
   
    <span data-ttu-id="1ac01-204">將您的 Web 應用程式部署至 Azure 的程序，應該只需幾秒鐘即可完成。</span><span class="sxs-lookup"><span data-stu-id="1ac01-204">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="1ac01-205">當您的應用程式就緒時，您會在 [狀態]  in the **已發佈** 的連結。</span><span class="sxs-lookup"><span data-stu-id="1ac01-205">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="1ac01-206">當您按一下連結時，就會將您帶至已部署的 Web 應用程式首頁。</span><span class="sxs-lookup"><span data-stu-id="1ac01-206">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="1ac01-207">更新 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ac01-207">Updating your web app</span></span>
<span data-ttu-id="1ac01-208">更新現有執行中的 Azure Web 應用程式是一項快速又簡單的程序，而且您有兩個更新選項：</span><span class="sxs-lookup"><span data-stu-id="1ac01-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="1ac01-209">您可以更新現有 Java Web 應用程式的部署。</span><span class="sxs-lookup"><span data-stu-id="1ac01-209">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="1ac01-210">您可以將其他的 Java 應用程式發佈到相同的 Web 應用程式容器。</span><span class="sxs-lookup"><span data-stu-id="1ac01-210">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="1ac01-211">在任一種情況中，程序都是相同的，而且只需幾秒鐘：</span><span class="sxs-lookup"><span data-stu-id="1ac01-211">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="1ac01-212">在 Eclipse 專案總管中，以右鍵按一下您要更新或新增到現有 Web 應用程式容器的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ac01-212">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="1ac01-213">操作功能表顯示時，選取 [Azure]，然後選取 [發佈為 Azure Web 應用程式...]</span><span class="sxs-lookup"><span data-stu-id="1ac01-213">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="1ac01-214">由於您之前已經登入，因此會看到您現有 Web 應用程式容器的清單。</span><span class="sxs-lookup"><span data-stu-id="1ac01-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="1ac01-215">選取您要發佈或重新發佈 Java 應用程式的 Web 應用程式容器，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1ac01-215">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="1ac01-216">幾秒鐘之後，[Azure 活動記錄檔] 檢視將會將您已更新的部署顯示為 [已發佈]，而您將可以在網頁瀏覽器中確認已更新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ac01-216">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="1ac01-217">啟動、停止或重新啟動現有的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ac01-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="1ac01-218">若要啟動或停止現有的 Azure Web 應用程式容器 (包括其中所有已部署的 Java 應用程式)，您可以使用 [Azure 總管]  檢視。</span><span class="sxs-lookup"><span data-stu-id="1ac01-218">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="1ac01-219">如果 **Azure Explorer** 檢視尚未開啟，您可以依序按一下 Eclipse 中的 [視窗] 功能表、[顯示檢視]、[其他...]、[Azure]，然後按一下 [Azure Explorer] 來開啟。</span><span class="sxs-lookup"><span data-stu-id="1ac01-219">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="1ac01-220">如果您之前尚未登入，系統將會提示您登入。</span><span class="sxs-lookup"><span data-stu-id="1ac01-220">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="1ac01-221">顯示 [Azure 總管]  之後，使用下列這些步驟來啟動或停止您的 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="1ac01-221">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="1ac01-222">展開 [Azure]  節點。</span><span class="sxs-lookup"><span data-stu-id="1ac01-222">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="1ac01-223">展開 [Web Apps]  節點。</span><span class="sxs-lookup"><span data-stu-id="1ac01-223">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="1ac01-224">以滑鼠右鍵按一下所需的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ac01-224">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="1ac01-225">當操作功能表出現時，按一下 [啟動]、[停止] 或 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-225">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="1ac01-226">請注意，功能表選項是內容感知的，因此您只能停止執行中的 Web 應用程式，或是啟動目前尚未執行的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ac01-226">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![停止現有的 Web 應用程式][13]

## <a name="next-steps"></a><span data-ttu-id="1ac01-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ac01-228">Next Steps</span></span>
<span data-ttu-id="1ac01-229">如需適用於 Java IDE 的 Azure 套件組的詳細資訊，請參閱下列連結：</span><span class="sxs-lookup"><span data-stu-id="1ac01-229">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="1ac01-230">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="1ac01-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1ac01-231">[安裝 Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1ac01-231">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1ac01-232">*在 Eclipse 中建立 Azure Hello World Web 應用程式 (本文)*</span><span class="sxs-lookup"><span data-stu-id="1ac01-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="1ac01-233">[適用於 Eclipse 的 Azure 工具組的新功能]</span><span class="sxs-lookup"><span data-stu-id="1ac01-233">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="1ac01-234">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1ac01-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1ac01-235">[安裝 Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1ac01-235">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1ac01-236">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="1ac01-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="1ac01-237">[適用於 IntelliJ 的 Azure 工具組新增功能]</span><span class="sxs-lookup"><span data-stu-id="1ac01-237">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="1ac01-238">如需如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-238">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="1ac01-239">如需建立 Azure Web Apps 的詳細資訊，請參閱 [Web 應用程式概觀]。</span><span class="sxs-lookup"><span data-stu-id="1ac01-239">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

<span data-ttu-id="1ac01-240">[適用於 Eclipse 的 Azure 工具組]: ../azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="1ac01-240">[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="1ac01-241">[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="1ac01-241">[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md</span></span>
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
<span data-ttu-id="1ac01-242">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="1ac01-242">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="1ac01-243">[安裝 Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="1ac01-243">[Installing the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="1ac01-244">[安裝 Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="1ac01-244">[Installing the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="1ac01-245">[適用於 Eclipse 的 Azure 工具組的新功能]: ../azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="1ac01-245">[What's New in the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="1ac01-246">[適用於 IntelliJ 的 Azure 工具組新增功能]: ../azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="1ac01-246">[What's New in the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="1ac01-247">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="1ac01-247">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="1ac01-248">[Web 應用程式概觀]: ./app-service-web-overview.md</span><span class="sxs-lookup"><span data-stu-id="1ac01-248">[Web Apps Overview]: ./app-service-web-overview.md</span></span>
<span data-ttu-id="1ac01-249">[Apache Tomcat]: http://tomcat.apache.org/</span><span class="sxs-lookup"><span data-stu-id="1ac01-249">[Apache Tomcat]: http://tomcat.apache.org/</span></span>
<span data-ttu-id="1ac01-250">[Jetty]: http://www.eclipse.org/jetty/</span><span class="sxs-lookup"><span data-stu-id="1ac01-250">[Jetty]: http://www.eclipse.org/jetty/</span></span>

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
