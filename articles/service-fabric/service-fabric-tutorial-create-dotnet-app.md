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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="96caf-103">建立和部署含有 ASP.NET Core Web API 前端服務和具狀態後端服務的應用程式</span><span class="sxs-lookup"><span data-stu-id="96caf-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="96caf-104">本教學課程是一個系列的第一部分。</span><span class="sxs-lookup"><span data-stu-id="96caf-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="96caf-105">您將學習如何 toocreate ASP.NET Core Web API 最上層的 Azure Service Fabric 應用程式結束，並可設定狀態的後端服務 toostore 您的資料。</span><span class="sxs-lookup"><span data-stu-id="96caf-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="96caf-106">當您完成時，必須具有 ASP.NET Core web 前端，將投票的結果儲存在可設定狀態的後端服務 hello 叢集中的投票應用程式。</span><span class="sxs-lookup"><span data-stu-id="96caf-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="96caf-107">如果您不想 toomanually 建立 hello 投票應用程式，您可以[hello 將原始程式碼下載](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/)hello 已完成應用程式，並跳過[逐步解說投票範例應用程式的 hello](#walkthrough_anchor)。</span><span class="sxs-lookup"><span data-stu-id="96caf-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![應用程式圖表](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="96caf-109">其中一個 hello 系列的一部分，在您了解如何：</span><span class="sxs-lookup"><span data-stu-id="96caf-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="96caf-110">建立 ASP.NET Core Web API 服務成為具狀態可靠服務</span><span class="sxs-lookup"><span data-stu-id="96caf-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="96caf-111">建立 ASP.NET Core Web 應用程式服務成為具狀態可靠服務</span><span class="sxs-lookup"><span data-stu-id="96caf-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="96caf-112">使用 hello 反向 proxy toocommunicate 與 hello 可設定狀態服務</span><span class="sxs-lookup"><span data-stu-id="96caf-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="96caf-113">在本教學課程系列中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="96caf-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="96caf-114">建置 .NET Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="96caf-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="96caf-115">部署 hello 應用程式 tooa 遠端叢集</span><span class="sxs-lookup"><span data-stu-id="96caf-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="96caf-116">使用 Visual Studio Team Services 設定 CI/CD</span><span class="sxs-lookup"><span data-stu-id="96caf-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="96caf-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="96caf-117">Prerequisites</span></span>
<span data-ttu-id="96caf-118">開始進行本教學課程之前：</span><span class="sxs-lookup"><span data-stu-id="96caf-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="96caf-119">如果您沒有 Azure 訂用帳戶，請建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="96caf-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="96caf-120">[安裝 Visual Studio 2017](https://www.visualstudio.com/)並安裝 hello **Azure 開發**和**ASP.NET 及 web 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="96caf-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="96caf-121">安裝 hello Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="96caf-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="96caf-122">建立 ASP.NET Web API 服務成為可靠的服務</span><span class="sxs-lookup"><span data-stu-id="96caf-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="96caf-123">首先，建立 hello web 前端的 hello 投票使用 ASP.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="96caf-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="96caf-124">ASP.NET Core 是輕量型、 跨平台的 web 開發架構，您可以使用 toocreate 新式 web UI 和 web 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="96caf-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="96caf-125">tooget 瞭解的 ASP.NET Core Service Fabric 與整合的方式，我們強烈建議您閱讀 hello [Service Fabric 可靠的服務中的 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="96caf-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="96caf-126">現在，您可以遵循這個快速入門的教學課程 tooget。</span><span class="sxs-lookup"><span data-stu-id="96caf-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="96caf-127">深入了解 ASP.NET Core toolearn 看到 hello [ASP.NET Core 文件集](https://docs.microsoft.com/aspnet/core/)。</span><span class="sxs-lookup"><span data-stu-id="96caf-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="96caf-128">本教學課程根據 hello [ASP.NET Core 工具的 Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc)。</span><span class="sxs-lookup"><span data-stu-id="96caf-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="96caf-129">Visual Studio 2015 的 hello.NET Core 工具不再正在更新。</span><span class="sxs-lookup"><span data-stu-id="96caf-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="96caf-130">以**系統管理員**身分啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="96caf-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="96caf-131">使用**檔案**->**新增**->**專案**建立專案</span><span class="sxs-lookup"><span data-stu-id="96caf-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="96caf-132">在 [hello**新專案**] 對話方塊中，選擇**雲端 > Service Fabric 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="96caf-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="96caf-133">Hello 應用程式命名**投票**按**確定**。</span><span class="sxs-lookup"><span data-stu-id="96caf-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Visual Studio 中的新增專案對話方塊](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="96caf-135">在 hello**新增 Service Fabric 服務**頁面上，選擇**無狀態的 ASP.NET Core**，並命名您的服務**VotingWeb**。</span><span class="sxs-lookup"><span data-stu-id="96caf-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![在 [hello 新增服務] 對話方塊中選擇 ASP.NET web 服務](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="96caf-137">hello 下一個頁面會提供一組 ASP.NET Core 專案範本。</span><span class="sxs-lookup"><span data-stu-id="96caf-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="96caf-138">在本教學課程中，選擇 [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="96caf-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![選擇 ASP.NET 專案類型](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="96caf-140">Visual Studio 會建立應用程式和服務專案，並顯示在 [方案總管] 中。</span><span class="sxs-lookup"><span data-stu-id="96caf-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![使用 ASP.NET Core Web API 服務建立應用程式後的方案總管]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="96caf-142">加入 AngularJS toohello VotingWeb 服務</span><span class="sxs-lookup"><span data-stu-id="96caf-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="96caf-143">新增[AngularJS](http://angularjs.org/) tooyour 服務使用 hello 內建[Bower 支援](/aspnet/core/client-side/bower)。</span><span class="sxs-lookup"><span data-stu-id="96caf-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="96caf-144">開啟 bower.json 並新增 Angular 和 Angular 啟動程序的項目，然後儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="96caf-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

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
<span data-ttu-id="96caf-145">在儲存 hello 時*bower.json* Angular 的檔案會安裝在您的專案*wwwroot/lib*資料夾。</span><span class="sxs-lookup"><span data-stu-id="96caf-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="96caf-146">此外，它會列在 hello*相依性/Bower*資料夾。</span><span class="sxs-lookup"><span data-stu-id="96caf-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="96caf-147">更新 hello site.js 檔案</span><span class="sxs-lookup"><span data-stu-id="96caf-147">Update hello site.js file</span></span>
<span data-ttu-id="96caf-148">開啟 hello *wwwroot/js/site.js*檔案。</span><span class="sxs-lookup"><span data-stu-id="96caf-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="96caf-149">取代 hello JavaScript 使用 hello 首頁檢視其內容：</span><span class="sxs-lookup"><span data-stu-id="96caf-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

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

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="96caf-150">更新 hello Index.cshtml 檔案</span><span class="sxs-lookup"><span data-stu-id="96caf-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="96caf-151">開啟 hello *Views/Home/Index.cshtml*檔案、 hello 檢視特定 toohello Home 控制器。</span><span class="sxs-lookup"><span data-stu-id="96caf-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="96caf-152">Hello 下列程式碼，以取代其內容，然後儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="96caf-152">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="96caf-153">更新 hello _Layout.cshtml 檔案</span><span class="sxs-lookup"><span data-stu-id="96caf-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="96caf-154">開啟 hello *Views/Shared/_Layout.cshtml*檔案、 hello hello ASP.NET 應用程式的預設版面配置。</span><span class="sxs-lookup"><span data-stu-id="96caf-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="96caf-155">Hello 下列程式碼，以取代其內容，然後儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="96caf-155">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="96caf-156">更新 hello VotingWeb.cs 檔案</span><span class="sxs-lookup"><span data-stu-id="96caf-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="96caf-157">開啟 hello *VotingWeb.cs*建立 hello ASP.NET Core WebHost hello 使用 hello WebListener web 伺服器的無狀態服務內的檔案。</span><span class="sxs-lookup"><span data-stu-id="96caf-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="96caf-158">新增 hello`using System.Net.Http;`指示詞 toohello hello 檔案的頂端。</span><span class="sxs-lookup"><span data-stu-id="96caf-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="96caf-159">取代 hello `CreateServiceInstanceListeners()` hello 下列函數，然後儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="96caf-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

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

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="96caf-160">加入 hello VotesController.cs 檔案</span><span class="sxs-lookup"><span data-stu-id="96caf-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="96caf-161">新增定義投票動作的控制器。</span><span class="sxs-lookup"><span data-stu-id="96caf-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="96caf-162">以滑鼠右鍵按一下 hello**控制器**資料夾，然後選取**新增-> 新增項目類別->** 。</span><span class="sxs-lookup"><span data-stu-id="96caf-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="96caf-163">將 hello 檔案 」 VotesController.cs"，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="96caf-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="96caf-164">Hello 檔案內容取代 hello 下列項目，然後儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="96caf-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="96caf-165">稍後在[更新 hello VotesController.cs 檔案](#updatevotecontroller_anchor)，這個檔案將已修改的 tooread 並從 hello 後端服務寫入投票資料。</span><span class="sxs-lookup"><span data-stu-id="96caf-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="96caf-166">現在，hello 控制站會傳回靜態字串資料 toohello 檢視。</span><span class="sxs-lookup"><span data-stu-id="96caf-166">For now, hello controller returns static string data toohello view.</span></span>

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



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="96caf-167">部署並在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="96caf-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="96caf-168">您現在可以繼續，並執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="96caf-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="96caf-169">在 Visual Studio 中，按`F5`toodeploy hello 應用程式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="96caf-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="96caf-170">如果您先前並未以**系統管理員**身分開啟 Visual Studio，`F5` 將失敗。</span><span class="sxs-lookup"><span data-stu-id="96caf-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="96caf-171">hello 第一次執行，並部署 hello 應用程式在本機，Visual Studio 會建立偵錯的本機叢集。</span><span class="sxs-lookup"><span data-stu-id="96caf-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="96caf-172">建立叢集可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="96caf-172">Cluster creation may take some time.</span></span> <span data-ttu-id="96caf-173">hello Visual Studio 輸出 視窗中會顯示 hello 叢集建立狀態。</span><span class="sxs-lookup"><span data-stu-id="96caf-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="96caf-174">此時，您的 web 應用程式看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="96caf-174">At this point, your web app should look like this:</span></span>

![ASP.NET Core 前端](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="96caf-176">toostop 偵錯 hello 應用程式，請返回 tooVisual Studio，然後按**Shift + F5**。</span><span class="sxs-lookup"><span data-stu-id="96caf-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="96caf-177">新增可設定狀態的後端服務 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="96caf-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="96caf-178">現在，我們已經在我們的應用程式中執行的 ASP.NET Web API 服務，請繼續進行，在我們的應用程式中新增可設定狀態的可靠服務 toostore 某些資料。</span><span class="sxs-lookup"><span data-stu-id="96caf-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="96caf-179">Service Fabric tooconsistently 可讓您和可靠地儲存在您的服務將資料直接使用可靠的集合。</span><span class="sxs-lookup"><span data-stu-id="96caf-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="96caf-180">可靠的集合是一組都已使用 C# 集合熟悉 tooanyone 的高度可用且可靠的集合類別。</span><span class="sxs-lookup"><span data-stu-id="96caf-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="96caf-181">在本教學課程中，您建立服務，將計數器值儲存於可靠集合中。</span><span class="sxs-lookup"><span data-stu-id="96caf-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="96caf-182">在 方案總管 中，以滑鼠右鍵按一下**服務**內 hello 應用程式專案，然後選擇 **新增 > 新增 Service Fabric 服務**。</span><span class="sxs-lookup"><span data-stu-id="96caf-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![加入新的服務 tooan 現有應用程式](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="96caf-184">在 hello**新增 Service Fabric 服務** 對話方塊中，選擇**可設定狀態的 ASP.NET Core**，和名稱 hello 服務**VotingData**按**確定**。</span><span class="sxs-lookup"><span data-stu-id="96caf-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Visual Studio 中的新增服務對話方塊](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="96caf-186">建立服務專案後，您的應用程式中會有兩個服務。</span><span class="sxs-lookup"><span data-stu-id="96caf-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="96caf-187">當您繼續 toobuild 您的應用程式，您就可以在 hello 中加入更多服務相同的方式。</span><span class="sxs-lookup"><span data-stu-id="96caf-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="96caf-188">每個服務都可以獨立設定版本和升級。</span><span class="sxs-lookup"><span data-stu-id="96caf-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="96caf-189">hello 下一個頁面會提供一組 ASP.NET Core 專案範本。</span><span class="sxs-lookup"><span data-stu-id="96caf-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="96caf-190">在本教學課程中，選擇 [Web API]。</span><span class="sxs-lookup"><span data-stu-id="96caf-190">For this tutorial, choose **Web API**.</span></span>

    ![選擇 ASP.NET 專案類型](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="96caf-192">Visual Studio 會建立服務專案，並顯示在 [方案總管] 中。</span><span class="sxs-lookup"><span data-stu-id="96caf-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Solution Explorer](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="96caf-194">加入 hello VoteDataController.cs 檔案</span><span class="sxs-lookup"><span data-stu-id="96caf-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="96caf-195">在 hello **VotingData**專案上的按一下滑鼠右鍵在 hello**控制站**資料夾，然後選取**新增-> 新增項目類別->** 。</span><span class="sxs-lookup"><span data-stu-id="96caf-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="96caf-196">將 hello 檔案 」 VoteDataController.cs"，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="96caf-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="96caf-197">Hello 檔案內容取代 hello 下列項目，然後儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="96caf-197">Replace hello file contents with hello following, then save your changes.</span></span>

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


## <a name="connect-hello-services"></a><span data-ttu-id="96caf-198">Hello 服務連接</span><span class="sxs-lookup"><span data-stu-id="96caf-198">Connect hello services</span></span>
<span data-ttu-id="96caf-199">在下一個步驟中，我們將連接 hello 兩個服務，然後讓 hello 前端 Web 應用程式取得和設定投票從 hello 後端服務的資訊。</span><span class="sxs-lookup"><span data-stu-id="96caf-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="96caf-200">對於您與可靠服務通訊的方式，Service Fabric 會提供完整的彈性。</span><span class="sxs-lookup"><span data-stu-id="96caf-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="96caf-201">在單一應用程式中，您可能有可透過 TCP 存取的服務。</span><span class="sxs-lookup"><span data-stu-id="96caf-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="96caf-202">可透過 HTTP 的 REST API 存取的其他服務以及其他任何服務可以透過 Web 通訊端存取。</span><span class="sxs-lookup"><span data-stu-id="96caf-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="96caf-203">如需有關可用的 hello 選項以及 hello 權衡取捨的背景，請參閱[與服務通訊](service-fabric-connect-and-communicate-with-services.md)。</span><span class="sxs-lookup"><span data-stu-id="96caf-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="96caf-204">在本教學課程中，我們會使用 [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md)。</span><span class="sxs-lookup"><span data-stu-id="96caf-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="96caf-205">更新 hello VotesController.cs 檔案</span><span class="sxs-lookup"><span data-stu-id="96caf-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="96caf-206">在 hello **VotingWeb**專案、 開啟 hello *Controllers/VotesController.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="96caf-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="96caf-207">取代 hello`VotesController`類別定義的內容，與 hello 下列項目，然後儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="96caf-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

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

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="96caf-208">逐步解說 hello 投票範例應用程式</span><span class="sxs-lookup"><span data-stu-id="96caf-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="96caf-209">hello 投票應用程式是由兩個服務所組成：</span><span class="sxs-lookup"><span data-stu-id="96caf-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="96caf-210">Web 前端服務 (VotingWeb)-ASP.NET Core web 前端服務，會做 hello 網頁，並公開 web Api toocommunicate 與 hello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="96caf-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="96caf-211">後端服務 (VotingData)-ASP.NET Core web 服務會公開 API toostore hello 投票結果可靠的字典中保存在磁碟。</span><span class="sxs-lookup"><span data-stu-id="96caf-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![應用程式圖表](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="96caf-213">當您在下列的 hello 應用程式 hello 投票事件就會發生：</span><span class="sxs-lookup"><span data-stu-id="96caf-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="96caf-214">JavaScript 會以 HTTP PUT 要求傳送 hello web 前端服務中的 hello 投票要求 toohello web API。</span><span class="sxs-lookup"><span data-stu-id="96caf-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="96caf-215">hello web 前端服務會使用 proxy toolocate 及轉送 HTTP PUT 要求 toohello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="96caf-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="96caf-216">hello 後端服務大約需要 hello 傳入的要求，並儲存區 hello 更新在可靠字典中，取得複寫的 toomultiple hello 叢集中的節點，並保存在磁碟上的結果。</span><span class="sxs-lookup"><span data-stu-id="96caf-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="96caf-217">所有 hello 應用程式的資料儲存在 hello 叢集中，因此不需要任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="96caf-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="96caf-218">在 Visual Studio 中偵錯</span><span class="sxs-lookup"><span data-stu-id="96caf-218">Debug in Visual Studio</span></span>
<span data-ttu-id="96caf-219">在 Visual Studio 中偵錯應用程式時，您會使用本機 Service Fabric 開發叢集。</span><span class="sxs-lookup"><span data-stu-id="96caf-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="96caf-220">您擁有 hello 選項 tooadjust 您偵錯的體驗 tooyour 案例。</span><span class="sxs-lookup"><span data-stu-id="96caf-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="96caf-221">在此應用程式中，我們將資料儲存在使用可靠字典的後端服務中。</span><span class="sxs-lookup"><span data-stu-id="96caf-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="96caf-222">Visual Studio 移除 hello 應用程式，根據預設，當您停止 hello 偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="96caf-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="96caf-223">移除 hello 應用程式造成 hello 資料在 hello 後端服務 tooalso 被移除。</span><span class="sxs-lookup"><span data-stu-id="96caf-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="96caf-224">toopersist hello 偵錯工作階段之間的資料，您可以變更 hello**應用程式偵錯模式**為 hello 屬性**投票**Visual Studio 專案中的。</span><span class="sxs-lookup"><span data-stu-id="96caf-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="96caf-225">在發生的事 hello 程式碼中，完成下列步驟的 hello toolook:</span><span class="sxs-lookup"><span data-stu-id="96caf-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="96caf-226">開啟 hello **VotesController.cs**檔案，並設定中斷點，在 hello web API 的**放**方法 （列 47）-您可以搜尋 hello Visual Studio 中的 [方案總管] 中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="96caf-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="96caf-227">開啟 hello **VoteDataController.cs**檔案，並設定中斷點，在這個 web API**放**方法 （行 50）。</span><span class="sxs-lookup"><span data-stu-id="96caf-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="96caf-228">返回 toohello 瀏覽器後，請按一下投票選項或加入新的投票選項。</span><span class="sxs-lookup"><span data-stu-id="96caf-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="96caf-229">您已達到 hello hello web 前端端的 api 控制器中的第一個中斷點。</span><span class="sxs-lookup"><span data-stu-id="96caf-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="96caf-230">這是其中 hello 瀏覽器中的 hello JavaScript 要求 toohello web API 控制器會以傳送 hello 前端服務。</span><span class="sxs-lookup"><span data-stu-id="96caf-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![新增投票前端服務](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="96caf-232">我們第一次針對我們的後端服務建構 hello URL toohello ReverseProxy **(1)**。</span><span class="sxs-lookup"><span data-stu-id="96caf-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="96caf-233">接著，我們將傳送嗨 HTTP PUT 要求 toohello ReverseProxy **(2)**。</span><span class="sxs-lookup"><span data-stu-id="96caf-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="96caf-234">最後 hello 我們決定傳回 hello 回應 hello 後端服務 toohello 用戶端從**(3)**。</span><span class="sxs-lookup"><span data-stu-id="96caf-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="96caf-235">按**F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="96caf-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="96caf-236">現在您已位於 hello 中斷點 hello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="96caf-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![新增投票後端服務](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="96caf-238">Hello hello 方法中的第一行**(1)**我們使用 hello `StateManager` tooget 或可靠的字典，稱為`counts`。</span><span class="sxs-lookup"><span data-stu-id="96caf-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="96caf-239">與可靠字典中的值進行的所有互動，都需要交易，這會使用陳述式 **(2)** 建立該交易。</span><span class="sxs-lookup"><span data-stu-id="96caf-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="96caf-240">在 hello 交易中，我們再更新 hello hello hello 投票選項的相關索引鍵的值，而且認可 hello 作業**(3)**。</span><span class="sxs-lookup"><span data-stu-id="96caf-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="96caf-241">一旦認可 hello 方法傳回時，hello 資料更新 hello 字典中，然後複寫 tooother hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="96caf-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="96caf-242">hello 現在會安全地儲存資料 hello 叢集中，hello 後端服務可以容錯移轉 tooother 節點，仍有可用的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="96caf-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="96caf-243">按**F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="96caf-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="96caf-244">偵錯工作階段，請按 toostop hello **Shift + F5**。</span><span class="sxs-lookup"><span data-stu-id="96caf-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="96caf-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96caf-245">Next steps</span></span>
<span data-ttu-id="96caf-246">在這個部分 hello 教學課程中，您學會如何：</span><span class="sxs-lookup"><span data-stu-id="96caf-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="96caf-247">建立 ASP.NET Core Web API 服務成為具狀態可靠服務</span><span class="sxs-lookup"><span data-stu-id="96caf-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="96caf-248">建立 ASP.NET Core Web 應用程式服務成為具狀態可靠服務</span><span class="sxs-lookup"><span data-stu-id="96caf-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="96caf-249">使用 hello 反向 proxy toocommunicate 與 hello 可設定狀態服務</span><span class="sxs-lookup"><span data-stu-id="96caf-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="96caf-250">進階 toohello 下一個教學課程：</span><span class="sxs-lookup"><span data-stu-id="96caf-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="96caf-251">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="96caf-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
