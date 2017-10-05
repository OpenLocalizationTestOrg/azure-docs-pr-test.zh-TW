---
title: "App Service 中的 CORS 支援 | Microsoft Docs"
description: "了解如何在 Azure App Service 中使用 CORS 支援。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: f8373cf5b2e06e6c71bce51cd9e9d5123eea7cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="9f812-103">使用 CORS 從 JavaScript 取用 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="9f812-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="9f812-104">App Service 提供內建的 [跨原始來源資源共用 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)支援，可讓 JavaScript 用戶端對 API 應用程式中所裝載的 API 進行跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="9f812-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients to make cross-domain calls to APIs that are hosted in API apps.</span></span> <span data-ttu-id="9f812-105">App Service 可讓您設定對 API 的 CORS 存取，而不需要在 API 中撰寫任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="9f812-105">App Service lets you configure CORS access to your API without writing any code in your API.</span></span>

<span data-ttu-id="9f812-106">本文包含兩個部分：</span><span class="sxs-lookup"><span data-stu-id="9f812-106">This article contains two sections:</span></span>

* <span data-ttu-id="9f812-107">[如何設定 CORS](#corsconfig) 一節說明一般會如何設定 API 應用程式、Web 應用程式或行動應用程式的 CORS。</span><span class="sxs-lookup"><span data-stu-id="9f812-107">The [How to configure CORS](#corsconfig) section explains in general how to configure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="9f812-108">本節一體適用於 App Service 支援的所有架構，包括 .NET、Node.js 和 Java。</span><span class="sxs-lookup"><span data-stu-id="9f812-108">It applies equally to all frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="9f812-109">從[繼續進行 .NET 入門教學課程](#tutorialstart)一節開始，本文就會成為示範 CORS 支援的教學課程，其示範方法是透過以您在[第一個 API Apps 入門教學課程](app-service-api-dotnet-get-started.md)中所做的為基礎進行建置。</span><span class="sxs-lookup"><span data-stu-id="9f812-109">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the article is a tutorial that demonstrates CORS support by building on what you did in [the first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="9f812-110"><a id="corsconfig"></a> 如何在 Azure App Service 中設定 CORS</span><span class="sxs-lookup"><span data-stu-id="9f812-110"><a id="corsconfig"></a> How to configure CORS in Azure App Service</span></span>
<span data-ttu-id="9f812-111">您可以在 Azure 入口網站中設定 CORS，或使用 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 工具設定。</span><span class="sxs-lookup"><span data-stu-id="9f812-111">You can configure CORS in the Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-the-azure-portal"></a><span data-ttu-id="9f812-112">在 Azure 入口網站中設定 CORS</span><span class="sxs-lookup"><span data-stu-id="9f812-112">Configure CORS in the Azure portal</span></span>
1. <span data-ttu-id="9f812-113">在瀏覽器中，移至 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="9f812-113">In a browser go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9f812-114">按一下 [應用程式服務] ，然後按一下您 API 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="9f812-114">Click **App Services**, and then click the name of your API app.</span></span>
   
    ![在入口網站中選取 API 應用程式](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="9f812-116">在 [API 應用程式] 右側開啟的 [設定] 刀鋒視窗中，尋找 [API] 區段，再按一下 [CORS]。</span><span class="sxs-lookup"><span data-stu-id="9f812-116">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![在 [設定] 刀鋒視窗中選取 CORS](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="9f812-118">在文字方塊中，輸入您想要允許的一或多個 JavaScript 呼叫來源 URL。</span><span class="sxs-lookup"><span data-stu-id="9f812-118">In the text box enter the URL or URLs that you want to allow JavaScript calls to come from.</span></span>

    <span data-ttu-id="9f812-119">例如，如果您已將 JavaScript 應用程式部署至名為 todolistangular 的 Web 應用程式，請輸入 " https://todolistangular.azurewebsites.net "。</span><span class="sxs-lookup"><span data-stu-id="9f812-119">For example, if you deployed your JavaScript application to a web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="9f812-120">或者，您也可以輸入星號 (*) 來指定接受所有的原始網域。</span><span class="sxs-lookup"><span data-stu-id="9f812-120">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="9f812-121">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9f812-121">Click **Save**.</span></span>
   
   ![按一下 [Save] (儲存)。](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="9f812-123">按一下 [儲存] 之後，API 應用程式會接受來自指定 URL 的 JavaScript 呼叫。</span><span class="sxs-lookup"><span data-stu-id="9f812-123">After you click **Save**, the API app will accept JavaScript calls from the specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="9f812-124">使用 Azure 資源管理員工具設定 CORS</span><span class="sxs-lookup"><span data-stu-id="9f812-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="9f812-125">您也可以使用 [Azure PowerShell](/powershell/azureps-cmdlets-docs) 和 [Azure CLI](../cli-install-nodejs.md) 等命令列工具中的 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)，設定 API 應用程式的 CORS。</span><span class="sxs-lookup"><span data-stu-id="9f812-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="9f812-126">如需可設定 CORS 屬性之 Azure Resource Manager 範本的範例，請開啟 [本教學課程的範例應用程式儲存機制中的 azuredeploy.json 檔案](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="9f812-126">For an example of an Azure Resource Manager template that sets the CORS property, open the [azuredeploy.json file in the repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="9f812-127">找出如下列範例所示的範本區段：</span><span class="sxs-lookup"><span data-stu-id="9f812-127">Find the section of the template that looks like the following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="9f812-128"><a id="tutorialstart"></a> 繼續進行 .NET 入門教學課程</span><span class="sxs-lookup"><span data-stu-id="9f812-128"><a id="tutorialstart"></a> Continuing the .NET getting-started tutorial</span></span>
<span data-ttu-id="9f812-129">如果您正遵循適用於 API 應用程式的 Node.js 或 Java 入門系列，則您已完成入門系列。</span><span class="sxs-lookup"><span data-stu-id="9f812-129">If you are following the Node.js or Java getting-started series for API apps, you have completed the getting started series.</span></span> <span data-ttu-id="9f812-130">請跳至 [後續步驟](#next-steps) 一節，尋找進一步了解 API Apps 的建議。</span><span class="sxs-lookup"><span data-stu-id="9f812-130">Skip to the [Next steps](#next-steps) section to find suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="9f812-131">本文其餘部分是 .NET 入門系列的延續，並假設您已成功完成 [第一個教學課程](app-service-api-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9f812-131">The remainder of this article is a continuation of the .NET getting-started series and assumes that you successfully completed [the first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-the-todolistangular-project-to-a-new-web-app"></a><span data-ttu-id="9f812-132">將 ToDoListAngular 專案部署到新的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9f812-132">Deploy the ToDoListAngular project to a new web app</span></span>
<span data-ttu-id="9f812-133">在 [第一個教學課程](app-service-api-dotnet-get-started.md)中，您建立了中介層 API 應用程式和資料層 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f812-133">In [the first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="9f812-134">在本教學課程中，您將建立單一頁面應用程式 (SPA) Web 應用程式來呼叫中介層 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f812-134">In this tutorial you create a single-page application (SPA) web app that calls the middle tier API app.</span></span> <span data-ttu-id="9f812-135">為了讓 SPA 正常運作，您必須在中介層 API 應用程式上啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="9f812-135">For the SPA to work you have to enable CORS on the middle tier API app.</span></span> 

<span data-ttu-id="9f812-136">在 [ToDoList 範例應用程式](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list)中，ToDoListAngular 專案是簡單的 AngularJS 用戶端，並且會呼叫中介層 ToDoListAPI Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="9f812-136">In the [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), the ToDoListAngular project is a simple AngularJS client that calls the middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="9f812-137">「app/scripts/todoListSvc.js」  檔案中的 JavaScript 程式碼會使用 AngularJS HTTP 提供者來呼叫 API。</span><span class="sxs-lookup"><span data-stu-id="9f812-137">The JavaScript code in the *app/scripts/todoListSvc.js* file calls the API by using the AngularJS HTTP provider.</span></span> 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-the-todolistangular-project"></a><span data-ttu-id="9f812-138">為 ToDoListAngular 專案建立新的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9f812-138">Create a new web app for the ToDoListAngular project</span></span>
<span data-ttu-id="9f812-139">建立新的 App Service Web 應用程式並對其部署專案的程序，和您 [在本系列的第一個教學課程中看到的建立及部署 API 應用程式](app-service-api-dotnet-get-started.md#createapiapp)的程序類似。</span><span class="sxs-lookup"><span data-stu-id="9f812-139">The procedure to create a new App Service web app and deploy a project to it is similar to what you saw for [creating and deploying an API app in the first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="9f812-140">唯一的差別在於應用程式類型為 [Web 應用程式] 而不是 [API 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9f812-140">The only difference is that the app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="9f812-141">如需對話方塊的螢幕擷取畫面，請參閱</span><span class="sxs-lookup"><span data-stu-id="9f812-141">For screen shots of the dialogs, see</span></span> 

1. <span data-ttu-id="9f812-142">在 [方案總管] 中，以滑鼠右鍵按一下 ToDoListAngular 專案，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="9f812-142">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="9f812-143">在 [發佈 Web] 精靈的 [設定檔] 索引標籤中，按一下 [Microsoft Azure App Service]。</span><span class="sxs-lookup"><span data-stu-id="9f812-143">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="9f812-144">在 [App Service] 對話方塊中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9f812-144">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="9f812-145">在 [建立 App Service] 對話方塊的 [主控] 索引標籤中，輸入 *azurewebsites.net* 網域中唯一的 [Web 應用程式名稱]。</span><span class="sxs-lookup"><span data-stu-id="9f812-145">In the **Hosting** tab of the **Create App Service** dialog box, enter a **Web App Name** that is unique in the *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="9f812-146">選擇您要使用的 Azure [訂用帳戶]  。</span><span class="sxs-lookup"><span data-stu-id="9f812-146">Choose the Azure **Subscription** you want to work with.</span></span>
6. <span data-ttu-id="9f812-147">在 [資源群組]  下拉式清單中，選擇您稍早建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9f812-147">In the **Resource Group** drop-down list, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="9f812-148">在 [App Service 方案]  下拉式清單中，選擇您稍早建立的同一個方案。</span><span class="sxs-lookup"><span data-stu-id="9f812-148">In the **App Service Plan** drop-down list, choose the same plan you created earlier.</span></span> 
8. <span data-ttu-id="9f812-149">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9f812-149">Click **Create**.</span></span>
   
    <span data-ttu-id="9f812-150">Visual Studio 會建立 Web 應用程式、建立其發佈設定檔，並顯示 [發佈 Web] 精靈的 [連接] 步驟。</span><span class="sxs-lookup"><span data-stu-id="9f812-150">Visual Studio creates the web app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="9f812-151">還不要按 [發佈]  。</span><span class="sxs-lookup"><span data-stu-id="9f812-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="9f812-152">在下一節中，您會設定新的 Web 應用程式以呼叫在 App Service 中執行的中介層 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f812-152">In the following section, you configure the new web app to call the middle tier API app that is running in App Service.</span></span> 

### <a name="set-the-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="9f812-153">在 Web 應用程式設定中設定中介層 URL</span><span class="sxs-lookup"><span data-stu-id="9f812-153">Set the middle tier URL in web app settings</span></span>
1. <span data-ttu-id="9f812-154">移至 [Azure 入口網站](https://portal.azure.com/)，然後瀏覽至您建立以裝載 TodoListAngular (前端) 專案的 Web 應用程式的 [Web 應用程式] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f812-154">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **Web App** blade for the web app that you created to host the TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="9f812-155">按一下 [設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="9f812-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="9f812-156">在 [應用程式設定]  區段中，新增下列金鑰和值：</span><span class="sxs-lookup"><span data-stu-id="9f812-156">In the **App settings** section, add the following key and value:</span></span>
   
   | <span data-ttu-id="9f812-157">金鑰</span><span class="sxs-lookup"><span data-stu-id="9f812-157">Key</span></span> | <span data-ttu-id="9f812-158">值</span><span class="sxs-lookup"><span data-stu-id="9f812-158">Value</span></span> | <span data-ttu-id="9f812-159">範例</span><span class="sxs-lookup"><span data-stu-id="9f812-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="9f812-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="9f812-160">toDoListAPIURL</span></span> |<span data-ttu-id="9f812-161">https://{您的中介層 API 應用程式名稱}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="9f812-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="9f812-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="9f812-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="9f812-163">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9f812-163">Click **Save**.</span></span>
   
    <span data-ttu-id="9f812-164">在 Azure 中執行程式碼時，這個值會覆寫「Web.config」  檔案中的 localhost URL。</span><span class="sxs-lookup"><span data-stu-id="9f812-164">When the code runs in Azure, this value overrides the localhost URL that is in the *Web.config* file.</span></span> 
   
    <span data-ttu-id="9f812-165">取得設定值的程式碼位於「index.cshtml」 ：</span><span class="sxs-lookup"><span data-stu-id="9f812-165">The code that gets the setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="9f812-166">「todoListSvc.js」  中的程式碼會使用設定：</span><span class="sxs-lookup"><span data-stu-id="9f812-166">The code in *todoListSvc.js* uses the setting:</span></span>
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-the-todolistangular-web-project-to-the-new-web-app"></a><span data-ttu-id="9f812-167">將 ToDoListAngular Web 專案部署到新的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9f812-167">Deploy the ToDoListAngular web project to the new web app</span></span>
* <span data-ttu-id="9f812-168">在 Visual Studio 的 [發佈 Web] 精靈的 [連接] 步驟中，按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="9f812-168">In Visual Studio, in the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="9f812-169">Visual Studio 會將 ToDoListAngular 專案部署到新的 Web 應用程式，並將瀏覽器開啟至 Web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="9f812-169">Visual Studio deploys the ToDoListAngular project to the new web app and opens a browser to the URL of the web app.</span></span> 

### <a name="test-the-application-without-cors-enabled"></a><span data-ttu-id="9f812-170">在不啟用 CORS 的情況下測試應用程式</span><span class="sxs-lookup"><span data-stu-id="9f812-170">Test the application without CORS enabled</span></span>
1. <span data-ttu-id="9f812-171">在瀏覽器開發人員工具中，開啟 [主控台] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9f812-171">In your browser Developer Tools, open the Console window.</span></span>
2. <span data-ttu-id="9f812-172">在顯示 AngularJS UI 的瀏覽器視窗中，按一下 [待辦事項清單]  連結。</span><span class="sxs-lookup"><span data-stu-id="9f812-172">In the browser window that displays the AngularJS UI, click the **To Do List** link.</span></span>
   
    <span data-ttu-id="9f812-173">JavaScript 程式碼會嘗試呼叫中介層 API 應用程式，但呼叫將會失敗，因為前端執行所在的網域與後端的不同。</span><span class="sxs-lookup"><span data-stu-id="9f812-173">The JavaScript code tries to call the middle tier API app, but the call fails because the front end is running in a different domain than the back end.</span></span> <span data-ttu-id="9f812-174">瀏覽器的 [開發人員工具主控台] 視窗會顯示跨原始來源錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="9f812-174">The browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![跨原始來源錯誤訊息](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-the-middle-tier-api-app"></a><span data-ttu-id="9f812-176">為中介層 API 應用程式設定 CORS</span><span class="sxs-lookup"><span data-stu-id="9f812-176">Configure CORS for the middle tier API app</span></span>
<span data-ttu-id="9f812-177">在本節中，您將會在 Azure 中設定中介層 ToDoListAPI API 應用程式的 CORS 設定。</span><span class="sxs-lookup"><span data-stu-id="9f812-177">In this section, you configure the CORS setting in Azure for the middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="9f812-178">此設定會允許中介層 API 應用程式從您為 ToDoListAngular 專案所建立的 Web 應用程式接收 JavaScript 呼叫。</span><span class="sxs-lookup"><span data-stu-id="9f812-178">This setting will allow the middle tier API app to receive JavaScript calls from the web app that you created for the ToDoListAngular project.</span></span>

1. <span data-ttu-id="9f812-179">在瀏覽器中，移至 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="9f812-179">In a browser, go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9f812-180">按一下 [應用程式服務] ，再按一下 ToDoListAPI (中介層) API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f812-180">Click **App Services**, and then click the ToDoListAPI (middle tier) API app.</span></span>
   
    ![在入口網站中選取 API 應用程式](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="9f812-182">在 [API 應用程式] 右側開啟的 [設定] 刀鋒視窗中，尋找 [API] 區段，再按一下 [CORS]。</span><span class="sxs-lookup"><span data-stu-id="9f812-182">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![在入口網站中選取 CORS](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="9f812-184">在文字方塊中輸入 ToDoListAngular (前端) Web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="9f812-184">In the text box, enter the URL for the ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="9f812-185">例如，如果您將 ToDoListAngular 專案部署到名為 todolistangular0121 的 Web 應用程式，則允許來自 URL `https://todolistangular0121.azurewebsites.net`的呼叫。</span><span class="sxs-lookup"><span data-stu-id="9f812-185">For example, if you deployed the ToDoListAngular project to a web app named todolistangular0121, allow calls from the URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="9f812-186">或者，您也可以輸入星號 (*) 來指定接受所有的原始網域。</span><span class="sxs-lookup"><span data-stu-id="9f812-186">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="9f812-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9f812-187">Click **Save**.</span></span>
   
   ![按一下 [Save] (儲存)。](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="9f812-189">按一下 [儲存] 之後，API 應用程式會接受來自指定 URL 的 JavaScript 呼叫。</span><span class="sxs-lookup"><span data-stu-id="9f812-189">After you click **Save**, the API app will accept JavaScript calls from the specified URL.</span></span> <span data-ttu-id="9f812-190">在這個螢幕擷取畫面中，ToDoListAPI0223 API 應用程式會接受來自 ToDoListAngular Web 應用程式的 JavaScript 用戶端呼叫。</span><span class="sxs-lookup"><span data-stu-id="9f812-190">In this screen shot, the ToDoListAPI0223 API app will accept JavaScript client calls from the ToDoListAngular web app.</span></span>

### <a name="test-the-application-with-cors-enabled"></a><span data-ttu-id="9f812-191">在啟用 CORS 的情況下測試應用程式</span><span class="sxs-lookup"><span data-stu-id="9f812-191">Test the application with CORS enabled</span></span>
* <span data-ttu-id="9f812-192">開啟瀏覽器至 Web 應用程式的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="9f812-192">Open a browser to the HTTPS URL of the web app.</span></span> 
  
    <span data-ttu-id="9f812-193">這一次，應用程式會讓您檢視、新增、編輯和刪除待辦事項項目。</span><span class="sxs-lookup"><span data-stu-id="9f812-193">This time the application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![範例應用程式的待辦事項清單頁面](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="9f812-195">App Service CORS 與 Web API CORS</span><span class="sxs-lookup"><span data-stu-id="9f812-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="9f812-196">在 Web API 專案中，您可以安裝 [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet 封裝，以便在程式碼中指定您的 API 將會接受來自哪些網域的 JavaScript 呼叫。</span><span class="sxs-lookup"><span data-stu-id="9f812-196">In a Web API project, you can install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package to specify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="9f812-197">Web API CORS 支援比 App Service CORS 支援更有彈性。</span><span class="sxs-lookup"><span data-stu-id="9f812-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="9f812-198">例如，在程式碼中您可以為不同動作方法指定不同的可接受原始來源，但對於 App Service CORS，您只能為所有 API 應用程式的方法指定一組可接受的原始來源。</span><span class="sxs-lookup"><span data-stu-id="9f812-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="9f812-199">請勿嘗試在一個 API 應用程式中同時使用 Web API CORS 和 App Service CORS。</span><span class="sxs-lookup"><span data-stu-id="9f812-199">Don't try to use both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="9f812-200">App Service CORS 會優先獲得採用，而 Web API CORS 不會有任何作用。</span><span class="sxs-lookup"><span data-stu-id="9f812-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="9f812-201">例如，如果您在 App Service 中啟用一個原始網域，並在您的 Web API 程式碼中啟用所有的原始網域，則 Azure API 應用程式僅接受來自您在 Azure 中指定之網域的呼叫。</span><span class="sxs-lookup"><span data-stu-id="9f812-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from the domain you specified in Azure.</span></span>
> 
> 

### <a name="how-to-enable-cors-in-web-api-code"></a><span data-ttu-id="9f812-202">如何在 Web API 程式碼中啟用 CORS</span><span class="sxs-lookup"><span data-stu-id="9f812-202">How to enable CORS in Web API code</span></span>
<span data-ttu-id="9f812-203">下列步驟概述啟用 Web API CORS 支援的程序。</span><span class="sxs-lookup"><span data-stu-id="9f812-203">The following steps summarize the process for enabling Web API CORS support.</span></span> <span data-ttu-id="9f812-204">如需詳細資訊，請參閱 [在 ASP.NET Web API 2 中啟用跨原始來源要求](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)。</span><span class="sxs-lookup"><span data-stu-id="9f812-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="9f812-205">在 Web API 專案中，安裝 [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="9f812-205">In a Web API project, install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="9f812-206">在 **WebApiConfig** 類別的 **Register** 方法中加入 `config.EnableCors()` 這行程式碼，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="9f812-206">Include a `config.EnableCors()` line of code in the **Register** method of the **WebApiConfig** class, as in the following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // The following line enables you to control CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. <span data-ttu-id="9f812-207">在 Web API 控制器中，加入 `System.Web.Http.Cors` 命名空間的 `using` 陳述式，並將 `EnableCors` 屬性加入至控制器類別或個別的動作方法。</span><span class="sxs-lookup"><span data-stu-id="9f812-207">In your Web API controller, add a `using` statement for the `System.Web.Http.Cors` namespace, and add the `EnableCors` attribute to the controller class or to individual action methods.</span></span> <span data-ttu-id="9f812-208">在下列範例中，整個控制器都適用 CORS 支援。</span><span class="sxs-lookup"><span data-stu-id="9f812-208">In the following example, CORS support applies to the entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="9f812-209">搭配 API Apps 使用 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="9f812-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="9f812-210">如果您搭配 API 應用程式使用 Azure API 管理，請在 API 管理而非 API 應用程式中設定 CORS。</span><span class="sxs-lookup"><span data-stu-id="9f812-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in the API app.</span></span> <span data-ttu-id="9f812-211">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="9f812-211">For more information, see the following resources:</span></span>

* [<span data-ttu-id="9f812-212">Azure API 管理概觀 (影片︰CORS 開始於 12:10)</span><span class="sxs-lookup"><span data-stu-id="9f812-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="9f812-213">API 管理跨網域原則</span><span class="sxs-lookup"><span data-stu-id="9f812-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="9f812-214">疑難排解</span><span class="sxs-lookup"><span data-stu-id="9f812-214">Troubleshooting</span></span>
<span data-ttu-id="9f812-215">如果您在瀏覽本教學課程時遇到問題，以下是一些疑難排解的相關說明。</span><span class="sxs-lookup"><span data-stu-id="9f812-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="9f812-216">確定您使用最新版本的 [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003)。</span><span class="sxs-lookup"><span data-stu-id="9f812-216">Make sure that you're using the latest version of the [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="9f812-217">確定您在 CORS 設定中輸入的是 `https`，並確定您是使用 `https` 來執行前端 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f812-217">Make sure that you entered `https` in the CORS setting, and make sure that you're using `https` to run the front-end web app.</span></span>
* <span data-ttu-id="9f812-218">確定您已在中介層 API 應用程式 (而非前端 Web 應用程式) 中輸入 CORS 設定。</span><span class="sxs-lookup"><span data-stu-id="9f812-218">Make sure that you entered the CORS setting in the middle tier API app, not in the front-end web app.</span></span>
* <span data-ttu-id="9f812-219">如果您同時在應用程式程式碼和 Azure App Service 中設定 CORS，請注意 App Service 的 CORS 設定會覆寫您在應用程式程式碼中所撰寫的任何內容。</span><span class="sxs-lookup"><span data-stu-id="9f812-219">If you're configuring CORS in both application code and Azure App Service, note that the App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="9f812-220">若要深入了解可簡化疑難排解程序的 Visual Studio 功能，請參閱 [在 Visual Studio 中針對 Azure App Service 應用程式進行疑難排解](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="9f812-220">To learn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f812-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f812-221">Next steps</span></span>
<span data-ttu-id="9f812-222">在本文中，您已看到如何啟用 App Service CORS 支援，以便用戶端 JavaScript 程式碼可以呼叫不同網域中的 API。</span><span class="sxs-lookup"><span data-stu-id="9f812-222">In this article, you saw how to enable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="9f812-223">若要深入了解 API 應用程式，請閱讀 [App Service 中的驗證簡介](../app-service/app-service-authentication-overview.md)，然後前往 [API 應用程式的使用者驗證](app-service-api-dotnet-user-principal-auth.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="9f812-223">To learn more about API apps, read the [introduction to authentication in App Service](../app-service/app-service-authentication-overview.md), and then go to the [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

