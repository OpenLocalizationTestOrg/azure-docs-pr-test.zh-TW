---
title: "aaaCreate ASP.NET web 應用程式在 Azure 中的 |Microsoft 文件"
description: "了解如何 toorun web 應用程式在 Azure App Service 中部署的 hello 預設 ASP.NET web 應用程式。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="5d103-103">在 Azure 中建立 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5d103-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="5d103-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="5d103-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="5d103-105">本快速入門示範如何 toodeploy 您的第一個 ASP.NET web 應用程式 tooAzure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d103-105">This quickstart shows how toodeploy your first ASP.NET web app tooAzure Web Apps.</span></span> <span data-ttu-id="5d103-106">當您完成時，您會有已部署 Web 應用程式的資源群，其中包含 App Service 方案和 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d103-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="5d103-107">觀看 hello 視訊 toosee 本快速入門中的動作，然後依照 hello 步驟自行 toopublish.NET 應用程式第一次在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="5d103-107">Watch hello video toosee this quickstart in action and then follow hello steps yourself toopublish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="5d103-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="5d103-108">Prerequisites</span></span>

<span data-ttu-id="5d103-109">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="5d103-109">toocomplete this tutorial:</span></span>

* <span data-ttu-id="5d103-110">安裝[Visual Studio 2017](https://www.visualstudio.com/downloads/)以下列工作負載的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d103-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
    - <span data-ttu-id="5d103-111">**ASP.NET 和 Web 開發**</span><span class="sxs-lookup"><span data-stu-id="5d103-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="5d103-112">**Azure 開發**</span><span class="sxs-lookup"><span data-stu-id="5d103-112">**Azure development**</span></span>

    ![ASP.NET 和 Web 開發及 Azure 開發 (在 [Web 和雲端] 之下)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="5d103-114">建立 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5d103-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="5d103-115">在 Visual Studio 中，選取 [檔案] > [新增] > [專案] 以建立專案。</span><span class="sxs-lookup"><span data-stu-id="5d103-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="5d103-116">在 hello**新專案**對話方塊中，選取**Visual C# > Web > ASP.NET Web 應用程式 (.NET Framework)**。</span><span class="sxs-lookup"><span data-stu-id="5d103-116">In hello **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="5d103-117">Hello 應用程式命名_myFirstAzureWebApp_，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="5d103-117">Name hello application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![New Project dialog box](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="5d103-119">您可以部署 ASP.NET web 應用程式 tooAzure 的任何型別。</span><span class="sxs-lookup"><span data-stu-id="5d103-119">You can deploy any type of ASP.NET web app tooAzure.</span></span> <span data-ttu-id="5d103-120">針對本快速入門中，選取 hello **MVC**範本，並確定驗證設定得**非驗證**。</span><span class="sxs-lookup"><span data-stu-id="5d103-120">For this quickstart, select hello **MVC** template, and make sure authentication is set too**No Authentication**.</span></span>
      
<span data-ttu-id="5d103-121">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5d103-121">Select **OK**.</span></span>

![[新增 ASP.NET 專案] 對話方塊](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="5d103-123">從 [hello] 功能表中，選取**偵錯 > 啟動但不偵錯**toorun hello web 應用程式在本機。</span><span class="sxs-lookup"><span data-stu-id="5d103-123">From hello menu, select **Debug > Start without Debugging** toorun hello web app locally.</span></span>

![在本機執行應用程式](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a><span data-ttu-id="5d103-125">發行 tooAzure</span><span class="sxs-lookup"><span data-stu-id="5d103-125">Publish tooAzure</span></span>

<span data-ttu-id="5d103-126">在 [hello**方案總管] 中**，以滑鼠右鍵按一下 hello **myFirstAzureWebApp**專案，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="5d103-126">In hello **Solution Explorer**, right-click hello **myFirstAzureWebApp** project and select **Publish**.</span></span>

![從方案總管發佈](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="5d103-128">確定已選取 [Microsoft Azure App Service]，然後選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="5d103-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![從專案概觀頁面發佈](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="5d103-130">這會開啟 hello**建立 App Service**對話方塊，可協助您在 Azure 中建立所有 hello 所需的 Azure 資源 toorun hello ASP.NET web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d103-130">This opens hello **Create App Service** dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="5d103-131">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="5d103-131">Sign in tooAzure</span></span>

<span data-ttu-id="5d103-132">在 hello**建立 App Service**對話方塊中，選取**將帳戶加入**，並登入 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d103-132">In hello **Create App Service** dialog, select **Add an account**, and sign in tooyour Azure subscription.</span></span> <span data-ttu-id="5d103-133">如果您已登入、 包含 hello 選取 hello 帳戶所需從 hello 下拉式清單中的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d103-133">If you're already signed in, select hello account containing hello desired subscription from hello dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="5d103-134">如果您已經登入，請勿選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5d103-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![登入 tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="5d103-136">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="5d103-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="5d103-137">下一步太**資源群組**，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="5d103-137">Next too**Resource Group**, select **New**.</span></span>

<span data-ttu-id="5d103-138">名稱 hello 資源群組**myResourceGroup**選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="5d103-138">Name hello resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="5d103-139">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="5d103-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="5d103-140">下一步太**App Service 方案**，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="5d103-140">Next too**App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="5d103-141">在 [hello**設定 App Service 方案**] 對話方塊中，使用下列 hello 螢幕擷取畫面的 hello 資料表中的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="5d103-141">In hello **Configure App Service Plan** dialog, use hello settings in hello table following hello screenshot.</span></span>

![建立 App Service 方案](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="5d103-143">設定</span><span class="sxs-lookup"><span data-stu-id="5d103-143">Setting</span></span> | <span data-ttu-id="5d103-144">建議的值</span><span class="sxs-lookup"><span data-stu-id="5d103-144">Suggested Value</span></span> | <span data-ttu-id="5d103-145">說明</span><span class="sxs-lookup"><span data-stu-id="5d103-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="5d103-146">App Service 方案</span><span class="sxs-lookup"><span data-stu-id="5d103-146">App Service Plan</span></span>| <span data-ttu-id="5d103-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="5d103-147">myAppServicePlan</span></span> | <span data-ttu-id="5d103-148">Hello 應用程式服務方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d103-148">Name of hello App Service plan.</span></span> |
| <span data-ttu-id="5d103-149">位置</span><span class="sxs-lookup"><span data-stu-id="5d103-149">Location</span></span> | <span data-ttu-id="5d103-150">西歐</span><span class="sxs-lookup"><span data-stu-id="5d103-150">West Europe</span></span> | <span data-ttu-id="5d103-151">hello 資料中心裝載 hello web 應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="5d103-151">hello datacenter where hello web app is hosted.</span></span> |
| <span data-ttu-id="5d103-152">大小</span><span class="sxs-lookup"><span data-stu-id="5d103-152">Size</span></span> | <span data-ttu-id="5d103-153">免費</span><span class="sxs-lookup"><span data-stu-id="5d103-153">Free</span></span> | <span data-ttu-id="5d103-154">[定價層](https://azure.microsoft.com/pricing/details/app-service/)可決定裝載功能。</span><span class="sxs-lookup"><span data-stu-id="5d103-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="5d103-155">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5d103-155">Select **OK**.</span></span>

## <a name="create-and-publish-hello-web-app"></a><span data-ttu-id="5d103-156">建立及發行 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5d103-156">Create and publish hello web app</span></span>

<span data-ttu-id="5d103-157">在**Web 應用程式名稱**，輸入唯一的應用程式名稱 (有效的字元是`a-z`， `0-9`，和`-`)，或接受 hello 自動產生的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="5d103-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept hello automatically generated unique name.</span></span> <span data-ttu-id="5d103-158">hello hello web 應用程式 URL 是`http://<app_name>.azurewebsites.net`，其中`<app_name>`是您的 web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="5d103-158">hello URL of hello web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="5d103-159">選取**建立**toostart 建立 hello Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="5d103-159">Select **Create** toostart creating hello Azure resources.</span></span>

![設定 Web 應用程式名稱](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="5d103-161">Hello 精靈完成後，其所發行 hello ASP.NET web 應用程式 tooAzure，然後啟動 hello hello 預設瀏覽器中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d103-161">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>

![Azure 中已發佈的 ASP.NET Web 應用程式](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="5d103-163">hello hello 中指定的 web 應用程式名稱[建立及發行步驟](#create-and-publish-the-web-app)hello hello 格式的 URL 前置詞作為`http://<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="5d103-163">hello web app name specified in hello [create and publish step](#create-and-publish-the-web-app) is used as hello URL prefix in hello format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="5d103-164">恭喜您，您的 ASP.NET Web 應用程式在 Azure App Service 中即時執行。</span><span class="sxs-lookup"><span data-stu-id="5d103-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="5d103-165">更新 hello 應用程式後再重新部署</span><span class="sxs-lookup"><span data-stu-id="5d103-165">Update hello app and redeploy</span></span>

<span data-ttu-id="5d103-166">從 hello**方案總管 中**，開啟_Views\Home\Index.cshtml_。</span><span class="sxs-lookup"><span data-stu-id="5d103-166">From hello **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="5d103-167">尋找 hello `<div class="jumbotron">` HTML 標記靠近 hello 頂端和 hello 整個項目取代為下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d103-167">Find hello `<div class="jumbotron">` HTML tag near hello top, and replace hello entire element with hello following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

<span data-ttu-id="5d103-168">tooredeploy tooAzure，以滑鼠右鍵按一下 hello **myFirstAzureWebApp**專案中**方案總管 中**選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="5d103-168">tooredeploy tooAzure, right-click hello **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="5d103-169">在 hello、 發行頁選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="5d103-169">In hello publish page, select **Publish**.</span></span>

<span data-ttu-id="5d103-170">當發行完成時，Visual Studio 會啟動瀏覽器 toohello hello web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="5d103-170">When publishing completes, Visual Studio launches a browser toohello URL of hello web app.</span></span>

![Azure 中已更新的 ASP.NET Web 應用程式](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="5d103-172">管理 hello Azure web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5d103-172">Manage hello Azure web app</span></span>

<span data-ttu-id="5d103-173">移 toohello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>toomanage hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d103-173">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app.</span></span>

<span data-ttu-id="5d103-174">從 hello 左窗格中，選取**應用程式服務**，然後選取 hello Azure web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="5d103-174">From hello left menu, select **App Services**, and then select hello name of your Azure web app.</span></span>

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="5d103-176">您會看到 Web 應用程式的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="5d103-176">You see your web app's Overview page.</span></span> <span data-ttu-id="5d103-177">您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="5d103-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure 入口網站中的 App Service 刀鋒視窗](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="5d103-179">hello 左側的功能表提供不同頁面設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d103-179">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="5d103-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d103-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d103-181">ASP.NET 搭配 SQL Database</span><span class="sxs-lookup"><span data-stu-id="5d103-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
