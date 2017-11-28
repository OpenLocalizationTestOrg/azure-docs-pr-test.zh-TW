---
title: "aaaCreate 您第一次在 Azure 中的 Java web 應用程式"
description: "了解如何 toorun web 部署基本的 Java 應用程式的 App Service 中的應用程式。"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="7f3cc-103">在 Azure 中建立第一個 Java Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7f3cc-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="7f3cc-104">hello [Web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)功能[Azure App Service](../app-service/app-service-value-prop-what-is.md)提供可高度擴充、 自我修補 web 主控服務。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="7f3cc-105">本快速入門示範 toodeploy Java web 應用程式 tooApp 服務使用 hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/)。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="7f3cc-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="7f3cc-108">Prerequisites</span></span>

<span data-ttu-id="7f3cc-109">toocomplete 本快速入門中，安裝：</span><span class="sxs-lookup"><span data-stu-id="7f3cc-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="7f3cc-110">可用的 hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="7f3cc-111">本快速入門使用 Eclipse Neon。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="7f3cc-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation)。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="7f3cc-113">在 Eclipse 中建立動態 Web 專案</span><span class="sxs-lookup"><span data-stu-id="7f3cc-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="7f3cc-114">在 Eclipse 中，選取 [檔案] > [新增] > [Dynamic Web Project]。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="7f3cc-115">在 hello**新動態 Web 專案**對話方塊中，名稱 hello 專案**MyFirstJavaOnAzureWebApp**，然後選取**完成**。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![新增動態 Web 專案對話方塊](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="7f3cc-117">新增 JSP 頁面</span><span class="sxs-lookup"><span data-stu-id="7f3cc-117">Add a JSP page</span></span>

<span data-ttu-id="7f3cc-118">如果未顯示 [專案總管]，請將它還原。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-118">If Project Explorer is not displayed, restore it.</span></span>

![適用於 Eclipse 的 Java EE 工作區](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="7f3cc-120">在 專案總管 中，展開 hello **MyFirstJavaOnAzureWebApp**專案。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="7f3cc-121">在 [WebContent] 上按一下滑鼠右鍵，然後選取 [新增] > [JSP 檔案]。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![專案總管中新 JSP 檔案的功能表](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="7f3cc-123">在 hello**新增 JSP 檔案**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="7f3cc-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="7f3cc-124">名稱 hello 檔**index.jsp**。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="7f3cc-125">選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-125">Select **Finish**.</span></span>

  ![[新增 JSP 檔案] 對話方塊](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="7f3cc-127">在 hello index.jsp 檔案，取代 hello `<body></body>` hello 下列標記的項目：</span><span class="sxs-lookup"><span data-stu-id="7f3cc-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="7f3cc-128">儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="7f3cc-129">發行 hello web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="7f3cc-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="7f3cc-130">在 專案總管 hello 專案中，以滑鼠右鍵按一下，然後選取**Azure** > **發佈 Azure Web 應用程式為**。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![[發佈為 Azure Web 應用程式] 內容功能表](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="7f3cc-132">在 hello **Azure 登入**對話方塊中，保留 hello**互動式**選項，然後再選取**登入**。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="7f3cc-133">請遵循 hello 登入指示。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="7f3cc-134">部署 Web 應用程式對話方塊</span><span class="sxs-lookup"><span data-stu-id="7f3cc-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="7f3cc-135">您登入 tooyour Azure 帳戶之後，hello**部署 Web 應用程式** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="7f3cc-136">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-136">Select **Create**.</span></span>

![部署 Web 應用程式對話方塊](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="7f3cc-138">建立 App Service 對話方塊</span><span class="sxs-lookup"><span data-stu-id="7f3cc-138">Create App Service dialog box</span></span>

<span data-ttu-id="7f3cc-139">hello**建立 App Service**對話方塊會顯示預設值。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="7f3cc-140">hello 數目**170602185241**示 hello 下列映像在對話方塊中會不同。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![建立 App Service 對話方塊](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="7f3cc-142">在 hello**建立 App Service**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="7f3cc-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="7f3cc-143">保留產生 hello hello web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="7f3cc-144">此名稱在整個 Azure 中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-144">This name must be unique across Azure.</span></span> <span data-ttu-id="7f3cc-145">hello 名稱是 hello hello web 應用程式的 URL 位址的一部分。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="7f3cc-146">例如： 如果 hello web 應用程式名稱是**MyJavaWebApp**，URL 是的 hello *myjavawebapp.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="7f3cc-147">保留 hello 預設網站容器。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-147">Keep hello default web container.</span></span>
* <span data-ttu-id="7f3cc-148">選取 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="7f3cc-149">在 [hello**應用程式服務方案**] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="7f3cc-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="7f3cc-150">**建立新**： 保留 hello 預設值，這是 hello hello App Service 方案名稱。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="7f3cc-151">**位置**︰選取 [西歐]，或您附近的區域。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="7f3cc-152">**定價層**： 選取 hello 可用的選項。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="7f3cc-153">如需詳細資訊，請參閱 [App Service 價格](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![建立 App Service 對話方塊](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="7f3cc-155">資源群組索引標籤</span><span class="sxs-lookup"><span data-stu-id="7f3cc-155">Resource group tab</span></span>

<span data-ttu-id="7f3cc-156">選取 hello**資源群組** 索引標籤。保留 hello 資源群組的 hello 產生的預設值。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![資源群組索引標籤](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="7f3cc-158">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="7f3cc-159">hello Azure Toolkit 建立 hello web 應用程式，並顯示進度對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![建立 App Service 進度對話方塊](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="7f3cc-161">部署 Web 應用程式對話方塊</span><span class="sxs-lookup"><span data-stu-id="7f3cc-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="7f3cc-162">在 hello**部署 Web 應用程式**對話方塊中，選取**部署 tooroot**。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="7f3cc-163">如果您有應用程式服務在*wingtiptoys.azurewebsites.net*和您不應部署 toohello 根，hello web 應用程式名為**MyFirstJavaOnAzureWebApp**太部署*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![部署 Web 應用程式對話方塊](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="7f3cc-165">hello 對話方塊所示 hello Azure、 JDK 和 web 容器選取項目。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="7f3cc-166">選取**部署**toopublish hello web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="7f3cc-167">Hello 發行完成時，選取 hello**發佈**hello 中的連結**Azure 活動記錄檔** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Azure 活動記錄對話方塊](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="7f3cc-169">恭喜！</span><span class="sxs-lookup"><span data-stu-id="7f3cc-169">Congratulations!</span></span> <span data-ttu-id="7f3cc-170">您已成功部署您的 web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-170">You have successfully deployed your web app tooAzure.</span></span> 

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="7f3cc-173">更新 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7f3cc-173">Update hello web app</span></span>

<span data-ttu-id="7f3cc-174">變更 hello 範例 JSP 程式碼 tooa 不同的訊息。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="7f3cc-175">儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-175">Save hello changes.</span></span>

<span data-ttu-id="7f3cc-176">在 專案總管 hello 專案中，以滑鼠右鍵按一下，然後選取**Azure** > **發佈 Azure Web 應用程式為**。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="7f3cc-177">hello**部署 Web 應用程式**對話方塊隨即出現並顯示 hello 您先前建立的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="7f3cc-178">選取**部署 tooroot**每次發佈。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="7f3cc-179">選取 hello web 應用程式，然後選取**部署**，將發佈 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="7f3cc-180">當 hello**發行**連結出現時，請選取它 toobrowse toohello web 應用程式看到 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="7f3cc-181">管理 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7f3cc-181">Manage hello web app</span></span>

<span data-ttu-id="7f3cc-182">移 toohello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>toosee hello web 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="7f3cc-183">從 hello 左窗格中，選取**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-183">From hello left menu, select **Resource Groups**.</span></span>

![入口網站瀏覽 tooresource 群組](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="7f3cc-185">選取 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-185">Select hello resource group.</span></span> <span data-ttu-id="7f3cc-186">hello 頁面會顯示您在本快速入門中建立的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-186">hello page shows hello resources that you created in this quickstart.</span></span>

![資源群組 myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="7f3cc-188">選取 hello web 應用程式 (**webapp 170602193915**在上述映像的 hello)。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="7f3cc-189">hello**概觀**頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-189">hello **Overview** page appears.</span></span> <span data-ttu-id="7f3cc-190">此頁面可讓您檢視 hello 應用程式執行的動作。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="7f3cc-191">您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="7f3cc-192">hello 上 hello hello 頁面左側的索引標籤會顯示 hello 不同的組態，您可以開啟。</span><span class="sxs-lookup"><span data-stu-id="7f3cc-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![Azure 入口網站中的 App Service 頁面](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="7f3cc-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7f3cc-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f3cc-195">對應自訂網域</span><span class="sxs-lookup"><span data-stu-id="7f3cc-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
