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
# <a name="consume-an-api-app-from-javascript-using-cors"></a>使用 CORS 從 JavaScript 取用 API 應用程式
應用程式服務提供的內建支援[跨原始資源共用 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)，可讓 JavaScript 用戶端 toomake 跨網域呼叫 tooAPIs 所裝載的應用程式開發介面應用程式。 應用程式服務可讓您設定 CORS 存取 tooyour 應用程式開發介面，而不需要撰寫任何程式碼中您的 API。

本文包含兩個部分：

* hello[如何 tooconfigure CORS](#corsconfig)章節將說明一般方式 tooconfigure CORS API 應用程式、 web 應用程式，或行動裝置應用程式。 這同樣適用於 tooall 架構應用程式服務，包括.NET、 Node.js 和 Java 支援。 
* 開頭為 hello[繼續 hello.NET 使用者入門教學課程](#tutorialstart)章節 hello 發行項是示範 CORS 支援藉由在您未建置的教學課程[hello 第一個應用程式開發介面應用程式取得入門教學課程](app-service-api-dotnet-get-started.md). 

## <a id="corsconfig"></a>如何在 Azure 應用程式服務的 CORS tooconfigure
您可以在 hello Azure 入口網站中，或藉由設定 CORS [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)工具。

#### <a name="configure-cors-in-hello-azure-portal"></a>在 hello Azure 入口網站中設定 CORS
1. 在瀏覽器中前往 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下**應用程式服務**，然後按一下hello API 應用程式名稱。
   
    ![在入口網站中選取 API 應用程式](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. 在 hello**設定**刀鋒視窗中開啟 toohello 右邊 hello **API 應用程式**刀鋒視窗中，尋找 hello **API**區段，然後再按一下**CORS**。
   
   ![在 [設定] 刀鋒視窗中選取 CORS](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. 在 [hello] 文字方塊中輸入 hello URL 或您想要從 tooallow JavaScript 呼叫 toocome 的 Url。

    例如，如果您部署 JavaScript 應用程式 tooa web 應用程式名為 todolistangular，輸入 「 https://todolistangular.azurewebsites.net"。 或者，您可以輸入接受的所有原始網域星號 （*） toospecify。


1. 按一下 [儲存] 。
   
   ![按一下 [Save] \(儲存)。](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   按一下 之後**儲存**，hello API 應用程式將會接受 JavaScript 呼叫 hello 從指定的 Url。

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a>使用 Azure 資源管理員工具設定 CORS
您也可以設定應用程式開發介面應用程式的 CORS，使用[Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)在命令列工具，像是[Azure PowerShell](/powershell/azureps-cmdlets-docs)和 hello [Azure CLI](../cli-install-nodejs.md)。 

例如 hello CORS 屬性設定的 Azure Resource Manager 範本中，開啟 hello [hello 儲存機制中用於本教學課程範例應用程式的 azuredeploy.json 檔案](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)。 尋找 hello 區段，看起來像下列範例中的 hello hello 範本：

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a>繼續 hello.NET 使用者入門教學課程
如果您要遵照 hello Node.js 或 Java 開始使用數列的 API 應用程式，您必須已完成的 hello 取得已啟動的數列。 略過 toohello[後續步驟](#next-steps)區段 toofind 進一步深入了解應用程式開發介面應用程式的建議。

hello 這篇文章的其餘部分將延續 hello.NET 開始使用數列的並假設您已成功完成[hello 第一個教學課程](app-service-api-dotnet-get-started.md)。

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a>部署 hello ToDoListAngular 專案 tooa 新 web 應用程式
在[hello 第一個教學課程](app-service-api-dotnet-get-started.md)，您所建立的中介層應用程式開發介面應用程式和資料層應用程式開發介面應用程式。 在此教學課程中您建立單一頁面應用程式 (SPA) web 應用程式呼叫 hello 中介層應用程式開發介面應用程式。 Hello SPA toowork 您還有 tooenable CORS hello 中介層應用程式開發介面應用程式上。 

在 hello [ToDoList 範例應用程式](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list)，hello ToDoListAngular 專案是簡單的 AngularJS 用戶端呼叫 hello 中介層 ToDoListAPI Web API 專案。 hello hello 中的 JavaScript 程式碼*app/scripts/todoListSvc.js*檔案呼叫 hello API 使用 hello AngularJS HTTP 提供者。 

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

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a>建立新的 web 應用程式 hello ToDoListAngular 專案
hello 程序 toocreate 新的 App Service web 應用程式並部署專案 tooit 是您所看到的類似 toowhat[建立及部署 API 應用程式在 hello 本系列的第一個教學課程](app-service-api-dotnet-get-started.md#createapiapp)。 hello 差異是該 hello 應用程式類型只是**Web 應用程式**而不是**API 應用程式**。  Hello 對話方塊的螢幕擷取畫面，請參閱 

1. 在**方案總管 中**hello ToDoListAngular 專案中，以滑鼠右鍵按一下，然後按**發行**。
2. 在 hello**設定檔**hello 索引標籤**發行 Web**精靈 中，按一下**Microsoft Azure App Service**。
3. 在 hello **App Service**對話方塊中，按一下 **新增**。
4. 在 [hello**主控**hello] 索引標籤**建立應用程式服務**對話方塊方塊中，輸入**Web 應用程式名稱**，都是唯一的 hello *.azurewebsites.net*網域。 
5. 選擇 hello Azure**訂用帳戶**想與 toowork。
6. 在 hello**資源群組**下拉式清單中，選擇 hello 您稍早建立的相同資源群組。
7. 在 hello**應用程式服務方案**下拉式清單中，選擇 hello 相同您稍早建立的計畫。 
8. 按一下 [建立] 。
   
    Visual Studio 建立 hello web 應用程式，建立的發行設定檔，並顯示 hello**連接**步驟 hello**發行 Web**精靈。
   
    還不要按 [發佈]  。 在 hello 下列區段，您可以設定 hello 新 web 應用程式 toocall hello 中介層應用程式開發介面應用程式正在執行中應用程式服務。 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a>Web 應用程式設定中設定 hello 中介層 URL
1. 移 toohello [Azure 入口網站](https://portal.azure.com/)，然後瀏覽 toohello **Web 應用程式**hello 您建立 toohost hello TodoListAngular （前端） 專案的 web 應用程式 刀鋒視窗。
2. 按一下 [設定] > [應用程式設定]。
3. 在 hello**應用程式設定**區段中，新增 hello 下列索引鍵和值：
   
   | Key | 值 | 範例 |
   | --- | --- | --- |
   | toDoListAPIURL |https://{您的中介層 API 應用程式名稱}.azurewebsites.net |https://todolistapi0121.azurewebsites.net |
4. 按一下 [儲存] 。
   
    當 hello 程式碼在 Azure 中執行時，這個值會覆寫 hello localhost URL 會在 hello *Web.config*檔案。 
   
    取得 hello 設定值的 hello 程式碼位於*index.cshtml*:
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    程式碼中的 hello *todoListSvc.js*使用 hello 設定：
   
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

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a>部署 hello ToDoListAngular web 專案 toohello 新 web 應用程式
* 在 Visual Studio，在 hello**連接**步驟 hello**發行 Web**精靈 中，按一下**發行**。
  
   Visual Studio 部署 hello ToDoListAngular 專案 toohello 新 web 應用程式，並開啟瀏覽器 toohello hello web 應用程式的 URL。 

### <a name="test-hello-application-without-cors-enabled"></a>未啟用 CORS 測試 hello 應用程式
1. 在瀏覽器開發人員工具中開啟 hello 主控台視窗。
2. 在顯示 hello AngularJS UI 的 hello 瀏覽器視窗中按一下 hello **tooDo 清單**連結。
   
    hello JavaScript 程式碼會嘗試 toocall hello 中介層應用程式開發介面應用程式，但 hello 呼叫失敗，因為結束執行 hello 前端 hello 回不同的網域中。 hello 瀏覽器的開發人員工具主控台 視窗會顯示 「 跨原始錯誤訊息。
   
    ![跨原始來源錯誤訊息](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a>設定 CORS hello 中介層應用程式開發介面應用程式
在本節中，您可以設定 hello CORS 設定，在 Azure 中的 hello 中介層 ToDoListAPI API 應用程式。 這項設定會讓 hello 中介層應用程式開發介面應用程式 tooreceive JavaScript 呼叫從您建立 hello ToDoListAngular 專案 hello web 應用程式。

1. 在瀏覽器，移 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下**應用程式服務**，然後按一下hello ToDoListAPI （中介層） API 應用程式。
   
    ![在入口網站中選取 API 應用程式](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. 在 hello**設定**刀鋒視窗中開啟 toohello 右邊 hello **API 應用程式**刀鋒視窗中，尋找 hello **API**區段，然後再按一下**CORS**。
   
   ![在入口網站中選取 CORS](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. 在 [hello] 文字方塊中，輸入 hello URL hello ToDoListAngular （前端） web 應用程式。 例如，如果您部署的 hello ToDoListAngular 專案 tooa web 應用程式名為 todolistangular0121，允許從 hello URL 呼叫`https://todolistangular0121.azurewebsites.net`。
   
   或者，您可以輸入接受的所有原始網域星號 （*） toospecify。
5. 按一下 [儲存] 。
   
   ![按一下 [Save] \(儲存)。](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   按一下 之後**儲存**，hello API 應用程式將會接受 JavaScript 呼叫 hello 從指定的 URL。 在這個螢幕擷取畫面，hello ToDoListAPI0223 API 應用程式會接受從 hello ToDoListAngular web 應用程式的 JavaScript 用戶端呼叫。

### <a name="test-hello-application-with-cors-enabled"></a>測試與啟用 CORS hello 應用程式
* 開啟瀏覽器 toohello hello web 應用程式的 HTTPS URL。 
  
    此時間 hello 應用程式可讓您檢視、 新增、 編輯和刪除待辦項目。 
  
    ![tooDo 清單的範例應用程式 頁面](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a>App Service CORS 與 Web API CORS
在 Web API 專案中，您可以安裝 hello[用於 Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet 封裝 toospecify 在您的 API 將會接受的網域從 JavaScript 呼叫的程式碼中。

Web API CORS 支援比 App Service CORS 支援更有彈性。 例如，在程式碼中您可以為不同動作方法指定不同的可接受原始來源，但對於 App Service CORS，您只能為所有 API 應用程式的方法指定一組可接受的原始來源。

> [!NOTE]
> 不要嘗試 toouse Web API CORS 和一個 API 應用程式中的應用程式服務 CORS。 App Service CORS 會優先獲得採用，而 Web API CORS 不會有任何作用。 比方說，如果您啟用一個 App Service 中的原始網域，並啟用 Web 應用程式開發介面程式碼中的所有原始網域，您的 Azure API 應用程式將只會接受來自您指定在 Azure 中的 hello 網域呼叫。
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a>如何在 Web API 的程式碼中的 tooenable CORS
hello 步驟摘要說明 hello 程序啟用 Web API CORS 支援。 如需詳細資訊，請參閱 [在 ASP.NET Web API 2 中啟用跨原始來源要求](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)。

1. 在 Web API 專案中，安裝 hello[用於 Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet 封裝。
2. 包含`config.EnableCors()`hello 的程式碼行**註冊**方法 hello**到 WebApiConfig**類別，如 hello 下列範例所示。 
   
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
3. 在您的 Web API 控制器加入`using`hello 陳述式`System.Web.Http.Cors`命名空間，並加入 hello`EnableCors`屬性 toohello 控制器類別或 tooindividual 動作方法。 在下列範例的 hello，CORS 支援適用於 toohello 整個控制器。
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a>搭配 API Apps 使用 Azure API 管理
如果您使用 Azure API 管理的應用程式開發介面應用程式時，請在 API 管理中設定 CORS hello API 應用程式中。 如需詳細資訊，請參閱下列資源的 hello:

* [Azure API 管理概觀 (影片︰CORS 開始於 12:10)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [API 管理跨網域原則](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a>疑難排解
如果您在瀏覽本教學課程時遇到問題，以下是一些疑難排解的相關說明。

* 請確定您使用 hello 最新版 hello [Azure SDK for.NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003)。
* 請確定您已輸入`https`在 hello CORS 設定，並請確定您使用`https`toorun hello 前端 web 應用程式。
* 請確定您輸入 hello CORS 設定，而非在 hello 前端 web 應用程式中 hello 中介層應用程式開發介面應用程式。
* 如果您在應用程式程式碼和 Azure App Service 中設定 CORS，請注意 hello 應用程式服務的 CORS 設定會覆寫您在應用程式程式碼中所做的任何內容。 

toolearn 進一步了解 Visual Studio 功能，可簡化疑難排解，請參閱[疑難排解 Azure App Service 應用程式，Visual Studio 中的](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)。

## <a name="next-steps"></a>後續步驟
在本文中，您已看到如何 tooenable 應用程式服務的 CORS 支援可讓用戶端 JavaScript 程式碼呼叫應用程式開發介面不同網域中。 深入了解應用程式開發介面應用程式，讀取 hello toolearn [App Service 中的簡介 tooauthentication](../app-service/app-service-authentication-overview.md)，並前往 toohello [API 應用程式的使用者驗證](app-service-api-dotnet-user-principal-auth.md)教學課程。

