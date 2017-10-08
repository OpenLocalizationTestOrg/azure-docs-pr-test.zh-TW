---
title: "aaaCreate 基本 Azure web 應用程式中 IntelliJ |Microsoft 文件"
description: "本教學課程會示範如何 toouse hello Azure Toolkit for IntelliJ toocreate Azure Hello World 網頁應用程式。"
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="16805-103">在 IntelliJ 中建立基本的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="16805-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="16805-104">本教學課程示範如何 toocreate 並將基本的 Hello World 應用程式 tooAzure 部署為 Web 應用程式中，使用 hello [Azure Toolkit for IntelliJ]。</span><span class="sxs-lookup"><span data-stu-id="16805-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="16805-105">以下所示的基本 JSP 範例乃力求簡潔，不過只要與 Azure 部署相關，類似的步驟皆適用於 Java servlet。</span><span class="sxs-lookup"><span data-stu-id="16805-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="16805-106">當您完成本教學課程時，您的應用程式看起來類似 toohello 您網頁瀏覽器中檢視時，下列實例：</span><span class="sxs-lookup"><span data-stu-id="16805-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![範例網頁][01]

## <a name="prerequisites"></a><span data-ttu-id="16805-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="16805-108">Prerequisites</span></span>
* <span data-ttu-id="16805-109">Java Developer Kit (JDK) 1.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="16805-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="16805-110">IntelliJ 概念旗艦版。</span><span class="sxs-lookup"><span data-stu-id="16805-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="16805-111">可以從 <https://www.jetbrains.com/idea/download/index.html> 下載。</span><span class="sxs-lookup"><span data-stu-id="16805-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="16805-112">Java 型 Web 伺服器或應用程式伺服器的散發套件，例如 [Apache Tomcat] 或 [Jetty]。</span><span class="sxs-lookup"><span data-stu-id="16805-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="16805-113">Azure 訂用帳戶，可以透過 <https://azure.microsoft.com/free/> 或 <http://azure.microsoft.com/pricing/purchase-options/> 取得。</span><span class="sxs-lookup"><span data-stu-id="16805-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="16805-114">hello [Azure Toolkit for IntelliJ]。</span><span class="sxs-lookup"><span data-stu-id="16805-114">hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="16805-115">如需安裝 Azure Toolkit hello 資訊，請參閱[安裝 hello Azure Toolkit for IntelliJ]。</span><span class="sxs-lookup"><span data-stu-id="16805-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="16805-116">toocreate Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="16805-116">toocreate a Hello World application</span></span>
<span data-ttu-id="16805-117">首先，我們將從建立 Java 專案開始。</span><span class="sxs-lookup"><span data-stu-id="16805-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="16805-118">啟動 IntelliJ，然後按一下 hello**檔案**功能表，然後按一下**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="16805-118">Start IntelliJ and click hello **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![專案 > 新增專案][02]
2. <span data-ttu-id="16805-120">在 hello 新增專案 對話方塊中，選取  **Java**，然後**Web 應用程式**，然後按一下**新增**tooadd 專案 SDK。</span><span class="sxs-lookup"><span data-stu-id="16805-120">In hello New Project dialog box, select **Java**, then **Web Application**, and then click **New** tooadd a Project SDK.</span></span>
   
    ![New Project Dialog][03a]
   
3. <span data-ttu-id="16805-122">JDK 對話方塊 hello 選擇主目錄中選取 hello JDK 安裝所在的資料夾，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="16805-122">In hello Select Home Directory for JDK dialog box, select hello folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="16805-123">按一下**下一步**hello 新增專案對話方塊方塊 toocontinue 中。</span><span class="sxs-lookup"><span data-stu-id="16805-123">Click **Next** in hello New Project dialog box toocontinue.</span></span>
   
    ![指定 JDK 主目錄][03b]
4. <span data-ttu-id="16805-125">本教學課程的目的而言，專案的名稱，hello **Java Web 層應用程式層上-Azure**，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="16805-125">For purposes of this tutorial, name hello project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![New Project Dialog][04]
5. <span data-ttu-id="16805-127">在 IntelliJ 的 [專案總管] 檢視中，依序展開 [Java-Web-App-On-Azure] 和 [web]，然後按兩下 [index.jsp]。</span><span class="sxs-lookup"><span data-stu-id="16805-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![開啟索引頁面][05c]
6. <span data-ttu-id="16805-129">當 IntelliJ 開啟 index.jsp 檔案時，加入在文字 toodynamically 顯示**Hello World ！**</span><span class="sxs-lookup"><span data-stu-id="16805-129">When your index.jsp file opens in IntelliJ, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="16805-130">在現有的 hello`<body>`項目。</span><span class="sxs-lookup"><span data-stu-id="16805-130">within hello existing `<body>` element.</span></span> <span data-ttu-id="16805-131">您已更新`<body>`內容應該類似下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="16805-131">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="16805-132">儲存 index.jsp。</span><span class="sxs-lookup"><span data-stu-id="16805-132">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="16805-133">toodeploy 您應用程式 tooan Azure Web 應用程式容器</span><span class="sxs-lookup"><span data-stu-id="16805-133">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="16805-134">有幾種的方式可以部署 Java web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="16805-134">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="16805-135">本教學課程說明 hello 最簡單的其中一個： 您的應用程式將會部署的 tooan Azure Web 應用程式的容器-沒有特殊專案類型和其他工具所需。</span><span class="sxs-lookup"><span data-stu-id="16805-135">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="16805-136">hello JDK 和 hello web 容器軟體將會提供給您的 Azure 中，所以不需要 tooupload 自己;您只需要為您的 Java Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16805-136">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="16805-137">如此一來，hello 發行程序，您的應用程式需要秒，不是分鐘。</span><span class="sxs-lookup"><span data-stu-id="16805-137">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="16805-138">在發行您的應用程式之前，您必須先 tooconfigure 模組設定。</span><span class="sxs-lookup"><span data-stu-id="16805-138">Before you publish your application, you first need tooconfigure your module settings.</span></span> <span data-ttu-id="16805-139">toodo 因此，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="16805-139">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="16805-140">IntelliJ 的專案總管 中以滑鼠右鍵按一下 hello **Java Web 層應用程式層上-Azure**專案。</span><span class="sxs-lookup"><span data-stu-id="16805-140">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="16805-141">Hello 操作功能表出現時，按一下**開啟模組設定**。</span><span class="sxs-lookup"><span data-stu-id="16805-141">When hello context menu appears, click **Open Module Settings**.</span></span>

    ![開啟模組設定][05a]
2. <span data-ttu-id="16805-143">Hello 專案結構對話方塊出現時：</span><span class="sxs-lookup"><span data-stu-id="16805-143">When hello Project Structure dialog box appears:</span></span>

   <span data-ttu-id="16805-144">a.</span><span class="sxs-lookup"><span data-stu-id="16805-144">a.</span></span> <span data-ttu-id="16805-145">按一下**成品**hello 清單中**專案設定**。</span><span class="sxs-lookup"><span data-stu-id="16805-145">Click **Artifacts** in hello list of **Project Settings**.</span></span>
   <span data-ttu-id="16805-146">b.</span><span class="sxs-lookup"><span data-stu-id="16805-146">b.</span></span> <span data-ttu-id="16805-147">在 hello 變更 hello 成品名稱**名稱**方塊，讓它不包含空格或特殊字元，這是必要的因為 hello 名稱將用於 hello 統一資源識別元 (URI)。</span><span class="sxs-lookup"><span data-stu-id="16805-147">Change hello artifact name in hello **Name** box so that it doesn't contain whitespace or special characters; this is necessary since hello name will be used in hello Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="16805-148">c.</span><span class="sxs-lookup"><span data-stu-id="16805-148">c.</span></span> <span data-ttu-id="16805-149">變更 hello**類型**太**Web 應用程式： 封存**。</span><span class="sxs-lookup"><span data-stu-id="16805-149">Change hello **Type** too**Web Application: Archive**.</span></span>
   <span data-ttu-id="16805-150">d.</span><span class="sxs-lookup"><span data-stu-id="16805-150">d.</span></span> <span data-ttu-id="16805-151">按一下**確定**tooclose hello 專案結構對話方塊。</span><span class="sxs-lookup"><span data-stu-id="16805-151">Click **OK** tooclose hello Project Structure dialog box.</span></span>

    ![開啟模組設定][05b]

<span data-ttu-id="16805-153">當您完成設定您的模組設定時，您可以使用下列步驟的 hello 發行應用程式 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="16805-153">When you have configured your module settings, you can publish your application tooAzure by using hello following steps:</span></span>

1. <span data-ttu-id="16805-154">IntelliJ 的專案總管 中以滑鼠右鍵按一下 hello **Java Web 層應用程式層上-Azure**專案。</span><span class="sxs-lookup"><span data-stu-id="16805-154">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="16805-155">Hello 操作功能表出現時，選取**Azure**，然後按一下**發行為 Azure Web 應用程式...**</span><span class="sxs-lookup"><span data-stu-id="16805-155">When hello context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Azure 發佈操作功能表][06]
2. <span data-ttu-id="16805-157">如果您有沒有登入從 IntelliJ Azure，您將會提示的 toosign 到您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="16805-157">If you have not already signed into Azure from IntelliJ, you will be prompted toosign into your Azure account.</span></span> <span data-ttu-id="16805-158">(如果您有多個 Azure 帳戶，一些 hello 提示 hello 登入程序期間可能會顯示一次以上，即使看起來 toobe hello 相同。</span><span class="sxs-lookup"><span data-stu-id="16805-158">(If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="16805-159">當發生這種情況，指示中繼續 toofollow hello 註冊）。</span><span class="sxs-lookup"><span data-stu-id="16805-159">When this happens, continue toofollow hello sign in instructions.)</span></span>
   
    ![Azure 登入對話方塊][07]
3. <span data-ttu-id="16805-161">您已成功登入您的 Azure 帳戶之後，hello**管理訂用帳戶**對話方塊會顯示您的認證與相關聯的訂用帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="16805-161">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="16805-162">（如果有多個列出的訂閱，而且您想 toowork 特定子集合的它們，您可能會選擇性地取消核取您不想 toouse hello 訂用帳戶。）當您選取訂用帳戶之後，按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="16805-162">(If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello subscriptions you don't want toouse.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![管理訂用帳戶][08]
4. <span data-ttu-id="16805-164">當 hello**部署 Web 應用程式容器 tooAzure**  對話方塊隨即出現，它會顯示您先前已經建立任何 Web 應用程式容器; 如果您尚未建立任何容器，hello 清單將會是空的。</span><span class="sxs-lookup"><span data-stu-id="16805-164">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![應用程式容器][09]
5. <span data-ttu-id="16805-166">如果您尚未建立 Azure Web 應用程式容器之前，或如果您想要 toopublish 應用程式 tooa 的新容器，，使用下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="16805-166">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="16805-167">否則，請選取現有的 Web 應用程式容器，並略過 toostep 6。</span><span class="sxs-lookup"><span data-stu-id="16805-167">Otherwise, select an existing Web App Container and skip toostep 6 below.</span></span>
   
   1. <span data-ttu-id="16805-168">按一下 **+**</span><span class="sxs-lookup"><span data-stu-id="16805-168">Click **+**</span></span>
      
       ![新增應用程式容器][10]
   2. <span data-ttu-id="16805-170">hello**新的 Web 應用程式容器**對話方塊將會顯示，它將會是用於 hello 接下來幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="16805-170">hello **New Web App Container** dialog box will be displayed, which will be used for hello next several steps.</span></span>
      
       ![新增應用程式容器][11a]
   3. <span data-ttu-id="16805-172">輸入**DNS 標籤**Web 應用程式容器; 這將會形成 hello 分葉 DNS 標籤 hello 主機 URL，web 應用程式在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="16805-172">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="16805-173">請注意該 hello 名稱必須可供使用且符合 tooAzure Web 應用程式命名需求。</span><span class="sxs-lookup"><span data-stu-id="16805-173">Note that hello name must be available and conform tooAzure Web App naming requirements.</span></span>
   4. <span data-ttu-id="16805-174">在 hello**網頁容器**下拉式功能表、 選取 hello 適當的軟體應用程式。</span><span class="sxs-lookup"><span data-stu-id="16805-174">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="16805-175">目前，您可以從 Tomcat 8、Tomcat 7 或 Jetty 9 選擇。</span><span class="sxs-lookup"><span data-stu-id="16805-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="16805-176">最近的 hello 選取軟體發佈將會由 Azure 中，提供，且可以在建立 Oracle 和 Azure 所提供的 JDK 8 最近發佈。</span><span class="sxs-lookup"><span data-stu-id="16805-176">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="16805-177">在 hello**訂用帳戶**下拉式選單中，您想要此部署 toouse 選取 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="16805-177">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="16805-178">在 hello**資源群組**下拉式功能表，選取 hello 與您想 tooassociate 您 Web 應用程式的資源群組。</span><span class="sxs-lookup"><span data-stu-id="16805-178">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="16805-179">（azure 資源群組允許您 toogroup 相關資源在一起，以便將，比方說，您可以先刪除這些一起）。</span><span class="sxs-lookup"><span data-stu-id="16805-179">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="16805-180">（如果有），您可以選取現有的資源群組，並略過 toostep g 以下或使用 hello 下列步驟 toocreate 新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="16805-180">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="16805-181">選取 **&lt; &lt;建立新的資源群組&gt; &gt;** 在 hello**資源群組**下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="16805-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in hello **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="16805-182">hello**新資源群組**對話方塊會顯示：</span><span class="sxs-lookup"><span data-stu-id="16805-182">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![新增資源群組][12]
      * <span data-ttu-id="16805-184">在 hello hello**名稱**文字方塊中，指定新的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="16805-184">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="16805-185">在 hello hello**區域**下拉式選單選取 hello 適當的 Azure 資料中心資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="16805-185">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="16805-186">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="16805-186">Click **OK**.</span></span>
   7. <span data-ttu-id="16805-187">hello **App Service 方案**下拉式功能表列出 hello 與 hello 您選取的資源群組相關聯的應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="16805-187">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="16805-188">（App Service 方案指定 Web 應用程式，hello 定價層和 hello 運算執行個體大小的 hello 位置等資訊。</span><span class="sxs-lookup"><span data-stu-id="16805-188">(An App Service Plan specifies information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="16805-189">單一 App Service 方案可用於多個 Web Apps，這也就是要與特定 Web 應用程式部署分開維護的原因。)</span><span class="sxs-lookup"><span data-stu-id="16805-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="16805-190">您可以選取現有的 App Service 方案 （如果有），並略過 toostep h，或使用下列新的 App Service 方案的步驟 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="16805-190">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="16805-191">選取 **&lt; &lt;建立新的應用程式服務計劃&gt; &gt;** 在 hello **App Service 方案**下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="16805-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in hello **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="16805-192">hello**新應用程式服務方案**對話方塊會顯示：</span><span class="sxs-lookup"><span data-stu-id="16805-192">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![新增 App Service 方案][13]
      * <span data-ttu-id="16805-194">在 hello hello**名稱**文字方塊中，指定您新的 App Service 方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="16805-194">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="16805-195">在 hello hello**位置**下拉式選單選取 hello 適當的 Azure 資料中心 hello 計劃的位置。</span><span class="sxs-lookup"><span data-stu-id="16805-195">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="16805-196">在 hello hello**定價層**下拉式功能表，選取 hello 適當定價 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="16805-196">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="16805-197">針對測試用途，您可以選擇 [免費] 。</span><span class="sxs-lookup"><span data-stu-id="16805-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="16805-198">在 hello hello**執行個體大小**下拉式功能表、 選取 hello hello 計劃的適當的執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="16805-198">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="16805-199">針對測試用途，您可以選擇 [小型] 。</span><span class="sxs-lookup"><span data-stu-id="16805-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="16805-200">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="16805-200">Click **OK**.</span></span>
   8. <span data-ttu-id="16805-201">（選擇性）根據預設，Java 8 最近發佈將會自動部署為您的 JVM Azure tooyour web 應用程式容器所。</span><span class="sxs-lookup"><span data-stu-id="16805-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure tooyour web app container.</span></span> <span data-ttu-id="16805-202">不過，您可以選取不同的版本和 hello JVM 的分佈。</span><span class="sxs-lookup"><span data-stu-id="16805-202">However, you can select a different version and distribution of hello JVM.</span></span> <span data-ttu-id="16805-203">toodo 因此，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="16805-203">toodo so, use hello following steps:</span></span>
      
      * <span data-ttu-id="16805-204">按一下 hello **JDK**  索引標籤中 hello**新的 Web 應用程式容器** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="16805-204">Click hello **JDK** tab in hello **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="16805-205">您可以選擇其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="16805-205">You can choose from one of hello following options:</span></span>
        
        * <span data-ttu-id="16805-206">部署 hello 預設由 Azure 所提供的 JDK</span><span class="sxs-lookup"><span data-stu-id="16805-206">Deploy hello default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="16805-207">從 Azure 提供的其他 JDK 下接式清單中部署協力廠商 JDK</span><span class="sxs-lookup"><span data-stu-id="16805-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="16805-208">部署自訂 JDK，這必須封裝為 ZIP 檔案，而且公開可用或位於您的 Azure 儲存體帳戶中</span><span class="sxs-lookup"><span data-stu-id="16805-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![新增應用程式容器 JDK 索引標籤][11b]
   9. <span data-ttu-id="16805-210">當您完成所有 hello 上述步驟時，hello 新的 Web 應用程式容器 對話方塊應該類似下列圖中的 hello:</span><span class="sxs-lookup"><span data-stu-id="16805-210">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![新增應用程式容器][14]
   10. <span data-ttu-id="16805-212">按一下**確定**toocomplete hello 建立新的 Web 應用程式容器。</span><span class="sxs-lookup"><span data-stu-id="16805-212">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="16805-213">等候數秒鐘，讓 hello Web 應用程式容器 toobe hello 清單重新整理，現在應 hello 清單中選取您新建立的 web 應用程式的容器。</span><span class="sxs-lookup"><span data-stu-id="16805-213">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
6. <span data-ttu-id="16805-214">現在您已經準備就緒 toocomplete hello 初始部署您的 Web 應用程式 tooAzure;按一下**確定**toodeploy 您的 Java 應用程式 toohello 選取 Web 應用程式的容器。</span><span class="sxs-lookup"><span data-stu-id="16805-214">You are now ready toocomplete hello initial deployment of your Web App tooAzure; click **OK** toodeploy your Java application toohello selected Web App container.</span></span> <span data-ttu-id="16805-215">根據預設，您的應用程式將會部署為 hello 應用程式伺服器的子目錄。</span><span class="sxs-lookup"><span data-stu-id="16805-215">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="16805-216">如果您想 toobe 部署為 hello 根應用程式，請檢查 hello**部署 tooroot**核取方塊後，再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="16805-216">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
   
    ![部署 tooAzure][15]
7. <span data-ttu-id="16805-218">接下來，您應該會看見 hello **Azure 活動記錄檔**檢視，其中將指出 hello Web 應用程式的部署狀態。</span><span class="sxs-lookup"><span data-stu-id="16805-218">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![進度指示器][16]
   
    <span data-ttu-id="16805-220">部署 Web 應用程式 tooAzure 的 hello 程序應該採取只有幾秒鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="16805-220">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="16805-221">當您的應用程式已備妥，您會看到名為的連結**發佈**在 hello**狀態**資料行。</span><span class="sxs-lookup"><span data-stu-id="16805-221">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="16805-222">當您按一下 hello 連結時，它會帶您 tooyour 部署 Web 應用程式的首頁上，或您可以使用 hello 跟隨 toobrowse tooyour web 應用程式 > 一節中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="16805-222">When you click hello link, it will take you tooyour deployed Web App's home page, or you can use hello steps in hello following section toobrowse tooyour web app.</span></span>

## <a name="browsing-tooyour-web-app-on-azure"></a><span data-ttu-id="16805-223">瀏覽 tooyour 在 Azure 上的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="16805-223">Browsing tooyour Web App on Azure</span></span>
<span data-ttu-id="16805-224">toobrowse tooyour 在 Azure 上的 Web 應用程式，您可以使用 hello **Azure 總管**檢視。</span><span class="sxs-lookup"><span data-stu-id="16805-224">toobrowse tooyour Web App on Azure, you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="16805-225">如果 hello **Azure 總管**檢視尚未開啟，您可以再按一下來開啟**檢視**功能表 IntelliJ，然後按一下**工具視窗**，然後按一下 **服務總管**。</span><span class="sxs-lookup"><span data-stu-id="16805-225">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="16805-226">如果您先前尚未登入，則會提示您 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="16805-226">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="16805-227">當 hello **Azure 總管**檢視隨即顯示，使用依照這些步驟 toobrowse tooyour Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="16805-227">When hello **Azure Explorer** view is displayed, use follow these steps toobrowse tooyour Web App:</span></span> 

1. <span data-ttu-id="16805-228">展開 hello **Azure**節點。</span><span class="sxs-lookup"><span data-stu-id="16805-228">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="16805-229">展開 hello **Web 應用程式**節點。</span><span class="sxs-lookup"><span data-stu-id="16805-229">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="16805-230">以滑鼠右鍵按一下 hello 所需的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16805-230">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="16805-231">Hello 操作功能表出現時，按一下**瀏覽器中開啟**。</span><span class="sxs-lookup"><span data-stu-id="16805-231">When hello context menu appears, click **Open in Browser**.</span></span>
   
    ![瀏覽 Web 應用程式][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="16805-233">更新 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="16805-233">Updating your web app</span></span>
<span data-ttu-id="16805-234">更新現有執行中的 Azure Web 應用程式是一項快速又簡單的程序，而且您有兩個更新選項：</span><span class="sxs-lookup"><span data-stu-id="16805-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="16805-235">您可以更新 hello 部署現有的 Java Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16805-235">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="16805-236">您可以將額外的 Java 應用程式 toohello 發行相同的 Web 應用程式容器。</span><span class="sxs-lookup"><span data-stu-id="16805-236">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="16805-237">在任一情況下，hello 程序相同，並需要只有幾秒鐘的時間：</span><span class="sxs-lookup"><span data-stu-id="16805-237">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="16805-238">在 hello IntelliJ 專案總管 中，以滑鼠右鍵按一下您想要 tooupdate 或加入現有的 Web 應用程式容器 tooan 的 hello Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16805-238">In hello IntelliJ project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="16805-239">Hello 操作功能表出現時，選取**Azure**然後**發行為 Azure Web 應用程式...**</span><span class="sxs-lookup"><span data-stu-id="16805-239">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="16805-240">由於您之前已經登入，因此會看到您現有 Web 應用程式容器的清單。</span><span class="sxs-lookup"><span data-stu-id="16805-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="16805-241">選取 hello 一您想要 toopublish 或重新發佈您的 Java 應用程式 tooand 按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="16805-241">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="16805-242">在幾秒鐘後，hello **Azure 活動記錄檔**檢視會顯示為您更新的部署**已發佈**而且您將會無法 tooverify 網頁瀏覽器應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="16805-242">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="16805-243">啟動、停止或重新啟動現有的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="16805-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="16805-244">toostart 或停止現有的 Azure Web 應用程式容器，（包括所有部署的 hello Java 應用程式中），您可以使用 hello **Azure 總管**檢視。</span><span class="sxs-lookup"><span data-stu-id="16805-244">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="16805-245">如果 hello **Azure 總管**檢視尚未開啟，您可以再按一下來開啟**檢視**功能表 IntelliJ，然後按一下**工具視窗**，然後按一下 **服務總管**。</span><span class="sxs-lookup"><span data-stu-id="16805-245">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="16805-246">如果您先前尚未登入，則會提示您 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="16805-246">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="16805-247">當 hello **Azure 總管**檢視隨即顯示，請遵循這些步驟 toostart 使用，或停止 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="16805-247">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="16805-248">展開 hello **Azure**節點。</span><span class="sxs-lookup"><span data-stu-id="16805-248">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="16805-249">展開 hello **Web 應用程式**節點。</span><span class="sxs-lookup"><span data-stu-id="16805-249">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="16805-250">以滑鼠右鍵按一下 hello 所需的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16805-250">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="16805-251">Hello 操作功能表出現時，按一下**啟動**，**停止**，或**重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="16805-251">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="16805-252">請注意，hello 功能表選項內容感知，所以您只可以停止正在執行的 web 應用程式或啟動 web 應用程式目前未執行的。</span><span class="sxs-lookup"><span data-stu-id="16805-252">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![停止 Web 應用程式][18]

## <a name="next-steps"></a><span data-ttu-id="16805-254">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16805-254">Next Steps</span></span>
<span data-ttu-id="16805-255">針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="16805-255">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="16805-256">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="16805-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="16805-257">[安裝 Azure Toolkit for Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="16805-257">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="16805-258">[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]</span><span class="sxs-lookup"><span data-stu-id="16805-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="16805-259">[功能 hello Azure Toolkit for Eclipse 中的新功能]</span><span class="sxs-lookup"><span data-stu-id="16805-259">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="16805-260">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="16805-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="16805-261">[安裝 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="16805-261">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <bpt id="p1">*</bpt>Create a Hello World Web App for Azure in IntelliJ (This Article)<ept id="p1">*</ept>
  * <span data-ttu-id="16805-263">[新功能 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="16805-263">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="16805-264">另請參閱</span><span class="sxs-lookup"><span data-stu-id="16805-264">See Also</span></span>
<span data-ttu-id="16805-265">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="16805-265">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="16805-266">如需有關建立 Azure Web 應用程式的詳細資訊，請參閱 hello [Web 應用程式的概觀]。</span><span class="sxs-lookup"><span data-stu-id="16805-266">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[適用於 Eclipse 的 Azure 工具組]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[安裝 Azure Toolkit for Eclipse hello]: ../azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[功能 hello Azure Toolkit for Eclipse 中的新功能]: ../azure-toolkit-for-eclipse-whats-new.md
[新功能 hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Web 應用程式的概觀]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
