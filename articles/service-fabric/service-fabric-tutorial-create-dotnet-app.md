---
title: "建立 Service Fabric 的 .NET 應用程式 |Microsoft Docs"
description: "了解如何建立含有 ASP.NET Core 前端和可靠服務具狀態後端的應用程式，並將應用程式部署到叢集。"
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
ms.openlocfilehash: ef50adf3af19bce494c3256308b443c8eaccdcea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="f640c-103">建立和部署含有 ASP.NET Core Web API 前端服務和具狀態後端服務的應用程式</span><span class="sxs-lookup"><span data-stu-id="f640c-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="f640c-104">本教學課程是一個系列的第一部分。</span><span class="sxs-lookup"><span data-stu-id="f640c-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="f640c-105">您將了解如何建立含有 ASP.NET Core Web API 前端和具狀態後端服務的 Azure Service Fabric 應用程式來儲存您的資料。</span><span class="sxs-lookup"><span data-stu-id="f640c-105">You will learn how to create an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service to store your data.</span></span> <span data-ttu-id="f640c-106">當您完成時，您會有一個投票應用程式，其 ASP.NET Core Web 前端會將投票結果儲存在叢集中具狀態的後端服務。</span><span class="sxs-lookup"><span data-stu-id="f640c-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in the cluster.</span></span> <span data-ttu-id="f640c-107">如果您不需要以手動建立投票應用程式，可以[下載已完成應用程式的原始程式碼](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/)並直接前往[逐步解說投票範例應用程式](#walkthrough_anchor)。</span><span class="sxs-lookup"><span data-stu-id="f640c-107">If you don't want to manually create the voting application, you can [download the source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for the completed application and skip ahead to [Walk through the voting sample application](#walkthrough_anchor).</span></span>

![應用程式圖表](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="f640c-109">在系列的第一部分中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="f640c-109">In part one of the series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f640c-110">建立 ASP.NET Core Web API 服務成為具狀態可靠服務</span><span class="sxs-lookup"><span data-stu-id="f640c-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="f640c-111">建立 ASP.NET Core Web 應用程式服務成為具狀態可靠服務</span><span class="sxs-lookup"><span data-stu-id="f640c-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="f640c-112">使用反向 proxy 來與具狀態服務進行通訊</span><span class="sxs-lookup"><span data-stu-id="f640c-112">Use the reverse proxy to communicate with the stateful service</span></span>

<span data-ttu-id="f640c-113">在本教學課程系列中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="f640c-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="f640c-114">建置 .NET Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="f640c-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="f640c-115">將應用程式部署到遠端叢集</span><span class="sxs-lookup"><span data-stu-id="f640c-115">Deploy the application to a remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="f640c-116">使用 Visual Studio Team Services 設定 CI/CD</span><span class="sxs-lookup"><span data-stu-id="f640c-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="f640c-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="f640c-117">Prerequisites</span></span>
<span data-ttu-id="f640c-118">開始進行本教學課程之前：</span><span class="sxs-lookup"><span data-stu-id="f640c-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="f640c-119">如果您沒有 Azure 訂用帳戶，請建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="f640c-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="f640c-120">[安裝 Visual Studio 2017](https://www.visualstudio.com/) 並安裝 **Azure 開發**以及 **ASP.NET 和 Web 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="f640c-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install the **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="f640c-121">安裝 Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="f640c-121">Install the Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="f640c-122">建立 ASP.NET Web API 服務成為可靠的服務</span><span class="sxs-lookup"><span data-stu-id="f640c-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="f640c-123">首先，使用 ASP.NET Core 建立投票應用程式的 web 前端。</span><span class="sxs-lookup"><span data-stu-id="f640c-123">First, create the web front-end of the voting application using ASP.NET Core.</span></span> <span data-ttu-id="f640c-124">ASP.NET Core 是輕量型、跨平台的 Web 開發架構，可供您用來建立新式 Web UI 和 Web API。</span><span class="sxs-lookup"><span data-stu-id="f640c-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> <span data-ttu-id="f640c-125">若要完整了解 ASP.NET Core 如何與 Service Fabric 整合，強烈建議您仔細閱讀 [Service Fabric Reliable Services 中的 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="f640c-125">To get a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through the [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="f640c-126">現在，您可以依照本教學課程來快速上手。</span><span class="sxs-lookup"><span data-stu-id="f640c-126">For now, you can follow this tutorial to get started quickly.</span></span> <span data-ttu-id="f640c-127">若要深入了解 ASP.NET Core，請參閱 [ASP.NET Core 文件](https://docs.microsoft.com/aspnet/core/)。</span><span class="sxs-lookup"><span data-stu-id="f640c-127">To learn more about ASP.NET Core, see the [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="f640c-128">本教學課程係根據[適用於 Visual Studio 2017 的 ASP.NET Core 工具](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc)。</span><span class="sxs-lookup"><span data-stu-id="f640c-128">This tutorial is based on the [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="f640c-129">適用於 Visual Studio 2015 的 .NET Core 工具不再進行更新。</span><span class="sxs-lookup"><span data-stu-id="f640c-129">The .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="f640c-130">以**系統管理員**身分啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f640c-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="f640c-131">使用**檔案**->**新增**->**專案**建立專案</span><span class="sxs-lookup"><span data-stu-id="f640c-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="f640c-132">在 [新增專案]  對話方塊中，選擇 [雲端] > [Service Fabric 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f640c-132">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="f640c-133">將應用程式命名為 **Voting**，然後按 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f640c-133">Name the application **Voting** and press **OK**.</span></span>

   ![Visual Studio 中的新增專案對話方塊](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="f640c-135">在**新增 Service Fabric 服務**頁面上，選擇**無狀態 ASP.NET Core**，並將服務命名為 **VotingWeb**。</span><span class="sxs-lookup"><span data-stu-id="f640c-135">On the **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![在新服務對話方塊中選擇 ASP.NET Web 服務](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="f640c-137">下一頁會提供一組 ASP.NET Core 專案範本。</span><span class="sxs-lookup"><span data-stu-id="f640c-137">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="f640c-138">在本教學課程中，選擇 [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f640c-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![選擇 ASP.NET 專案類型](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="f640c-140">Visual Studio 會建立應用程式和服務專案，並顯示在 [方案總管] 中。</span><span class="sxs-lookup"><span data-stu-id="f640c-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![使用 ASP.NET Core Web API 服務建立應用程式後的方案總管]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-to-the-votingweb-service"></a><span data-ttu-id="f640c-142">將 AngularJS 新增至 VotingWeb 服務</span><span class="sxs-lookup"><span data-stu-id="f640c-142">Add AngularJS to the VotingWeb service</span></span>
<span data-ttu-id="f640c-143">使用內建 [Bower 支援](/aspnet/core/client-side/bower)將 [AngularJS](http://angularjs.org/) 新增至您的服務。</span><span class="sxs-lookup"><span data-stu-id="f640c-143">Add [AngularJS](http://angularjs.org/) to your service using the built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="f640c-144">開啟 bower.json 並新增 Angular 和 Angular 啟動程序的項目，然後儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="f640c-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

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
<span data-ttu-id="f640c-145">在儲存 bower.json 檔案時，Angular 會安裝在您專案的 wwwroot/lib 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f640c-145">Upon saving the *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="f640c-146">此外，它會列在 Dependencies/Bower 資料夾內。</span><span class="sxs-lookup"><span data-stu-id="f640c-146">Additionally, it is listed within the *Dependencies/Bower* folder.</span></span>

### <a name="update-the-sitejs-file"></a><span data-ttu-id="f640c-147">更新 site.js 檔案</span><span class="sxs-lookup"><span data-stu-id="f640c-147">Update the site.js file</span></span>
<span data-ttu-id="f640c-148">開啟 wwwroot/js/site.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="f640c-148">Open the *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="f640c-149">將其內容取代為 [首頁] 檢視所使用的 JavaScript：</span><span class="sxs-lookup"><span data-stu-id="f640c-149">Replace its contents with the JavaScript used by the Home views:</span></span>

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

### <a name="update-the-indexcshtml-file"></a><span data-ttu-id="f640c-150">更新 Index.cshtml 檔案</span><span class="sxs-lookup"><span data-stu-id="f640c-150">Update the Index.cshtml file</span></span>
<span data-ttu-id="f640c-151">開啟 Views/Home/Index.cshtml 檔案，檢視為 [首頁] 控制器特定。</span><span class="sxs-lookup"><span data-stu-id="f640c-151">Open the *Views/Home/Index.cshtml* file, the view specific to the Home controller.</span></span>  <span data-ttu-id="f640c-152">將其內容取代為下列項目，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f640c-152">Replace its contents with the following, then save your changes.</span></span>

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
                        Click to vote
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

### <a name="update-the-layoutcshtml-file"></a><span data-ttu-id="f640c-153">更新 _Layout.cshtml 檔案</span><span class="sxs-lookup"><span data-stu-id="f640c-153">Update the _Layout.cshtml file</span></span>
<span data-ttu-id="f640c-154">開啟 Views/Shared/_Layout.cshtml 檔案，ASP.NET 應用程式的預設版面配置。</span><span class="sxs-lookup"><span data-stu-id="f640c-154">Open the *Views/Shared/_Layout.cshtml* file, the default layout for the ASP.NET app.</span></span>  <span data-ttu-id="f640c-155">將其內容取代為下列項目，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f640c-155">Replace its contents with the following, then save your changes.</span></span>

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

### <a name="update-the-votingwebcs-file"></a><span data-ttu-id="f640c-156">更新 VotingWeb.cs 檔案</span><span class="sxs-lookup"><span data-stu-id="f640c-156">Update the VotingWeb.cs file</span></span>
<span data-ttu-id="f640c-157">開啟 VotingWeb.cs 檔案，該檔案會使用 WebListener web 伺服器，在無狀態服務內建立 ASP.NET Core WebHost。</span><span class="sxs-lookup"><span data-stu-id="f640c-157">Open the *VotingWeb.cs* file, which creates the ASP.NET Core WebHost inside the stateless service using the WebListener web server.</span></span>  <span data-ttu-id="f640c-158">將 `using System.Net.Http;` 指示詞新增至檔案開頭處。</span><span class="sxs-lookup"><span data-stu-id="f640c-158">Add the `using System.Net.Http;` directive to the top of the file.</span></span>  <span data-ttu-id="f640c-159">將 `CreateServiceInstanceListeners()` 函式取代為下列項目，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f640c-159">Replace the `CreateServiceInstanceListeners()` function with the following, then save your changes.</span></span>

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

### <a name="add-the-votescontrollercs-file"></a><span data-ttu-id="f640c-160">新增 VotesController.cs 檔案</span><span class="sxs-lookup"><span data-stu-id="f640c-160">Add the VotesController.cs file</span></span>
<span data-ttu-id="f640c-161">新增定義投票動作的控制器。</span><span class="sxs-lookup"><span data-stu-id="f640c-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="f640c-162">以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [新增 -> 新增項目 -> 類別]。</span><span class="sxs-lookup"><span data-stu-id="f640c-162">Right-click on the **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="f640c-163">將檔案命名為 "VotesController.cs"，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f640c-163">Name the file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="f640c-164">將檔案內容取代為下列項目，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f640c-164">Replace the file contents with the following, then save your changes.</span></span>  <span data-ttu-id="f640c-165">稍後，在[更新 VotesController.cs 檔案](#updatevotecontroller_anchor)中，將會修改這個檔案，以從後端服務讀取和寫入投票資料。</span><span class="sxs-lookup"><span data-stu-id="f640c-165">Later, in [Update the VotesController.cs file](#updatevotecontroller_anchor), this file will be modified to read and write voting data from the back-end service.</span></span>  <span data-ttu-id="f640c-166">現在，控制器會將靜態字串資料傳回至檢視。</span><span class="sxs-lookup"><span data-stu-id="f640c-166">For now, the controller returns static string data to the view.</span></span>

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



### <a name="deploy-and-run-the-application-locally"></a><span data-ttu-id="f640c-167">在本機部署和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f640c-167">Deploy and run the application locally</span></span>
<span data-ttu-id="f640c-168">您現在可以繼續執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f640c-168">You can now go ahead and run the application.</span></span> <span data-ttu-id="f640c-169">在 Visual Studio 中，按 `F5` 部署應用程式以供偵錯。</span><span class="sxs-lookup"><span data-stu-id="f640c-169">In Visual Studio, press `F5` to deploy the application for debugging.</span></span> <span data-ttu-id="f640c-170">如果您先前並未以**系統管理員**身分開啟 Visual Studio，`F5` 將失敗。</span><span class="sxs-lookup"><span data-stu-id="f640c-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="f640c-171">您第一次在本機執行及部署應用程式時，Visual Studio 會建立本機叢集以供偵錯。</span><span class="sxs-lookup"><span data-stu-id="f640c-171">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="f640c-172">建立叢集可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="f640c-172">Cluster creation may take some time.</span></span> <span data-ttu-id="f640c-173">叢集建立狀態會顯示在 Visual Studio 輸出視窗中。</span><span class="sxs-lookup"><span data-stu-id="f640c-173">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="f640c-174">此時，您的 web 應用程式看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="f640c-174">At this point, your web app should look like this:</span></span>

![ASP.NET Core 前端](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="f640c-176">若要停止應用程式偵錯，請返回 Visual Studio 並且按**Shift+F5**。</span><span class="sxs-lookup"><span data-stu-id="f640c-176">To stop debugging the application, go back to Visual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-to-your-application"></a><span data-ttu-id="f640c-177">將具狀態後端服務新增到應用程式</span><span class="sxs-lookup"><span data-stu-id="f640c-177">Add a stateful back-end service to your application</span></span>
<span data-ttu-id="f640c-178">現在，應用程式中有 ASP.NET Web API 服務正在執行，讓我們繼續新增具狀態可靠服務，將一些資料儲存於應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f640c-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service to store some data in our application.</span></span>

<span data-ttu-id="f640c-179">Service Fabric 可讓您使用可靠集合，直接在服務內以一致且可靠的方式儲存資料。</span><span class="sxs-lookup"><span data-stu-id="f640c-179">Service Fabric allows you to consistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="f640c-180">可靠集合是一組高可用性和可靠的集合類別，用過 C# 集合的任何人都會很熟悉。</span><span class="sxs-lookup"><span data-stu-id="f640c-180">Reliable collections are a set of highly available and reliable collection classes that are familiar to anyone who has used C# collections.</span></span>

<span data-ttu-id="f640c-181">在本教學課程中，您建立服務，將計數器值儲存於可靠集合中。</span><span class="sxs-lookup"><span data-stu-id="f640c-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="f640c-182">在 [方案總管] 中，以滑鼠右鍵按一下應用程式專案中的 [服務]，然後選擇 [新增] > [新增 Service Fabric Explorer]。</span><span class="sxs-lookup"><span data-stu-id="f640c-182">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![將新服務加入至現有的應用程式](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="f640c-184">在 [新增 Service Fabric 服務] 對話方塊中，選擇 [具狀態 ASP.NET Core]，並將服務命名為 **VotingData**，然後按 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f640c-184">In the **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name the service **VotingData** and press **OK**.</span></span>

    ![Visual Studio 中的新增服務對話方塊](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="f640c-186">建立服務專案後，您的應用程式中會有兩個服務。</span><span class="sxs-lookup"><span data-stu-id="f640c-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="f640c-187">隨著您繼續組建應用程式，您可以用相同的方式新增更多服務。</span><span class="sxs-lookup"><span data-stu-id="f640c-187">As you continue to build your application, you can add more services in the same way.</span></span> <span data-ttu-id="f640c-188">每個服務都可以獨立設定版本和升級。</span><span class="sxs-lookup"><span data-stu-id="f640c-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="f640c-189">下一頁會提供一組 ASP.NET Core 專案範本。</span><span class="sxs-lookup"><span data-stu-id="f640c-189">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="f640c-190">在本教學課程中，選擇 [Web API]。</span><span class="sxs-lookup"><span data-stu-id="f640c-190">For this tutorial, choose **Web API**.</span></span>

    ![選擇 ASP.NET 專案類型](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="f640c-192">Visual Studio 會建立服務專案，並顯示在 [方案總管] 中。</span><span class="sxs-lookup"><span data-stu-id="f640c-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Solution Explorer](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-the-votedatacontrollercs-file"></a><span data-ttu-id="f640c-194">新增 VoteDataController.cs 檔案</span><span class="sxs-lookup"><span data-stu-id="f640c-194">Add the VoteDataController.cs file</span></span>

<span data-ttu-id="f640c-195">在 **VotingData** 專案中，以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [新增 -> 新增項目 -> 類別]。</span><span class="sxs-lookup"><span data-stu-id="f640c-195">In the **VotingData** project right-click on the **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="f640c-196">將檔案命名為 "VoteDataController.cs"，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f640c-196">Name the file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="f640c-197">將檔案內容取代為下列項目，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f640c-197">Replace the file contents with the following, then save your changes.</span></span>

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


## <a name="connect-the-services"></a><span data-ttu-id="f640c-198">連接服務</span><span class="sxs-lookup"><span data-stu-id="f640c-198">Connect the services</span></span>
<span data-ttu-id="f640c-199">在下一個步驟中，我們會將這兩項服務連線，並讓前端 Web 應用程式從後端服務取得和設定投票資訊。</span><span class="sxs-lookup"><span data-stu-id="f640c-199">In this next step, we will connect the two services and make the front-end Web application get and set voting information from the back-end service.</span></span>

<span data-ttu-id="f640c-200">對於您與可靠服務通訊的方式，Service Fabric 會提供完整的彈性。</span><span class="sxs-lookup"><span data-stu-id="f640c-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="f640c-201">在單一應用程式中，您可能有可透過 TCP 存取的服務。</span><span class="sxs-lookup"><span data-stu-id="f640c-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="f640c-202">可透過 HTTP 的 REST API 存取的其他服務以及其他任何服務可以透過 Web 通訊端存取。</span><span class="sxs-lookup"><span data-stu-id="f640c-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="f640c-203">如需可用選項和相關權衡取捨的背景，請參閱 [與服務進行通訊](service-fabric-connect-and-communicate-with-services.md)。</span><span class="sxs-lookup"><span data-stu-id="f640c-203">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="f640c-204">在本教學課程中，我們會使用 [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md)。</span><span class="sxs-lookup"><span data-stu-id="f640c-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-the-votescontrollercs-file"></a><span data-ttu-id="f640c-205">更新 VotesController.cs 檔案</span><span class="sxs-lookup"><span data-stu-id="f640c-205">Update the VotesController.cs file</span></span>
<span data-ttu-id="f640c-206">在 **VotingWeb** 專案中，開啟 Controllers/VotesController.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="f640c-206">In the **VotingWeb** project, open the *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="f640c-207">將 `VotesController` 類別定義內容取代為下列項目，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f640c-207">Replace the `VotesController` class definition contents with the following, then save your changes.</span></span>

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

## <a name="walk-through-the-voting-sample-application"></a><span data-ttu-id="f640c-208">逐步解說投票範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f640c-208">Walk through the voting sample application</span></span>
<span data-ttu-id="f640c-209">投票應用程式包含兩個服務：</span><span class="sxs-lookup"><span data-stu-id="f640c-209">The voting application consists of two services:</span></span>
- <span data-ttu-id="f640c-210">Web 前端服務 (VotingWeb) 是 ASP.NET Core Web 前端服務，可作為網頁，並公開 Web API 來與後端服務通訊。</span><span class="sxs-lookup"><span data-stu-id="f640c-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves the web page and exposes web APIs to communicate with the backend service.</span></span>
- <span data-ttu-id="f640c-211">後端服務 (VotingData) 是 ASP.NET Core Web 服務，會公開 API 來將投票結果儲存在磁碟上所保存的可靠字典中。</span><span class="sxs-lookup"><span data-stu-id="f640c-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API to store the vote results in a reliable dictionary persisted on disk.</span></span>

![應用程式圖表](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="f640c-213">當您在應用程式中投票時，會發生下列事件：</span><span class="sxs-lookup"><span data-stu-id="f640c-213">When you vote in the application the following events occur:</span></span>
1. <span data-ttu-id="f640c-214">JavaScript 會將投票要求當做 HTTP PUT 要求，傳送至 Web 前端服務中的 Web API。</span><span class="sxs-lookup"><span data-stu-id="f640c-214">A JavaScript sends the vote request to the web API in the web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="f640c-215">Web 前端服務使用 Proxy 來尋找 HTTP PUT 要求，並將其轉送至後端服務。</span><span class="sxs-lookup"><span data-stu-id="f640c-215">The web front-end service uses a proxy to locate and forward an HTTP PUT request to the back-end service.</span></span>

3. <span data-ttu-id="f640c-216">後端服務會接受傳入要求，並將更新的結果儲存在可靠的字典中，以複寫至叢集中的多個節點並保存在磁碟上。</span><span class="sxs-lookup"><span data-stu-id="f640c-216">The back-end service takes the incoming request, and stores the updated result in a reliable dictionary, which gets replicated to multiple nodes within the cluster and persisted on disk.</span></span> <span data-ttu-id="f640c-217">應用程式的所有資料都會儲存在叢集中，因此不需要資料庫。</span><span class="sxs-lookup"><span data-stu-id="f640c-217">All the application's data is stored in the cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="f640c-218">在 Visual Studio 中偵錯</span><span class="sxs-lookup"><span data-stu-id="f640c-218">Debug in Visual Studio</span></span>
<span data-ttu-id="f640c-219">在 Visual Studio 中偵錯應用程式時，您會使用本機 Service Fabric 開發叢集。</span><span class="sxs-lookup"><span data-stu-id="f640c-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="f640c-220">您可以根據自己的情況選擇調整偵錯體驗。</span><span class="sxs-lookup"><span data-stu-id="f640c-220">You have the option to adjust your debugging experience to your scenario.</span></span> <span data-ttu-id="f640c-221">在此應用程式中，我們將資料儲存在使用可靠字典的後端服務中。</span><span class="sxs-lookup"><span data-stu-id="f640c-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="f640c-222">當您停止偵錯工具時，Visual Studio 預設會移除應用程式。</span><span class="sxs-lookup"><span data-stu-id="f640c-222">Visual Studio removes the application per default when you stop the debugger.</span></span> <span data-ttu-id="f640c-223">移除應用程式也會導致移除後端服務中的資料。</span><span class="sxs-lookup"><span data-stu-id="f640c-223">Removing the application causes the data in the back-end service to also be removed.</span></span> <span data-ttu-id="f640c-224">若要保存偵錯工作階段之間的資料，您可以在 Visual Studio 中，將 [應用程式偵錯模式] 當做 [投票] 專案上的屬性來變更。</span><span class="sxs-lookup"><span data-stu-id="f640c-224">To persist the data between debugging sessions, you can change the **Application Debug Mode** as a property on the **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="f640c-225">若要查看對程式碼的影響，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f640c-225">To look at what happens in the code, complete the following steps:</span></span>
1. <span data-ttu-id="f640c-226">開啟 **VotesController.cs** 檔案，並在 Web API 的 **Put** 方法 (第 47 行) 中設定中斷點 - 您可以在 Visual Studio 的方案總管中搜尋此檔案。</span><span class="sxs-lookup"><span data-stu-id="f640c-226">Open the **VotesController.cs** file and set a breakpoint in the web API's **Put** method (line 47) - You can search for the file in the Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="f640c-227">開啟 **VoteDataController.cs** 檔案，並在此 Web API 的 **Put** 方法 (第 50 行) 中設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="f640c-227">Open the **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="f640c-228">返回到瀏覽器，並按一下投票選項或新增投票選項。</span><span class="sxs-lookup"><span data-stu-id="f640c-228">Go back to the browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="f640c-229">您到達 Web 前端之 API 控制器的第一個中斷點。</span><span class="sxs-lookup"><span data-stu-id="f640c-229">You hit the first breakpoint in the web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="f640c-230">瀏覽器中的 JavaScript 會在此位置，將要求傳送至前端服務中的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="f640c-230">This is where the JavaScript in the browser sends a request to the web API controller in the front-end service.</span></span>
    
    ![新增投票前端服務](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="f640c-232">首先，我們會針對後端服務 **(1)** 建構 ReverseProxy 的 URL。</span><span class="sxs-lookup"><span data-stu-id="f640c-232">First we construct the URL to the ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="f640c-233">接著，我們會將 HTTP PUT 要求傳送至 ReverseProxy **(2)**。</span><span class="sxs-lookup"><span data-stu-id="f640c-233">Then we send the HTTP PUT Request to the ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="f640c-234">最後我們會將後端服務的回應傳回至用戶端 **(3)**。</span><span class="sxs-lookup"><span data-stu-id="f640c-234">Finally the we return the response from the back-end service to the client **(3)**.</span></span>

4. <span data-ttu-id="f640c-235">按 **F5** 繼續</span><span class="sxs-lookup"><span data-stu-id="f640c-235">Press **F5** to continue</span></span>
    1. <span data-ttu-id="f640c-236">您現在位於後端服務的中斷點。</span><span class="sxs-lookup"><span data-stu-id="f640c-236">You are now at the break point in the back-end service.</span></span>
    
    ![新增投票後端服務](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="f640c-238">在方法的第一行 **(1)** 中，我們使用 `StateManager` 取得或新增名為 `counts` 的可靠字典。</span><span class="sxs-lookup"><span data-stu-id="f640c-238">In the first line in the method **(1)** we are using the `StateManager` to get or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="f640c-239">與可靠字典中的值進行的所有互動，都需要交易，這會使用陳述式 **(2)** 建立該交易。</span><span class="sxs-lookup"><span data-stu-id="f640c-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="f640c-240">在交易中，我們會接著更新投票選項的相關索引鍵值，然後認可作業 **(3)**。</span><span class="sxs-lookup"><span data-stu-id="f640c-240">In the transaction, we then update the value of the relevant key for the voting option and commits the operation **(3)**.</span></span> <span data-ttu-id="f640c-241">一旦傳回認可方法，字典中的資料會更新並複寫至叢集中的其他節點。</span><span class="sxs-lookup"><span data-stu-id="f640c-241">Once the commit method returns, the data is updated in the dictionary and replicated to other nodes in the cluster.</span></span> <span data-ttu-id="f640c-242">資料現在會安全地儲存在叢集中，而且後端服務可以容錯移轉到仍有可用資料的其他節點。</span><span class="sxs-lookup"><span data-stu-id="f640c-242">The data is now safely stored in the cluster, and the back-end service can fail over to other nodes, still having the data available.</span></span>
5. <span data-ttu-id="f640c-243">按 **F5** 繼續</span><span class="sxs-lookup"><span data-stu-id="f640c-243">Press **F5** to continue</span></span>

<span data-ttu-id="f640c-244">若要停止偵錯工作階段，請按 **Shift+F5**。</span><span class="sxs-lookup"><span data-stu-id="f640c-244">To stop the debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f640c-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f640c-245">Next steps</span></span>
<span data-ttu-id="f640c-246">在教學課程的這個部分中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="f640c-246">In this part of the tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f640c-247">建立 ASP.NET Core Web API 服務成為具狀態可靠服務</span><span class="sxs-lookup"><span data-stu-id="f640c-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="f640c-248">建立 ASP.NET Core Web 應用程式服務成為具狀態可靠服務</span><span class="sxs-lookup"><span data-stu-id="f640c-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="f640c-249">使用反向 proxy 來與具狀態服務進行通訊</span><span class="sxs-lookup"><span data-stu-id="f640c-249">Use the reverse proxy to communicate with the stateful service</span></span>

<span data-ttu-id="f640c-250">前進到下一個教學課程：</span><span class="sxs-lookup"><span data-stu-id="f640c-250">Advance to the next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f640c-251">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="f640c-251">Deploy the application to Azure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)