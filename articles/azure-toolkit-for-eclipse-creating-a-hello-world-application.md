---
title: "aaaCreate Hello World Azure 雲端服務在 Eclipse 中"
description: "了解如何 toocreate 簡單的 Hello World 應用程式使用 hello Azure Toolkit for Eclipse。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: dfb81374aaf78e933c0bf83a1dbd98023801491a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a><span data-ttu-id="318ba-103">在 Eclipse 中為 Azure 建立 Hello World 雲端服務</span><span class="sxs-lookup"><span data-stu-id="318ba-103">Create a Hello World Cloud Service for Azure in Eclipse</span></span>
<span data-ttu-id="318ba-104">hello 下列步驟說明如何 toocreate 及部署使用 hello Azure Toolkit for Eclipse 的基本 JSP 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="318ba-104">hello following steps show you how toocreate and deploy a basic JSP application tooAzure using hello Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="318ba-105">下文所示的 JSP 範例乃力求簡潔，不過只要與 Azure 部署相關，幾乎類似的步驟皆適用於 Java servlet。</span><span class="sxs-lookup"><span data-stu-id="318ba-105">A JSP example is shown for simplicity, but highly similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="318ba-106">hello 應用程式看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="318ba-106">hello application will look similar toohello following:</span></span>

![][ic600360]

## <a name="prerequisites"></a><span data-ttu-id="318ba-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="318ba-107">Prerequisites</span></span>
* <span data-ttu-id="318ba-108">Java Developer Kit (JDK) 1.7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="318ba-108">A Java Developer Kit (JDK), v 1.7 or later.</span></span>
* <span data-ttu-id="318ba-109">Eclipse IDE for Java EE Developers (Indigo 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="318ba-109">Eclipse IDE for Java EE Developers, Indigo or later.</span></span> <span data-ttu-id="318ba-110">這可透過 <http://www.eclipse.org/downloads/> 下載。</span><span class="sxs-lookup"><span data-stu-id="318ba-110">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="318ba-111">Java 型 Web 伺服器或應用程式伺服器的散發套件，例如 Apache Tomcat、GlassFish、JBoss Application Server、Jetty 或 IBM® WebSphere® Application Server Liberty Core。</span><span class="sxs-lookup"><span data-stu-id="318ba-111">A distribution of a Java-based web server or application server, such as Apache Tomcat, GlassFish, JBoss Application Server, Jetty, or IBM® WebSphere® Application Server Liberty Core.</span></span>
* <span data-ttu-id="318ba-112">Azure 訂用帳戶，可從 <http://azure.microsoft.com/pricing/purchase-options/> 取得。</span><span class="sxs-lookup"><span data-stu-id="318ba-112">An Azure subscription, which can be acquired from <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="318ba-113">hello Azure Toolkit for Eclipse。</span><span class="sxs-lookup"><span data-stu-id="318ba-113">hello Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="318ba-114">如需詳細資訊，請參閱[安裝 hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="318ba-114">For more information, see [Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="318ba-115">toocreate Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="318ba-115">toocreate a Hello World application</span></span>
<span data-ttu-id="318ba-116">首先，我們將從建立 Java 專案開始。</span><span class="sxs-lookup"><span data-stu-id="318ba-116">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="318ba-117">啟動 Eclipse 中，並在 hello 功能表按一下**檔案**，按一下 **新增**，然後按一下**動態 Web 專案**。</span><span class="sxs-lookup"><span data-stu-id="318ba-117">Start Eclipse, and at hello menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="318ba-118">(如果您沒有看到**動態 Web 專案**列為可用的專案，按一下後**檔案**，**新增**，請勿然後 hello 遵循： 按一下**檔案**，按一下 **新增**，按一下 **專案...**，依序展開**Web**，按一下 **動態 Web 專案**，然後按一下**下一步**。)</span><span class="sxs-lookup"><span data-stu-id="318ba-118">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File**, **New**, then do hello following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

1. <span data-ttu-id="318ba-119">本教學課程的目的而言，專案的名稱，hello **MyHelloWorld**。</span><span class="sxs-lookup"><span data-stu-id="318ba-119">For purposes of this tutorial, name hello project **MyHelloWorld**.</span></span> <span data-ttu-id="318ba-120">(請確定您使用此名稱，在本教學課程的後續步驟預期您 WAR 檔案 toobe 命名為 MyHelloWorld)。</span><span class="sxs-lookup"><span data-stu-id="318ba-120">(Ensure you use this name, subsequent steps in this tutorial expect your WAR file toobe named MyHelloWorld).</span></span> <span data-ttu-id="318ba-121">您的畫面會出現類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="318ba-121">Your screen will appear similar toohello following:</span></span>

   ![][ic589576]

1. <span data-ttu-id="318ba-122">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="318ba-122">Click **Finish**.</span></span>

1. <span data-ttu-id="318ba-123">在 Eclipse 的 [專案總管] 檢視中，展開 [MyHelloWorld]。</span><span class="sxs-lookup"><span data-stu-id="318ba-123">Within Eclipse's Project Explorer view, expand **MyHelloWorld**.</span></span> <span data-ttu-id="318ba-124">在 WebContent 上按一下滑鼠右鍵、按一下 新增，然後按一下JSP 檔案。</span><span class="sxs-lookup"><span data-stu-id="318ba-124">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

1. <span data-ttu-id="318ba-125">在 hello**新增 JSP 檔案**對話方塊中，名稱 hello 檔**index.jsp**。</span><span class="sxs-lookup"><span data-stu-id="318ba-125">In hello **New JSP File** dialog, name hello file **index.jsp**.</span></span> <span data-ttu-id="318ba-126">保留 hello 父資料夾為**MyHelloWorld/WebContent**hello 下列所示：</span><span class="sxs-lookup"><span data-stu-id="318ba-126">Keep hello parent folder as **MyHelloWorld/WebContent**, as shown in hello following:</span></span>

   ![][ic659262]

1. <span data-ttu-id="318ba-127">在 hello**選取 JSP 範本**對話方塊中的，針對這個教學課程，請選取目的**新增 JSP 檔案 (html)**按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="318ba-127">In hello **Select JSP Template** dialog, for purposes of this tutorial select **New JSP File (html)** and click **Finish**.</span></span>

1. <span data-ttu-id="318ba-128">Hello index.jsp 檔案開啟時在 Eclipse 中，增益集文字 toodynamically 顯示**Hello World ！**</span><span class="sxs-lookup"><span data-stu-id="318ba-128">When hello index.jsp file opens in Eclipse, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="318ba-129">在現有的 hello`<body>`項目。</span><span class="sxs-lookup"><span data-stu-id="318ba-129">within hello existing `<body>` element.</span></span> <span data-ttu-id="318ba-130">您已更新`<body>`內容應該會出現如下所示 hello:</span><span class="sxs-lookup"><span data-stu-id="318ba-130">Your updated `<body>` content should appear as hello following:</span></span>
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. <span data-ttu-id="318ba-131">儲存 index.jsp。</span><span class="sxs-lookup"><span data-stu-id="318ba-131">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooazure-hello-quick-and-simple-way"></a><span data-ttu-id="318ba-132">toodeploy 您的應用程式 tooAzure、 hello 快速且簡單的方式</span><span class="sxs-lookup"><span data-stu-id="318ba-132">toodeploy your application tooAzure, hello quick and simple way</span></span>
<span data-ttu-id="318ba-133">只要您有 Java web 應用程式準備好 tootest，您可以使用下列捷徑 tootry 它編寫直接 hello Azure 在雲端的 hello。</span><span class="sxs-lookup"><span data-stu-id="318ba-133">As soon as you have a Java web application ready tootest, you can use hello following shortcut tootry it out directly on hello Azure cloud.</span></span>

1. <span data-ttu-id="318ba-134">在 Eclipse 的 [專案總管] 中，按一下 [MyHelloWorld] 。</span><span class="sxs-lookup"><span data-stu-id="318ba-134">In Eclipse's Project Explorer, click **MyHelloWorld**.</span></span>

2. <span data-ttu-id="318ba-135">在 hello Eclipse 工具列中，按一下 hello**發行**下拉式按鈕，然後按一下**發佈做為 Azure 雲端服務**</span><span class="sxs-lookup"><span data-stu-id="318ba-135">In hello Eclipse toolbar, click hello **Publish** drop down button and then click **Publish As Azure Cloud Service**</span></span>

   ![][publishDropdownButton]

3. <span data-ttu-id="318ba-136">如果您要發行的 hello 這個應用程式 tooAzure 第一次，而且您尚未建立 Azure 部署專案之前此應用程式，Azure 部署專案會自動建立。</span><span class="sxs-lookup"><span data-stu-id="318ba-136">If you are publishing this application tooAzure for hello first time and you have not created an Azure deployment project for this application before, an Azure deployment project be created for you automatically.</span></span> <span data-ttu-id="318ba-137">您應該會看到 hello 遵循提示字元中，也會列出 hello JDK 封裝和應用程式伺服器將會自動部署 toorun 應用程式。</span><span class="sxs-lookup"><span data-stu-id="318ba-137">You should see hello following prompt, which also lists hello JDK package and application server that will be automatically deployed toorun your application.</span></span>

   ![][ic789598]
   
   <span data-ttu-id="318ba-138">這個快顯方法可讓快速且輕鬆 tootest 您在 Azure 中的應用程式而不需要 tooconfigure 特定伺服器或與 hello 預設值不同的 JDK。</span><span class="sxs-lookup"><span data-stu-id="318ba-138">This shortcut approach enables a quick and easy way tootest your application in Azure without having tooconfigure a specific server or JDK that is different from hello defaults.</span></span> <span data-ttu-id="318ba-139">如果您滿意 hello 預設值，您可以按一下**確定**toocontinue 以 hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="318ba-139">If you are satisfied with hello defaults, you can click **OK** toocontinue with hello following steps.</span></span>
   <span data-ttu-id="318ba-140">不過，如果您想 toochange hello JDK 或應用程式伺服器 toouse 應用程式，您稍後可以執行，藉由編輯 hello Azure 部署專案會自動建立，或者您可以按一下**取消**現在和讀取hello**關於 Azure 部署專案區段**本教學課程。</span><span class="sxs-lookup"><span data-stu-id="318ba-140">However, if you want toochange hello JDK or application server toouse for your application, you can do that later by editing hello Azure deployment project that was automatically created for you, or you can click **Cancel** now and read hello **About Azure deployment projects section** of this tutorial.</span></span>

4. <span data-ttu-id="318ba-141">在 hello**發行 tooAzure**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="318ba-141">In hello **Publish tooAzure** dialog:</span></span>

   1. <span data-ttu-id="318ba-142">如果 hello 中不有任何訂閱 tooselect**訂用帳戶**清單，但您的訂用帳戶資訊，請遵循這些步驟 tooimport:</span><span class="sxs-lookup"><span data-stu-id="318ba-142">If there are no subscriptions tooselect in hello **Subscription** list yet, follow these steps tooimport your subscription information:</span></span>
      1. <span data-ttu-id="318ba-143">按一下 [從 PUBLISH-SETTINGS 檔案匯入] 。</span><span class="sxs-lookup"><span data-stu-id="318ba-143">Click **Import from PUBLISH-SETTINGS file**.</span></span>
      2. <span data-ttu-id="318ba-144">在 hello**匯入訂用帳戶資訊** 對話方塊中，按一下 **下載發行設定檔案**。</span><span class="sxs-lookup"><span data-stu-id="318ba-144">In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="318ba-145">如果尚未登入您的 Azure 帳戶，您將會提示的 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="318ba-145">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="318ba-146">然後系統會提示您 toosave Azure 發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="318ba-146">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="318ba-147">將它儲存 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="318ba-147">Save it tooyour local machine.</span></span>
      3. <span data-ttu-id="318ba-148">仍在 hello**匯入訂用帳戶資訊** 對話方塊中，按一下 hello**瀏覽**按鈕、 選取 hello 發行在 hello 先前步驟中，在本機儲存的設定檔，然後按一下 **開啟**。</span><span class="sxs-lookup"><span data-stu-id="318ba-148">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally in hello previous step, and then click **Open**.</span></span> <span data-ttu-id="318ba-149">您的畫面應該看起來類似 toohello 下列：![][ic644267]</span><span class="sxs-lookup"><span data-stu-id="318ba-149">Your screen should look similar toohello following: ![][ic644267]</span></span>
      4. <span data-ttu-id="318ba-150">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="318ba-150">Click **OK**.</span></span>
   2. <span data-ttu-id="318ba-151">如**訂用帳戶**，選取您要使用您的部署的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="318ba-151">For **Subscription**, select hello subscription that you want use for your deployment.</span></span>
   3. <span data-ttu-id="318ba-152">如**儲存體帳戶**，選取您想 toouse，或按一下 hello 儲存體帳戶**新增**toocreate 新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="318ba-152">For **Storage account**, select hello storage account that you want toouse, or click **New** toocreate a new storage account.</span></span>
   4. <span data-ttu-id="318ba-153">如**服務名稱**，選取您想 toouse，或按一下 hello 雲端服務**新增**toocreate 新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="318ba-153">For **Service name**, select hello cloud service that you want toouse, or click **New** toocreate a new cloud service.</span></span>
   5. <span data-ttu-id="318ba-154">如**目標 OS**，選取您為您的部署想 toouse hello 作業系統 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="318ba-154">For **Target OS**, select hello version of hello operating system that you want toouse for your deployment.</span></span>
   6. <span data-ttu-id="318ba-155">針對 [目標環境]，基於本教學課程的目的，請選取 [預備]。</span><span class="sxs-lookup"><span data-stu-id="318ba-155">For **Target environment**, for purposes of this tutorial, select **Staging**.</span></span> <span data-ttu-id="318ba-156">(當您準備好 toodeploy tooyour 生產網站時，您要變更這太**生產**。)</span><span class="sxs-lookup"><span data-stu-id="318ba-156">(When you're ready toodeploy tooyour production site, you'll change this too**Production**.)</span></span>
   7. <span data-ttu-id="318ba-157">選擇性： 請確定**覆寫先前部署**會檢查您是否新的部署 tooautomatically 覆寫 hello 先前的部署。</span><span class="sxs-lookup"><span data-stu-id="318ba-157">Optional: Ensure that **Overwrite previous deployment** is checked if you want your new deployment tooautomatically overwrite hello previous deployment.</span></span> <span data-ttu-id="318ba-158">當您啟用此選項時，您會不出現 「 409 衝突 」 問題發佈 toohello 時相同的位置。</span><span class="sxs-lookup"><span data-stu-id="318ba-158">When you enable this option, you will not experience "409 conflict" issues when publishing toohello same location.</span></span>
      <span data-ttu-id="318ba-159">請注意該 hello**發行 tooAzure**對話方塊包含的區段**遠端存取**。</span><span class="sxs-lookup"><span data-stu-id="318ba-159">Note that hello **Publish tooAzure** dialog contains a section for **Remote Access**.</span></span> <span data-ttu-id="318ba-160">根據預設，不會啟用遠端存取，而且我們不會針對此範例啟用它。</span><span class="sxs-lookup"><span data-stu-id="318ba-160">By default, Remote Access is not enabled and we will not enable it for this example.</span></span> <span data-ttu-id="318ba-161">tooenable 遠端存取，您會輸入使用者名稱和密碼 toouse 時從遠端登入。</span><span class="sxs-lookup"><span data-stu-id="318ba-161">tooenable Remote Access, you would enter a user name and password toouse when remotely logging in.</span></span> <span data-ttu-id="318ba-162">如需有關遠端存取的詳細資訊，請參閱[在 Eclipse 中啟用 Azure 部署的遠端存取][Enabling Remote Access for Azure Deployments in Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="318ba-162">For more information about Remote Access, see [Enabling Remote Access for Azure Deployments in Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].</span></span>
      <span data-ttu-id="318ba-163">您**發行 tooAzure**對話方塊將會出現類似 toohello 下列：![][ic719488]</span><span class="sxs-lookup"><span data-stu-id="318ba-163">Your **Publish tooAzure** dialog will appear similar toohello following: ![][ic719488]</span></span>

5. <span data-ttu-id="318ba-164">按一下**發行**toopublish toohello 預備環境。</span><span class="sxs-lookup"><span data-stu-id="318ba-164">Click **Publish** toopublish toohello Staging environment.</span></span>

   <span data-ttu-id="318ba-165">當提示的 tooperform 完整建置，按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="318ba-165">When prompted tooperform a full build, click **Yes**.</span></span> <span data-ttu-id="318ba-166">這可能需要幾分鐘的時間 hello 第一次組建。</span><span class="sxs-lookup"><span data-stu-id="318ba-166">This may take several minutes for hello first build.</span></span>
   <span data-ttu-id="318ba-167">[Azure 活動記錄檔]  會顯示在 Eclipse 索引標籤式的檢視區段。</span><span class="sxs-lookup"><span data-stu-id="318ba-167">An **Azure Activity Log** will display in your Eclipse tabbed views section.</span></span>
   <span data-ttu-id="318ba-168">![][ic719489]您可以使用此記錄檔，以及 hello**主控台**檢視，您的部署 toosee hello 進度。</span><span class="sxs-lookup"><span data-stu-id="318ba-168">![][ic719489] You can use this log, as well as hello **Console** view, toosee hello progress of your deployment.</span></span> <span data-ttu-id="318ba-169">替代方式是在 toohello toolog [Azure 管理入口網站][Azure Management Portal]，並使用 hello**雲端服務**區段 toomonitor hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="318ba-169">An alternative is toolog in toohello [Azure Management Portal][Azure Management Portal], and use hello **Cloud Services** section toomonitor hello status.</span></span>

6. <span data-ttu-id="318ba-170">已成功部署您的部署時，hello **Azure 活動記錄檔**將顯示的狀態**發佈**。</span><span class="sxs-lookup"><span data-stu-id="318ba-170">When your deployment is successfully deployed, hello **Azure Activity Log** will show a status of **Published**.</span></span> <span data-ttu-id="318ba-171">按一下**發佈**，如下所示 hello 下列映像，以及您的瀏覽器會開啟您的部署的執行個體。</span><span class="sxs-lookup"><span data-stu-id="318ba-171">Click **Published**, as shown in hello following image, and your browser will open an instance of your deployment.</span></span>

   ![][ic719490]

<span data-ttu-id="318ba-172">由於這是預備環境部署 tooa，hello DNS 名稱會是 hello 格式 http:// 的&lt;*guid*&gt;。.cloudapp.net，且 hello URL 將包含 hello DNS 名稱再加上您的應用程式的尾碼。</span><span class="sxs-lookup"><span data-stu-id="318ba-172">Because this was a deployment tooa staging environment, hello DNS name will be of hello form http://&lt;*guid*&gt;.cloudapp.net, and hello URL will contain hello DNS name plus a suffix for your application.</span></span> <span data-ttu-id="318ba-173">例如，http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld。</span><span class="sxs-lookup"><span data-stu-id="318ba-173">For example, http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld.</span></span> <span data-ttu-id="318ba-174">(hello **MyHelloWorld**部分會區分大小寫。)您也可以查看 hello DNS 名稱，如果您按一下 hello （hello 雲端服務部分 hello 管理入口網站） 中的 hello Azure 平台管理入口網站中的部署名稱。</span><span class="sxs-lookup"><span data-stu-id="318ba-174">(hello **MyHelloWorld** portion is case-sensitive.) You can also see hello DNS name if you click hello deployment name in hello Azure Platform Management Portal (within hello Cloud Services portion of hello management portal).</span></span>

<span data-ttu-id="318ba-175">雖然本逐步解說是針對預備環境部署 toohello，部署 tooproduction 遵循除了 hello 相同的步驟，在 hello**發行 tooAzure**對話方塊中，選取**生產**而不是**臨時**hello**目標環境**。</span><span class="sxs-lookup"><span data-stu-id="318ba-175">Although this walk-through was for a deployment toohello staging environment, a deployment tooproduction follows hello same steps, except within hello **Publish tooAzure** dialog, select **Production** instead of **Staging** for hello **Target environment**.</span></span> <span data-ttu-id="318ba-176">部署 tooproduction 會導致根據您的選擇，而不是所使用的臨時的 GUID hello DNS 名稱的 URL。</span><span class="sxs-lookup"><span data-stu-id="318ba-176">A deployment tooproduction results in a URL based on hello DNS name of your choice, instead of a GUID as used for staging.</span></span>

> [!WARNING]
> <span data-ttu-id="318ba-177">此時您已部署 Azure 應用程式 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="318ba-177">At this point you have deployed your Azure application toohello cloud.</span></span> <span data-ttu-id="318ba-178">不過，再繼續進行，請注意，部署的應用程式，即使未執行，會繼續 tooaccrue 訂用帳戶的計費時間。</span><span class="sxs-lookup"><span data-stu-id="318ba-178">However, before proceeding, realize that a deployed application, even if it is not running, will continue tooaccrue billable time for your subscription.</span></span> <span data-ttu-id="318ba-179">因此，請務必從 Azure 訂用帳戶刪除任何不需要的部署。</span><span class="sxs-lookup"><span data-stu-id="318ba-179">Therefore, it is extremely important that you delete unwanted deployments from your Azure subscription.</span></span>
> 
> 

## <a name="about-azure-deployment-projects"></a><span data-ttu-id="318ba-180">關於 Azure 部署專案</span><span class="sxs-lookup"><span data-stu-id="318ba-180">About Azure deployment projects</span></span>
<span data-ttu-id="318ba-181">在順序 toodeploy 一或多個 Java 應用程式 tooAzure，需要 Azure 部署專案。</span><span class="sxs-lookup"><span data-stu-id="318ba-181">In order toodeploy one or more Java applications tooAzure, an Azure Deployment Project is needed.</span></span> <span data-ttu-id="318ba-182">它扮演 「 封裝 」，應用程式需要包裝成，在 Azure 上發行的順序 toobe toobe hello hello 角色。</span><span class="sxs-lookup"><span data-stu-id="318ba-182">It plays hello role of hello "package" that your applications need toobe wrapped into in order toobe published on Azure.</span></span>

<span data-ttu-id="318ba-183">除了 hello 您應用程式的資訊，Azure 部署專案也包含其他索引鍵的元件、 以部署的資訊最重要的是： hello，在 web 應用程式的應用程式伺服器容器 toorun 和 hello Java 執行階段 toorun 它上。</span><span class="sxs-lookup"><span data-stu-id="318ba-183">Besides hello information about your applications, an Azure deployment project also contains information about other key components of your deployment, most importantly: hello application server container toorun your web app in, and hello Java runtime toorun it on.</span></span> <span data-ttu-id="318ba-184">Azure 支援大範圍的 Java 執行階段和 Java 應用程式伺服器，讓您可以從中選擇。</span><span class="sxs-lookup"><span data-stu-id="318ba-184">Azure supports a large selection of Java runtimes and Java application servers you can choose from.</span></span>

<span data-ttu-id="318ba-185">雖然這裡使用的 hello 範例基於教育目的，已大幅簡化，Azure 部署專案也可以包含其他重要組態資訊，可讓您 toocreate 幾乎各種複雜、 可調整、 高可用性多層式雲端服務與您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="318ba-185">Although hello example used here is greatly simplified for educational purposes, an Azure deployment project can also contain other important configuration information that enables you toocreate almost arbitrarily complex, scalable, highly available, multi-tier cloud services with your applications.</span></span> <span data-ttu-id="318ba-186">您可以啟用**工作階段親和性** (「黏性工作階段」)、**快速快取**、**SSL 卸載**、**防火牆/連接埠路由**、**遠端存取**和一些其他強大功能。</span><span class="sxs-lookup"><span data-stu-id="318ba-186">You can enable **session affinity ("sticky sessions")**, **fast caching**, **SSL offloading**, **firewall/port routing**, **remote access**, and a number of other powerful capabilities.</span></span>

<span data-ttu-id="318ba-187">如果您已經完成本教學課程的 hello 前一節 (「 toodeploy 您的應用程式 tooAzure、 hello 快速且簡單的方式 」)，您現在可以看到新的 Azure 部署專案，在 [專案總管] 會自動為您產生與名為的 hello"**MyHelloWorld_onAzure**"。</span><span class="sxs-lookup"><span data-stu-id="318ba-187">If you've completed hello previous section of this tutorial ("toodeploy your application tooAzure, hello quick and simple way"), you will now see a new Azure deployment project in hello Project Explorer generated for you automatically and named "**MyHelloWorld_onAzure**".</span></span>

<span data-ttu-id="318ba-188">您可能有也開始本教學課程先自行建立空白的 Azure 部署專案，然後將加入您的應用程式 tooit。</span><span class="sxs-lookup"><span data-stu-id="318ba-188">You could have also started this tutorial by first creating a blank Azure deployment project yourself and then adding your application(s) tooit.</span></span> <span data-ttu-id="318ba-189">它是較長程序，但讓您更充分掌控 hello hello 開頭的初始組態。</span><span class="sxs-lookup"><span data-stu-id="318ba-189">It is a longer process, but giving you more control over hello initial configuration from hello beginning.</span></span>

<span data-ttu-id="318ba-190">toocreate 從頭，新的 Azure 部署專案按一下 hello**新增 Azure 部署專案**按鈕![][ic710876]。</span><span class="sxs-lookup"><span data-stu-id="318ba-190">toocreate a new Azure deployment project from scratch, click hello **New Azure Deployment Project** button ![][ic710876].</span></span>

<span data-ttu-id="318ba-191">不論您是使用現有的 Azure 部署專案，還是從頭建立，您可以 toochange 其組態設定和元件，例如 hello JDK 或 hello 應用程式伺服器，也同樣容易在任何時間。</span><span class="sxs-lookup"><span data-stu-id="318ba-191">Regardless of whether you are working with an already existing Azure deployment project, or creating one from scratch, you are able toochange its configuration settings and components, such as hello JDK or hello application server, equally easily at any time.</span></span>

<span data-ttu-id="318ba-192">toochange hello JDK、 hello 應用程式伺服器或在現有的 Azure 部署專案中的 hello 應用程式清單：</span><span class="sxs-lookup"><span data-stu-id="318ba-192">toochange hello JDK, or hello application server, or hello application list in an existing Azure deployment project:</span></span>

1. <span data-ttu-id="318ba-193">展開 [hello] 專案節點 (例如**MyHelloWorld_onAzure**) hello [專案總管] 中</span><span class="sxs-lookup"><span data-stu-id="318ba-193">Expand hello project node (e.g. **MyHelloWorld_onAzure**) in hello Project Explorer</span></span>

2. <span data-ttu-id="318ba-194">以滑鼠右鍵按一下 [WorkerRole1] </span><span class="sxs-lookup"><span data-stu-id="318ba-194">Right-click **WorkerRole1**</span></span>

3. <span data-ttu-id="318ba-195">展開 hello **Azure** hello 內容功能表中的子功能表</span><span class="sxs-lookup"><span data-stu-id="318ba-195">Expand hello **Azure** submenu in hello context menu</span></span>

4. <span data-ttu-id="318ba-196">按一下 [伺服器組態] </span><span class="sxs-lookup"><span data-stu-id="318ba-196">Click **Server Configuration**</span></span>

<span data-ttu-id="318ba-197">不論是否您藉由編輯現有的 Azure 部署專案，如上所示，啟動這些伺服器組態設定步驟，或建立一個新從頭，您會看到 hello 相同類型的對話方塊，可讓您 tooconfigure JDK、 伺服器和應用程式元件。</span><span class="sxs-lookup"><span data-stu-id="318ba-197">Regardless of whether you started these server configuration steps by editing an existing Azure deployment project as shown above, or creating a new one from scratch, you will see hello same type of dialogs allowing you tooconfigure your JDK, server and application components.</span></span> <span data-ttu-id="318ba-198">toolearn toochange hello 設定這些對話方塊中，例如 toochange hello JDK、 更如何 hello 應用程式伺服器以及新增或移除應用程式在部署中，請參閱 hello[伺服器組態屬性][ Server configuration properties]發行項。</span><span class="sxs-lookup"><span data-stu-id="318ba-198">toolearn more how toochange hello settings in those dialogs, for example toochange hello JDK, hello application server and add or remove applications in a deployment, see hello [Server configuration properties][Server configuration properties] article.</span></span>

## <a name="windows-only-toodeploy-your-application-toohello-compute-emulator"></a><span data-ttu-id="318ba-199">僅限 Windows: toodeploy 應用程式 toohello 計算模擬器</span><span class="sxs-lookup"><span data-stu-id="318ba-199">Windows only: toodeploy your application toohello compute emulator</span></span>

> [!NOTE]
> <span data-ttu-id="318ba-200">在 Windows 上，才可使用 hello Azure 模擬器。</span><span class="sxs-lookup"><span data-stu-id="318ba-200">hello Azure emulator is only available on Windows.</span></span> <span data-ttu-id="318ba-201">如果您使用 Windows 以外的作業系統，請略過本節。</span><span class="sxs-lookup"><span data-stu-id="318ba-201">Skip this section if you are using an operating system other than Windows.</span></span>
> 
> 

<span data-ttu-id="318ba-202">如果您已經建立新的 Azure 部署專案 hello 步驟描述之前，也就是隱含的方式，藉由發行您的應用程式 tooAzure，hello JDK 和應用程式伺服器已設定 hello 雲端，但不是會針對本機模擬。</span><span class="sxs-lookup"><span data-stu-id="318ba-202">If you have created a new Azure deployment project following hello steps described earlier, i.e. implicitly, by publishing your application tooAzure, hello JDK and application servers have been configured for hello cloud, but not for local emulation.</span></span> <span data-ttu-id="318ba-203">tooprepare 在 hello 本機模擬器中，測試專案，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="318ba-203">tooprepare your project for testing in hello local emulator, follow these steps:</span></span>

1. <span data-ttu-id="318ba-204">在 Eclipse 的 [專案總管] 中，按一下 [MyHelloWorld_onAzure]。</span><span class="sxs-lookup"><span data-stu-id="318ba-204">In Eclipse's Project Explorer, click **MyHelloWorld_onAzure**.</span></span>

2. <span data-ttu-id="318ba-205">以滑鼠右鍵按一下 [WorkerRole1] 。</span><span class="sxs-lookup"><span data-stu-id="318ba-205">Right-click on **WorkerRole1**.</span></span>

3. <span data-ttu-id="318ba-206">展開 hello **Azure** hello 內容功能表中的子功能表。</span><span class="sxs-lookup"><span data-stu-id="318ba-206">Expand hello **Azure** submenu in hello context menu.</span></span>

4. <span data-ttu-id="318ba-207">按一下 [伺服器組態] 。</span><span class="sxs-lookup"><span data-stu-id="318ba-207">Click **Server Configuration**.</span></span>

5. <span data-ttu-id="318ba-208">在 hello **JDK**索引標籤上，檢查是否 hello 工具組已預先設定預設值為您的本機 JDK。</span><span class="sxs-lookup"><span data-stu-id="318ba-208">On hello **JDK** tab, check if hello toolkit has pre-configured a default local JDK for you.</span></span> <span data-ttu-id="318ba-209">如果沒有，或如果您想 toochange hello 假設預設值，請確定該 hello**使用 hello JDK 進行本機測試此檔案路徑**核取方塊，並指定 hello 想 toouse JDK 安裝位置。</span><span class="sxs-lookup"><span data-stu-id="318ba-209">If not, or if you want toochange hello assumed defaults, ensure that hello **Use hello JDK from this file path for testing locally** checkbox is checked and hello JDK installation location that you want toouse is specified.</span></span> <span data-ttu-id="318ba-210">如果您想 toochange，按一下 hello**瀏覽**按鈕，然後使用 hello 瀏覽控制項，選取 hello JDK toouse hello 目錄位置。</span><span class="sxs-lookup"><span data-stu-id="318ba-210">If you want toochange it, click hello **Browse** button and using hello browse control, select hello directory location of hello JDK toouse.</span></span>

6. <span data-ttu-id="318ba-211">按一下 hello**伺服器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="318ba-211">Click hello **Server** tab.</span></span>

7. <span data-ttu-id="318ba-212">在 hello**本機伺服器路徑**在 hello hello 對話方塊底部的文字方塊中，輸入本機安裝的伺服器符合 hello 類型和底下選取頂端 hello hello 對話方塊中的 hello 伺服器主要版本號碼的 hello 路徑hello**部署這種伺服器**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="318ba-212">In hello **Local server path** text box at hello bottom of hello dialog box, enter hello path of a locally-installed server that matches hello type and major version number of hello server selected at hello top of hello dialog box, under hello **Deploy a server of this type** checkbox.</span></span> <span data-ttu-id="318ba-213">如果您想 toouse，不同的類型或 hello 應用程式伺服器的主要版本，請先變更 hello 選取該核取方塊底下。</span><span class="sxs-lookup"><span data-stu-id="318ba-213">If you want toouse a different type or major version of hello application server, change hello selection under that checkbox first.</span></span>

8. <span data-ttu-id="318ba-214">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="318ba-214">Click **OK**.</span></span>

9. <span data-ttu-id="318ba-215">在 hello Eclipse 工具列中，按一下 [hello**在 Azure 模擬器中執行**] 按鈕， ![][ic710879]。</span><span class="sxs-lookup"><span data-stu-id="318ba-215">In hello Eclipse toolbar, click hello **Run in Azure Emulator** button, ![][ic710879].</span></span> <span data-ttu-id="318ba-216">如果 hello**在 Azure 模擬器中執行**按鈕未啟用，請確定**MyHelloWorld_onAzure**已在 Eclipse 的專案總管 中選取，並確定 Eclipse 的專案總管 焦點為 hello目前的視窗。</span><span class="sxs-lookup"><span data-stu-id="318ba-216">If hello **Run in Azure Emulator** button is not enabled, ensure that **MyHelloWorld_onAzure** is selected in Eclipse's Project Explorer, and ensure that Eclipse's Project Explorer has focus as hello current window.</span></span> <span data-ttu-id="318ba-217">這將會第一次開始完整建置您的專案，然後啟動 hello 計算模擬器中的 Java web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="318ba-217">This will first start a full build of your project and then launch your Java web application in hello compute emulator.</span></span> <span data-ttu-id="318ba-218">（請注意，根據您的電腦效能特性，hello 第一次建置可能需要花費幾秒 tooa 幾分鐘的時間，但後續建置會更快）。Hello 第一次建置步驟完成後，系統會提示 Windows 使用者帳戶控制 (UAC) tooallow 由這個命令 toomake 變更 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="318ba-218">(Note that depending on your computer's performance characteristics, hello first build may take between a few seconds tooa few minutes, but subsequent builds will get faster.) After hello first build step has been completed, you will be prompted by Windows User Account Control (UAC) tooallow this command toomake changes tooyour computer.</span></span> <span data-ttu-id="318ba-219">按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="318ba-219">Click **Yes**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="318ba-220">如果您沒有看到 hello UAC 提示 核取 hello Windows 工作列的 hello UAC 圖示，然後先按一下它。</span><span class="sxs-lookup"><span data-stu-id="318ba-220">If you do not see hello UAC prompt, check hello Windows taskbar for hello UAC icon and click it first.</span></span> <span data-ttu-id="318ba-221">有時 hello UAC 提示不會顯示為最上層視窗，但只會顯示為工作列圖示。</span><span class="sxs-lookup"><span data-stu-id="318ba-221">Sometimes hello UAC prompt does not show up as a topmost window, but is visible only as a taskbar icon.</span></span>
> 
> 

1. <span data-ttu-id="318ba-222">如果有任何問題，您的專案，請檢查 hello 計算模擬器 UI toodetermine hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="318ba-222">Examine hello output of hello compute emulator UI toodetermine if there are any issues with your project.</span></span> <span data-ttu-id="318ba-223">根據您的部署的 hello 內容，它可能需要幾分鐘，您的應用程式 toobe 完全 hello 計算模擬器中啟動。</span><span class="sxs-lookup"><span data-stu-id="318ba-223">Depending on hello contents of your deployment, it may take a couple minutes for your application toobe fully started within hello compute emulator.</span></span>

2. <span data-ttu-id="318ba-224">啟動您的瀏覽器，並使用 hello URL `http://localhost:8080/MyHelloWorld` hello 位址 (hello `MyHelloWorld` hello URL 的部分會區分大小寫)。</span><span class="sxs-lookup"><span data-stu-id="318ba-224">Start your browser and use hello URL `http://localhost:8080/MyHelloWorld` as hello address (hello `MyHelloWorld` portion of hello URL is case-sensitive).</span></span> <span data-ttu-id="318ba-225">您應該會看到您的 MyHelloWorld 應用程式 （index.jsp 的 hello 輸出），類似 toohello 下列映像：</span><span class="sxs-lookup"><span data-stu-id="318ba-225">You should see your MyHelloWorld application (hello output of index.jsp), similar toohello following image:</span></span>

   ![][ic589579]

<span data-ttu-id="318ba-226">當您準備好 toostop hello Eclipse 工具列中的 hello 計算模擬器中執行您的應用程式按一下 hello**重設 Azure 模擬器** 按鈕， ![][ic710880]。</span><span class="sxs-lookup"><span data-stu-id="318ba-226">When you are ready toostop your application from running in hello compute emulator, in hello Eclipse toolbar, click hello **Reset Azure Emulator** button, ![][ic710880].</span></span>

## <a name="toodelete-your-deployment"></a><span data-ttu-id="318ba-227">toodelete 您的部署</span><span class="sxs-lookup"><span data-stu-id="318ba-227">toodelete your deployment</span></span>
<span data-ttu-id="318ba-228">您的部署內 hello Azure Toolkit for Eclipse，請確認 toodelete **MyHelloWorld_onAzure**已在 Eclipse 的專案總管] 中選取，請 hello Eclipse [專案總管] 具有焦點，，然後按一下hello 目前視窗hello**取消發行** 按鈕， ![][ic710883]，hello Eclipse 工具列中。</span><span class="sxs-lookup"><span data-stu-id="318ba-228">toodelete your deployment within hello Azure Toolkit for Eclipse, ensure that **MyHelloWorld_onAzure** is selected in Eclipse's Project Explorer, ensure hello Eclipse Project Explorer has hello current window focus, and then click hello **Unpublish** button, ![][ic710883], in hello Eclipse toolbar.</span></span> <span data-ttu-id="318ba-229">(您可以執行 hello 相同的作業，以滑鼠右鍵按一下**MyHelloWorld_onAzure**在 Eclipse 的專案總管 中，按一下**Azure** ，然後按一下**從 Azure 雲端解除部署**.)這會顯示 hello**取消發行 Azure 專案**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="318ba-229">(You could do hello same operation by right-clicking **MyHelloWorld_onAzure** in Eclipse's Project Explorer, clicking **Azure** and then clicking **Undeploy from Azure Cloud**.) This will display hello **Unpublish Azure Project** dialog.</span></span>

![][ic719491]

<span data-ttu-id="318ba-230">選取包含您的部署，您想 toodelete，然後再按一下選取的 hello 部署的 hello 訂用帳戶和雲端服務**取消發行**。</span><span class="sxs-lookup"><span data-stu-id="318ba-230">Select hello subscription and cloud service that contains your deployment, select hello deployment that you want toodelete, and then click **Unpublish**.</span></span>

<span data-ttu-id="318ba-231">(替代 toousing hello toolkit toodelete hello 部署為 toouse hello**雲端服務**hello Azure 管理入口網站區段： 巡覽 tooyour 部署，加以選取，然後按 [hello**刪除** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="318ba-231">(An alternative toousing hello toolkit toodelete hello deployment is toouse hello **Cloud Services** section of hello Azure Management Portal: Navigate tooyour deployment, select it, and then click hello **Delete** button.</span></span> <span data-ttu-id="318ba-232">這將會停止，然後再刪除，hello 部署。</span><span class="sxs-lookup"><span data-stu-id="318ba-232">This will stop, and then delete, hello deployment.</span></span> <span data-ttu-id="318ba-233">如果您只想 toostop hello 部署，並將它刪除，請按一下 hello**停止**按鈕而不是 hello**刪除**按鈕，如上述，但如果您不會刪除 hello 部署，則可計費費用將為您的部署 tooaccrue 即使繼續已停止）。</span><span class="sxs-lookup"><span data-stu-id="318ba-233">If you only want toostop hello deployment and not delete it, click hello **Stop** button instead of hello **Delete** button, but as mentioned above, if you do not delete hello deployment, billable charges will continue tooaccrue for your deployment even if it is stopped).</span></span>

## <a name="see-also"></a><span data-ttu-id="318ba-234">另請參閱</span><span class="sxs-lookup"><span data-stu-id="318ba-234">See Also</span></span>
<span data-ttu-id="318ba-235">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="318ba-235">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="318ba-236">[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="318ba-236">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="318ba-237">[功能 hello Azure Toolkit for Eclipse 中的新功能][What's New in hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="318ba-237">[What's New in hello Azure Toolkit for Eclipse][What's New in hello Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="318ba-238">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="318ba-238">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
