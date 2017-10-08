---
title: "aaaGet 入門 API 應用程式和應用程式服務中的 ASP.NET |Microsoft 文件"
description: "了解如何 toocreate，部署和使用 Visual Studio 2015 使用 Azure 應用程式服務，ASP.NET 應用程式開發介面應用程式。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a>在 Azure App Service 中開始使用 API Apps、ASP.NET 和 Swagger
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

這是 hello 第一次在一系列的說明如何 toouse 功能的 Azure 應用程式服務的教學課程，是為了開發和裝載 RESTful Api。  本教學課程涵蓋 Swagger 格式 API 中繼資料的支援。

您將了解：

* 如何 toocreate 和部署[API apps](app-service-api-apps-why-best-platform.md)使用內建於 Visual Studio 2015 工具的 Azure App Service 中。
* 如何使用 hello tooautomate API 探索 Swashbuckle NuGet 封裝 toodynamically 產生 Swagger API 中繼資料。
* Toouse Swagger API 中繼資料 tooautomatically 產生 API 應用程式的用戶端程式碼的方式。

## <a name="sample-application-overview"></a>範例應用程式概觀
在本教學課程中，您會使用簡單的待辦事項清單範例應用程式。 hello 應用程式必須在單一頁面應用程式 (SPA) 的前端、 ASP.NET Web API 的中介層和 ASP.NET Web API 的資料層。

![API Apps 範例應用程式圖表](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

以下是 hello 的螢幕擷取畫面[AngularJS](https://angularjs.org/)前端。

![API 的應用程式範例應用程式 toodo 清單](./media/app-service-api-dotnet-get-started/todospa.png)

hello Visual Studio 方案包含三個專案：

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* **ToDoListAngular** -hello 前端： 呼叫 hello 中介層 AngularJS SPA。
* **ToDoListAPI** -hello 中介層： 呼叫 hello 資料層 tooperform 待辦項目上的 CRUD 作業的 ASP.NET Web API 專案。
* **ToDoListDataAPI** -hello 資料層： 執行待辦項目上的 CRUD 作業的 ASP.NET Web API 專案。

hello 三層式架構是許多架構，您可以使用 API Apps 實作用於此處僅供示範之用。 每個階層中的 hello 程式碼很簡單，可能 toodemonstrate API 應用程式功能;例如，hello 資料層會使用伺服器記憶體，而非資料庫做為其持續性機制。

完成本教學課程，您必須設定 hello 兩個 Web API 專案和應用程式服務 API 應用程式中的 hello 雲端中執行。

hello hello 數列中的下一個教學課程部署 hello SPA 前端 toohello 雲端。

## <a name="prerequisites"></a>必要條件
* ASP.NET Web API-hello 教學課程的指示假設您已經有基本知識的方式使用 ASP.NET toowork [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) Visual Studio 中。
* Azure 帳戶 - 您可以[申請免費 Azure 帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)或[啟用 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。
  
    如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務已啟動，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)。 如此，您可以在 App Service 中立即建立短期的入門應用程式 — **不需信用卡**，不需任何承諾。
* Visual Studio 2015 hello [Azure SDK for.NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK 會安裝 Visual Studio 2015 的自動如果還沒有。
  
  * 在 Visual Studio 中，按一下 [說明] -> [關於 Microsoft Visual Studio]，並確定您已安裝 "Azure App Service Tools v2.9.1" 或更新版本。
    
    ![Azure App Tools 版本](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > 根據多少 hello SDK 相依性的您已經在電腦上，安裝 hello SDK 可能需要很長的時間，從 tooa 半小時或更多幾分鐘的時間。
    > 
    > 

## <a name="download-hello-sample-application"></a>下載 hello 範例應用程式
1. 下載 hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list)儲存機制。
   
    您可以按一下 hello **Download ZIP**在本機電腦上的按鈕或再製 hello 儲存機制。
2. 開啟 Visual Studio 2015 或 2013 hello ToDoList 方案。
   
   1. 您將需要 tootrust 每個解決方案。
         ![安全性警告](./media/app-service-api-dotnet-get-started/securitywarning.png)
3. 建立 hello 解決方案 （CTRL + SHIFT + B） toorestore hello NuGet 封裝。
   
    如果您在部署之前，您會想 toosee hello 應用程式在作業中的，您可以在本機執行。 請確定 ToDoListDataAPI 您的啟始專案和方案執行的 hello。 在您的瀏覽器中，您應該預期 toosee HTTP 403 錯誤。

## <a name="use-swagger-api-metadata-and-ui"></a>使用 Swagger API 中繼資料和 UI
Azure App Service 內建支援 [Swagger 2.0](http://swagger.io/) API 中繼資料。 每個應用程式開發介面應用程式可以指定之 URL 端點的 Swagger JSON 格式傳回 hello API 的中繼資料。 hello 傳回來自該端點的中繼資料可以是使用 toogenerate 用戶端程式碼。

ASP.NET Web API 專案可以動態地產生 Swagger 中繼資料使用 hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet 封裝。 hello Swashbuckle NuGet 封裝已安裝在您下載的 hello ToDoListDataAPI 和 ToDoListAPI 專案中。

在本節中的 hello 教學課程，您查看產生的 hello Swagger 2.0 中繼資料，，然後再次嘗試測試 hello Swagger 中繼資料為基礎的 UI。

1. 設定 hello ToDoListDataAPI 專案 (**不**hello ToDoListAPI 專案) 為 hello 啟始專案。
   
    ![將 ToDoDataAPI 設定為啟始專案](./media/app-service-api-dotnet-get-started/startupproject.png)
2. 按 F5 或按一下**偵錯 > 開始偵錯**toorun hello 專案在偵錯模式。
   
    hello 瀏覽器會開啟並顯示 hello HTTP 403 錯誤頁面。
3. 在您的瀏覽器網址列中加入`swagger/docs/v1`toohello hello 列，然後按下 Return 結束。 (URL 是的 hello `http://localhost:45914/swagger/docs/v1`。)
   
    這是 hello Swashbuckle tooreturn Swagger 2.0 JSON 中繼資料用於 hello 應用程式開發介面的預設 URL。
   
    如果您使用 Internet Explorer，hello 瀏覽器會提示您 toodownload *v1.json*檔案。
   
    ![在 IE 中下載 JSON 中繼資料](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    如果您使用 Chrome、 Firefox 或邊緣 hello 瀏覽器會顯示 hello JSON hello 瀏覽器視窗中。 處理 JSON 的方式，不同的瀏覽器和瀏覽器視窗可能看起來不完全與 hello 範例。
   
    ![Chrome 中的 JSON 中繼資料](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    hello 下列範例顯示 hello hello API，hello Swagger 中繼資料的第一個區段與 hello 的 hello 定義 Get 方法。 此中繼資料是哪些磁碟機 hello Swagger UI 和使用它在稍後的章節的 hello 教學課程 tooautomatically 中 hello 下列步驟，使用產生的用戶端程式碼。
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. 關閉 hello 瀏覽器，並停止 Visual Studio 偵錯。
5. 在專案中 hello ToDoListDataAPI**方案總管 中**，開啟 hello *App_Start\SwaggerConfig.cs*檔案，然後向下 tooline 174 並取消註解下列程式碼的 hello 捲軸。
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    hello *SwaggerConfig.cs*當您安裝在專案中的 hello Swashbuckle 封裝，建立檔案。 hello 檔案提供數種方式 tooconfigure Swashbuckle。
   
    已取消註解 Swagger UI 中用於 hello 遵循的步驟啟用 hello hello 程式碼。 當您使用 hello API 應用程式專案範本建立 Web API 專案時，這段程式碼會標記為註解預設基於安全性考量。
6. 再次執行 hello 專案。
7. 在您的瀏覽器網址列中加入`swagger`toohello hello 列，然後按下 Return 結束。 (URL 是的 hello `http://localhost:45914/swagger`。)
8. Hello Swagger UI 頁面出現時，按一下**ToDoList** toosee hello 可供使用的方法。
   
    ![Swagger UI 可用的方法](./media/app-service-api-dotnet-get-started/methods.png)
9. 請先按一下 hello**取得**hello 清單中的按鈕。
10. 在 hello**參數**區段中，輸入星號做為 hello hello 值`owner`參數，然後再按一下**現在就試試看**。
    
    當您在之後的教學課程中加入驗證時，hello 中介層將提供 hello 實際的使用者識別碼 toohello 資料層。 現在，所有工作將會都有星號做為其擁有者識別碼而 hello 應用程式執行時不會啟用驗證。
    
    ![Swagger UI 試用](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    hello Swagger UI 呼叫 hello ToDoList Get 方法，並顯示 hello 回應程式碼和 JSON 結果。
    
    ![Swagger UI 試用結果](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. 按一下**Post**，然後按一下hello 下的**模型結構描述**。
    
    按一下 hello 模型結構描述 prefills hello 輸入的方塊，您可以指定 hello hello Post 方法的參數值。 （如果這無法在 Internet Explorer 中運作，使用不同的瀏覽器或 hello 下一個步驟中手動輸入 hello 參數值）。  
    
    ![Swagger UI 試用文章](./media/app-service-api-dotnet-get-started/post.png)
12. 在 hello 變更 hello JSON`todo`參數輸入方塊，讓它看起來像下列範例，hello 或取代您自己的描述文字：
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. 按一下 [立即試用] 。
    
    hello ToDoList 應用程式開發介面會傳回 HTTP 204 回應碼之表示成功。
14. 請先按一下 hello**取得**按鈕，然後在該區段中的 hello 頁面 hello**現在就試試看** 按鈕。
    
    Get 方法回應 hello 現在包含 hello 新 toodo 項目。
15. 選擇性： 也 hello Put、 Delete，再取得識別碼的方法。
16. 關閉 hello 瀏覽器，並停止 Visual Studio 偵錯。

Swashbuckle 可搭配任何 ASP.NET Web API 專案使用。 如果您想 tooadd Swagger 中繼資料產生 tooan 現有專案時，只安裝 hello Swashbuckle 封裝。

> [!NOTE]
> Swagger 中繼資料包含每個 API 作業的唯一識別碼。 根據預設，Swashbuckle 可能會為 Web API 控制器方法產生重複的 Swagger 作業識別碼。 如果控制器有多載的 HTTP 方法，例如 `Get()` 和 `Get(id)`，就會發生此情況。 如需 toohandle 的多載，請參閱[自訂 Swashbuckle 產生應用程式開發介面定義](app-service-api-dotnet-swashbuckle-customize.md)。 如果您在 Visual Studio 中建立 Web API 專案使用 hello Azure API 應用程式範本時，會產生的唯一作業識別碼的程式碼會自動加入 toohello *SwaggerConfig.cs*檔案。  
> 
> 

## <a id="createapiapp"></a>在 Azure 中建立 API 應用程式和部署程式碼 tooit
在本節中，您可以使用 Azure 工具已整合至 Visual Studio hello**發行 Web**精靈 toocreate 新 API 的應用程式在 Azure 中。 然後您部署 hello ToDoListDataAPI 專案 toohello 新 API 的應用程式，然後執行 hello Swagger UI 來呼叫 hello API。

1. 在**方案總管 中**hello ToDoListDataAPI 專案中，以滑鼠右鍵按一下，然後按**發行**。
   
    ![在 Visual Studio 中按一下 [發佈]](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. 在 [hello**設定檔**hello 的步驟**發行 Web**精靈] 中，按一下**Microsoft Azure App Service**。
   
   ![在 [發佈 Web] 中按一下 [Azure App Service]](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. 登入 tooyour Azure 帳戶，如果您有不這樣做，或重新整理您的認證，如果過期。
4. 在 [hello 應用程式服務] 對話方塊中選擇 hello Azure**訂用帳戶**toouse，然後再按一下**新增**。
   
    ![在 [App Service] 對話方塊中按一下 [新增]](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    hello**主控** 索引標籤的 hello**建立 App Service**  對話方塊隨即出現。
   
    因為您要部署已安裝的 Swashbuckle Web API 專案，Visual Studio 會假設您想 toocreate API 應用程式。 這會由 hello **API 應用程式名稱**標題，並由 hello 事實該 hello**變更類型**下拉式清單設定得**API 應用程式**。
   
    ![[App Service] 對話方塊中的應用程式類型](./media/app-service-api-dotnet-get-started/apptype.png)
5. 輸入**API 應用程式名稱**，都是唯一的 hello *.azurewebsites.net*網域。 您可以接受 hello Visual Studio 所建議的預設名稱。
   
    如果您輸入其他人已使用的名稱，您會看到紅色驚嘆號 toohello 權限。
   
    hello hello API 應用程式的 URL 會`{API app name}.azurewebsites.net`。
6. 在 hello**資源群組**下拉式清單中，按一下**新增**，如果您想要的話，然後輸入"ToDoListGroup 」 或另一個名稱。
   
    資源群組是 Azure 資源的集合，例如 API 應用程式、資料庫、VM 等等。    此教學課程中，它會是最佳 toocreate 新的資源群組，因為，能讓您輕鬆 toodelete 所有 hello hello 教學課程中建立的 Azure 資源的一個步驟。
   
    此方塊可讓您選取現有的[資源群組](../azure-resource-manager/resource-group-overview.md)，或藉由輸入與您的訂用帳戶中任何現有的資源群組不同的名稱，以建立新的資源群組。
7. 按一下 hello**新增**按鈕的下一個 toohello **App Service 方案**下拉式清單。
   
    hello 螢幕擷取畫面顯示範例值**API 應用程式名稱**，**訂用帳戶**，和**資源群組**-您的值將會不同。
   
    ![建立 App Service 對話方塊](./media/app-service-api-dotnet-get-started/createas.png)
   
    Hello 步驟中，您會建立 App Service 方案 hello 新資源群組。 App Service 方案指定 hello 您 API 應用程式執行的計算資源。 比方說，如果您選擇 hello 免費層，您 API 應用程式會執行共用的 Vm 上的部分付費層次中執行專用的 Vm 上時。 如需 App Service 方案的詳細資訊，請參閱 [App Service 方案概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。
8. 在 [hello**設定 App Service 方案**] 對話方塊中，輸入"ToDoListPlan 」 或另一個名稱，如果您偏好。
9. 在 hello**位置**下拉式清單中，選擇最接近 tooyou hello 位置。
   
    這個設定會指定應用程式將執行所在的 Azure 資料中心。 選擇位置關閉 tooyou toominimize[延遲](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090)。
10. 在 hello**大小**下拉式清單中，按一下**免費**。
    
    本教學課程，hello 免費定價層會提供足夠的效能。
11. 在 [hello**設定 App Service 方案**] 對話方塊中，按一下**確定**。
    
    ![在 [設定 App Service 方案] 中按一下 [確定]](./media/app-service-api-dotnet-get-started/configasp.png)
12. 在 hello**建立 App Service**對話方塊中，按一下 **建立**。
    
    ![在 [建立 App Service] 對話方塊中按一下 [建立]](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    Visual Studio 建立 hello API 應用程式和發行設定檔，其中包含所有所需的 hello hello API 應用程式的設定。 然後它會開啟 hello**發行 Web**精靈中，您將使用此 toodeploy hello 專案。
    
    hello**發行 Web**精靈 隨即開啟上 hello**連接** 索引標籤 （如下所示）。
    
    在 hello**連接**索引標籤上，hello**伺服器**和**站台名稱**設定點 tooyour API 應用程式。 hello**使用者名**和**密碼**會為您建立 Azure 的部署認證。 部署之後，Visual Studio 會開啟瀏覽器 toohello**目的地 URL** (也就是說 hello 唯一目的**目的地 URL**)。  
13. 按一下 [下一步] 。
    
    ![在 [發佈 Web] 的 [連線] 索引標籤中按 [下一步]](./media/app-service-api-dotnet-get-started/connnext.png)
    
    hello 下一個索引標籤為 hello**設定** 索引標籤 （如下所示）。 這裡您可以變更 hello 組建組態 索引標籤 toodeploy 的偵錯組建[遠端偵錯](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)。 hello 索引標籤也提供數個**檔案發行選項**:
    
    * 在目的地移除多餘的檔案
    * 在發行期間預先編譯
    * 排除 hello App_Data 資料夾中的檔案
    
    在本教學課程中，您不需要這些。 如需它們執行了哪些作業的說明，請參閱 [操作說明：在 Visual Studio 中使用單鍵發佈來部署 Web 專案](https://msdn.microsoft.com/library/dd465337.aspx)。
14. 按一下 [下一步] 。
    
    ![在 [發佈 Web] 的 [設定] 索引標籤中按 [下一步]](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    接下來是 hello**預覽** 索引標籤 （如下所示），它將提供您哪些檔案即將從您的專案 toohello API 應用程式複製 toobe 機會 toosee。 當您要部署專案 tooan API 的應用程式，您已部署 tooearlier 時，只變更的檔案都會複製。 如果您想 toosee 複製內容的清單，您可以按一下 hello**啟動預覽** 按鈕。
15. 按一下 [發行] 。
    
    ![在 [發佈 Web] 的 [預覽] 索引標籤中按一下 [發佈]](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    Visual Studio 部署 hello ToDoListDataAPI 專案 toohello 新 API 的應用程式。 hello**輸出**視窗會記錄成功的部署，而且 」 已成功建立"頁面會出現在瀏覽器視窗開啟 toohello hello API 應用程式的 URL。
    
    ![成功部署的輸出視窗](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![新的 API 應用程式已成功建立頁面](./media/app-service-api-dotnet-get-started/appcreated.png)
16. 在 hello 瀏覽器的網址列中加入"swagger"toohello URL，然後按 Enter 鍵。 (URL 是的 hello `http://{apiappname}.azurewebsites.net/swagger`。)
    
    hello 瀏覽器會顯示的 hello hello 雲端中執行您稍早所見相同 Swagger 的 UI，但現在它。 試用 hello Get 方法，而且您會看到您正在回復 toohello 預設 2 待辦項目。 hello 您稍早所做的變更已儲存在記憶體中 hello 本機電腦。
17. 開啟 hello [Azure 入口網站](https://portal.azure.com/)。
    
    hello Azure 入口網站是管理 Azure 資源，例如應用程式開發介面應用程式的網頁介面。
18. 按一下 [其他服務] > [應用程式服務]。
    
    ![瀏覽應用程式服務](./media/app-service-api-dotnet-get-started/browseas.png)
19. 在 hello**應用程式服務**刀鋒視窗中，尋找並按一下新的 API 應用程式。 (在 hello Azure 入口網站，稱為開啟 toohello 權限的 windows*刀鋒*。)
    
    ![[應用程式服務] 刀鋒視窗](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    有兩個刀鋒視窗會開啟。 一個分頁有概觀 hello API 應用程式，並有一長串，您可以檢視和變更的設定。
20. 在 hello**設定**刀鋒視窗中，尋找 hello **API**區段，然後按一下**API 定義**。
    
    ![[設定] 刀鋒視窗中的 API 定義](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    hello **API 定義**刀鋒視窗可讓您指定 hello URL 以 JSON 格式傳回 Swagger 2.0 中繼資料。 當 Visual Studio 建立 hello API 應用程式時，它會將 hello API 定義 URL toohello 預設值用於 Swashbuckle 產生的中繼資料更早版本，您所看到的 hello API 應用程式的基底 URL 加上`/swagger/docs/v1`。
    
    ![API 定義 URL](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    當您所選取的應用程式開發介面應用程式 toogenerate 用戶端程式碼時，則 Visual Studio 會擷取 hello 中繼資料從這個 URL。

## <a id="codegen"></a>產生 hello 資料層的用戶端程式碼
將 Swagger 整合到 Azure API 應用程式的 hello 優點之一是自動產生程式碼。 產生的用戶端類別會讓它更容易 toowrite 程式碼呼叫 API 應用程式。

hello ToDoListAPI 專案已經有 hello 產生用戶端程式碼，但 hello 步驟中，則會將其刪除並重新產生的 toosee toodo hello 程式碼的產生方式。

1. 在 Visual Studio**方案總管 中**、 hello ToDoListAPI 在專案中，刪除 hello *ToDoListDataAPI*資料夾。 **注意： 只有 hello 資料夾刪除，hello ToDoListDataAPI 專案。**
   
    ![刪除產生的用戶端程式碼](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    使用 hello 程式碼產生程序，您需透過 toogo 建立這個資料夾。
2. Hello ToDoListAPI 專案中，以滑鼠右鍵按一下，然後按一下**新增 > REST API 用戶端**。
   
    ![在 Visual Studio 中新增 REST API 用戶端](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. 在 hello**新增 REST API 用戶端**對話方塊中，按一下**Swagger URL**，然後按一下**選取 Azure 資產**。
   
    ![選取 Azure 資產](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. 在 hello **App Service**對話方塊中，展開您使用此教學課程中的 hello 資源群組並選取您的應用程式開發介面應用程式，然後按一下**確定**。
   
    ![選取用於產生程式碼的 API 應用程式](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    請注意，當您傳回 toohello**新增 REST API 用戶端**對話方塊中，hello 文字方塊中已填入入 hello API 定義 URL 您稍早在 hello 入口網站中看到的值。
   
    ![API 定義 URL](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > 用於產生程式碼的替代方式 tooget 中繼資料是 tooenter hello URL 直接而不是經過 hello 瀏覽對話方塊。 如果您想 toogenerate 用戶端程式碼部署 tooAzure 之前，您無法在本機執行 hello Web API 專案提供 hello Swagger JSON 檔案，儲存 hello 檔案 toohello URL，請使用 hello 或**選取現有 Swagger 中繼資料檔案**選項。
   > 
   > 
5. 在 hello**新增 REST API 用戶端**對話方塊中，按一下**確定**。
   
    Visual Studio 會建立名為 hello API 應用程式之後的資料夾，並產生用戶端類別。
   
    ![所產生用戶端的程式碼檔案](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. 在 hello ToDoListAPI 專案中，開啟*Controllers\ToDoListController.cs* toosee hello 的程式碼行 40，呼叫 hello API 使用 hello 產生用戶端。
   
    下列程式碼片段的 hello 顯示 hello 程式碼如何具現化 hello 用戶端物件並呼叫 hello Get 方法。
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    hello 建構函式參數取得 hello 端點 URL 從 hello`toDoListDataAPIURL`應用程式設定。 在 hello Web.config 檔案中，該值會是組 toohello 本機 IIS Express 的 URL hello API 專案，您可以在本機執行 hello 應用程式。 如果您省略 hello 建構函式參數，hello 預設端點。 產生 hello 的程式碼的 hello URL
7. 用戶端類別將會產生具有不同的名稱，根據您應用程式開發介面的應用程式名稱;變更中的程式碼 hello *Controllers\ToDoListController.cs*使 hello 類型名稱符合您的專案中產生功能。 例如，如果您將 API 應用程式命名為 ToDoListDataAPI071316，則會將此程式碼︰
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

toothis:

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a>建立 API 應用程式 toohost hello 中介層
先前您[建立 hello 資料層應用程式開發介面應用程式和部署程式碼 tooit](#createapiapp)。  現在您遵循 hello hello 中介層應用程式開發介面應用程式相同的程序。

1. 在**方案總管 中**，以滑鼠右鍵按一下 hello 中介層 ToDoListAPI 專案 （不 hello 資料層 ToDoListDataAPI），然後按一下**發行**。
   
    ![在 Visual Studio 中按一下 [發佈]](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. 在 hello**設定檔**hello 索引標籤**發行 Web**精靈 中，按一下**Microsoft Azure App Service**。
3. 在 hello **App Service**對話方塊中，按一下 **新增**。
4. 在 hello**主控**hello 索引標籤**建立 App Service**對話方塊方塊中，接受預設 hello **API 應用程式名稱**輸入 hello 中是唯一的名稱或*名稱是.azurewebsites.net*網域。
5. 選擇 hello Azure**訂用帳戶**已經使用。
6. 在 hello**資源群組**下拉式清單中，選擇 hello 您稍早建立的相同資源群組。
7. 在 hello**應用程式服務方案**下拉式清單中，選擇 hello 相同您稍早建立的計畫。 它將預設 toothat 值。
8. 按一下 [建立] 。
   
    Visual Studio 建立 hello API 應用程式，建立的發行設定檔，並顯示 hello**連接**步驟 hello**發行 Web**精靈。
9. 在 hello**連接**步驟 hello**發行 Web**精靈 中，按一下**發行**。
   
   Visual Studio 部署 hello ToDoListAPI 專案 toohello 新 API 的應用程式，並開啟瀏覽器 toohello hello API 應用程式的 URL。 「 成功建立"hello 頁面隨即出現。

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a>設定 hello 中介層 toocall hello 資料層
如果您現在稱為 hello 中介層應用程式開發介面應用程式，它就會嘗試使用仍在 hello Web.config 檔案中的 hello localhost URL toocall hello 資料層。 這一節中，您可以輸入 hello 資料層應用程式開發介面應用程式 URL 到 hello 中介層應用程式開發介面應用程式中的環境設定。 當 hello hello 中介層應用程式開發介面應用程式中的程式碼擷取 hello 資料層 URL 設定時，hello 環境設定，將會覆寫何謂 hello Web.config 檔案中。

1. 移 toohello [Azure 入口網站](https://portal.azure.com/)，然後瀏覽 toohello **API 應用程式**刀鋒視窗，您建立 toohost hello TodoListAPI （中介層） 專案的 hello API 應用程式。
2. 在 hello API 應用程式**設定**刀鋒視窗中，按一下 **應用程式設定**。
3. 在 hello API 應用程式**應用程式設定**刀鋒視窗中，捲動 toohello**應用程式設定**區段，加入 hello 下列索引鍵和值。 hello 值將是 hello 的 hello 第一個 API 在這個教學課程中您發行應用程式的 URL。
   
   | **金鑰** | toDoListDataAPIURL |
   | --- | --- |
   | **值** |https://{您的資料層 API 應用程式名稱}.azurewebsites.net |
   | **範例** |https://todolistdataapi.azurewebsites.net |
4. 按一下 [儲存] 。
   
    ![按一下 [應用程式設定] 的 [儲存]](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    當 hello 程式碼在 Azure 中執行時，此值現在會覆寫 hello Web.config 檔案中的 hello localhost URL。

## <a name="test"></a>測試
1. 在瀏覽器視窗中，瀏覽 hello 新中介層應用程式開發介面應用程式，您剛才建立的 ToDoListAPI toohello URL。 您可以按一下 hello 入口網站中的 hello API 應用程式的主要刀鋒視窗中的 hello URL 那里取得。
2. 在 hello 瀏覽器的網址列中加入"swagger"toohello URL，然後按 Enter 鍵。 (URL 是的 hello `http://{apiappname}.azurewebsites.net/swagger`。)
   
    hello 瀏覽器顯示 hello 相同 Swagger UI 之前看到的 ToDoListDataAPI，但現在`owner`是不必要的欄位 hello Get 作業，因為 hello 中介層應用程式開發介面應用程式正在為您傳送該值 toohello 資料層應用程式開發介面應用程式。 (當您執行 hello 驗證教學課程時，hello 中介層會將傳送 hello 的實際使用者識別碼`owner`參數; 若為現在它硬式編碼星號。)
3. Hello Get 方法與 hello hello 中介層應用程式開發介面應用程式其他方法 toovalidate 成功呼叫 hello 資料層應用程式開發介面應用程式，請試試看。
   
    ![Swagger UI Get 方法](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a>疑難排解
如果您在瀏覽本教學課程時遇到問題，以下是一些疑難排解的相關說明︰

* 請確定您使用 hello 最新版 hello [Azure SDK for.NET](http://go.microsoft.com/fwlink/?linkid=518003)。
* Hello 專案名稱是類似 (ToDoListAPI，ToDoListDataAPI)。 如果項目看起來如下 hello 指示中所述，當您使用的專案，，請確定您已開啟 hello 正確的專案。
* 如果您的公司網路，並嘗試透過防火牆 toodeploy tooAzure 應用程式服務，請確定連接埠 443 和 8172 已開啟的 Web Deploy。 如果您無法開啟這些連接埠，則可以使用其他部署方法。  請參閱[部署您的應用程式服務的應用程式 tooAzure](../app-service-web/web-sites-deploy.md)。
* 「 路由名稱必須唯一 」 的錯誤-您可以取得這些如果您不小心將 hello 錯誤的專案 tooan API 應用程式部署，然後稍後部署 hello 正確一個 tooit。 toocorrect 如此，重新部署 hello 正確的專案 toohello API 應用程式，在 hello**設定**hello 索引標籤**發行 Web**精靈選取**移除其他檔案，在目的地**.

Azure App Service 中執行的 ASP.NET 應用程式開發介面應用程式之後，您可能想 toolearn 深入了解 Visual Studio 功能，可簡化疑難排解。 如需記錄和遠端偵錯等功能的相關資訊，請參閱[在 Visual Studio 中針對 Azure App Service 應用程式進行疑難排解](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)。

## <a name="next-steps"></a>後續步驟
您已經看到如何 toodeploy 現有 Web API 專案 tooAPI 應用程式產生針對應用程式開發介面應用程式，用戶端程式碼和使用來自.NET 用戶端應用程式開發介面應用程式。 hello 這系列中的下一個教學課程會示範如何太[使用 CORS 從 JavaScript 用戶端的 tooconsume API 應用程式](app-service-api-cors-consume-javascript.md)。

如需有關用戶端產生程式碼的詳細資訊，請參閱 hello [Azure/AutoRest](https://github.com/azure/autorest) GitHub.com 上的儲存機制。有關使用 hello 產生用戶端的問題，請開啟[hello AutoRest 儲存機制中的問題](https://github.com/azure/autorest/issues)。

如果您想 toocreate 新 API 的應用程式專案從頭，使用 hello **Azure API 應用程式**範本。

![Visual Studio 中的 API 應用程式範本](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

hello **Azure API 應用程式**專案範本為對等 toochoosing hello**空**ASP.NET 4.5.2 範本中，按一下 [hello] 核取方塊 tooadd Web API 支援，並安裝 hello Swashbuckle NuGet 封裝。 此外，hello 範本加入某些 Swashbuckle 組態程式碼設計 tooprevent hello 建立重複的 Swagger 作業識別碼。 一旦您已建立 API 應用程式專案，您可以將它部署 tooan API 應用程式 hello 您在本教學課程中看到的一樣。

