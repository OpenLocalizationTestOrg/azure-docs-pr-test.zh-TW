---
title: "aaaCreate 連接 tooMongoDB 虛擬機器上執行的 Azure 中的 web 應用程式"
description: "教學課程，教導您如何 toouse Git toodeploy 應用程式服務的 ASP.NET 應用程式 tooAzure 連接 tooMongoDB Azure 虛擬機器上。"
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: 1f5f42c28c3c294d92c9ebf1499374931d47c010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a>在連接 tooMongoDB 虛擬機器上執行的 Azure 中建立 web 應用程式
使用 Git，您可以部署 ASP.NET 應用程式 tooAzure App Service Web 應用程式。 在本教學課程中，您將建立簡單的前端的 ASP.NET MVC 連接 tooa MongoDB 資料庫在 Azure 中的虛擬機器上執行的工作清單應用程式。  [MongoDB][MongoDB] 是熱門的高效能開放原始碼 NoSQL 資料庫。 執行和測試您的開發電腦上的 hello ASP.NET 應用程式之後, 您將上傳 hello 應用程式 tooApp Service Web 應用程式使用 Git。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="background-knowledge"></a>背景知識
本教學課程，但是不需要的 hello 下列知識很有用的：

* MongoDB hello C# 驅動程式。 如需有關開發針對 MongoDB 的 C# 應用程式的詳細資訊，請參閱 hello MongoDB [CSharp 語言 Center][MongoC#LangCenter]。 
* hello ASP.NET web 應用程式架構。 您可以了解在 hello [ASP.net 網站][ASP.NET]。
* hello ASP.NET MVC web 應用程式架構。 您可以了解在 hello [ASP.NET MVC 網站][MVCWebSite]。
* Azure。 您可以在 [Azure][WindowsAzure] 開始閱讀。

## <a name="prerequisites"></a>必要條件
* [Visual Studio Express 2013 for Web][VSEWeb] 或 [Visual Studio 2013][VSUlt]
* [Azure SDK for .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* 使用中的 Microsoft Azure 訂用帳戶

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>建立虛擬機器和安裝 MongoDB
本教學課程假設您已在 Azure 中建立虛擬機器。 建立 hello 虛擬機器之後，您需要 tooinstall MongoDB hello 虛擬機器上：

* toocreate Windows 虛擬機器並安裝 MongoDB，請參閱[在 Azure 中執行 Windows Server 的虛擬機器上安裝的 MongoDB][InstallMongoOnWindowsVM]。

您已在 Azure 中建立 hello 虛擬機器並安裝 MongoDB 之後，是確定 tooremember hello DNS 名稱 hello 虛擬機器 ("testlinuxvm.cloudapp.net"，例如) 和 hello 外部連接埠的 for MongoDB。 您在 hello 端點中指定。  您必須稍後在 hello 教學課程的這項資訊。

<a id="createapp"></a>

## <a name="create-hello-application"></a>建立 hello 應用程式
本節中您會建立稱為 「 我的工作清單 」 使用 Visual Studio 的 ASP.NET 應用程式，並執行初始部署 tooAzure App Service Web 應用程式。 您將在本機執行 hello 應用程式，但是將 tooyour 在 Azure 上的虛擬機器連線，並使用您所建立的 hello MongoDB 執行個體。

1. 在 Visual Studio 中按一下 [新增專案] 。
   
    ![Start Page New Project][StartPageNewProject]
2. 在 hello**新專案**視窗中的，hello 左窗格中，選取**Visual C#**，然後選取**Web**。 在 [hello] 中間窗格中，選取**ASP.NET Web 應用程式**。 底部 hello，"MyTaskListApp 」，您專案的名稱，然後按一下**確定**。
   
    ![New Project Dialog][NewProjectMyTaskListApp]
3. 在 hello**新增 ASP.NET 專案**對話方塊中，選取**MVC**，然後按一下**確定**。
   
    ![Select MVC Template][VS2013SelectMVCTemplate]
4. 如果您尚未登入 Microsoft Azure，您將會提示的 toosign 中。 遵循 hello 提示 toosign 至 Azure。
5. 當您登入之後，即可開始設定您的 App Service Web 應用程式。 指定 hello **Web 應用程式名稱**， **App Service 方案**，**資源群組**，和**區域**，然後按一下 **建立**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Hello 專案建立完成之後，等待 hello hello 所示，在 Azure App Service 中建立的 web 應用程式 toobe **Azure 應用程式服務活動**視窗。 然後，按一下 **發行 MyTaskListApp toothis Web 應用程式現在**。
7. 按一下 [發行] 。
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    一旦您預設的 ASP.NET 應用程式發行的 tooAzure App Service Web 應用程式，它就會啟動 hello 瀏覽器中。

## <a name="install-hello-mongodb-c-driver"></a>安裝 hello C# MongoDB 驅動程式
MongoDB 提供 C# 應用程式透過您所需要的驅動程式的用戶端支援 tooinstall 本機開發電腦上的。 hello C# 驅動程式會透過 NuGet 提供。

tooinstall hello C# MongoDB 驅動程式：

1. 在**方案總管 中**，以滑鼠右鍵按一下 hello **MyTaskListApp**專案，然後選取**管理 NuGetPackages**。
   
    ![Manage NuGet Packages][VS2013ManageNuGetPackages]
2. 在 hello**管理 NuGet 封裝**視窗 hello 左窗格中，按一下**線上**。 在 hello**線上搜尋**上 hello 右邊方塊中，輸入 「 mongodb.driver"。  按一下**安裝**tooinstall hello 驅動程式。
   
    ![Search for MongoDB C# Driver][SearchforMongoDBCSharpDriver]
3. 按一下**我接受**tooaccept hello 10gen，Inc.授權條款。
4. 按一下**關閉**hello 驅動程式安裝之後。
    ![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]

hello C# MongoDB 驅動程式現在已安裝。  參考 toohello **MongoDB.Bson**， **MongoDB.Driver**，和**MongoDB.Driver.Core**已加入文件庫 toohello 專案。

![MongoDB C# Driver References][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>新增模型
在**方案總管 中**，以滑鼠右鍵按一下 hello*模型*資料夾和**新增**新**類別**並將其命名*TaskModel.cs*.  在*TaskModel.cs*，hello 現有程式碼取代為下列程式碼的 hello:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-hello-data-access-layer"></a>新增 hello 資料存取層
在**方案總管 中**，以滑鼠右鍵按一下 hello *MyTaskListApp*專案和**新增****新資料夾**名為*DAL*.  以滑鼠右鍵按一下 hello *DAL*資料夾和**新增**新**類別**。 名稱 hello 類別檔*Dal.cs*。  在*Dal.cs*，hello 現有程式碼取代為下列程式碼的 hello:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }

            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }

            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            # region IDisposable

            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a>新增控制器
開啟 hello *Controllers\HomeController.cs*檔案**方案總管 中**並 hello 現有程式碼取代 hello 下列：

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-hello-styles"></a>設定 hello 樣式
toochange hello 標題上方的 hello 頁面上，開啟 hello hello *_layout.cshtml\\_Layout.cshtml*檔案**方案總管 中**hello 導覽列的標頭中的"Application name"取代"My 工作列出應用程式 」，讓它看起來像這樣：

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

在訂單 tooset hello 工作清單] 功能表上，開啟 [hello *\Views\Home\Index.cshtml*檔案，然後以下列程式碼的 hello 取代 hello 現有程式碼：

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


tooadd hello 能力 toocreate 新的工作，以滑鼠右鍵按一下 hello *Views\Home\\* 資料夾和**新增****檢視**。  命名 hello 檢視*建立*。 Hello 程式碼取代 hello 下列：

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

**Controllers\HomeController.cs** 看起來如下所示：

![Solution Explorer][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a>設定 hello MongoDB 連接字串
在**方案總管 中**，開啟 hello *DAL/Dal.cs*檔案。 尋找下列程式碼行 hello:

    private string connectionString = "mongodb://<vm-dns-name>";

取代`<vm-dns-name>`hello hello 執行的 MongoDB hello 中建立的虛擬機器的 DNS 名稱[建立虛擬機器並安裝 MongoDB] [ Create a virtual machine and install MongoDB]本教學課程的步驟。  toofind hello DNS 名稱的虛擬機器，請移 toohello Azure 入口網站中，選取**虛擬機器**，並尋找**DNS 名稱**。

如果 hello hello 虛擬機器的 DNS 名稱是"testlinuxvm.cloudapp.net"MongoDB 接聽預設通訊埠 hello 27017，hello 連接字串的程式碼行看起來像：

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

如果 hello 虛擬機器端點指定不同的外部連接埠的 MongoDB，您可以指定 hello 連接字串中的 hello 連接埠：

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

如需 MongoDB 連接字串的詳細資訊，請參閱[連接][MongoConnectionStrings]。

## <a name="test-hello-local-deployment"></a>測試 hello 本機部署
toorun 您的開發電腦上的應用程式選取**開始偵錯**從 hello**偵錯**功能表或叫用**F5**。 IIS Express 會啟動並在瀏覽器會開啟，並啟動 hello 應用程式的首頁。  您可以加入新的工作，將會加入您在 Azure 中的虛擬機器上執行的 toohello MongoDB 資料庫。

![My Task List Application][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a>發行 tooAzure App Service Web 應用程式
在本節中，您將發行您的變更 tooAzure App Service Web 應用程式。

1. 在 [方案總管] 中，再次以滑鼠右鍵按一下 **MyTaskListApp**，然後按一下 [發佈]。
2. 按一下 [發行] 。
   
    您現在應該會看到您 web 應用程式，Azure App Service 中執行，而且存取 hello MongoDB 資料庫在 Azure 虛擬機器。

## <a name="summary"></a>摘要
您現在已成功部署您的 ASP.NET 應用程式 tooAzure App Service Web 應用程式。 tooview hello web 應用程式：

1. 登入 hello Azure 入口網站。
2. 按一下 [Web 應用程式] 。 
3. 選取您的 web 應用程式在 hello **Web 應用程式**清單。

如需針對 MongoDB 開發 C# 應用程式的詳細資訊，請參閱 [CSharp Language Center][MongoC#LangCenter]。 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: ./media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: ./media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp
