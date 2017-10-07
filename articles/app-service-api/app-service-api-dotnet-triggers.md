---
title: "aaaApp 服務 API 的應用程式觸發程序 |Microsoft 文件"
description: "Tooimplement 觸發程序在 Azure App Service API 應用程式中"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a>Azure App Service API 應用程式觸發程序
> [!NOTE]
> 這個版本的 hello 文件適用於 tooAPI 應用程式 2014年-12-01-預覽結構描述版本。
>
>

## <a name="overview"></a>概觀
本文說明如何觸發 tooimplement API 應用程式，並從邏輯應用程式中使用它們。

所有 hello 本主題中的程式碼片段會從 hello 複製[監看員活動 API 應用程式程式碼範例](http://go.microsoft.com/fwlink/?LinkId=534802)。

請注意，您必須遵循本文章 toobuild 中的 hello 程式碼的 nuget 封裝，並執行 toodownload hello: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/)。

## <a name="what-are-api-app-triggers"></a>何謂 API 應用程式觸發程序？
它是 API 應用程式 toofire 事件的常見案例，以便 hello API 應用程式的用戶端可以採取回應 toohello 事件中的 hello 適當的動作。 hello REST API 為基礎的機制，支援這種情況下會呼叫的應用程式開發介面應用程式觸發程序。

例如，假設您的用戶端程式碼會使用 hello [Twitter 連接器 API 應用程式](../connectors/connectors-create-api-twitter.md)和您的程式碼需要的 tooperform 新推文包含特定文字為基礎的動作。 在此情況下，您可能設定輪詢或推播的觸發程序 toofacilitate 這項需求。

## <a name="poll-trigger-versus-push-trigger"></a>輪詢觸發程序與推入觸發程序
目前支援兩種類型的觸發程序：

* 輪詢觸發程序-用戶端輪詢 hello API 的應用程式的需要被引發的事件通知
* 推入觸發程序-用戶端會收到 hello API 應用程式時就會引發事件

### <a name="poll-trigger"></a>輪詢觸發程序
輪詢觸發程序實作為一般的 REST API，而且必須要有其用戶端 （例如邏輯應用程式） toopoll 順序 tooget 通知中。 Hello 用戶端可能會維護狀態，而 hello 輪詢觸發程序本身是無狀態。

hello 遵循 hello 要求和回應封包的相關資訊說明 hello 輪詢觸發程序合約的一些重要的層面：

* 要求
  * HTTP 方法：GET
  * 參數
    * triggerState-此選用參數可讓用戶端 toospecify 其狀態，因此，hello 輪詢觸發程序才能正確地決定 tooreturn 通知或未根據的 hello 特定狀態。
    * API 特有的參數
* Response
  * 狀態碼**200** -要求無效，而且沒有從 hello 觸發程序的通知。 hello 通知的 hello 內容會 hello 回應主體。 「 重試-呼叫後 」 標頭 hello 回應中的指出必須擷取的後續要求呼叫的其他通知資料。
  * 狀態碼**202** -要求有效，但沒有任何新的通知，從 hello 觸發程序。
  * 狀態碼 **4xx** - 要求無效。 hello 用戶端應該不會重試 hello 要求。
  * 狀態碼 **5xx** - 要求導致內部伺服器錯誤及/或暫時性問題。 hello 用戶端應該重試 hello 要求。

下列程式碼片段的 hello 是如何 tooimplement 輪詢觸發程序的範例。

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

tootest 輪詢此觸發程序，請遵循下列步驟：

1. 部署 hello API 應用程式與驗證設定的**匿名公用**。
2. 呼叫 hello**觸控**作業 tootouch 檔案。 hello 下列影像顯示的範例要求透過郵差。
   ![透過 Postman 呼叫接觸作業](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. 呼叫 hello 輪詢觸發程序以 hello **triggerState**參數設定 tooa 時間戳記之前 tooStep #2。 hello 下圖顯示透過郵差 hello 範例要求。
   ![透過 Postman 呼叫輪詢觸發程序](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>推入觸發程序
推入觸發程序會實作為一般的 REST API，將推入通知 tooclients 註冊了 toobe 引發特定事件時收到通知。

hello 遵循 hello 要求和回應封包的相關資訊說明 hello 推入觸發程序合約某些重要的部分。

* 要求
  * HTTP 方法：PUT
  * 參數
    * triggerId： 需要-不透明的字串 （例如 GUID) 代表 hello 註冊推入觸發程序。
    * callbackUrl： 需要-hello 回呼 tooinvoke hello 事件引發時的 URL。 hello 引動過程是簡單的 POST HTTP 呼叫。
    * API 特有的參數
* Response
  * 狀態碼**200** -成功的要求 tooregister 用戶端。
  * 狀態碼 **4xx** - 要求無效。 hello 用戶端應該不會重試 hello 要求。
  * 狀態碼 **5xx** - 要求導致內部伺服器錯誤及/或暫時性問題。 hello 用戶端應該重試 hello 要求。
* 回呼
  * HTTP 方法：POST
  * 要求內文： 通知內容。

下列程式碼片段的 hello 是如何 tooimplement 推入觸發程序的範例：

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

tootest 輪詢此觸發程序，請遵循下列步驟：

1. 部署 hello API 應用程式與驗證設定的**匿名公用**。
2. 瀏覽過[http://requestb.in/](http://requestb.in/) toocreate RequestBin 這將做為回呼 URL。
3. 呼叫 hello 推入觸發程序以做為 GUID **triggerId**和 hello RequestBin URL 做為**callbackUrl**。
   ![透過 Postman 呼叫推入觸發程序](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. 呼叫 hello**觸控**作業 tootouch 檔案。 hello 下列影像顯示的範例要求透過郵差。
   ![透過 Postman 呼叫接觸作業](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. 請檢查 hello 推入觸發程序回呼的 hello RequestBin tooconfirm 用來叫用輸出屬性。
   ![透過 Postman 呼叫輪詢觸發程序](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>在 API 定義中描述觸發程序
實作 hello 觸發程序及部署之後您的應用程式開發介面應用程式 tooAzure，瀏覽 toohello **API 定義**刀鋒視窗中 hello Azure preview 入口網站，而且您會看到觸發程序會自動辨識在 UI，由所驅動 hellohello Swagger 2.0 API 中定義的 hello API 應用程式。

![API 定義刀鋒視窗](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

如果您按一下 hello**下載 Swagger**按鈕並開啟 hello JSON 檔案，您會看到下列結果類似 toohello:

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

hello 延伸模組屬性**x-ms-schedular-觸發程序**是觸發程序的應用程式開發介面定義中所述的方式，而且當您要求透過 hello 閘道 hello API 定義如果 hello 要求的 tooone 會自動加入 hello API 應用程式閘道下列準則的 hello。 (您也可以手動加入這個屬性。)

* 輪詢觸發程序
  * 如果 HTTP 方法 hello**取得**。
  * 如果 hello **operationId**屬性包含字串 hello**觸發程序**。
  * 如果 hello**參數**屬性包含具有參數**名稱**屬性設定太**triggerState**。
* 推入觸發程序
  * 如果 HTTP 方法 hello**放**。
  * 如果 hello **operationId**屬性包含字串 hello**觸發程序**。
  * 如果 hello**參數**屬性包含具有參數**名稱**屬性設定太**triggerId**。

## <a name="use-api-app-triggers-in-logic-apps"></a>在邏輯應用程式中使用 API 應用程式觸發程序
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>列出及 hello 邏輯應用程式的設計工具中設定應用程式開發介面應用程式觸發程序
如果您在 hello 中建立邏輯應用程式相同的資源群組，做為 hello API 應用程式，您將會無法 tooadd 它 toohello 設計工具的畫布，只要按一下它。 下列映像的 hello 來說明這點：

![邏輯應用程式設計工具中的觸發程序](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![在邏輯應用程式設計工具中設定輸詢觸發程序](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![在邏輯應用程式設計工具中設定推入觸發程序](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>為邏輯應用程式最佳化 API 應用程式觸發程序
新增觸發程序 tooan API 應用程式之後，有幾件事，在邏輯應用程式中使用 hello API 應用程式時，您可以執行 tooimprove hello 體驗。

比方說，hello **triggerState**輪詢觸發程序的參數應設 toohello 下列 hello 邏輯應用程式中的運算式。 這個運算式應該評估 hello hello 邏輯應用程式，從 hello 觸發程序的最後一個引動過程，傳回的值。  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

注意： 如需使用在上面的 hello 運算式中的 hello 函式的說明，請參閱 toohello 文件上[邏輯應用程式工作流程定義語言](https://msdn.microsoft.com/library/azure/dn948512.aspx)。

邏輯應用程式的使用者將需要 tooprovide hello 運算式上方 hello **triggerState**時使用 hello 觸發程序的參數。 它是透過 hello 延伸模組屬性的 hello 邏輯應用程式設計師可能 toohave 此值預設**x ms-排程器建議**。  hello **x ms 可見度**延伸模組屬性可以設定 tooa 值*內部*以便 hello 參數本身不會顯示 hello 設計工具上。  hello，下列程式碼片段將說明。

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

推入觸發程序，hello **triggerId**參數必須唯一識別 hello 邏輯應用程式。 建議的最佳作法是的 tooset hello 工作流程使用的這個屬性 toohello 名稱 hello 下列運算式：

    @workflow().name

使用 hello **x ms-排程器建議**和**x ms 可見度**其應用程式開發介面的定義，hello API 應用程式中的擴充功能屬性可以傳遞 toohello 邏輯應用程式的設計工具 tooautomatically 設定hello 使用者的運算式。

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>在 API 定義中加入延伸模組屬性
其他中繼資料資訊-例如 hello 延伸模組屬性**x ms-排程器建議**和**x ms 可見度**-可以加入 hello 應用程式開發介面定義中有兩種： 靜態或動態。

對於靜態中繼資料，您可以直接編輯 hello */metadata/apiDefinition.swagger.json*檔案在您的專案，然後手動加入 hello 屬性。

應用程式開發介面使用的應用程式動態中繼資料，您可以編輯 hello SwaggerConfig.cs 檔案 tooadd 可以加入這些擴充功能作業篩選器。

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


hello 以下是如何這個類別可以實作的 toofacilitate hello 動態中繼資料案例的範例。

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
