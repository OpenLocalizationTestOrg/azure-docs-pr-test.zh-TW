---
title: ".NET 應用程式適用於 Service Fabric aaaCreate |Microsoft 文件"
description: "了解如何 toocreate 前端的 ASP.NET Core 和可靠的應用程式服務可設定狀態的後端，並部署 hello 應用程式 tooa 叢集。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>建立和部署含有 ASP.NET Core Web API 前端服務和具狀態後端服務的應用程式
本教學課程是一個系列的第一部分。  您將學習如何 toocreate ASP.NET Core Web API 最上層的 Azure Service Fabric 應用程式結束，並可設定狀態的後端服務 toostore 您的資料。 當您完成時，必須具有 ASP.NET Core web 前端，將投票的結果儲存在可設定狀態的後端服務 hello 叢集中的投票應用程式。 如果您不想 toomanually 建立 hello 投票應用程式，您可以[hello 將原始程式碼下載](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/)hello 已完成應用程式，並跳過[逐步解說投票範例應用程式的 hello](#walkthrough_anchor)。

![應用程式圖表](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

其中一個 hello 系列的一部分，在您了解如何：

> [!div class="checklist"]
> * 建立 ASP.NET Core Web API 服務成為具狀態可靠服務
> * 建立 ASP.NET Core Web 應用程式服務成為具狀態可靠服務
> * 使用 hello 反向 proxy toocommunicate 與 hello 可設定狀態服務

在本教學課程系列中，您將了解如何：
> [!div class="checklist"]
> * 建置 .NET Service Fabric 應用程式
> * [部署 hello 應用程式 tooa 遠端叢集](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [使用 Visual Studio Team Services 設定 CI/CD](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前：
- 如果您沒有 Azure 訂用帳戶，請建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [安裝 Visual Studio 2017](https://www.visualstudio.com/)並安裝 hello **Azure 開發**和**ASP.NET 及 web 開發**工作負載。
- [安裝 hello Service Fabric SDK](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>建立 ASP.NET Web API 服務成為可靠的服務
首先，建立 hello web 前端的 hello 投票使用 ASP.NET Core 應用程式。 ASP.NET Core 是輕量型、 跨平台的 web 開發架構，您可以使用 toocreate 新式 web UI 和 web 應用程式開發介面。 tooget 瞭解的 ASP.NET Core Service Fabric 與整合的方式，我們強烈建議您閱讀 hello [Service Fabric 可靠的服務中的 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)發行項。 現在，您可以遵循這個快速入門的教學課程 tooget。 深入了解 ASP.NET Core toolearn 看到 hello [ASP.NET Core 文件集](https://docs.microsoft.com/aspnet/core/)。

> [!NOTE]
> 本教學課程根據 hello [ASP.NET Core 工具的 Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc)。 Visual Studio 2015 的 hello.NET Core 工具不再正在更新。

1. 以**系統管理員**身分啟動 Visual Studio。

2. 使用**檔案**->**新增**->**專案**建立專案

3. 在 [hello**新專案**] 對話方塊中，選擇**雲端 > Service Fabric 應用程式**。

4. Hello 應用程式命名**投票**按**確定**。

   ![Visual Studio 中的新增專案對話方塊](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. 在 hello**新增 Service Fabric 服務**頁面上，選擇**無狀態的 ASP.NET Core**，並命名您的服務**VotingWeb**。
   
   ![在 [hello 新增服務] 對話方塊中選擇 ASP.NET web 服務](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. hello 下一個頁面會提供一組 ASP.NET Core 專案範本。 在本教學課程中，選擇 [Web 應用程式]。 
   
   ![選擇 ASP.NET 專案類型](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio 會建立應用程式和服務專案，並顯示在 [方案總管] 中。

   ![使用 ASP.NET Core Web API 服務建立應用程式後的方案總管]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>加入 AngularJS toohello VotingWeb 服務
新增[AngularJS](http://angularjs.org/) tooyour 服務使用 hello 內建[Bower 支援](/aspnet/core/client-side/bower)。 開啟 bower.json 並新增 Angular 和 Angular 啟動程序的項目，然後儲存您的變更。

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
在儲存 hello 時*bower.json* Angular 的檔案會安裝在您的專案*wwwroot/lib*資料夾。 此外，它會列在 hello*相依性/Bower*資料夾。

### <a name="update-hello-sitejs-file"></a>更新 hello site.js 檔案
開啟 hello *wwwroot/js/site.js*檔案。  取代 hello JavaScript 使用 hello 首頁檢視其內容：

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-hello-indexcshtml-file"></a>更新 hello Index.cshtml 檔案
開啟 hello *Views/Home/Index.cshtml*檔案、 hello 檢視特定 toohello Home 控制器。  Hello 下列程式碼，以取代其內容，然後儲存您的變更。

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click toovote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-hello-layoutcshtml-file"></a>更新 hello _Layout.cshtml 檔案
開啟 hello *Views/Shared/_Layout.cshtml*檔案、 hello hello ASP.NET 應用程式的預設版面配置。  Hello 下列程式碼，以取代其內容，然後儲存您的變更。

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-hello-votingwebcs-file"></a>更新 hello VotingWeb.cs 檔案
開啟 hello *VotingWeb.cs*建立 hello ASP.NET Core WebHost hello 使用 hello WebListener web 伺服器的無狀態服務內的檔案。  新增 hello`using System.Net.Http;`指示詞 toohello hello 檔案的頂端。  取代 hello `CreateServiceInstanceListeners()` hello 下列函數，然後儲存您的變更。

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-hello-votescontrollercs-file"></a>加入 hello VotesController.cs 檔案
新增定義投票動作的控制器。 以滑鼠右鍵按一下 hello**控制器**資料夾，然後選取**新增-> 新增項目類別->** 。  將 hello 檔案 」 VotesController.cs"，然後按一下**新增**。  Hello 檔案內容取代 hello 下列項目，然後儲存您的變更。  稍後在[更新 hello VotesController.cs 檔案](#updatevotecontroller_anchor)，這個檔案將已修改的 tooread 並從 hello 後端服務寫入投票資料。  現在，hello 控制站會傳回靜態字串資料 toohello 檢視。

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-hello-application-locally"></a>部署並在本機執行 hello 應用程式
您現在可以繼續，並執行 hello 應用程式。 在 Visual Studio 中，按`F5`toodeploy hello 應用程式進行偵錯。 如果您先前並未以**系統管理員**身分開啟 Visual Studio，`F5` 將失敗。

> [!NOTE]
> hello 第一次執行，並部署 hello 應用程式在本機，Visual Studio 會建立偵錯的本機叢集。  建立叢集可能需要一些時間。 hello Visual Studio 輸出 視窗中會顯示 hello 叢集建立狀態。

此時，您的 web 應用程式看起來應該像這樣：

![ASP.NET Core 前端](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

toostop 偵錯 hello 應用程式，請返回 tooVisual Studio，然後按**Shift + F5**。

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>新增可設定狀態的後端服務 tooyour 應用程式
現在，我們已經在我們的應用程式中執行的 ASP.NET Web API 服務，請繼續進行，在我們的應用程式中新增可設定狀態的可靠服務 toostore 某些資料。

Service Fabric tooconsistently 可讓您和可靠地儲存在您的服務將資料直接使用可靠的集合。 可靠的集合是一組都已使用 C# 集合熟悉 tooanyone 的高度可用且可靠的集合類別。

在本教學課程中，您建立服務，將計數器值儲存於可靠集合中。

1. 在 方案總管 中，以滑鼠右鍵按一下**服務**內 hello 應用程式專案，然後選擇 **新增 > 新增 Service Fabric 服務**。
   
    ![加入新的服務 tooan 現有應用程式](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. 在 hello**新增 Service Fabric 服務** 對話方塊中，選擇**可設定狀態的 ASP.NET Core**，和名稱 hello 服務**VotingData**按**確定**。

    ![Visual Studio 中的新增服務對話方塊](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    建立服務專案後，您的應用程式中會有兩個服務。 當您繼續 toobuild 您的應用程式，您就可以在 hello 中加入更多服務相同的方式。 每個服務都可以獨立設定版本和升級。

3. hello 下一個頁面會提供一組 ASP.NET Core 專案範本。 在本教學課程中，選擇 [Web API]。

    ![選擇 ASP.NET 專案類型](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio 會建立服務專案，並顯示在 [方案總管] 中。

    ![Solution Explorer](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>加入 hello VoteDataController.cs 檔案

在 hello **VotingData**專案上的按一下滑鼠右鍵在 hello**控制站**資料夾，然後選取**新增-> 新增項目類別->** 。 將 hello 檔案 」 VoteDataController.cs"，然後按一下**新增**。 Hello 檔案內容取代 hello 下列項目，然後儲存您的變更。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-hello-services"></a>Hello 服務連接
在下一個步驟中，我們將連接 hello 兩個服務，然後讓 hello 前端 Web 應用程式取得和設定投票從 hello 後端服務的資訊。

對於您與可靠服務通訊的方式，Service Fabric 會提供完整的彈性。 在單一應用程式中，您可能有可透過 TCP 存取的服務。 可透過 HTTP 的 REST API 存取的其他服務以及其他任何服務可以透過 Web 通訊端存取。 如需有關可用的 hello 選項以及 hello 權衡取捨的背景，請參閱[與服務通訊](service-fabric-connect-and-communicate-with-services.md)。

在本教學課程中，我們會使用 [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md)。

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>更新 hello VotesController.cs 檔案
在 hello **VotingWeb**專案、 開啟 hello *Controllers/VotesController.cs*檔案。  取代 hello`VotesController`類別定義的內容，與 hello 下列項目，然後儲存您的變更。

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-hello-voting-sample-application"></a>逐步解說 hello 投票範例應用程式
hello 投票應用程式是由兩個服務所組成：
- Web 前端服務 (VotingWeb)-ASP.NET Core web 前端服務，會做 hello 網頁，並公開 web Api toocommunicate 與 hello 後端服務。
- 後端服務 (VotingData)-ASP.NET Core web 服務會公開 API toostore hello 投票結果可靠的字典中保存在磁碟。

![應用程式圖表](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

當您在下列的 hello 應用程式 hello 投票事件就會發生：
1. JavaScript 會以 HTTP PUT 要求傳送 hello web 前端服務中的 hello 投票要求 toohello web API。

2. hello web 前端服務會使用 proxy toolocate 及轉送 HTTP PUT 要求 toohello 後端服務。

3. hello 後端服務大約需要 hello 傳入的要求，並儲存區 hello 更新在可靠字典中，取得複寫的 toomultiple hello 叢集中的節點，並保存在磁碟上的結果。 所有 hello 應用程式的資料儲存在 hello 叢集中，因此不需要任何資料庫。

## <a name="debug-in-visual-studio"></a>在 Visual Studio 中偵錯
在 Visual Studio 中偵錯應用程式時，您會使用本機 Service Fabric 開發叢集。 您擁有 hello 選項 tooadjust 您偵錯的體驗 tooyour 案例。 在此應用程式中，我們將資料儲存在使用可靠字典的後端服務中。 Visual Studio 移除 hello 應用程式，根據預設，當您停止 hello 偵錯工具。 移除 hello 應用程式造成 hello 資料在 hello 後端服務 tooalso 被移除。 toopersist hello 偵錯工作階段之間的資料，您可以變更 hello**應用程式偵錯模式**為 hello 屬性**投票**Visual Studio 專案中的。

在發生的事 hello 程式碼中，完成下列步驟的 hello toolook:
1. 開啟 hello **VotesController.cs**檔案，並設定中斷點，在 hello web API 的**放**方法 （列 47）-您可以搜尋 hello Visual Studio 中的 [方案總管] 中的 hello 檔案。

2. 開啟 hello **VoteDataController.cs**檔案，並設定中斷點，在這個 web API**放**方法 （行 50）。

3. 返回 toohello 瀏覽器後，請按一下投票選項或加入新的投票選項。 您已達到 hello hello web 前端端的 api 控制器中的第一個中斷點。
    
    1. 這是其中 hello 瀏覽器中的 hello JavaScript 要求 toohello web API 控制器會以傳送 hello 前端服務。
    
    ![新增投票前端服務](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. 我們第一次針對我們的後端服務建構 hello URL toohello ReverseProxy **(1)**。
    3. 接著，我們將傳送嗨 HTTP PUT 要求 toohello ReverseProxy **(2)**。
    4. 最後 hello 我們決定傳回 hello 回應 hello 後端服務 toohello 用戶端從**(3)**。

4. 按**F5** toocontinue
    1. 現在您已位於 hello 中斷點 hello 後端服務。
    
    ![新增投票後端服務](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. Hello hello 方法中的第一行**(1)**我們使用 hello `StateManager` tooget 或可靠的字典，稱為`counts`。
    3. 與可靠字典中的值進行的所有互動，都需要交易，這會使用陳述式 **(2)** 建立該交易。
    4. 在 hello 交易中，我們再更新 hello hello hello 投票選項的相關索引鍵的值，而且認可 hello 作業**(3)**。 一旦認可 hello 方法傳回時，hello 資料更新 hello 字典中，然後複寫 tooother hello 叢集中的節點。 hello 現在會安全地儲存資料 hello 叢集中，hello 後端服務可以容錯移轉 tooother 節點，仍有可用的 hello 資料。
5. 按**F5** toocontinue

偵錯工作階段，請按 toostop hello **Shift + F5**。


## <a name="next-steps"></a>後續步驟
在這個部分 hello 教學課程中，您學會如何：

> [!div class="checklist"]
> * 建立 ASP.NET Core Web API 服務成為具狀態可靠服務
> * 建立 ASP.NET Core Web 應用程式服務成為具狀態可靠服務
> * 使用 hello 反向 proxy toocommunicate 與 hello 可設定狀態服務

進階 toohello 下一個教學課程：
> [!div class="nextstepaction"]
> [部署 hello 應用程式 tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md)
