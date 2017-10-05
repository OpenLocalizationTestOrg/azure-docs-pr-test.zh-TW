---
title: "使用 ASP.NET 和 SQL DB 在 Azure 中建立 REST API | Microsoft Docs"
description: "指導如何使用 Visual Studio，將使用 ASP.NET Web API 的應用程式部署至 Azure Web 應用程式的教學課程。"
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
ms.openlocfilehash: 64c18f2cfabbb7af6ffd89b4c2a9095fca1cf799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="ecc8b-103">在 Azure App Service 中使用 ASP.NET Web API 和 SQL Database 建立 REST 服務</span><span class="sxs-lookup"><span data-stu-id="ecc8b-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="ecc8b-104">本教學課程示範如何使用 Visual Studio 2013 或 Visual Studio 2013 Community Edition 中的 [發佈 Web] 精靈，將 ASP.NET Web 應用程式部署至 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-104">This tutorial shows how to deploy an ASP.NET web app to an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using the Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="ecc8b-105">您可以免費申請 Azure 帳戶，而且如果您還沒有 Visual Studio 2013，SDK 會自動安裝 Visual Studio 2013 for Web Express。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, the SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="ecc8b-106">如此您就能開始免費進行 Azure 相關開發。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="ecc8b-107">本教學課程假設您先前沒有使用 Azure 的經驗。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="ecc8b-108">完成本教學課程後，您將有個簡單的 Web 應用程式已在雲端中啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-108">On completing this tutorial, you'll have a simple web app up and running in the cloud.</span></span>

<span data-ttu-id="ecc8b-109">您將了解：</span><span class="sxs-lookup"><span data-stu-id="ecc8b-109">You'll learn:</span></span>

* <span data-ttu-id="ecc8b-110">如何安裝 Azure SDK 好讓電腦適合用於進行 Azure 開發。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-110">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="ecc8b-111">如何建立 Visual Studio ASP.NET MVC 5 專案，並將它發行至 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-111">How to create a Visual Studio ASP.NET MVC 5 project and publish it to an Azure app.</span></span>
* <span data-ttu-id="ecc8b-112">如何使用 ASP.NET Web API 來啟用符合 REST 限制的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-112">How to use the ASP.NET Web API to enable Restful API calls.</span></span>
* <span data-ttu-id="ecc8b-113">如何使用 SQL 資料庫在 Azure 中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-113">How to use a SQL database to store data in Azure.</span></span>
* <span data-ttu-id="ecc8b-114">如何將應用程式更新發行至 Azure。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-114">How to publish application updates to Azure.</span></span>

<span data-ttu-id="ecc8b-115">您將建立一個簡單的連絡人清單 Web 應用程式，該應用程式建立於 ASP.NET MVC 5 之上，並使用 ADO.NET Entity Framework 進行資料庫存取。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses the ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="ecc8b-116">下圖顯示完成的應用程式：</span><span class="sxs-lookup"><span data-stu-id="ecc8b-116">The following illustration shows the completed application:</span></span>

![網站的螢幕擷取畫面][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a><span data-ttu-id="ecc8b-118">建立專案</span><span class="sxs-lookup"><span data-stu-id="ecc8b-118">Create the project</span></span>
1. <span data-ttu-id="ecc8b-119">啟動 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="ecc8b-120">從 [檔案] 功能表，按一下 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-120">From the **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="ecc8b-121">在 [新增專案] 對話方塊中，展開 [Visual C#] 並選取 [Web]，再選取 [ASP.NET Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-121">In the **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="ecc8b-122">將應用程式命名為 **ContactManager**，再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-122">Name the application **ContactManager** and click **OK**.</span></span>
   
    ![New Project dialog box](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="ecc8b-124">在 [New ASP.NET Project] 對話方塊中，選取 [MVC] 範本，勾選 [Web API]，再按一下 [變更驗證]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-124">In the **New ASP.NET Project** dialog box, select the **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="ecc8b-125">在 [變更驗證] 對話方塊中，按一下 [不需要驗證]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-125">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![不需要驗證](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="ecc8b-127">您要建立的範例應用程式將不會有需要使用者登入的功能。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-127">The sample application you're creating won't have features that require users to log in.</span></span> <span data-ttu-id="ecc8b-128">如需關於如何實作驗證與授權功能的詳細資訊，請參閱本教學課程最後的 [後續步驟](#nextsteps) 小節。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-128">For information about how to implement authentication and authorization features, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
6. <span data-ttu-id="ecc8b-129">在 [新增 ASP.NET 專案] 對話方塊中，請確定已勾選 [雲端中的主機]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-129">In the **New ASP.NET Project** dialog box, make sure the **Host in the Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="ecc8b-130">如果您先前未登入 Azure，系統將提示您登入。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-130">If you have not previously signed in to Azure, you will be prompted to sign in.</span></span>

1. <span data-ttu-id="ecc8b-131">[組態] 精靈會根據 *ContactManager* 建議唯一名稱 (請參閱下圖)。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-131">The configuration wizard will suggest a unique name based on *ContactManager* (see the image below).</span></span> <span data-ttu-id="ecc8b-132">選取您附近的區域。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-132">Select a region near you.</span></span> <span data-ttu-id="ecc8b-133">若要尋找最低延遲的資料中心，您可以使用 [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") to find the lowest latency data center.</span></span> 
2. <span data-ttu-id="ecc8b-134">如果您之前尚未建立資料庫伺服器，請選取 [建立新的伺服器] ，並輸入資料庫使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![設定 Azure 網站](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="ecc8b-136">如果您有資料庫伺服器，請用它來建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-136">If you have a database server, use that to create a new database.</span></span> <span data-ttu-id="ecc8b-137">資料庫伺服器是非常寶貴的資源，通常您會想要在相同伺服器上建立多個資料庫進行測試和開發，而非在每個資料庫上建立資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-137">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="ecc8b-138">請確定您的網站和資料庫位於相同的區域。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-138">Make sure your web site and database are in the same region.</span></span>

![設定 Azure 網站](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a><span data-ttu-id="ecc8b-140">設定頁首及頁尾</span><span class="sxs-lookup"><span data-stu-id="ecc8b-140">Set the page header and footer</span></span>
1. <span data-ttu-id="ecc8b-141">在 [方案總管] 中，展開 Views\Shared 資料夾，然後開啟 _Layout.cshtml 檔案。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-141">In **Solution Explorer**, expand the *Views\Shared* folder and open the *_Layout.cshtml* file.</span></span>
   
    ![方案總管中的 _Layout.cshtml][newapp004]
2. <span data-ttu-id="ecc8b-143">以下列程式碼取代 Views\Shared_Layout.cshtml 檔案中的內容：</span><span class="sxs-lookup"><span data-stu-id="ecc8b-143">Replace the contents of the *Views\Shared_Layout.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="ecc8b-144">以上的標記會將應用程式名稱從 "My ASP.NET App" 變更為 "Contact Manager"，同時也移除 **Home**、**About** 及 **Contact** 的連結。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-144">The markup above changes the app name from "My ASP.NET App" to "Contact Manager", and it removes the links to **Home**, **About** and **Contact**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="ecc8b-145">在本機執行應用程式</span><span class="sxs-lookup"><span data-stu-id="ecc8b-145">Run the application locally</span></span>
1. <span data-ttu-id="ecc8b-146">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-146">Press CTRL+F5 to run the application.</span></span>
   <span data-ttu-id="ecc8b-147">應用程式首頁隨即出現在預設瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-147">The application home page appears in the default browser.</span></span>
    <span data-ttu-id="ecc8b-148">![待辦事項清單首頁](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="ecc8b-148">![To Do List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="ecc8b-149">只需執行上述作業，即可建立稍後要部署至 Azure 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-149">This is all you need to do for now to create the application that you'll deploy to Azure.</span></span> <span data-ttu-id="ecc8b-150">稍後您將新增資料庫功能。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-150">Later you'll add database functionality.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="ecc8b-151">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="ecc8b-151">Deploy the application to Azure</span></span>
1. <span data-ttu-id="ecc8b-152">在 Visual Studio 的 [方案總管] 中以滑鼠右鍵按一下專案，再選取內容功能表中的 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-152">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    ![專案內容功能表中的 [發行]][PublishVSSolution]
   
    <span data-ttu-id="ecc8b-154">此時會開啟 [發行 Web]  精靈。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-154">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="ecc8b-155">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-155">Click **Publish**.</span></span>

![[設定] 索引標籤](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="ecc8b-157">Visual Studio 隨即開始進行將檔案複製至 Azure 伺服器的程序。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-157">Visual Studio begins the process of copying the files to the Azure server.</span></span> <span data-ttu-id="ecc8b-158">[輸出]  視窗會顯示已採取的部署動作，並報告部署作業已順利完成。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-158">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>

1. <span data-ttu-id="ecc8b-159">預設瀏覽器會自動開啟已部署之網站的 URL。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-159">The default browser automatically opens to the URL of the deployed site.</span></span>
   
   <span data-ttu-id="ecc8b-160">您建立的應用程式現在正在雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-160">The application you created is now running in the cloud.</span></span>
   
   ![在 Azure 中執行的待辦事項清單首頁][rxz2]

## <a name="add-a-database-to-the-application"></a><span data-ttu-id="ecc8b-162">新增資料庫至應用程式</span><span class="sxs-lookup"><span data-stu-id="ecc8b-162">Add a database to the application</span></span>
<span data-ttu-id="ecc8b-163">接下來，您將更新 MVC 應用程式，以加上顯示和更新資料庫中的連絡人，以及在資料庫中儲存資料的能力。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-163">Next, you'll update the MVC application to add the ability to display and update contacts and store the data in a database.</span></span> <span data-ttu-id="ecc8b-164">應用程式將使用 Entity Framework，以建立資料庫以及讀取和更新資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-164">The application will use the Entity Framework to create the database and to read and update data in the database.</span></span>

### <a name="add-data-model-classes-for-the-contacts"></a><span data-ttu-id="ecc8b-165">新增連絡人的資料模型類別</span><span class="sxs-lookup"><span data-stu-id="ecc8b-165">Add data model classes for the contacts</span></span>
<span data-ttu-id="ecc8b-166">首先，您會在程式碼中建立簡單的資料模型。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="ecc8b-167">在 [方案總管]，於 Models 資料夾上按一下滑鼠右鍵，按一下 [新增]，再按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-167">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span></span>
   
    ![在 Models 資料夾內容功能表中新增類別][adddb001]
2. <span data-ttu-id="ecc8b-169">在 [加入新項目] 對話方塊中，將新的類別檔案命名為 *Contact.cs*，再按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-169">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![[加入新項目] 對話方塊][adddb002]
3. <span data-ttu-id="ecc8b-171">以下列程式碼取代 Contacts.cs 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-171">Replace the contents of the Contacts.cs file with the following code.</span></span>
   
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

<span data-ttu-id="ecc8b-172">**Contact** 類別定義您將為每個連絡人儲存的資料，加上資料庫需要的主要索引鍵 ContactID。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-172">The **Contact** class defines the data that you will store for each contact, plus a primary key, ContactID, that is needed by the database.</span></span> <span data-ttu-id="ecc8b-173">您可以在本教學課程結尾處的 [後續步驟](#nextsteps) 一節取得資料模型的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-173">You can get more information about data models in the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a><span data-ttu-id="ecc8b-174">建立可讓應用程式使用者使用連絡人的網頁</span><span class="sxs-lookup"><span data-stu-id="ecc8b-174">Create web pages that enable app users to work with the contacts</span></span>
<span data-ttu-id="ecc8b-175">ASP.NET MVC 樣板功能可自動產生程式碼來執行建立、讀取、更新和刪除 (CRUD) 動作。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-175">The ASP.NET MVC the scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-the-data"></a><span data-ttu-id="ecc8b-176">新增控制器和資料檢視</span><span class="sxs-lookup"><span data-stu-id="ecc8b-176">Add a Controller and a view for the data</span></span>
1. <span data-ttu-id="ecc8b-177">在 [方案總管] 中展開 Controllers 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-177">In **Solution Explorer**, expand the Controllers folder.</span></span>
2. <span data-ttu-id="ecc8b-178">建置專案 **(Ctrl+Shift+B)**。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-178">Build the project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="ecc8b-179">(使用樣板機制前必須先建置專案。)</span><span class="sxs-lookup"><span data-stu-id="ecc8b-179">(You must build the project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="ecc8b-180">在 Controllers 資料夾上按一下滑鼠右鍵，按一下 [新增]，再按一下 [控制器]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-180">Right-click the Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![在 Controllers 資料夾內容功能表中新增控制器][addcode001]
4. <span data-ttu-id="ecc8b-182">在 [Add Scaffold] 對話方塊中，選取 [MVC Controller with views, using Entity Framework]，再按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-182">In the **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![新增控制器](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="ecc8b-184">將控制器名稱設定為 **HomeController**。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-184">Set the controller name to **HomeController**.</span></span> <span data-ttu-id="ecc8b-185">選取 [Contact]  模型類別。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="ecc8b-186">按一下 [新資料內容] 按鈕，並接受 [新資料內容類型] 的預設值 "ContactManager.Models.ContactManagerContext"。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-186">Click the **New data context** button and accept the default "ContactManager.Models.ContactManagerContext" for the **New data context type**.</span></span> <span data-ttu-id="ecc8b-187">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-187">Click **Add**.</span></span>

    <span data-ttu-id="ecc8b-188">對話方塊會提示您：「名為 HomeController 的檔案已存在。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-188">A dialog box will prompt you: "A file with the name HomeController already exits.</span></span> <span data-ttu-id="ecc8b-189">您要取代該檔案嗎？</span><span class="sxs-lookup"><span data-stu-id="ecc8b-189">Do you want to replace it?".</span></span> <span data-ttu-id="ecc8b-190">」按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-190">Click **Yes**.</span></span> <span data-ttu-id="ecc8b-191">我們會覆寫隨著新專案一同建立的首頁控制器。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-191">We are overwriting the Home Controller that was created with the new project.</span></span> <span data-ttu-id="ecc8b-192">我們會將新的首頁控制器用於連絡人清單。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-192">We will use the new Home Controller for our contact list.</span></span>

    <span data-ttu-id="ecc8b-193">Visual Studio 隨即針對 **Contact** 物件的 CRUD 資料庫操作，建立控制器方法與檢視。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="ecc8b-194">啟用移轉、建立資料庫、新增範例資料和資料初始設定式</span><span class="sxs-lookup"><span data-stu-id="ecc8b-194">Enable Migrations, create the database, add sample data and a data initializer</span></span>
<span data-ttu-id="ecc8b-195">下一個工作是啟用 [Code First 移轉](http://curah.microsoft.com/55220) 功能，以便根據建立的資料模型建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-195">The next task is to enable the [Code First Migrations](http://curah.microsoft.com/55220) feature in order to create the database based on the data model you created.</span></span>

1. <span data-ttu-id="ecc8b-196">在 [工具] 功能表中，依序選取 [Library Package Manager] 及 [Package Manager Console]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-196">In the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![[工具] 功能表中的 Package Manager Console][addcode008]
2. <span data-ttu-id="ecc8b-198">在 [Package Manager Console]  視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="ecc8b-198">In the **Package Manager Console** window, enter the following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="ecc8b-199">**enable-migrations** 命令會建立 *Migrations* 資料夾，並在該資料夾置入 *Configuration.cs* 檔案，您可以編輯該檔案來設定 [移轉]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-199">The **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span></span> 
3. <span data-ttu-id="ecc8b-200">在 [Package Manager Console]  視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="ecc8b-200">In the **Package Manager Console** window, enter the following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="ecc8b-201">**add-migration Initial** 命令會產生可建立資料庫、名為 **&lt;date_stamp&gt;Initial** 的類別。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-201">The **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates the database.</span></span> <span data-ttu-id="ecc8b-202">第一個參數 ( *Initial* ) 是任意的，用於建立檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-202">The first parameter ( *Initial* ) is arbitrary and used to create the name of the file.</span></span> <span data-ttu-id="ecc8b-203">您可以在 [方案總管] 中看到新的類別檔案。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-203">You can see the new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="ecc8b-204">在 **Initial** 類別中，**Up** 方法會建立 Contacts 資料表，**Down** 方法 (當您希望返回前個狀態時使用) 則會捨棄該資料表。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-204">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span></span>
4. <span data-ttu-id="ecc8b-205">開啟 *Migrations\Configuration.cs* 檔案。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-205">Open the *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="ecc8b-206">新增下列命名空間。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-206">Add the following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="ecc8b-207">以下列程式碼取代 *Seed* 方法：</span><span class="sxs-lookup"><span data-stu-id="ecc8b-207">Replace the *Seed* method with the following code:</span></span>
   
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
   
    <span data-ttu-id="ecc8b-208">以上的這個程式碼會以連絡人資訊初始化資料庫。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-208">This code above will initialize the database with the contact information.</span></span> <span data-ttu-id="ecc8b-209">如需植入資料庫的詳細資訊，請參閱 [植入及偵錯 Entity Framework (EF) DB](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)(英文)。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-209">For more information on seeding the database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="ecc8b-210">在 [Package Manager Console]  中輸入命令：</span><span class="sxs-lookup"><span data-stu-id="ecc8b-210">In the **Package Manager Console** enter the command:</span></span>
   
        update-database
   
    ![Package Manager Console commands][addcode009]
   
    <span data-ttu-id="ecc8b-212">**update-database** 會執行第一次移轉，使資料庫建立。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-212">The **update-database** runs the first migration which creates the database.</span></span> <span data-ttu-id="ecc8b-213">根據預設，資料庫會以 SQL Server Express LocalDB 資料庫的形式建立。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-213">By default, the database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="ecc8b-214">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-214">Press CTRL+F5 to run the application.</span></span> 

<span data-ttu-id="ecc8b-215">應用程式隨即顯示種子資料並提供編輯、詳細資料和刪除連結。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-215">The application shows the seed data and provides edit, details and delete links.</span></span>

![資料的 MVC 檢視][rxz3]

## <a name="edit-the-view"></a><span data-ttu-id="ecc8b-217">編輯檢視</span><span class="sxs-lookup"><span data-stu-id="ecc8b-217">Edit the View</span></span>
1. <span data-ttu-id="ecc8b-218">開啟 *Views\Home\Index.cshtml* 檔案。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-218">Open the *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="ecc8b-219">在下一個步驟中，我們會將產生的標記取代為使用 [jQuery](http://jquery.com/) 和 [Knockout.js](http://knockoutjs.com/) 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-219">In the next step, we will replace the generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="ecc8b-220">這個新的程式碼會使用 Web API 和 JSON 來擷取連絡人清單，然後再使用 knockout.js 使連絡人資料與 UI 繫結。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-220">This new code retrieves the list of contacts from using web API and JSON and then binds the contact data to the UI using knockout.js.</span></span> <span data-ttu-id="ecc8b-221">如需詳細資訊，請參閱本教學課程結尾處的 [後續步驟](#nextsteps) 一節。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-221">For more information, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
2. <span data-ttu-id="ecc8b-222">以下列程式碼取代檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-222">Replace the contents of the file with the following code.</span></span>
   
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
3. <span data-ttu-id="ecc8b-223">在 Content 資料夾上按一下滑鼠右鍵，按一下 [新增]，再按一下 [新增項目...]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-223">Right-click the Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Content 資料夾內容功能表中的 [加入樣式表]][addcode005]
4. <span data-ttu-id="ecc8b-225">在 [加入新項目] 對話方塊中，於右上角的搜尋方塊中輸入 **Style**，然後選取 [樣式表]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-225">In the **Add New Item** dialog box, enter **Style** in the upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="ecc8b-226">![[加入新項目] 對話方塊][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="ecc8b-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="ecc8b-227">將檔案命名為 *Contacts.css*，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-227">Name the file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="ecc8b-228">以下列程式碼取代檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-228">Replace the contents of the file with the following code.</span></span>
   
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
   
    <span data-ttu-id="ecc8b-229">我們會將此樣式表用於 Contact Manager 應用程式所用的版面配置、色彩及樣式。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-229">We will use this style sheet for the layout, colors and styles used in the contact manager app.</span></span>
6. <span data-ttu-id="ecc8b-230">開啟 *App_Start\BundleConfig.cs* 檔案。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-230">Open the *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="ecc8b-231">新增以下程式碼以註冊 [Knockout](http://knockoutjs.com/index.html "KO") 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-231">Add the following code to register the [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="ecc8b-232">此範例使用 knockout 來簡化處理螢幕範本的動態 JavaScript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-232">This sample using knockout to simplify dynamic JavaScript code that handles the screen templates.</span></span>
8. <span data-ttu-id="ecc8b-233">修改 contents/css 項目以註冊 *contacts.css* 樣式表。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-233">Modify the contents/css entry to register the *contacts.css* style sheet.</span></span> <span data-ttu-id="ecc8b-234">變更以下文字行：</span><span class="sxs-lookup"><span data-stu-id="ecc8b-234">Change the following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="ecc8b-235">變更為：</span><span class="sxs-lookup"><span data-stu-id="ecc8b-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="ecc8b-236">在 Package Manager Console 中，執行下列命令以安裝 Knockout。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-236">In the Package Manager Console, run the following command to install Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a><span data-ttu-id="ecc8b-237">為符合 REST 限制的 Web API 介面新增控制器</span><span class="sxs-lookup"><span data-stu-id="ecc8b-237">Add a controller for the Web API Restful interface</span></span>
1. <span data-ttu-id="ecc8b-238">在 [方案總管]，於 Controllers 上按一下滑鼠右鍵，按一下 [新增]，再按一下 [控制器...]</span><span class="sxs-lookup"><span data-stu-id="ecc8b-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="ecc8b-239">在 [Add Scaffold] 對話方塊中，選取 [Web API 2 Controller with actions, using Entity Framework]，再按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-239">In the **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![新增 API 控制器](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="ecc8b-241">在 [加入控制器]  對話方塊中，輸入 "ContactsController" 作為控制器名稱。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-241">In the **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="ecc8b-242">選取 "Contact (ContactManager.Models)" [模型類別] 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-242">Select "Contact (ContactManager.Models)" for the **Model class**.</span></span>  <span data-ttu-id="ecc8b-243">保留 [資料內容類別] 的預設值。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-243">Keep the default value for the **Data context class**.</span></span> 
4. <span data-ttu-id="ecc8b-244">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-244">Click **Add**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="ecc8b-245">在本機執行應用程式</span><span class="sxs-lookup"><span data-stu-id="ecc8b-245">Run the application locally</span></span>
1. <span data-ttu-id="ecc8b-246">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-246">Press CTRL+F5 to run the application.</span></span>
   
    ![索引頁面][intro001]
2. <span data-ttu-id="ecc8b-248">輸入連絡人，然後按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="ecc8b-249">應用程式會返回首頁並顯示您輸入的連絡人。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-249">The app returns to the home page and displays the contact you entered.</span></span>
   
    ![含有待辦事項清單的索引頁面][addwebapi004]
3. <span data-ttu-id="ecc8b-251">在瀏覽器中，於 URL 後方加上 **/api/contacts** 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-251">In the browser, append **/api/contacts** to the URL.</span></span>
   
    <span data-ttu-id="ecc8b-252">產生的 URL 將類似 http://localhost:1234/api/contacts。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-252">The resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="ecc8b-253">您新增之符合 REST 限制的 Web API 會傳回儲存的連絡人。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-253">The RESTful web API you added returns the stored contacts.</span></span> <span data-ttu-id="ecc8b-254">Firefox 和 Chrome 會顯示 XML 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-254">Firefox and Chrome will display the data in XML format.</span></span>
   
    ![含有待辦事項清單的索引頁面][rxFFchrome]

    <span data-ttu-id="ecc8b-256">IE 會提示您開啟或儲存連絡人。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-256">IE will prompt you to open or save the contacts.</span></span>

    ![Web API 儲存對話方塊][addwebapi006]


    <span data-ttu-id="ecc8b-258">您可以利用記事本或瀏覽器開啟傳回的連絡人。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-258">You can open the returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="ecc8b-259">行動網頁或應用程式之類的其他應用程式亦可取用此輸出。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Web API 儲存對話方塊][addwebapi007]

    <span data-ttu-id="ecc8b-261">**安全性警告**：此時您的應用程式並未受到保護，且容易遭受 CSRF 攻擊。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-261">**Security Warning**: At this point, your application is insecure and vulnerable to CSRF attack.</span></span> <span data-ttu-id="ecc8b-262">在本教學課程稍後的內容中，我們將移除這項弱點。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-262">Later in the tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="ecc8b-263">如需詳細資訊，請參閱[避免跨網站偽造要求 (CSRF) 攻擊][prevent-csrf-attacks]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="ecc8b-264">新增 XSRF 保護</span><span class="sxs-lookup"><span data-stu-id="ecc8b-264">Add XSRF Protection</span></span>
<span data-ttu-id="ecc8b-265">跨網站偽造要求 (亦稱為 XSRF 或 CSRF) 為以 Web 主控之應用程式為目標的攻擊，惡意網站能藉此影響用戶端瀏覽器和該瀏覽器信任之網站間的互動。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence the interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="ecc8b-266">這些攻擊之所以能得逞，是因為網頁瀏覽器會隨著對網站的每個要求自動傳送驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="ecc8b-267">ASP.NET 的 Forms Authentication 票證即是驗證 Cookie 的標準範例。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-267">The canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="ecc8b-268">然而，使用任何持續驗證機制 (如 Windows 驗證、基本驗證等等) 的網站都可能成為這些攻擊的目標。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="ecc8b-269">XSRF 攻擊與網路釣魚攻擊不同。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="ecc8b-270">網路釣魚攻擊需要與受害者互動。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-270">Phishing attacks require interaction from the victim.</span></span> <span data-ttu-id="ecc8b-271">對於網路釣魚攻擊，惡意網站會偽裝成目標網站，致使受害者因受騙而將機密資訊提供給攻擊者。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-271">In a phishing attack, a malicious website will mimic the target website, and the victim is fooled into providing sensitive information to the attacker.</span></span> <span data-ttu-id="ecc8b-272">XSRF 攻擊則通常不需要與受害者互動。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-272">In an XSRF attack, there is often no interaction necessary from the victim.</span></span> <span data-ttu-id="ecc8b-273">反之，攻擊者需仰賴瀏覽器將所有相關的 Cookie 自動傳送給目的地網站。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-273">Rather, the attacker is relying on the browser automatically sending all relevant cookies to the destination website.</span></span>

<span data-ttu-id="ecc8b-274">如需詳細資訊，請參閱 [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\))。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-274">For more information, see the [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="ecc8b-275">在 [方案總管] 中，於 **ContactManager** 專案上按一下滑鼠右鍵，按一下 [新增]，再按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="ecc8b-276">將檔案命名為 *ValidateHttpAntiForgeryTokenAttribute.cs* ，然後新增以下程式碼：</span><span class="sxs-lookup"><span data-stu-id="ecc8b-276">Name the file *ValidateHttpAntiForgeryTokenAttribute.cs* and add the following code:</span></span>
   
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
3. <span data-ttu-id="ecc8b-277">將以下 *using* 陳述式新增至連絡人控制器，使您得以存取 **[ValidateHttpAntiForgeryToken]** 屬性。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-277">Add the following *using* statement to the contracts controller so you have access to the **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="ecc8b-278">將 [ValidateHttpAntiForgeryToken] 屬性新增至 **ContactsController** 的 Post 方法，使其免於遭受 XSRF 威脅的攻擊。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-278">Add the **[ValidateHttpAntiForgeryToken]** attribute to the Post methods of the **ContactsController** to protect it from XSRF threats.</span></span> <span data-ttu-id="ecc8b-279">您需要將其新增至 PutContact"、"PostContact" 及 **DeleteContact** 動作方法。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-279">You will add it to the "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="ecc8b-280">更新 Views\Home\Index.cshtml 檔案的 Scripts 區段，使其包含取得 XSRF 權杖的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-280">Update the *Scripts* section of the *Views\Home\Index.cshtml* file to include code to get the XSRF tokens.</span></span>
   
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

## <a name="publish-the-application-update-to-azure-and-sql-database"></a><span data-ttu-id="ecc8b-281">將應用程式更新發行至 Azure 和 SQL Database</span><span class="sxs-lookup"><span data-stu-id="ecc8b-281">Publish the application update to Azure and SQL Database</span></span>
<span data-ttu-id="ecc8b-282">若要發行應用程式，您需要重複先前遵循過的程序。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-282">To publish the application, you repeat the procedure you followed earlier.</span></span>

1. <span data-ttu-id="ecc8b-283">在 [方案總管] 中以滑鼠右鍵按一下專案，再選取 [發行]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-283">In **Solution Explorer**, right click the project and select **Publish**.</span></span>
   
    ![發佈][rxP]
2. <span data-ttu-id="ecc8b-285">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-285">Click the **Settings** tab.</span></span>
3. <span data-ttu-id="ecc8b-286">在 **ContactsManagerContext(ContactsManagerContext)** 下方按一下 **v** 圖示，將 *Remote connection string* 變更為連絡人資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-286">Under **ContactsManagerContext(ContactsManagerContext)**, click the **v** icon to change *Remote connection string* to the connection string for the contact database.</span></span> <span data-ttu-id="ecc8b-287">按一下 [ContactDB] 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-287">Click **ContactDB**.</span></span>
   
    ![設定](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="ecc8b-289">勾選 [Execute Code First Migrations (runs on application start)] 的方塊。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-289">Check the box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="ecc8b-290">依序按 [下一步] 和 [預覽]。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="ecc8b-291">Visual Studio 會顯示即將新增或更新的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-291">Visual Studio displays a list of the files that will be added or updated.</span></span>
6. <span data-ttu-id="ecc8b-292">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-292">Click **Publish**.</span></span>
   <span data-ttu-id="ecc8b-293">部署完成後，瀏覽器會開啟應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-293">After the deployment completes, the browser opens to the home page of the application.</span></span>
   
    ![Index page with no contacts][intro001]
   
    <span data-ttu-id="ecc8b-295">Visual Studio 發行程序會自動設定已部署之 *Web.config* 檔案中的連接字串，使其指向 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-295">The Visual Studio publish process automatically configured the connection string in the deployed *Web.config* file to point to the SQL database.</span></span> <span data-ttu-id="ecc8b-296">它也設定了 Code First 移轉，使其在應用程式於部署完成後首次存取資料庫時，將資料庫自動升級為最新版本。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-296">It also configured Code First Migrations to automatically upgrade the database to the latest version the first time the application accesses the database after deployment.</span></span>
   
    <span data-ttu-id="ecc8b-297">由於這項組態的關係，Code First 會執行您稍早於 **Initial** 類別中建立的程式碼，進而建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-297">As a result of this configuration, Code First created the database by running the code in the **Initial** class that you created earlier.</span></span> <span data-ttu-id="ecc8b-298">它會在應用程式於部署完成後首次嘗試存取資料庫時執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-298">It did this the first time the application tried to access the database after deployment.</span></span>
7. <span data-ttu-id="ecc8b-299">與在本機執行應用程式時一樣的方式輸入連絡人，以驗證資料庫部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-299">Enter a contact as you did when you ran the app locally, to verify that database deployment succeeded.</span></span>

<span data-ttu-id="ecc8b-300">當您發現輸入的項目已儲存且出現在 Contact Manager 頁面時，表示該項目已儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-300">When you see that the item you enter is saved and appears on the contact manager page, you know that it has been stored in the database.</span></span>

![含有連絡人的索引頁面][addwebapi004]

<span data-ttu-id="ecc8b-302">應用程式現已在雲端運作，並使用 SQL Database 來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-302">The application is now running in the cloud, using SQL Database to store its data.</span></span> <span data-ttu-id="ecc8b-303">在 Azure 中完成應用程式測試後，請將應用程式刪除。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-303">After you finish testing the application in Azure, delete it.</span></span> <span data-ttu-id="ecc8b-304">應用程式已處於公開狀態且不具有限制存取權限的機制。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-304">The application is public and doesn't have a mechanism to limit access.</span></span>

> [!NOTE]
> <span data-ttu-id="ecc8b-305">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-305">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ecc8b-306">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ecc8b-307">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecc8b-307">Next Steps</span></span>
<span data-ttu-id="ecc8b-308">另一個儲存 Azure 應用程式資料的方法是使用 Azure 儲存體，它能以 Blob 和資料表的形式提供非關聯式的資料儲存。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-308">Another way to store data in an Azure application is to use Azure storage, which provide non-relational data storage in the form of blobs and tables.</span></span> <span data-ttu-id="ecc8b-309">以下連結提供 Web API、ASP.NET MVC 及 Window Azure 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-309">The following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="ecc8b-310">[使用 MVC 的 Entity Framework 入門][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="ecc8b-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="ecc8b-311">ASP.NET MVC 5 入門</span><span class="sxs-lookup"><span data-stu-id="ecc8b-311">Intro to ASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="ecc8b-312">您的第一個 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="ecc8b-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="ecc8b-313">偵錯 WAWS</span><span class="sxs-lookup"><span data-stu-id="ecc8b-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="ecc8b-314">本教學課程和範例應用程式是由 [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) 在 Tom Dykstra 和 Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)) 的協助下所撰寫。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-314">This tutorial and the sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="ecc8b-315">如果您發現喜歡的地方或希望我們改善的地方 (不論是針對本教學課程或其示範的產品)，歡迎留下意見反應。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-315">Please leave feedback on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span></span> <span data-ttu-id="ecc8b-316">您的意見反應將協助我們訂出優先改善要務。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="ecc8b-317">我們非常希望能了解您對於將設定和部署成員資格資料庫之程序更進一步自動化的期待為何。</span><span class="sxs-lookup"><span data-stu-id="ecc8b-317">We are especially interested in finding out how much interest there is in more automation for the process of configuring and deploying the membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="ecc8b-318">變更的項目</span><span class="sxs-lookup"><span data-stu-id="ecc8b-318">What's changed</span></span>
* <span data-ttu-id="ecc8b-319">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ecc8b-319">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles to the Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2
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

