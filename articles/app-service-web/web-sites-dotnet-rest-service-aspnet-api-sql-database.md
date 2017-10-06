---
title: "aaaCreate REST API 在 Azure 中使用 ASP.NET 和 SQL DB |Microsoft 文件"
description: "教學課程，教導您 toodeploy 使用的應用程式如何使用 Visual Studio hello ASP.NET Web API tooan Azure web 應用程式。"
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>在 Azure App Service 中使用 ASP.NET Web API 和 SQL Database 建立 REST 服務
本教學課程示範如何 toodeploy ASP.NET web 應用程式 tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)使用 hello 發行網站精靈，在 Visual Studio 2013 或 Visual Studio 2013 Community 版本。 

您可以免費，開啟 Azure 帳戶和 hello SDK 如果您還沒有 Visual Studio 2013，自動安裝適用於 Web Express Visual Studio 2013。 如此您就能開始免費進行 Azure 相關開發。

本教學課程假設您先前沒有使用 Azure 的經驗。 完成本教學課程，您必須設定簡單的 web 應用程式和 hello 雲端中執行。

您將了解：

* 如何 tooenable 電腦所安裝的 Azure 開發 hello Azure SDK。
* 如何 toocreate Visual Studio ASP.NET MVC 5 專案，並將它發行 tooan Azure 應用程式。
* 如何 toouse hello ASP.NET Web API tooenable Restful API 呼叫。
* 如何 toouse SQL 資料庫 toostore Azure 中的資料。
* Toopublish 應用程式更新 tooAzure 的方式。

您將建置簡單的連絡人清單 web 應用程式建置在 ASP.NET MVC 5 並使用 hello ADO.NET Entity Framework 來存取資料庫。 下列圖例顯示 hello hello 完成應用程式：

![網站的螢幕擷取畫面][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>建立 hello 專案
1. 啟動 Visual Studio 2013。
2. 從 hello**檔案**功能表上，按一下**新專案**。
3. 在 hello**新專案**對話方塊方塊中，展開  **Visual C#**選取**Web** ，然後選取  **ASP.NET Web 應用程式**。 Hello 應用程式命名**ContactManager**按一下**確定**。
   
    ![New Project dialog box](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. 在 hello**新增 ASP.NET 專案**對話方塊中，選取 hello **MVC**範本中，核取**Web API** ，然後按一下**變更驗證**。
5. 在 hello**變更驗證**對話方塊中，按一下**非驗證**，然後按一下**確定**。
   
    ![不需要驗證](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    您要建立 hello 範例應用程式將不會有需要使用者 toolog 中的功能。 如需有關資訊 tooimplement 驗證和授權功能，請參閱 hello[接下來的步驟](#nextsteps)在本教學課程中的 hello 結尾區段。 
6. 在 hello**新增 ASP.NET 專案**對話方塊中，請確定 hello **hello 雲端中的主機**已選取，然後按一下**確定**。

如果您不先簽署 tooAzure 中，您將會提示的 toosign 中。

1. hello 組態精靈將會建議唯一的名稱，根據*ContactManager* （請參閱下面的 hello 影像）。 選取您附近的區域。 您可以使用[azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello 最低延遲的資料中心。 
2. 如果您之前尚未建立資料庫伺服器，請選取 [建立新的伺服器] ，並輸入資料庫使用者名稱和密碼。
   
    ![設定 Azure 網站](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

如果您有資料庫伺服器時，使用該 toocreate 新的資料庫。 資料庫伺服器是非常寶貴的資源，而您通常想 toocreate hello 上的多個資料庫來進行測試和開發而建立的每個資料庫的資料庫伺服器的同一部伺服器。 請確定您的網站和資料庫位於 hello 相同的區域。

![設定 Azure 網站](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>設定 hello 頁首和頁尾
1. 在**方案總管] 中**，依序展開 [hello *_layout.cshtml*資料夾，然後開啟 hello *_Layout.cshtml*檔案。
   
    ![方案總管中的 _Layout.cshtml][newapp004]
2. 取代 hello hello 內容*Views\Shared_Layout.cshtml*檔案以下列程式碼的 hello:

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

hello 標記上方 hello 應用程式將名稱變更從 「 我的 ASP.NET 應用程式 」 太"連絡人管理員 」，並移除 hello 連結太**首頁**，**有關**和**連絡人**。

### <a name="run-hello-application-locally"></a>在本機執行 hello 應用程式
1. 按 CTRL + F5 toorun hello 應用程式。
   hello 應用程式的首頁上會出現在 hello 預設瀏覽器。
    ![tooDo 清單首頁](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

這是您只需要 toodo 現在 toocreate hello 應用程式會將部署 tooAzure。 稍後您將新增資料庫功能。

## <a name="deploy-hello-application-tooazure"></a>部署 hello 應用程式 tooAzure
1. 在 Visual Studio 中，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**選取**發行**hello 操作功能表中。
   
    ![專案內容功能表中的 [發行]][PublishVSSolution]
   
    hello**發行 Web**精靈 隨即開啟。
2. 按一下 [發行] 。

![[設定] 索引標籤](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio 開始複製 hello 檔案 toohello Azure 伺服器 hello 程序。 hello**輸出**視窗會顯示所執行的部署動作，並報告 hello 部署成功完成。

1. hello 預設瀏覽器會自動開啟 toohello 部署的 hello 網站 URL。
   
   您建立的 hello 應用程式現在正在 hello 雲端中執行。
   
   ![在 Azure 中執行將 tooDo 清單首頁][rxz2]

## <a name="add-a-database-toohello-application"></a>新增資料庫 toohello 應用程式
接下來，您將更新 hello MVC 應用程式 tooadd hello 能力 toodisplay 和更新連絡人並儲存在資料庫中的 hello 資料。 hello 應用程式會使用 hello Entity Framework toocreate hello 資料庫和 tooread，並更新 hello 資料庫中的資料。

### <a name="add-data-model-classes-for-hello-contacts"></a>新增 hello 連絡人的資料模型類別
首先，您會在程式碼中建立簡單的資料模型。

1. 在**方案總管 中**hello Models 資料夾上按一下滑鼠右鍵、 按一下**新增**，然後**類別**。
   
    ![在 Models 資料夾內容功能表中新增類別][adddb001]
2. 在 hello**加入新項目**對話方塊中，名稱 hello 新的類別檔案*Contact.cs*，然後按一下**新增**。
   
    ![[加入新項目] 對話方塊][adddb002]
3. 取代下列程式碼的 hello hello hello Contacts.cs 檔案內容。
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

hello**連絡**類別定義儲存每個連絡人，再加上主索引鍵，ContactID hello 資料庫所需的 hello 資料。 您可以取得有關資料模型的詳細資訊，在 hello[接下來的步驟](#nextsteps)在本教學課程中的 hello 結尾區段。

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>建立網頁可讓應用程式使用者 toowork 與 hello 連絡人
hello ASP.NET MVC hello scaffolding 功能可以自動產生程式碼會執行建立、 讀取、 更新和刪除 (CRUD) 動作。

## <a name="add-a-controller-and-a-view-for-hello-data"></a>加入控制器與 hello 資料檢視
1. 在**方案總管 中**，依序展開 hello Controllers 資料夾中。
2. 建置專案 hello **(Ctrl + Shift + B)**。 （您必須建置 hello 專案之前使用 scaffolding 機制）。 
3. Hello 控制器 資料夾上按一下滑鼠右鍵，然後按一下**新增**，然後按一下**控制器**。
   
    ![在 Controllers 資料夾內容功能表中新增控制器][addcode001]
4. 在 hello**加入 Scaffold**對話方塊中，選取**使用 Entity Framework 的檢視，MVC 控制器**按一下**新增**。
   
   ![新增控制器](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. 設定 hello 控制器名稱太**HomeController**。 選取 [Contact]  模型類別。 按一下 hello**新的資料內容**按鈕，然後接受 hello 預設"ContactManager.Models.ContactManagerContext"hello**新資料內容型別**。 按一下 [新增] 。

    對話方塊會提示您:"hello 名稱的檔案 HomeController 已經結束。 您想 tooreplace 它嗎？ 」。 按一下 [是] 。 我們會覆寫 hello 首頁建立 hello 新專案中的控制站。 我們將使用 hello 新主控制器的連絡人清單。

    Visual Studio 隨即針對 **Contact** 物件的 CRUD 資料庫操作，建立控制器方法與檢視。

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>啟用移轉，建立 hello 資料庫、 加入範例資料和資料的初始設定式
hello 下一個工作是 tooenable hello [Code First 移轉](http://curah.microsoft.com/55220)順序 toocreate hello 資料庫中的功能會根據您所建立的 hello 資料模型。

1. 在 hello**工具**功能表上，選取**程式庫套件管理員**然後**Package Manager Console**。
   
    ![[工具] 功能表中的 Package Manager Console][addcode008]
2. 在 hello **Package Manager Console**視窗中，輸入下列命令的 hello:
   
        enable-migrations 
   
    hello**啟用移轉**命令會建立*移轉*資料夾，然後將該資料夾中*configuration.cs 中*您可以編輯 tooconfigure 移轉的檔案。 
3. 在 hello **Package Manager Console**視窗中，輸入下列命令的 hello:
   
        add-migration Initial
   
    hello**新增移轉初始**命令會產生類別，名為 **&lt;date_stamp&gt;初始**會建立 hello 資料庫。 hello 第一個參數 (*初始*) 是任意和已使用 toocreate hello hello 檔案名稱。 您可以看到 hello 新類別檔案中的**方案總管 中**。
   
    在 [hello**初始**類別，hello**向上**方法會建立 hello 連絡人] 資料表和 hello**向下**（當您想要讓 tooreturn toohello 先前狀態時使用） 的方法會卸除它。
4. 開啟 hello *Migrations\Configuration.cs*檔案。 
5. 新增下列命名空間的 hello。 
   
         using ContactManager.Models;
6. 取代 hello*種子*方法，以下列程式碼的 hello:
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    上述這段程式碼將會初始化 hello 與 hello 連絡資訊的資料庫。 如需有關植入 hello 資料庫的詳細資訊，請參閱[偵錯 Entity Framework (EF) 資料庫使用](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)。
7. 在 hello **Package Manager Console**輸入 hello 命令：
   
        update-database
   
    ![Package Manager Console commands][addcode009]
   
    hello**更新資料庫**執行 hello 第一次移轉會建立 hello 資料庫。 根據預設，會建立 hello 資料庫做為 SQL Server Express LocalDB 資料庫。
8. 按 CTRL + F5 toorun hello 應用程式。 

hello 應用程式顯示 hello 種子資料，並提供編輯詳細資料以及刪除連結。

![資料的 MVC 檢視][rxz3]

## <a name="edit-hello-view"></a>編輯 hello 檢視
1. 開啟 hello *Views\Home\Index.cshtml*檔案。 在 hello 下一個步驟中，我們將使用的程式碼以取代 hello 產生標記[jQuery](http://jquery.com/)和[解 Knockout.js](http://knockoutjs.com/)。 這個新的程式碼會從使用 web 應用程式開發介面擷取 hello 的連絡人清單和 JSON，然後繫結 hello 連絡資料 toohello UI 使用解 knockout.js。 如需詳細資訊，請參閱 hello[接下來的步驟](#nextsteps)在本教學課程中的 hello 結尾區段。 
2. 取代下列程式碼的 hello hello hello 檔案內容。
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. Hello 內容的資料夾上按一下滑鼠右鍵，然後按一下**新增**，然後按一下**新項目...**.
   
    ![Content 資料夾內容功能表中的 [加入樣式表]][addcode005]
4. 在 hello**加入新項目**對話方塊方塊中，輸入**樣式**在 hello 上方右邊的搜尋方塊，然後選取 **樣式表**。
    ![[加入新項目] 對話方塊][rxStyle]
5. 名稱 hello 檔*Contacts.css*按一下**新增**。 取代下列程式碼的 hello hello hello 檔案內容。
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    我們將使用這個樣式表 hello 版面配置、 色彩和樣式 hello 連絡人管理員應用程式中使用。
6. 開啟 hello *App_Start\BundleConfig.cs*檔案。
7. 新增下列程式碼 tooregister hello hello [Knockout](http://knockoutjs.com/index.html "僅限 KO")外掛程式。
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    這個範例使用 knockout toosimplify 動態 JavaScript 程式碼會處理 hello 螢幕範本。
8. 修改 hello 內容/css 項目 tooregister hello *contacts.css*樣式表。 變更下列行 hello:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   變更為：
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. 在 hello Package Manager Console 中，執行下列命令 tooinstall Knockout hello。
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>新增 hello Web API Restful 介面的控制站
1. 在 [方案總管]，於 Controllers 上按一下滑鼠右鍵，按一下 [新增]，再按一下 [控制器...] 
2. 在 hello**新增 Scaffold**對話方塊方塊中，輸入**Web API 2 控制器動作，使用 Entity Framework** ，然後按一下**新增**。
   
    ![新增 API 控制器](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. 在 hello**加入控制器**對話方塊方塊中，輸入 「 ContactsController"做為控制器名稱。 選取"Contact (ContactManager.Models)"hello**模型類別**。  保留 hello 預設值為 hello**資料內容類別**。 
4. 按一下 [新增] 。

### <a name="run-hello-application-locally"></a>在本機執行 hello 應用程式
1. 按 CTRL + F5 toorun hello 應用程式。
   
    ![索引頁面][intro001]
2. 輸入連絡人，然後按一下 [新增] 。 hello 應用程式傳回 toohello 首頁上，並顯示您輸入的 hello 連絡人。
   
    ![含有待辦事項清單的索引頁面][addwebapi004]
3. 在 hello 瀏覽器附加**/api/連絡人**toohello URL。
   
    hello 產生的 URL 會類似 http://localhost:1234/api/連絡人。 hello RESTful web API 新增傳回 hello 儲存連絡人。 Firefox 和 Chrome 會顯示 hello 資料以 XML 格式。
   
    ![含有待辦事項清單的索引頁面][rxFFchrome]

    將會提示您 tooopen IE，或儲存 hello 連絡人。

    ![Web API 儲存對話方塊][addwebapi006]


    您可以開啟 [記事本] 或瀏覽器中傳回的連絡人 hello。

    行動網頁或應用程式之類的其他應用程式亦可取用此輸出。

    ![Web API 儲存對話方塊][addwebapi007]

    **安全性警告**： 此時，您的應用程式是不安全且易於遭受 tooCSRF 攻擊。 稍後在 hello 教學課程中我們將會移除這項弱點。 如需詳細資訊，請參閱[避免跨網站偽造要求 (CSRF) 攻擊][prevent-csrf-attacks]。
## <a name="add-xsrf-protection"></a>新增 XSRF 保護
跨站台要求偽造 （也稱為 XSRF 或 CSRF） 是對 web 裝載的應用程式讓惡意網站可能會影響用戶端瀏覽器和瀏覽器的受信任的網站之間的 hello 互動的攻擊。 因為網頁瀏覽器會傳送驗證 token，與每個要求 tooa 網站會自動進行這些攻擊可能。 hello 標準範例是驗證 cookie，例如 ASP。網路的表單驗證票證。 然而，使用任何持續驗證機制 (如 Windows 驗證、基本驗證等等) 的網站都可能成為這些攻擊的目標。

XSRF 攻擊與網路釣魚攻擊不同。 網路釣魚攻擊需要互動，舉凡 hello 犧牲者。 在詐騙攻擊中，惡意網站會模仿 hello 目標網站，並提供機密資訊 toohello 攻擊者到騙 hello 犧牲者，是。 在 XSRF 攻擊中，通常會沒有互動所需從 hello 犧牲者。 相反地，hello 攻擊者依賴 hello 瀏覽器會自動傳送所有相關的 cookie toohello 目的地網站。

如需詳細資訊，請參閱 hello[開啟 Web 應用程式安全性專案](https://www.owasp.org/index.php/Main_Page)(OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\))。

1. 在 [方案總管] 中，於 **ContactManager** 專案上按一下滑鼠右鍵，按一下 [新增]，再按一下 [類別]。
2. 名稱 hello 檔*ValidateHttpAntiForgeryTokenAttribute.cs*並加入下列程式碼的 hello:
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. 新增下列 hello*使用*陳述式 toohello 合約控制器，因此您需要存取 toohello **[ValidateHttpAntiForgeryToken]**屬性。
   
        using ContactManager.Filters;
4. 新增 hello **[ValidateHttpAntiForgeryToken]**屬性 toohello Post 方法的 hello **ContactsController** tooprotect 從 XSRF 威脅。 您會將它加入 toohello"PutContact"，"PostContact 」 和**DeleteContact**動作方法。
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. 更新 hello*指令碼*區段 hello *Views\Home\Index.cshtml*檔案 tooinclude 程式碼 tooget hello XSRF 權杖。
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>發行 hello 應用程式更新 tooAzure 和 SQL Database
toopublish hello 應用程式，您可以重複 hello 您稍早遵循的程序。

1. 在**方案總管 中**，以滑鼠右鍵按一下 hello 專案並選取**發行**。
   
    ![發佈][rxP]
2. 按一下 hello**設定** 索引標籤。
3. 在下**ContactsManagerContext(ContactsManagerContext)**，按一下 hello **v**圖示 toochange*遠端的連接字串*toohello hello 連絡人的連接字串資料庫。 按一下 [ContactDB] 。
   
    ![設定](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. 核取方塊 hello**執行 Code First 移轉 （在應用程式啟動時執行）**。
5. 依序按 [下一步] 和 [預覽]。 Visual Studio 會顯示 hello 檔案會加入或更新的清單。
6. 按一下 [發行] 。
   Hello 部署完成之後，hello 瀏覽器會開啟 toohello hello 應用程式的首頁。
   
    ![Index page with no contacts][intro001]
   
    hello Visual Studio 發行處理程序會自動設定 hello 連接字串中部署的 hello *Web.config*檔案 toopoint toohello SQL 資料庫。 它也會設定 Code First 移轉 tooautomatically 升級 hello 資料庫 toohello 最新版本 hello 第一個時間 hello 應用程式部署後存取 hello 資料庫。
   
    由於這個設定，Code First 建立 hello 資料庫執行 hello 程式碼中 hello**初始**您稍早建立的類別。 這個 hello 第一個階段 hello 應用程式嘗試 tooaccess hello 資料庫成功部署之後。
7. 如同執行 hello 應用程式在本機，已成功將資料庫部署的 tooverify 時，請輸入連絡人。

當您看到您輸入該 hello 項目儲存，而且會出現在 hello 連絡人的管理員 頁面上時，您知道它已在 hello 資料庫中已儲存。

![含有連絡人的索引頁面][addwebapi004]

hello 應用程式現在正在 hello 雲端中使用 SQL Database toostore 其資料。 在 Azure 中測試 hello 應用程式完成之後，請將其刪除。 hello 應用程式時為公用，且沒有機制 toolimit 存取權限。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="next-steps"></a>後續步驟
Azure 應用程式中的另一個方式 toostore 資料是 toouse 提供 hello 格式的 blob 和資料表的非關聯式資料儲存體的 Azure 儲存體。 下列連結查看 hello 提供 Web API、 ASP.NET MVC 和 Windows Azure 的詳細資訊。

* [使用 MVC 的 Entity Framework 入門][EFCodeFirstMVCTutorial]
* [簡介 tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [您的第一個 ASP.NET Web API](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [偵錯 WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

此教學課程和 hello 範例應用程式由寫入[Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) Tom Dykstra 和 Barry Dorrans 的協助 (Twitter [ @blowdart](https://twitter.com/blowdart)). 

請留下您喜歡的功能，或您想獲得改善，關於本身 hello 教學課程不僅 hello 的產品，它會示範 toosee 上的意見反應。 您的意見反應將協助我們訂出優先改善要務。 我們會特別有興趣了解更多自動化 hello 程序的設定和部署 hello 成員資格資料庫中已有多少感興趣。 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

