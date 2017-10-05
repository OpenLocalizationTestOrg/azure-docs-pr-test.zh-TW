---
title: "在 Azure 中建立第一個 Java Web 應用程式"
description: "藉由部署基本 Java 應用程式，了解如何在 App Service 中執行 Web 應用程式。"
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
ms.openlocfilehash: b91b9bde5eb8ea0d7e2196056b635fe54095e748
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="8ee64-103">在 Azure 中建立第一個 Java Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8ee64-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="8ee64-104">[Azure App Service](../app-service/app-service-value-prop-what-is.md) 的 [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 功能提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="8ee64-104">The [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="8ee64-105">本快速入門示範如何使用 [Eclipse IDE for Java EE Developers](http://www.eclipse.org/) 將 Java Web 應用程式部署到 App Service。</span><span class="sxs-lookup"><span data-stu-id="8ee64-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="8ee64-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="8ee64-108">Prerequisites</span></span>

<span data-ttu-id="8ee64-109">若要完成本快速入門，請安裝：</span><span class="sxs-lookup"><span data-stu-id="8ee64-109">To complete this quickstart, install:</span></span>

* <span data-ttu-id="8ee64-110">免費的 [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="8ee64-110">The free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="8ee64-111">本快速入門使用 Eclipse Neon。</span><span class="sxs-lookup"><span data-stu-id="8ee64-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="8ee64-112">[適用於 Eclipse 的 Azure 工具組](/azure/azure-toolkit-for-eclipse-installation)。</span><span class="sxs-lookup"><span data-stu-id="8ee64-112">The [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="8ee64-113">在 Eclipse 中建立動態 Web 專案</span><span class="sxs-lookup"><span data-stu-id="8ee64-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="8ee64-114">在 Eclipse 中，選取 [檔案] > [新增] > [Dynamic Web Project]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="8ee64-115">在 [新增動態 Web 專案] 對話方塊中，將專案命名為 **MyFirstJavaOnAzureWebApp**，然後選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-115">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![新增動態 Web 專案對話方塊](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="8ee64-117">新增 JSP 頁面</span><span class="sxs-lookup"><span data-stu-id="8ee64-117">Add a JSP page</span></span>

<span data-ttu-id="8ee64-118">如果未顯示 [專案總管]，請將它還原。</span><span class="sxs-lookup"><span data-stu-id="8ee64-118">If Project Explorer is not displayed, restore it.</span></span>

![適用於 Eclipse 的 Java EE 工作區](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="8ee64-120">在 [專案總管] 中，展開 **MyFirstJavaOnAzureWebApp** 專案。</span><span class="sxs-lookup"><span data-stu-id="8ee64-120">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="8ee64-121">在 [WebContent] 上按一下滑鼠右鍵，然後選取 [新增] > [JSP 檔案]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![專案總管中新 JSP 檔案的功能表](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="8ee64-123">在 [新增 JSP 檔案] 對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="8ee64-123">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="8ee64-124">將檔案命名為 **index.jsp**。</span><span class="sxs-lookup"><span data-stu-id="8ee64-124">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="8ee64-125">選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-125">Select **Finish**.</span></span>

  ![[新增 JSP 檔案] 對話方塊](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="8ee64-127">在 index.jsp 檔案中，以下列標記取代 `<body></body>` 元素：</span><span class="sxs-lookup"><span data-stu-id="8ee64-127">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="8ee64-128">儲存變更。</span><span class="sxs-lookup"><span data-stu-id="8ee64-128">Save the changes.</span></span>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="8ee64-129">將 Web 應用程式發佈至 Azure</span><span class="sxs-lookup"><span data-stu-id="8ee64-129">Publish the web app to Azure</span></span>

<span data-ttu-id="8ee64-130">在 [專案總管] 中，以滑鼠右鍵按一下專案名稱，然後選取 [Azure] > [發佈為 Azure Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-130">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![[發佈為 Azure Web 應用程式] 內容功能表](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="8ee64-132">在 [Azure 登入] 對話方塊中，保留 [互動式]，然後選取 [登入]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-132">In the **Azure Sign In** dialog box, keep the **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="8ee64-133">遵循登入指示進行。</span><span class="sxs-lookup"><span data-stu-id="8ee64-133">Follow the sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="8ee64-134">部署 Web 應用程式對話方塊</span><span class="sxs-lookup"><span data-stu-id="8ee64-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="8ee64-135">在您登入 Azure 帳戶後，[部署 Web 應用程式] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="8ee64-135">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="8ee64-136">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-136">Select **Create**.</span></span>

![部署 Web 應用程式對話方塊](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="8ee64-138">建立 App Service 對話方塊</span><span class="sxs-lookup"><span data-stu-id="8ee64-138">Create App Service dialog box</span></span>

<span data-ttu-id="8ee64-139">顯示的 [建立 App Service] 對話方塊會包含預設值。</span><span class="sxs-lookup"><span data-stu-id="8ee64-139">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="8ee64-140">下圖中顯示的數字 **170602185241** 不同於您的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8ee64-140">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![建立 App Service 對話方塊](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="8ee64-142">在 [建立 App Service] 對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="8ee64-142">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="8ee64-143">保留針對 Web 應用程式產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="8ee64-143">Keep the generated name for the web app.</span></span> <span data-ttu-id="8ee64-144">此名稱在整個 Azure 中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="8ee64-144">This name must be unique across Azure.</span></span> <span data-ttu-id="8ee64-145">名稱是 Web 應用程式 URL 位址的一部分。</span><span class="sxs-lookup"><span data-stu-id="8ee64-145">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="8ee64-146">例如：如果 Web 應用程式名稱是 **MyJavaWebApp**，URL 是 *myjavawebapp.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="8ee64-146">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="8ee64-147">保留預設 Web 容器。</span><span class="sxs-lookup"><span data-stu-id="8ee64-147">Keep the default web container.</span></span>
* <span data-ttu-id="8ee64-148">選取 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ee64-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="8ee64-149">在 [App Service 方案] 索引標籤上：</span><span class="sxs-lookup"><span data-stu-id="8ee64-149">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="8ee64-150">**新建**：保留預設值，這是 App Service 方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="8ee64-150">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="8ee64-151">**位置**︰選取 [西歐]，或您附近的區域。</span><span class="sxs-lookup"><span data-stu-id="8ee64-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="8ee64-152">**定價層**：選取免費選項。</span><span class="sxs-lookup"><span data-stu-id="8ee64-152">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="8ee64-153">如需詳細資訊，請參閱 [App Service 價格](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="8ee64-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![建立 App Service 對話方塊](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="8ee64-155">資源群組索引標籤</span><span class="sxs-lookup"><span data-stu-id="8ee64-155">Resource group tab</span></span>

<span data-ttu-id="8ee64-156">選取 [資源群組] 索引標籤。保留針對資源群組產生的預設值。</span><span class="sxs-lookup"><span data-stu-id="8ee64-156">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![資源群組索引標籤](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="8ee64-158">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-158">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="8ee64-159">Azure Toolkit 會建立 Web 應用程式並顯示進度對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8ee64-159">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![建立 App Service 進度對話方塊](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="8ee64-161">部署 Web 應用程式對話方塊</span><span class="sxs-lookup"><span data-stu-id="8ee64-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="8ee64-162">在 [部署 Web 應用程式] 對話方塊中，選取 [部署至根目錄]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-162">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="8ee64-163">如果您有位於 wingtiptoys.azurewebsites.net 的應用程式服務，而您未將它部署至根目錄，則命名為 **MyFirstJavaOnAzureWebApp** 的 Web 應用程式會部署至 wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp。</span><span class="sxs-lookup"><span data-stu-id="8ee64-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![部署 Web 應用程式對話方塊](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="8ee64-165">此對話方塊會顯示 Azure、JDK 和 Web 容器選取項目。</span><span class="sxs-lookup"><span data-stu-id="8ee64-165">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="8ee64-166">選取 [部署] 將 Web 應用程式發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="8ee64-166">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="8ee64-167">當發佈完成時，選取 [Azure 活動記錄] 對話方塊中的 [已發佈] 連結。</span><span class="sxs-lookup"><span data-stu-id="8ee64-167">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Azure 活動記錄對話方塊](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="8ee64-169">恭喜！</span><span class="sxs-lookup"><span data-stu-id="8ee64-169">Congratulations!</span></span> <span data-ttu-id="8ee64-170">您已成功將 Web 應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="8ee64-170">You have successfully deployed your web app to Azure.</span></span> 

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="8ee64-173">更新 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8ee64-173">Update the web app</span></span>

<span data-ttu-id="8ee64-174">將範例 JSP 程式碼變更為不同的訊息。</span><span class="sxs-lookup"><span data-stu-id="8ee64-174">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="8ee64-175">儲存變更。</span><span class="sxs-lookup"><span data-stu-id="8ee64-175">Save the changes.</span></span>

<span data-ttu-id="8ee64-176">在 [專案總管] 中，以滑鼠右鍵按一下專案名稱，然後選取 [Azure] > [發佈為 Azure Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-176">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="8ee64-177">[部署 Web 應用程式] 對話方塊隨即出現，並顯示您先前建立的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="8ee64-177">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="8ee64-178">每次發佈時都選取 [部署至根目錄]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-178">Select **Deploy to root** each time you publish.</span></span>
>

<span data-ttu-id="8ee64-179">選取 Web 應用程式，然後選取 [部署] 來發佈變更。</span><span class="sxs-lookup"><span data-stu-id="8ee64-179">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="8ee64-180">當 [發佈] 連結出現時，請加以選取來瀏覽至 Web 應用程式並查看變更。</span><span class="sxs-lookup"><span data-stu-id="8ee64-180">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="8ee64-181">管理 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8ee64-181">Manage the web app</span></span>

<span data-ttu-id="8ee64-182">請移至 <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>，以查看您所建立的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ee64-182">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="8ee64-183">從左功能表，選取 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="8ee64-183">From the left menu, select **Resource Groups**.</span></span>

![入口網站瀏覽至資源群組](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="8ee64-185">選取資源群組。</span><span class="sxs-lookup"><span data-stu-id="8ee64-185">Select the resource group.</span></span> <span data-ttu-id="8ee64-186">此頁面會顯示您在本快速入門中建立的資源。</span><span class="sxs-lookup"><span data-stu-id="8ee64-186">The page shows the resources that you created in this quickstart.</span></span>

![資源群組 myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="8ee64-188">選取 Web 應用程式 (上圖中的 **webapp 170602193915**)。</span><span class="sxs-lookup"><span data-stu-id="8ee64-188">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="8ee64-189">[概觀] 頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="8ee64-189">The **Overview** page appears.</span></span> <span data-ttu-id="8ee64-190">此頁面可讓您檢視應用程式的執行方式。</span><span class="sxs-lookup"><span data-stu-id="8ee64-190">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="8ee64-191">您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="8ee64-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="8ee64-192">頁面左側的索引標籤會顯示您可以開啟的各種組態。</span><span class="sxs-lookup"><span data-stu-id="8ee64-192">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![Azure 入口網站中的 App Service 頁面](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="8ee64-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ee64-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8ee64-195">對應自訂網域</span><span class="sxs-lookup"><span data-stu-id="8ee64-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
