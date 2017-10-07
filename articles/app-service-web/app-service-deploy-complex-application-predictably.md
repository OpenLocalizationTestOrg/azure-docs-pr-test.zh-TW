---
title: "aaaProvision 和部署在 Azure 中如預期般 microservices"
description: "了解 microservices 當做單一單位的 Azure App Service 中，並使用 JSON 資源群組範本和 PowerShell 指令碼的方式可預測的 toodeploy 應用程式的組成方式。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: d32c2fc82a8b09e89224ec437e5819b65b2e9e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a>透過可預測方式在 Azure 中佈建和部署微服務
本教學課程示範如何 tooprovision 及部署應用程式組成[microservices](https://en.wikipedia.org/wiki/Microservices)中[Azure App Service](/services/app-service/)當做單一單位和可預測的方式使用 JSON 資源群組範本和PowerShell 指令碼。 

當佈建，部署高階應用程式所組成的高度分離 microservices 重複性和可預測性是重要 toosuccess。 [Azure App Service](/services/app-service/)可讓您 toocreate microservices 包含 web 應用程式、 行動裝置應用程式、 應用程式開發介面應用程式，以及邏輯應用程式。 [Azure 資源管理員](../azure-resource-manager/resource-group-overview.md)可讓您 toomanage 所有 hello microservices 為一個單位，以及資源相依性，例如資料庫和原始檔控制設定。 現在，您也可以使用 JSON 範本和簡單 PowerShell 指令碼來部署這類應用程式。 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>將執行的作業
在 hello 教學課程中，您將部署的應用程式，包括：

* 兩個 Web 應用程式 (即兩個微服務)
* 後端 SQL Database
* 應用程式設定、連接字串和原始檔控制
* Application insights、警示、自動調整設定

## <a name="tools-you-will-use"></a>將使用的工具
在本教學課程中，您將使用下列工具 hello。 因為它不是工具的完整討論，我即將 toostick toohello 端對端案例，並只需要為您提供簡短的簡介 tooeach，而且您可以在其中找到更多有關。 

### <a name="azure-resource-manager-templates-json"></a>Azure 資源管理員範本 (JSON)
每次您在 Azure App Service 中建立 web 應用程式，例如，Azure 資源管理員會使用 JSON 範本 toocreate hello 整個資源群組與 hello 元件資源。 複雜的範本，從 hello [Azure Marketplace](/marketplace)像 hello[可擴充 WordPress](/marketplace/partners/wordpress/scalablewordpress/) hello MySQL 資料庫，儲存體帳戶、 hello 應用程式服務方案、 hello web 應用程式本身、 警示規則，應用程式，可以包含應用程式設定、 自動調整規模設定，以及詳細，和所有這些範本是透過 PowerShell 可用 tooyou。 如需有關如何 toodownload 以及使用這些範本，請參閱詳細[使用 Azure PowerShell 的 Azure Resource Manager](../powershell-azure-resource-manager.md)。

如需有關 hello Azure Resource Manager 範本的詳細資訊，請參閱[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)

### <a name="azure-sdk-26-for-visual-studio"></a>Azure SDK 2.6 for Visual Studio
hello 最新 SDK 包含改良 toohello hello JSON 編輯器中的資源管理員範本支援。 您可以使用這個 tooquickly 從頭開始建立資源群組範本或開啟現有 JSON 範本 （例如下載組件庫範本） 進行修改並填入 hello 參數檔案，以及如何即使部署直接從 Azure 的 hello 資源群組資源群組的方案。

如需詳細資訊，請參閱 [Azure SDK 2.6 for Visual Studio](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/)。

### <a name="azure-powershell-080-or-later"></a>Azure PowerShell 0.8.0 或更新版本
Hello Azure PowerShell 安裝從 0.8.0 版開始，加法 toohello Azure 模組中包含 hello Azure 資源管理員模組。 這個新模組可讓您 tooscript hello 部署的資源群組。

如需詳細資訊，請參閱 [搭配使用 Azure PowerShell 與 Azure 資源管理員](../powershell-azure-resource-manager.md)

### <a name="azure-resource-explorer"></a>Azure 資源總管
這[預覽工具](https://resources.azure.com)可讓您 tooexplore hello JSON 定義中您的訂用帳戶和 hello 個別資源的所有 hello 資源群組。 在 hello 工具中，您可以編輯 hello JSON 定義的資源、 刪除整個階層的資源，並建立新的資源。  hello 資訊都可以使用此工具是非常有幫助範本撰寫，因為它會顯示您所需 tooset 的特定類型的資源，hello 屬性更正值等等。您甚至可以建立資源群組中 hello [Azure 入口網站](https://portal.azure.com/)，然後檢查其 JSON 定義中 hello 總管工具 toohelp 您能樣版化 hello 資源群組。

### <a name="deploy-tooazure-button"></a>部署 tooAzure 按鈕
如果您將 GitHub 用於原始檔控制時，您可以將[部署 tooAzure 按鈕](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/)到您的讀我檔案。MD 中，可讓部署周全 UI tooAzure。 雖然您可以針對任何簡單的 web 應用程式，您可以擴充此 tooenable 部署將 azuredeploy.json 檔案放在 hello 儲存機制的根目錄中整個資源群組。 此 JSON 檔案，其中包含 hello 資源群組範本，將供 hello 部署 tooAzure 按鈕 toocreate hello 資源群組。 如需範例，請參閱 hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp)範例中，您將在本教學課程中使用。

## <a name="get-hello-sample-resource-group-template"></a>取得 hello 範例資源群組範本
因此，現在讓我們取得右 tooit。

1. 瀏覽 toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp)應用程式服務範例。
2. 在 readme.md，按一下 **部署 tooAzure**。
3. 您正在進入 toohello[部署至 azure](https://deploy.azure.com)站台和問的 tooinput 部署參數。 請注意，大部分的 hello 欄位會針對您填入 hello 儲存機制名稱與某些隨機字串。 如果您想，但 hello 唯一項目有 tooenter hello SQL Server 系統管理員登入和 hello 密碼，然後按一下，您可以變更所有 hello 欄位**下一步**。
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. 接下來，按一下**部署**toostart hello 部署程序。 一旦執行 toocompletion hello 處理序，按一下 hello http://todoapp*XXXX*。 名稱是.azurewebsites.net 連結 toobrowse hello 部署應用程式。 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   當您第一次瀏覽 tooit 因為 hello 應用程式剛開始，但說服自己是完整功能的應用程式，會比較慢 hello UI。
5. 在 hello 部署 頁面上，按一下 hello**管理**連結 toosee hello 新的應用程式在 hello Azure 入口網站中。
6. 在 hello **Essentials**下拉式清單中，按一下 hello 資源群組的連結。 請注意該 hello web 應用程式也是已連接下的 toohello GitHub 儲存機制**外部專案**。 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. 在 hello 資源群組 刀鋒視窗，請注意，已經有兩個 web 應用程式和 hello 資源群組中的一個 SQL 資料庫。
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

所有項目，您只看到幾分鐘的時間短完整部署的兩個微服務應用程式，與所有 hello 元件、 相依性、 設定、 資料庫和持續的發行設定的設定自動化的協調流程在 Azure 資源管理員。 這項作業是透過兩件事完成：

* hello 部署 tooAzure 按鈕
* 在 hello 儲存機制根 azuredeploy.json

您可以部署此相同的應用程式數十、 數百或數千次，而且有 hello 完全相同的設定每次。 hello 重複性和 hello 可預測性這種方法可讓您 toodeploy 高延展的應用程式輕鬆而信心。

## <a name="examine-or-edit-azuredeployjson"></a>檢查 (或編輯) AZUREDEPLOY.JSON
現在讓我們看看 hello GitHub 儲存機制已設定。 您將會使用 hello JSON 編輯器在 hello Azure.NET SDK，因此，如果您尚未安裝[Azure.NET SDK 2.6](/downloads/)，立即執行它的作業。

1. 複製 hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp)儲存機制使用您最愛的 git 工具。 在 hello 以下螢幕擷取畫面，我現在做這 hello Visual Studio 2013 中的 Team Explorer 中。
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. 從 hello 儲存機制的根目錄，請在 Visual Studio 中開啟 azuredeploy.json。 如果您沒有看到 hello JSON 大綱 窗格，您會需要 tooinstall Azure.NET SDK。
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

我在未進行 toodescribe 的 hello JSON 格式，每個詳細資料，但 hello[更資源](#resources)區段具有學習 hello 資源群組範本語言的連結。 在這裡，我將的 tooshow 您 hello 有趣的功能，可協助您開始進行您自己自訂的範本，應用程式部署。

### <a name="parameters"></a>參數
看看 hello 參數區段 toosee 大部分的這些參數是何種 hello**部署 tooAzure**按鈕會提示您 tooinput。 hello hello 背後的站台**部署 tooAzure**按鈕會填入 hello 輸入 UI 使用 azuredeploy.json 中定義的 hello 參數。 這些參數會使用整個 hello 資源定義，例如資源名稱、 屬性值等等。

### <a name="resources"></a>資源
在 hello 資源 節點，您可以看到定義 4 個最上層資源，包括 SQL Server 執行個體、 App Service 方案，以及兩個 web 應用程式。 

#### <a name="app-service-plan"></a>App Service 方案
讓我們開始與 hello JSON 中的簡單根層級資源。 在 hello JSON 大綱中，按一下 hello App Service 方案名稱為**[hostingPlanName]** toohighlight hello JSON 對應的程式碼。 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

請注意該 hello`type`項目會指定應用程式服務方案 （呼叫伺服器陣列前 long、 長時間），hello 字串和其他項目和屬性會填入使用 hello 參數，定義在 hello JSON 檔案中，此資源不會有任何巢狀的資源。

> [!NOTE]
> 也請注意 hello 該值的`apiVersion`會告訴的 Azure hello REST API toouse hello JSON 資源定義，和它的版本可能會影響您如何格式化 hello 資源內 hello `{}`。 
> 
> 

#### <a name="sql-server"></a>SQL Server
接下來，名為 hello SQL Server 資源上按一下**SQLServer** hello JSON 大綱中。

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

下列關於 hello 注意 hello 反白顯示 JSON 程式碼：

* hello 使用參數可確保會命名為和設定，使其與另一個一致的方式建立 hello 資源。
* hello SQLServer 資源有兩個巢狀的資源，各有不同的值`type`。
* hello 巢狀內部資源`“resources”: […]`、 定義 hello 資料庫和 hello 防火牆規則、 擁有`dependsOn`指定 hello hello 根層級之 sql Server 資源的資源識別碼的項目。 這會告訴 Azure 資源管理員 中，"才能建立此資源的其他資源必須已經存在。如果 hello 範本中定義的其他資源，然後建立一個第一次 」。
  
  > [!NOTE]
  > 如需詳細資訊 toouse hello`resourceId()`函式，請參閱[Azure 資源管理員範本函式](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid)。
  > 
  > 
* hello 的 hello 效果`dependsOn`項目，則可以平行建立哪些資源，而且必須依序建立哪些資源，就可以知道 Azure 資源管理員。 

#### <a name="web-app"></a>Web 應用程式
現在，讓我們前進 toohello 實際的 web 應用程式本身，也就是更複雜。 按一下 [variables('apiSiteName')] hello web 應用程式在 hello JSON 大綱 toohighlight 其 JSON 程式碼。 您會發現事情變得越來越有趣。 基於此目的，我將討論 hello 功能一個：

##### <a name="root-resource"></a>根資源
hello web 應用程式取決於兩個不同的資源。 這表示 Azure 資源管理員會建立 hello web 應用程式之後，才會建立應用程式服務方案和 SQL Server 執行個體 hello 這兩個 hello。

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a>應用程式設定
hello 應用程式設定也會定義為巢狀資源。

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

在 hello`properties`元素`config/appsettings`，hello 格式中有兩個應用程式設定`“<name>” : “<value>”`。

* `PROJECT`是[KUDU 設定](https://github.com/projectkudu/kudu/wiki/Customizing-deployments)，會告訴 Azure 部署的專案 toouse 多專案的 Visual Studio 方案中。 我將示範如何設定原始檔控制，但因為 hello ToDoApp 程式碼是在多專案的 Visual Studio 方案，我們需要這項設定。
* `clientUrl`是只設定該 hello 應用程式程式碼的應用程式使用。

##### <a name="connection-strings"></a>連接字串
hello 連接字串也會定義為巢狀資源。

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

在 hello`properties`元素`config/connectionstrings`，每個連接字串也會定義為具有 hello 特定格式的名稱： 值組， `“<name>” : {“value”: “…”, “type”: “…”}`。 Hello`type`項目，可能的值為`MySql`， `SQLServer`， `SQLAzure`，和`Custom`。

> [!TIP]
> 最終 hello 連接字串型別的清單，執行下列命令，在 Azure PowerShell 中的 hello: \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")
> 
> 

##### <a name="source-control"></a>原始檔控制
hello 原始檔控制設定也會定義為巢狀資源。 Azure 資源管理員會使用此資源 tooconfigure 持續發行 (請參閱注意`IsManualIntegration`稍後) 和也 tookick hello 應用程式程式碼中的部署期間 hello 處理 hello JSON 檔案的自動關閉。

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

`RepoUrl`和`branch`應該其實很好，而且應該指向 toohello Git 儲存機制和 hello 名稱從 hello 分支 toopublish。 同樣地，這些是透過輸入參數所定義。 

請注意，在 hello`dependsOn`項目，在加法 toohello web 應用程式資源本身，`sourcecontrols/web`也取決於`config/appsettings`和`config/connectionstrings`。 這是因為一旦`sourcecontrols/web`是設定，hello Azure 的部署程序將會自動嘗試 toodeploy，建置和啟動 hello 應用程式程式碼。 因此，插入這個相依性會協助您確定該 hello 應用程式必須存取所需的 toohello 應用程式設定和連接字串 hello 應用程式程式碼執行之前。 

> [!NOTE]
> 也請注意，`IsManualIntegration`設定得`true`。 這個屬性是在本教學課程所需，因為您實際上並未擁有 hello GitHub 儲存機制，並因此無法實際授與從的權限 tooAzure tooconfigure 持續發行[ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) （也就是推播自動儲存機制更新 tooAzure）。 您可以使用 hello 預設值`false`hello 指定儲存機制，只有當您已在 hello hello 擁有者的 GitHub 認證[Azure 入口網站](https://portal.azure.com/)之前。 換句話說，如果您已經設定原始檔控制 tooGitHub 或 BitBucket 任何應用程式在 hello [Azure 入口網站](https://portal.azure.com/)之前，使用您的使用者認證，則 Azure 會記住 hello 認證，並使用它們，每當您從任何應用程式部署GitHub 或 BitBucket hello 未來中。 不過，如果您沒有這樣做，請部署 hello JSON 範本將會失敗，當 Azure 資源管理員會嘗試 tooconfigure hello web 應用程式的原始檔控制設定，因為它無法與 hello 儲存機制擁有者的認證登入 GitHub 或 BitBucket。
> 
> 

## <a name="compare-hello-json-template-with-deployed-resource-group"></a>比較 hello JSON 範本部署的資源群組
在這裡，您可以瀏覽所有 hello web 應用程式的刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com/)，但還有其他工具一樣，如果不是多個。 移 toohello [Azure 資源總管](https://resources.azure.com)預覽工具，為您提供所有 hello 資源群組的 JSON 表示法中您的訂閱，如此它們實際存在於 hello Azure 後端。 您也可以查看如何在 Azure 中的 hello 資源群組的 JSON 階層對應於已使用 toocreate 的 hello 範本檔案中的 hello 階層它。

例如，當我該怎麼 toohello [Azure 資源總管](https://resources.azure.com)工具和展開 hello 總管中的 hello 節點，我是否可以查看 hello 資源群組以及其個別資源類型底下所收集的 hello 根層級資源。

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

如果您 tooa web 應用程式向下鑽研，您應該能夠 toosee web 應用程式組態詳細資料類似 toohello 下列螢幕擷取畫面：

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

同樣地，hello 巢狀的資源應該具有階層的非常類似 toothose 在 JSON 範本檔案中，而且您應該會看見 hello 應用程式設定、 連接字串等，正確地反映在 hello JSON 窗格中。 這裡設定 hello 缺少可能表示發生問題，使用您的 JSON 檔案，並可協助您疑難排解您的 JSON 範本檔案。

## <a name="deploy-hello-resource-group-template-yourself"></a>自行部署 hello 資源群組範本
hello**部署 tooAzure**按鈕很棒，但是它可讓您 toodeploy hello 資源群組範本中 azuredeploy.json 只有當您已經有推送 azuredeploy.json tooGitHub。 hello Azure.NET SDK 也提供 hello 工具您 toodeploy 任何直接從您的本機電腦的 JSON 範本檔案。 toodo，後續 hello 步驟：

1. 在 Visual Studio 中，按一下 [檔案] > [新增] > [專案]。
2. 按一下 [Visual C#] > [雲端] > [Azure 資源群組]，然後按一下 [確定]。
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. 在 [選取 Azure 範本] 中，選取 [空白範本]，然後按一下 [確定]。
4. 拖曳 hello azuredeploy.json**範本**新專案的資料夾。
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. 從 方案總管 中，開啟 hello 複製 azuredeploy.json。
6. 只針對 hello 示範的 hello 起見，我們加入一些標準 Application Insight 資源 tooour JSON 檔案，請按一下**加入資源**。 如果您只想在部署 hello JSON 檔案，請略過 toohello 部署步驟。
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. 選取 Web Apps 的 Application Insights，並確定已選取現有 App Service 方案和 Web 應用程式，然後按一下新增。
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   現在，您就是可以 toosee 數個新的資源，視 hello 資源及其功能，對任一 hello App Service 方案或 hello web 應用程式具有相依性。 這些資源不會啟用現有的定義，您將 toochange 的。
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. 在 hello JSON 大綱中，按一下  **appInsights 自動調整規模**toohighlight 其 JSON 程式碼。 這是 hello 縮放您 App Service 方案的設定。
9. 在 hello 反白顯示的 JSON 程式碼中找出 hello`location`和`enabled`屬性並加以設定，如下所示。
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. 在 hello JSON 大綱中，按一下  **CPUHigh appInsights** toohighlight 其 JSON 程式碼。 這是警示。
11. 找出 hello`location`和`isEnabled`屬性並加以設定，如下所示。 請勿 hello 相同的 hello 其他三個警示 （紫色強大）。
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. 您現在準備好 toodeploy。 Hello 專案上按一下滑鼠右鍵，然後選取**部署** > **新部署**。
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. 登入 Azure 帳戶 (如果您尚未這樣做)。
14. 在您的訂用帳戶中選取現有的資源群組，或選取 **azuredeploy.json**，然後按一下編輯參數 建立新的資源群組。
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    您現在將會無法 tooedit nice 資料表中的 hello 範本檔案中定義的所有 hello 參數。 定義預設值的參數已經有其預設值，而定義允許值清單的參數則會顯示為下拉式清單。
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. 填寫所有 hello 空白參數，並使用 hello [ToDoApp GitHub 儲存機制位址](https://github.com/azure-appservice-samples/ToDoApp.git)中**repoUrl**。 然後按一下 [ **儲存**]。
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > 自動調整是中提供的功能**標準**層或更高版本，並計劃層級的警示會提供的功能**基本**層或更高版本，您將需要 tooset hello **sku**參數太**標準**或**Premium**中排序 toosee 所有新 App Insights 資源亮燈。
    > 
    > 
16. 按一下 [ **部署**]。 如果您選取**儲存密碼**，hello 密碼將儲存在 hello 參數檔**以純文字**。 否則，您會在 hello 部署程序期間詢問 tooinput hello 資料庫密碼。

這樣就大功告成了！ 現在您只需要 toogo toohello [Azure 入口網站](https://portal.azure.com/)和 hello [Azure 資源總管](https://resources.azure.com)工具 toosee hello 新警示，以及新增 tooyour JSON 部署應用程式的自動調整規模設定。

您在這一節中的步驟主要完成 hello 下列：

1. 已備妥的 hello 範本檔案
2. 建立參數檔案 toogo 與 hello 範本檔案
3. 已部署的 hello 與 hello 參數檔案的範本檔案

PowerShell cmdlet 輕鬆地完成作業 hello 最後一個步驟。 toosee 哪些 Visual Studio 未部署您應用程式，請開啟 Scripts\Deploy AzureResourceGroup.ps1 時。 有大量程式碼，但我將 toohighlight 所有 hello 相關程式碼需要 toodeploy hello 範本檔案與 hello 參數檔案。

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

hello 最後一個 cmdlet， `New-AzureResourceGroup`，為 hello hello 動作會實際執行的其中一個。 這應該示範 tooyou，hello 協助工具，它是相當直接 toodeploy 您雲端應用程式如預期般。 每當您 hello 執行 hello cmdlet 相同的範本與 hello 相同參數檔案，您將在 tooget hello 相同的結果。

## <a name="summary"></a>摘要
在 DevOps，重複性和可預測性是金鑰 tooany 成功部署 microservices 所組成的大型應用程式。 在本教學課程中，您已部署兩個微服務應用程式 tooAzure 為單一資源群組使用 hello Azure Resource Manager 範本。 希望它已提供您 hello 知識，您需要在您的應用程式在 Azure 中轉換範本的順序 toostart 和可以佈建並將其部署如預期般。 

## <a name="next-steps"></a>後續步驟
過了解如何[套用 agile 方法，並持續發行 microservices 應用程式，就能輕鬆](app-service-agile-software-development.md)以及進階部署技術，如[測試部署](app-service-web-test-in-production-controlled-test-flight.md)輕鬆。

<a name="resources"></a>

## <a name="more-resources"></a>其他資源
* [Azure 資源管理員範本語言](../azure-resource-manager/resource-group-authoring-templates.md)
* [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)
* [Azure 資源管理員範本函式](../azure-resource-manager/resource-group-template-functions.md)
* [使用 Azure 資源管理員範本部署應用程式](../azure-resource-manager/resource-group-template-deploy.md)
* [搭配使用 Azure PowerShell 與 Azure 資源管理員](../azure-resource-manager/powershell-azure-resource-manager.md)
* [Azure 中的資源群組部署疑難排解](../azure-resource-manager/resource-manager-common-deployment-errors.md)

