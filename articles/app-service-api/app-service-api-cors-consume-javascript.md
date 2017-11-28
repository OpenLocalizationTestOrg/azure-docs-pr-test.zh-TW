---
title: "App Service 中支援 aaaCORS |Microsoft 文件"
description: "了解如何 toouse CORS 支援 Azure Azure App Service 中。"
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
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="2f93d-103">使用 CORS 從 JavaScript 取用 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="2f93d-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="2f93d-104">應用程式服務提供的內建支援[跨原始資源共用 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)，可讓 JavaScript 用戶端 toomake 跨網域呼叫 tooAPIs 所裝載的應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f93d-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients toomake cross-domain calls tooAPIs that are hosted in API apps.</span></span> <span data-ttu-id="2f93d-105">應用程式服務可讓您設定 CORS 存取 tooyour 應用程式開發介面，而不需要撰寫任何程式碼中您的 API。</span><span class="sxs-lookup"><span data-stu-id="2f93d-105">App Service lets you configure CORS access tooyour API without writing any code in your API.</span></span>

<span data-ttu-id="2f93d-106">本文包含兩個部分：</span><span class="sxs-lookup"><span data-stu-id="2f93d-106">This article contains two sections:</span></span>

* <span data-ttu-id="2f93d-107">hello[如何 tooconfigure CORS](#corsconfig)章節將說明一般方式 tooconfigure CORS API 應用程式、 web 應用程式，或行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f93d-107">hello [How tooconfigure CORS](#corsconfig) section explains in general how tooconfigure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="2f93d-108">這同樣適用於 tooall 架構應用程式服務，包括.NET、 Node.js 和 Java 支援。</span><span class="sxs-lookup"><span data-stu-id="2f93d-108">It applies equally tooall frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="2f93d-109">開頭為 hello[繼續 hello.NET 使用者入門教學課程](#tutorialstart)章節 hello 發行項是示範 CORS 支援藉由在您未建置的教學課程[hello 第一個應用程式開發介面應用程式取得入門教學課程](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2f93d-109">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello article is a tutorial that demonstrates CORS support by building on what you did in [hello first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="2f93d-110"><a id="corsconfig"></a>如何在 Azure 應用程式服務的 CORS tooconfigure</span><span class="sxs-lookup"><span data-stu-id="2f93d-110"><a id="corsconfig"></a> How tooconfigure CORS in Azure App Service</span></span>
<span data-ttu-id="2f93d-111">您可以在 hello Azure 入口網站中，或藉由設定 CORS [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)工具。</span><span class="sxs-lookup"><span data-stu-id="2f93d-111">You can configure CORS in hello Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-hello-azure-portal"></a><span data-ttu-id="2f93d-112">在 hello Azure 入口網站中設定 CORS</span><span class="sxs-lookup"><span data-stu-id="2f93d-112">Configure CORS in hello Azure portal</span></span>
1. <span data-ttu-id="2f93d-113">在瀏覽器中前往 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="2f93d-113">In a browser go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2f93d-114">按一下**應用程式服務**，然後按一下hello API 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="2f93d-114">Click **App Services**, and then click hello name of your API app.</span></span>
   
    ![在入口網站中選取 API 應用程式](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="2f93d-116">在 hello**設定**刀鋒視窗中開啟 toohello 右邊 hello **API 應用程式**刀鋒視窗中，尋找 hello **API**區段，然後再按一下**CORS**。</span><span class="sxs-lookup"><span data-stu-id="2f93d-116">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![在 [設定] 刀鋒視窗中選取 CORS](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="2f93d-118">在 [hello] 文字方塊中輸入 hello URL 或您想要從 tooallow JavaScript 呼叫 toocome 的 Url。</span><span class="sxs-lookup"><span data-stu-id="2f93d-118">In hello text box enter hello URL or URLs that you want tooallow JavaScript calls toocome from.</span></span>

    <span data-ttu-id="2f93d-119">例如，如果您部署 JavaScript 應用程式 tooa web 應用程式名為 todolistangular，輸入 「 https://todolistangular.azurewebsites.net"。</span><span class="sxs-lookup"><span data-stu-id="2f93d-119">For example, if you deployed your JavaScript application tooa web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="2f93d-120">或者，您可以輸入接受的所有原始網域星號 （*） toospecify。</span><span class="sxs-lookup"><span data-stu-id="2f93d-120">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="2f93d-121">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2f93d-121">Click **Save**.</span></span>
   
   ![按一下 [Save] \(儲存)。](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="2f93d-123">按一下 之後**儲存**，hello API 應用程式將會接受 JavaScript 呼叫 hello 從指定的 Url。</span><span class="sxs-lookup"><span data-stu-id="2f93d-123">After you click **Save**, hello API app will accept JavaScript calls from hello specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="2f93d-124">使用 Azure 資源管理員工具設定 CORS</span><span class="sxs-lookup"><span data-stu-id="2f93d-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="2f93d-125">您也可以設定應用程式開發介面應用程式的 CORS，使用[Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)在命令列工具，像是[Azure PowerShell](/powershell/azureps-cmdlets-docs)和 hello [Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="2f93d-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="2f93d-126">例如 hello CORS 屬性設定的 Azure Resource Manager 範本中，開啟 hello [hello 儲存機制中用於本教學課程範例應用程式的 azuredeploy.json 檔案](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="2f93d-126">For an example of an Azure Resource Manager template that sets hello CORS property, open hello [azuredeploy.json file in hello repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="2f93d-127">尋找 hello 區段，看起來像下列範例中的 hello hello 範本：</span><span class="sxs-lookup"><span data-stu-id="2f93d-127">Find hello section of hello template that looks like hello following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="2f93d-128"><a id="tutorialstart"></a>繼續 hello.NET 使用者入門教學課程</span><span class="sxs-lookup"><span data-stu-id="2f93d-128"><a id="tutorialstart"></a> Continuing hello .NET getting-started tutorial</span></span>
<span data-ttu-id="2f93d-129">如果您要遵照 hello Node.js 或 Java 開始使用數列的 API 應用程式，您必須已完成的 hello 取得已啟動的數列。</span><span class="sxs-lookup"><span data-stu-id="2f93d-129">If you are following hello Node.js or Java getting-started series for API apps, you have completed hello getting started series.</span></span> <span data-ttu-id="2f93d-130">略過 toohello[後續步驟](#next-steps)區段 toofind 進一步深入了解應用程式開發介面應用程式的建議。</span><span class="sxs-lookup"><span data-stu-id="2f93d-130">Skip toohello [Next steps](#next-steps) section toofind suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="2f93d-131">hello 這篇文章的其餘部分將延續 hello.NET 開始使用數列的並假設您已成功完成[hello 第一個教學課程](app-service-api-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="2f93d-131">hello remainder of this article is a continuation of hello .NET getting-started series and assumes that you successfully completed [hello first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a><span data-ttu-id="2f93d-132">部署 hello ToDoListAngular 專案 tooa 新 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2f93d-132">Deploy hello ToDoListAngular project tooa new web app</span></span>
<span data-ttu-id="2f93d-133">在[hello 第一個教學課程](app-service-api-dotnet-get-started.md)，您所建立的中介層應用程式開發介面應用程式和資料層應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f93d-133">In [hello first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="2f93d-134">在此教學課程中您建立單一頁面應用程式 (SPA) web 應用程式呼叫 hello 中介層應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f93d-134">In this tutorial you create a single-page application (SPA) web app that calls hello middle tier API app.</span></span> <span data-ttu-id="2f93d-135">Hello SPA toowork 您還有 tooenable CORS hello 中介層應用程式開發介面應用程式上。</span><span class="sxs-lookup"><span data-stu-id="2f93d-135">For hello SPA toowork you have tooenable CORS on hello middle tier API app.</span></span> 

<span data-ttu-id="2f93d-136">在 hello [ToDoList 範例應用程式](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list)，hello ToDoListAngular 專案是簡單的 AngularJS 用戶端呼叫 hello 中介層 ToDoListAPI Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="2f93d-136">In hello [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular project is a simple AngularJS client that calls hello middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="2f93d-137">hello hello 中的 JavaScript 程式碼*app/scripts/todoListSvc.js*檔案呼叫 hello API 使用 hello AngularJS HTTP 提供者。</span><span class="sxs-lookup"><span data-stu-id="2f93d-137">hello JavaScript code in hello *app/scripts/todoListSvc.js* file calls hello API by using hello AngularJS HTTP provider.</span></span> 

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

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a><span data-ttu-id="2f93d-138">建立新的 web 應用程式 hello ToDoListAngular 專案</span><span class="sxs-lookup"><span data-stu-id="2f93d-138">Create a new web app for hello ToDoListAngular project</span></span>
<span data-ttu-id="2f93d-139">hello 程序 toocreate 新的 App Service web 應用程式並部署專案 tooit 是您所看到的類似 toowhat[建立及部署 API 應用程式在 hello 本系列的第一個教學課程](app-service-api-dotnet-get-started.md#createapiapp)。</span><span class="sxs-lookup"><span data-stu-id="2f93d-139">hello procedure toocreate a new App Service web app and deploy a project tooit is similar toowhat you saw for [creating and deploying an API app in hello first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="2f93d-140">hello 差異是該 hello 應用程式類型只是**Web 應用程式**而不是**API 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2f93d-140">hello only difference is that hello app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="2f93d-141">Hello 對話方塊的螢幕擷取畫面，請參閱</span><span class="sxs-lookup"><span data-stu-id="2f93d-141">For screen shots of hello dialogs, see</span></span> 

1. <span data-ttu-id="2f93d-142">在**方案總管 中**hello ToDoListAngular 專案中，以滑鼠右鍵按一下，然後按**發行**。</span><span class="sxs-lookup"><span data-stu-id="2f93d-142">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="2f93d-143">在 hello**設定檔**hello 索引標籤**發行 Web**精靈 中，按一下**Microsoft Azure App Service**。</span><span class="sxs-lookup"><span data-stu-id="2f93d-143">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="2f93d-144">在 hello **App Service**對話方塊中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="2f93d-144">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="2f93d-145">在 [hello**主控**hello] 索引標籤**建立應用程式服務**對話方塊方塊中，輸入**Web 應用程式名稱**，都是唯一的 hello *.azurewebsites.net*網域。</span><span class="sxs-lookup"><span data-stu-id="2f93d-145">In hello **Hosting** tab of hello **Create App Service** dialog box, enter a **Web App Name** that is unique in hello *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="2f93d-146">選擇 hello Azure**訂用帳戶**想與 toowork。</span><span class="sxs-lookup"><span data-stu-id="2f93d-146">Choose hello Azure **Subscription** you want toowork with.</span></span>
6. <span data-ttu-id="2f93d-147">在 hello**資源群組**下拉式清單中，選擇 hello 您稍早建立的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="2f93d-147">In hello **Resource Group** drop-down list, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="2f93d-148">在 hello**應用程式服務方案**下拉式清單中，選擇 hello 相同您稍早建立的計畫。</span><span class="sxs-lookup"><span data-stu-id="2f93d-148">In hello **App Service Plan** drop-down list, choose hello same plan you created earlier.</span></span> 
8. <span data-ttu-id="2f93d-149">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="2f93d-149">Click **Create**.</span></span>
   
    <span data-ttu-id="2f93d-150">Visual Studio 建立 hello web 應用程式，建立的發行設定檔，並顯示 hello**連接**步驟 hello**發行 Web**精靈。</span><span class="sxs-lookup"><span data-stu-id="2f93d-150">Visual Studio creates hello web app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="2f93d-151">還不要按 [發佈]  。</span><span class="sxs-lookup"><span data-stu-id="2f93d-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="2f93d-152">在 hello 下列區段，您可以設定 hello 新 web 應用程式 toocall hello 中介層應用程式開發介面應用程式正在執行中應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="2f93d-152">In hello following section, you configure hello new web app toocall hello middle tier API app that is running in App Service.</span></span> 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="2f93d-153">Web 應用程式設定中設定 hello 中介層 URL</span><span class="sxs-lookup"><span data-stu-id="2f93d-153">Set hello middle tier URL in web app settings</span></span>
1. <span data-ttu-id="2f93d-154">移 toohello [Azure 入口網站](https://portal.azure.com/)，然後瀏覽 toohello **Web 應用程式**hello 您建立 toohost hello TodoListAngular （前端） 專案的 web 應用程式 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2f93d-154">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **Web App** blade for hello web app that you created toohost hello TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="2f93d-155">按一下 [設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="2f93d-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="2f93d-156">在 hello**應用程式設定**區段中，新增 hello 下列索引鍵和值：</span><span class="sxs-lookup"><span data-stu-id="2f93d-156">In hello **App settings** section, add hello following key and value:</span></span>
   
   | <span data-ttu-id="2f93d-157">Key</span><span class="sxs-lookup"><span data-stu-id="2f93d-157">Key</span></span> | <span data-ttu-id="2f93d-158">值</span><span class="sxs-lookup"><span data-stu-id="2f93d-158">Value</span></span> | <span data-ttu-id="2f93d-159">範例</span><span class="sxs-lookup"><span data-stu-id="2f93d-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="2f93d-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="2f93d-160">toDoListAPIURL</span></span> |<span data-ttu-id="2f93d-161">https://{您的中介層 API 應用程式名稱}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="2f93d-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="2f93d-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="2f93d-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="2f93d-163">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2f93d-163">Click **Save**.</span></span>
   
    <span data-ttu-id="2f93d-164">當 hello 程式碼在 Azure 中執行時，這個值會覆寫 hello localhost URL 會在 hello *Web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="2f93d-164">When hello code runs in Azure, this value overrides hello localhost URL that is in hello *Web.config* file.</span></span> 
   
    <span data-ttu-id="2f93d-165">取得 hello 設定值的 hello 程式碼位於*index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="2f93d-165">hello code that gets hello setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="2f93d-166">程式碼中的 hello *todoListSvc.js*使用 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="2f93d-166">hello code in *todoListSvc.js* uses hello setting:</span></span>
   
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

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a><span data-ttu-id="2f93d-167">部署 hello ToDoListAngular web 專案 toohello 新 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2f93d-167">Deploy hello ToDoListAngular web project toohello new web app</span></span>
* <span data-ttu-id="2f93d-168">在 Visual Studio，在 hello**連接**步驟 hello**發行 Web**精靈 中，按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="2f93d-168">In Visual Studio, in hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="2f93d-169">Visual Studio 部署 hello ToDoListAngular 專案 toohello 新 web 應用程式，並開啟瀏覽器 toohello hello web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="2f93d-169">Visual Studio deploys hello ToDoListAngular project toohello new web app and opens a browser toohello URL of hello web app.</span></span> 

### <a name="test-hello-application-without-cors-enabled"></a><span data-ttu-id="2f93d-170">未啟用 CORS 測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="2f93d-170">Test hello application without CORS enabled</span></span>
1. <span data-ttu-id="2f93d-171">在瀏覽器開發人員工具中開啟 hello 主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="2f93d-171">In your browser Developer Tools, open hello Console window.</span></span>
2. <span data-ttu-id="2f93d-172">在顯示 hello AngularJS UI 的 hello 瀏覽器視窗中按一下 hello **tooDo 清單**連結。</span><span class="sxs-lookup"><span data-stu-id="2f93d-172">In hello browser window that displays hello AngularJS UI, click hello **tooDo List** link.</span></span>
   
    <span data-ttu-id="2f93d-173">hello JavaScript 程式碼會嘗試 toocall hello 中介層應用程式開發介面應用程式，但 hello 呼叫失敗，因為結束執行 hello 前端 hello 回不同的網域中。</span><span class="sxs-lookup"><span data-stu-id="2f93d-173">hello JavaScript code tries toocall hello middle tier API app, but hello call fails because hello front end is running in a different domain than hello back end.</span></span> <span data-ttu-id="2f93d-174">hello 瀏覽器的開發人員工具主控台 視窗會顯示 「 跨原始錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="2f93d-174">hello browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![跨原始來源錯誤訊息](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a><span data-ttu-id="2f93d-176">設定 CORS hello 中介層應用程式開發介面應用程式</span><span class="sxs-lookup"><span data-stu-id="2f93d-176">Configure CORS for hello middle tier API app</span></span>
<span data-ttu-id="2f93d-177">在本節中，您可以設定 hello CORS 設定，在 Azure 中的 hello 中介層 ToDoListAPI API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f93d-177">In this section, you configure hello CORS setting in Azure for hello middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="2f93d-178">這項設定會讓 hello 中介層應用程式開發介面應用程式 tooreceive JavaScript 呼叫從您建立 hello ToDoListAngular 專案 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f93d-178">This setting will allow hello middle tier API app tooreceive JavaScript calls from hello web app that you created for hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="2f93d-179">在瀏覽器，移 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="2f93d-179">In a browser, go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2f93d-180">按一下**應用程式服務**，然後按一下hello ToDoListAPI （中介層） API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f93d-180">Click **App Services**, and then click hello ToDoListAPI (middle tier) API app.</span></span>
   
    ![在入口網站中選取 API 應用程式](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="2f93d-182">在 hello**設定**刀鋒視窗中開啟 toohello 右邊 hello **API 應用程式**刀鋒視窗中，尋找 hello **API**區段，然後再按一下**CORS**。</span><span class="sxs-lookup"><span data-stu-id="2f93d-182">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![在入口網站中選取 CORS](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="2f93d-184">在 [hello] 文字方塊中，輸入 hello URL hello ToDoListAngular （前端） web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f93d-184">In hello text box, enter hello URL for hello ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="2f93d-185">例如，如果您部署的 hello ToDoListAngular 專案 tooa web 應用程式名為 todolistangular0121，允許從 hello URL 呼叫`https://todolistangular0121.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="2f93d-185">For example, if you deployed hello ToDoListAngular project tooa web app named todolistangular0121, allow calls from hello URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="2f93d-186">或者，您可以輸入接受的所有原始網域星號 （*） toospecify。</span><span class="sxs-lookup"><span data-stu-id="2f93d-186">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="2f93d-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2f93d-187">Click **Save**.</span></span>
   
   ![按一下 [Save] \(儲存)。](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="2f93d-189">按一下 之後**儲存**，hello API 應用程式將會接受 JavaScript 呼叫 hello 從指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="2f93d-189">After you click **Save**, hello API app will accept JavaScript calls from hello specified URL.</span></span> <span data-ttu-id="2f93d-190">在這個螢幕擷取畫面，hello ToDoListAPI0223 API 應用程式會接受從 hello ToDoListAngular web 應用程式的 JavaScript 用戶端呼叫。</span><span class="sxs-lookup"><span data-stu-id="2f93d-190">In this screen shot, hello ToDoListAPI0223 API app will accept JavaScript client calls from hello ToDoListAngular web app.</span></span>

### <a name="test-hello-application-with-cors-enabled"></a><span data-ttu-id="2f93d-191">測試與啟用 CORS hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="2f93d-191">Test hello application with CORS enabled</span></span>
* <span data-ttu-id="2f93d-192">開啟瀏覽器 toohello hello web 應用程式的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="2f93d-192">Open a browser toohello HTTPS URL of hello web app.</span></span> 
  
    <span data-ttu-id="2f93d-193">此時間 hello 應用程式可讓您檢視、 新增、 編輯和刪除待辦項目。</span><span class="sxs-lookup"><span data-stu-id="2f93d-193">This time hello application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![tooDo 清單的範例應用程式 頁面](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="2f93d-195">App Service CORS 與 Web API CORS</span><span class="sxs-lookup"><span data-stu-id="2f93d-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="2f93d-196">在 Web API 專案中，您可以安裝 hello[用於 Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet 封裝 toospecify 在您的 API 將會接受的網域從 JavaScript 呼叫的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="2f93d-196">In a Web API project, you can install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package toospecify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="2f93d-197">Web API CORS 支援比 App Service CORS 支援更有彈性。</span><span class="sxs-lookup"><span data-stu-id="2f93d-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="2f93d-198">例如，在程式碼中您可以為不同動作方法指定不同的可接受原始來源，但對於 App Service CORS，您只能為所有 API 應用程式的方法指定一組可接受的原始來源。</span><span class="sxs-lookup"><span data-stu-id="2f93d-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="2f93d-199">不要嘗試 toouse Web API CORS 和一個 API 應用程式中的應用程式服務 CORS。</span><span class="sxs-lookup"><span data-stu-id="2f93d-199">Don't try toouse both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="2f93d-200">App Service CORS 會優先獲得採用，而 Web API CORS 不會有任何作用。</span><span class="sxs-lookup"><span data-stu-id="2f93d-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="2f93d-201">比方說，如果您啟用一個 App Service 中的原始網域，並啟用 Web 應用程式開發介面程式碼中的所有原始網域，您的 Azure API 應用程式將只會接受來自您指定在 Azure 中的 hello 網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="2f93d-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from hello domain you specified in Azure.</span></span>
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a><span data-ttu-id="2f93d-202">如何在 Web API 的程式碼中的 tooenable CORS</span><span class="sxs-lookup"><span data-stu-id="2f93d-202">How tooenable CORS in Web API code</span></span>
<span data-ttu-id="2f93d-203">hello 步驟摘要說明 hello 程序啟用 Web API CORS 支援。</span><span class="sxs-lookup"><span data-stu-id="2f93d-203">hello following steps summarize hello process for enabling Web API CORS support.</span></span> <span data-ttu-id="2f93d-204">如需詳細資訊，請參閱 [在 ASP.NET Web API 2 中啟用跨原始來源要求](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)。</span><span class="sxs-lookup"><span data-stu-id="2f93d-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="2f93d-205">在 Web API 專案中，安裝 hello[用於 Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="2f93d-205">In a Web API project, install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="2f93d-206">包含`config.EnableCors()`hello 的程式碼行**註冊**方法 hello**到 WebApiConfig**類別，如 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="2f93d-206">Include a `config.EnableCors()` line of code in hello **Register** method of hello **WebApiConfig** class, as in hello following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
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
3. <span data-ttu-id="2f93d-207">在您的 Web API 控制器加入`using`hello 陳述式`System.Web.Http.Cors`命名空間，並加入 hello`EnableCors`屬性 toohello 控制器類別或 tooindividual 動作方法。</span><span class="sxs-lookup"><span data-stu-id="2f93d-207">In your Web API controller, add a `using` statement for hello `System.Web.Http.Cors` namespace, and add hello `EnableCors` attribute toohello controller class or tooindividual action methods.</span></span> <span data-ttu-id="2f93d-208">在下列範例的 hello，CORS 支援適用於 toohello 整個控制器。</span><span class="sxs-lookup"><span data-stu-id="2f93d-208">In hello following example, CORS support applies toohello entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="2f93d-209">搭配 API Apps 使用 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="2f93d-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="2f93d-210">如果您使用 Azure API 管理的應用程式開發介面應用程式時，請在 API 管理中設定 CORS hello API 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="2f93d-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in hello API app.</span></span> <span data-ttu-id="2f93d-211">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="2f93d-211">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="2f93d-212">Azure API 管理概觀 (影片︰CORS 開始於 12:10)</span><span class="sxs-lookup"><span data-stu-id="2f93d-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="2f93d-213">API 管理跨網域原則</span><span class="sxs-lookup"><span data-stu-id="2f93d-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="2f93d-214">疑難排解</span><span class="sxs-lookup"><span data-stu-id="2f93d-214">Troubleshooting</span></span>
<span data-ttu-id="2f93d-215">如果您在瀏覽本教學課程時遇到問題，以下是一些疑難排解的相關說明。</span><span class="sxs-lookup"><span data-stu-id="2f93d-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="2f93d-216">請確定您使用 hello 最新版 hello [Azure SDK for.NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003)。</span><span class="sxs-lookup"><span data-stu-id="2f93d-216">Make sure that you're using hello latest version of hello [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="2f93d-217">請確定您已輸入`https`在 hello CORS 設定，並請確定您使用`https`toorun hello 前端 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f93d-217">Make sure that you entered `https` in hello CORS setting, and make sure that you're using `https` toorun hello front-end web app.</span></span>
* <span data-ttu-id="2f93d-218">請確定您輸入 hello CORS 設定，而非在 hello 前端 web 應用程式中 hello 中介層應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f93d-218">Make sure that you entered hello CORS setting in hello middle tier API app, not in hello front-end web app.</span></span>
* <span data-ttu-id="2f93d-219">如果您在應用程式程式碼和 Azure App Service 中設定 CORS，請注意 hello 應用程式服務的 CORS 設定會覆寫您在應用程式程式碼中所做的任何內容。</span><span class="sxs-lookup"><span data-stu-id="2f93d-219">If you're configuring CORS in both application code and Azure App Service, note that hello App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="2f93d-220">toolearn 進一步了解 Visual Studio 功能，可簡化疑難排解，請參閱[疑難排解 Azure App Service 應用程式，Visual Studio 中的](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="2f93d-220">toolearn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f93d-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f93d-221">Next steps</span></span>
<span data-ttu-id="2f93d-222">在本文中，您已看到如何 tooenable 應用程式服務的 CORS 支援可讓用戶端 JavaScript 程式碼呼叫應用程式開發介面不同網域中。</span><span class="sxs-lookup"><span data-stu-id="2f93d-222">In this article, you saw how tooenable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="2f93d-223">深入了解應用程式開發介面應用程式，讀取 hello toolearn [App Service 中的簡介 tooauthentication](../app-service/app-service-authentication-overview.md)，並前往 toohello [API 應用程式的使用者驗證](app-service-api-dotnet-user-principal-auth.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="2f93d-223">toolearn more about API apps, read hello [introduction tooauthentication in App Service](../app-service/app-service-authentication-overview.md), and then go toohello [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

