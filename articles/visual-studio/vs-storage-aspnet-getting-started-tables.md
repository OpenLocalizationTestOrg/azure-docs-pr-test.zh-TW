---
title: "aaaGet 開始使用 Azure 資料表儲存體和 Visual Studio 已連接服務 (ASP.NET) |Microsoft 文件"
description: "Tooget 啟動連接 tooa 使用 Visual Studio 已連接服務的儲存體帳戶之後，Visual Studio 中 ASP.NET 專案中使用 Azure 資料表儲存體的方式"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraigb
ms.openlocfilehash: 04f79db7aad60ca51c3c866da1f4b01d9e11ac52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="b78bb-103">開始使用 Azure 資料表儲存體和 Visual Studio 已連線的服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b78bb-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="b78bb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b78bb-104">Overview</span></span>

<span data-ttu-id="b78bb-105">Azure 資料表儲存體可讓您 toostore 大量結構化資料。</span><span class="sxs-lookup"><span data-stu-id="b78bb-105">Azure Table storage enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="b78bb-106">hello 服務是可接受來自內部和外部 hello Azure 雲端的已驗證的呼叫的 NoSQL 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b78bb-106">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="b78bb-107">Azure 資料表很適合儲存結構化、非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="b78bb-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="b78bb-108">本教學課程會示範 toowrite ASP.NET 為使用 Azure 資料表儲存體實體一些常見案例的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b78bb-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="b78bb-109">這些案例包括建立資料表，以及新增、查詢和刪除資料表實體。</span><span class="sxs-lookup"><span data-stu-id="b78bb-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="b78bb-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b78bb-110">Prerequisites</span></span>

* [<span data-ttu-id="b78bb-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b78bb-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="b78bb-112">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b78bb-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="b78bb-113">建立 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="b78bb-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="b78bb-114">在 hello**方案總管 中**，以滑鼠右鍵按一下**控制站**，並從 hello 內容功能表中，選取**加入控制器->** 。</span><span class="sxs-lookup"><span data-stu-id="b78bb-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![加入控制器 tooan ASP.NET MVC 應用程式](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="b78bb-116">在 hello**新增 Scaffold**對話方塊中，選取**MVC 5 控制器空白**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![指定 MVC 控制器類型](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="b78bb-118">在 hello**加入控制器**對話方塊中，名稱 hello 控制器*TablesController*，並選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-118">On hello **Add Controller** dialog, name hello controller *TablesController*, and select **Add**.</span></span>

    ![名稱 hello MVC 控制器](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="b78bb-120">新增下列 hello*使用*指示詞 toohello`TablesController.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="b78bb-120">Add hello following *using* directives toohello `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="b78bb-121">建立模型類別</span><span class="sxs-lookup"><span data-stu-id="b78bb-121">Create a model class</span></span>

<span data-ttu-id="b78bb-122">中的 hello 範例的許多發行項使用**TableEntity**-衍生的類別呼叫**CustomerEntity**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-122">Many of hello examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="b78bb-123">hello 步驟會引導您宣告這個類別做為模型類別：</span><span class="sxs-lookup"><span data-stu-id="b78bb-123">hello following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="b78bb-124">在 hello**方案總管 中**，以滑鼠右鍵按一下**模型**，並從 hello 內容功能表中，選取**新增類別->** 。</span><span class="sxs-lookup"><span data-stu-id="b78bb-124">In hello **Solution Explorer**, right-click **Models**, and, from hello context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="b78bb-125">在 hello**加入新項目**對話方塊中，名稱 hello 類別， **CustomerEntity**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-125">On hello **Add New Item** dialog, name hello class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="b78bb-126">開啟 hello`CustomerEntity.cs`檔並加入下列 hello**使用**指示詞：</span><span class="sxs-lookup"><span data-stu-id="b78bb-126">Open hello `CustomerEntity.cs` file, and add hello following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="b78bb-127">修改 hello 類別，以便完成後，請 hello 類別的宣告方式如下列程式碼的 hello 所示。</span><span class="sxs-lookup"><span data-stu-id="b78bb-127">Modify hello class so that, when finished, hello class is declared as in hello following code.</span></span> <span data-ttu-id="b78bb-128">hello 類別會宣告稱為實體類別**CustomerEntity**使用 hello hello 資料列索引鍵為客戶的名字和姓氏 hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b78bb-128">hello class declares an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a><span data-ttu-id="b78bb-129">建立資料表</span><span class="sxs-lookup"><span data-stu-id="b78bb-129">Create a table</span></span>

<span data-ttu-id="b78bb-130">hello 下列步驟說明如何 toocreate 資料表：</span><span class="sxs-lookup"><span data-stu-id="b78bb-130">hello following steps illustrate how toocreate a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b78bb-131">本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-131">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b78bb-132">開啟 hello`TablesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="b78bb-132">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="b78bb-133">新增名為 **CreateTable** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="b78bb-134">在 hello **CreateTable**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b78bb-134">Within hello **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b78bb-135">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="b78bb-135">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="b78bb-136">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="b78bb-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="b78bb-137">取得**CloudTable**物件，表示參考 toohello 所需的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="b78bb-137">Get a **CloudTable** object that represents a reference toohello desired table name.</span></span> <span data-ttu-id="b78bb-138">hello **CloudTableClient.GetTableReference**方法不會針對資料表儲存體的要求。</span><span class="sxs-lookup"><span data-stu-id="b78bb-138">hello **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="b78bb-139">不論是否 hello 資料表存在，則會傳回 hello 參考。</span><span class="sxs-lookup"><span data-stu-id="b78bb-139">hello reference is returned whether or not hello table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="b78bb-140">呼叫 hello **CloudTable.CreateIfNotExists**方法 toocreate hello 資料表如果尚不存在。</span><span class="sxs-lookup"><span data-stu-id="b78bb-140">Call hello **CloudTable.CreateIfNotExists** method toocreate hello table if it does not yet exist.</span></span> <span data-ttu-id="b78bb-141">hello **CloudTable.CreateIfNotExists**方法會傳回**true**如果 hello 資料表不存在，而且已成功建立。</span><span class="sxs-lookup"><span data-stu-id="b78bb-141">hello **CloudTable.CreateIfNotExists** method returns **true** if hello table does not exist, and is successfully created.</span></span> <span data-ttu-id="b78bb-142">否則，會傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="b78bb-143">更新 hello **ViewBag** hello hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="b78bb-143">Update hello **ViewBag** with hello name of hello table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="b78bb-144">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="b78bb-144">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b78bb-145">在 [hello**加入檢視**] 對話方塊中，輸入**CreateTable** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-145">On hello **Add View** dialog, enter **CreateTable** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b78bb-146">開啟`CreateTable.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="b78bb-146">Open `CreateTable.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="b78bb-147">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="b78bb-147">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b78bb-148">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b78bb-148">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="b78bb-149">執行 hello 應用程式，並選取**建立資料表**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="b78bb-149">Run hello application, and select **Create table** toosee results similar toohello following screen shot:</span></span>
  
    ![建立資料表](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="b78bb-151">如先前所述，hello **CloudTable.CreateIfNotExists**方法會傳回**true**只當 hello 資料表不存在，而且會建立。</span><span class="sxs-lookup"><span data-stu-id="b78bb-151">As mentioned previously, hello **CloudTable.CreateIfNotExists** method returns **true** only when hello table doesn't exist and is created.</span></span> <span data-ttu-id="b78bb-152">因此，如果 hello 資料表存在時，您可以執行 hello 應用程式，hello 方法會傳回**false**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-152">Therefore, if you run hello app when hello table exists, hello method returns **false**.</span></span> <span data-ttu-id="b78bb-153">toorun hello 應用程式多次，必須刪除 hello 資料表，才能再次執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b78bb-153">toorun hello app multiple times, you must delete hello table before running hello app again.</span></span> <span data-ttu-id="b78bb-154">正在刪除 hello 資料表可透過 hello **CloudTable.Delete**方法。</span><span class="sxs-lookup"><span data-stu-id="b78bb-154">Deleting hello table can be done via hello **CloudTable.Delete** method.</span></span> <span data-ttu-id="b78bb-155">您也可以刪除 hello 資料表使用 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)或 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-155">You can also delete hello table using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="b78bb-156">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="b78bb-156">Add an entity tooa table</span></span>

<span data-ttu-id="b78bb-157">*實體*對應 tooC\#物件使用的自訂類別衍生自**TableEntity**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-157">*Entities* map tooC\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="b78bb-158">tooadd 實體 tooa 資料表，建立一個類別來定義實體的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="b78bb-158">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="b78bb-159">在本節中，您會看到如何使用的實體類別 toodefine hello hello 資料列索引鍵為客戶的名字和姓氏 hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b78bb-159">In this section, you'll see how toodefine an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="b78bb-160">在一起，實體的資料分割和資料列索引鍵可唯一識別 hello 資料表中的 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="b78bb-160">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="b78bb-161">查詢具有相同分割區索引鍵的實體，其速度快於查詢具有不同分割區索引鍵的實體，但使用不同的資料分割索引鍵可提供更佳的延展性或平行作業。</span><span class="sxs-lookup"><span data-stu-id="b78bb-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="b78bb-162">應該儲存在 hello 表格服務的所有屬性，hello 屬性必須是支援的型別可公開設定和擷取值的公用屬性。</span><span class="sxs-lookup"><span data-stu-id="b78bb-162">For any property that should be stored in hello table service, hello property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="b78bb-163">hello 實體類別*必須*宣告公用的無參數建構函式。</span><span class="sxs-lookup"><span data-stu-id="b78bb-163">hello entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b78bb-164">本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-164">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="b78bb-165">開啟 hello`TablesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="b78bb-165">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="b78bb-166">新增下列指示詞，因此的 hello hello 中的程式碼的 hello`TablesController.cs`檔案可以存取 hello **CustomerEntity**類別：</span><span class="sxs-lookup"><span data-stu-id="b78bb-166">Add hello following directive so that hello code in hello `TablesController.cs` file can access hello **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="b78bb-167">新增名為 **AddEntity** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="b78bb-168">在 hello **AddEntity**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b78bb-168">Within hello **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b78bb-169">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="b78bb-169">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="b78bb-170">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="b78bb-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="b78bb-171">取得**CloudTable**物件，代表要 tooadd hello 新實體參考 toohello 資料表 toowhich。</span><span class="sxs-lookup"><span data-stu-id="b78bb-171">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="b78bb-172">具現化，並初始化 hello **CustomerEntity**類別。</span><span class="sxs-lookup"><span data-stu-id="b78bb-172">Instantiate and initialize hello **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="b78bb-173">建立**TableOperation**插入 hello customer 實體的物件。</span><span class="sxs-lookup"><span data-stu-id="b78bb-173">Create a **TableOperation** object that inserts hello customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="b78bb-174">執行呼叫 hello hello 插入作業**CloudTable.Execute**方法。</span><span class="sxs-lookup"><span data-stu-id="b78bb-174">Execute hello insert operation by calling hello **CloudTable.Execute** method.</span></span> <span data-ttu-id="b78bb-175">您可以藉由檢查 hello 確認 hello 作業結果的 hello **TableResult.HttpStatusCode**屬性。</span><span class="sxs-lookup"><span data-stu-id="b78bb-175">You can verify hello result of hello operation by inspecting hello **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="b78bb-176">2xx 狀態碼表示已成功處理 hello hello 用戶端要求的動作。</span><span class="sxs-lookup"><span data-stu-id="b78bb-176">A status code of 2xx indicates hello action requested by hello client was processed successfully.</span></span> <span data-ttu-id="b78bb-177">例如，成功插入新的實體會導致 HTTP 狀態碼 204，也就是說，hello 作業已成功處理，而且 hello 伺服器未傳回任何內容。</span><span class="sxs-lookup"><span data-stu-id="b78bb-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that hello operation was successfully processed and hello server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="b78bb-178">更新 hello **ViewBag** hello 資料表名稱，與 hello 的 hello 插入作業的結果。</span><span class="sxs-lookup"><span data-stu-id="b78bb-178">Update hello **ViewBag** with hello table name, and hello results of hello insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="b78bb-179">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="b78bb-179">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b78bb-180">在 [hello**加入檢視**] 對話方塊中，輸入**AddEntity** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-180">On hello **Add View** dialog, enter **AddEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b78bb-181">開啟`AddEntity.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="b78bb-181">Open `AddEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="b78bb-182">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="b78bb-182">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b78bb-183">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b78bb-183">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="b78bb-184">執行 hello 應用程式，並選取**加入實體**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="b78bb-184">Run hello application, and select **Add entity** toosee results similar toohello following screen shot:</span></span>
  
    ![新增實體](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="b78bb-186">您可以確認 hello 實體已加入 hello 區段中的 hello 步驟[取得單一實體](#get-a-single-entity)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-186">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="b78bb-187">您也可以使用 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)tooview 所有 hello 出資料表的實體。</span><span class="sxs-lookup"><span data-stu-id="b78bb-187">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-tooa-table"></a><span data-ttu-id="b78bb-188">加入實體 tooa 資料表的批次</span><span class="sxs-lookup"><span data-stu-id="b78bb-188">Add a batch of entities tooa table</span></span>

<span data-ttu-id="b78bb-189">中可以加入 toobeing 太[一次新增一個實體 tooa 表](#add-an-entity-to-a-table)，您也可以加入實體批次中。</span><span class="sxs-lookup"><span data-stu-id="b78bb-189">In addition toobeing able too[add an entity tooa table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="b78bb-190">加入實體批次中可減少您的程式碼與 hello Azure 資料表服務之間的來回的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="b78bb-190">Adding entities in batch reduces hello number of round-trips between your code and hello Azure table service.</span></span> <span data-ttu-id="b78bb-191">hello 下列步驟說明如何 tooadd 多個實體 tooa 資料表具有單一 insert 作業：</span><span class="sxs-lookup"><span data-stu-id="b78bb-191">hello following steps illustrate how tooadd multiple entities tooa table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b78bb-192">本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-192">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="b78bb-193">開啟 hello`TablesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="b78bb-193">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="b78bb-194">新增名為 **AddEntity** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="b78bb-195">在 hello **AddEntities**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b78bb-195">Within hello **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b78bb-196">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="b78bb-196">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="b78bb-197">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="b78bb-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="b78bb-198">取得**CloudTable**物件，表示會持續 tooadd hello 新實體參考 toohello 資料表 toowhich。</span><span class="sxs-lookup"><span data-stu-id="b78bb-198">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="b78bb-199">根據 hello 某些客戶物件具現化**CustomerEntity**模型類別 hello 區段中呈現[加入實體 tooa 表](#add-an-entity-to-a-table)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-199">Instantiate some customer objects based on hello **CustomerEntity** model class presented in hello section, [Add an entity tooa table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="b78bb-200">取得 **TableBatchOperation** 物件。</span><span class="sxs-lookup"><span data-stu-id="b78bb-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="b78bb-201">加入實體 toohello 批次插入作業物件。</span><span class="sxs-lookup"><span data-stu-id="b78bb-201">Add entities toohello batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="b78bb-202">執行呼叫 hello hello 批次插入作業**CloudTable.ExecuteBatch**方法。</span><span class="sxs-lookup"><span data-stu-id="b78bb-202">Execute hello batch insert operation by calling hello **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="b78bb-203">hello **CloudTable.ExecuteBatch**方法會傳回一份**TableResult**物件其中每個**TableResult**物件可以檢查的 toodetermine hello 成功或失敗每個個別作業。</span><span class="sxs-lookup"><span data-stu-id="b78bb-203">hello **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined toodetermine hello success or failure of each individual operation.</span></span> <span data-ttu-id="b78bb-204">例如，傳遞 hello 清單 tooa 檢視，讓 hello 檢視顯示每個作業的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="b78bb-204">For this example, pass hello list tooa view and let hello view display hello results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="b78bb-205">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="b78bb-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b78bb-206">在 [hello**加入檢視**] 對話方塊中，輸入**AddEntities** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-206">On hello **Add View** dialog, enter **AddEntities** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b78bb-207">開啟`AddEntities.cshtml`，並使它看起來類似下列 hello 加以修改。</span><span class="sxs-lookup"><span data-stu-id="b78bb-207">Open `AddEntities.cshtml`, and modify it so that it looks like hello following.</span></span>

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="b78bb-208">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="b78bb-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b78bb-209">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b78bb-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="b78bb-210">執行 hello 應用程式，並選取**加入實體**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="b78bb-210">Run hello application, and select **Add entities** toosee results similar toohello following screen shot:</span></span>
  
    ![新增實體](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="b78bb-212">您可以確認 hello 實體已加入 hello 區段中的 hello 步驟[取得單一實體](#get-a-single-entity)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-212">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="b78bb-213">您也可以使用 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)tooview 所有 hello 出資料表的實體。</span><span class="sxs-lookup"><span data-stu-id="b78bb-213">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="b78bb-214">取得單一實體</span><span class="sxs-lookup"><span data-stu-id="b78bb-214">Get a single entity</span></span>

<span data-ttu-id="b78bb-215">本節說明如何從資料表使用的單一實體 tooget hello 實體的資料列索引鍵和資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b78bb-215">This section illustrates how tooget a single entity from a table using hello entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="b78bb-216">本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)，並使用來自資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-216">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="b78bb-217">開啟 hello`TablesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="b78bb-217">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="b78bb-218">新增名為 **GetSingle** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="b78bb-219">在 hello **GetSingle**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b78bb-219">Within hello **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b78bb-220">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="b78bb-220">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="b78bb-221">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="b78bb-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="b78bb-222">取得**CloudTable**物件，代表擷取 hello 實體參考 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="b78bb-222">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="b78bb-223">建立擷取作業物件，其採用衍生自 **TableEntity** 的實體物件。</span><span class="sxs-lookup"><span data-stu-id="b78bb-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="b78bb-224">hello 第一個參數是 hello *partitionKey*，hello 第二個參數則是 hello *rowKey*。</span><span class="sxs-lookup"><span data-stu-id="b78bb-224">hello first parameter is hello *partitionKey*, and hello second parameter is hello *rowKey*.</span></span> <span data-ttu-id="b78bb-225">使用 hello **CustomerEntity**類別和 hello 區段中顯示資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)，下列程式碼片段查詢 hello 資料表 hello **CustomerEntity**實體*partitionKey* "Smith"的值和*rowKey* "Ben"的值：</span><span class="sxs-lookup"><span data-stu-id="b78bb-225">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="b78bb-226">執行 hello 擷取作業。</span><span class="sxs-lookup"><span data-stu-id="b78bb-226">Execute hello retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="b78bb-227">傳遞顯示 hello 結果 toohello 檢視。</span><span class="sxs-lookup"><span data-stu-id="b78bb-227">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="b78bb-228">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="b78bb-228">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b78bb-229">在 [hello**加入檢視**] 對話方塊中，輸入**GetSingle** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-229">On hello **Add View** dialog, enter **GetSingle** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b78bb-230">開啟`GetSingle.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="b78bb-230">Open `GetSingle.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. <span data-ttu-id="b78bb-231">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="b78bb-231">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b78bb-232">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b78bb-232">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="b78bb-233">執行 hello 應用程式，並選取**取得單一**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="b78bb-233">Run hello application, and select **Get Single** toosee results similar toohello following screen shot:</span></span>
  
    ![取得單一](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="b78bb-235">取得資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="b78bb-235">Get all entities in a partition</span></span>

<span data-ttu-id="b78bb-236">Hello 區段中所述[加入實體 tooa 表](#add-an-entity-to-a-table)，hello 組合的磁碟分割和資料列索引鍵會唯一識別資料表中的實體。</span><span class="sxs-lookup"><span data-stu-id="b78bb-236">As mentioned in hello section, [Add an entity tooa table](#add-an-entity-to-a-table), hello combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="b78bb-237">相較於查詢具有不同資料分割索引鍵的實體，查詢具有相同資料分割索引鍵的實體速度會較快。</span><span class="sxs-lookup"><span data-stu-id="b78bb-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="b78bb-238">本節說明如何 tooquery 所有 hello 實體，從指定的資料分割的資料表。</span><span class="sxs-lookup"><span data-stu-id="b78bb-238">This section illustrates how tooquery a table for all hello entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="b78bb-239">本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)，並使用來自資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-239">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="b78bb-240">開啟 hello`TablesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="b78bb-240">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="b78bb-241">新增名為 **GetPartition** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="b78bb-242">在 hello **GetPartition**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b78bb-242">Within hello **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b78bb-243">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="b78bb-243">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="b78bb-244">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="b78bb-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="b78bb-245">取得**CloudTable**物件，代表擷取 hello 實體參考 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="b78bb-245">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="b78bb-246">具現化**TableQuery**物件，指定在 hello hello 查詢**其中**子句。</span><span class="sxs-lookup"><span data-stu-id="b78bb-246">Instantiate a **TableQuery** object specifying hello query in hello **Where** clause.</span></span> <span data-ttu-id="b78bb-247">使用 hello **CustomerEntity**類別和 hello 區段中顯示資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)，hello 下列程式碼片段查詢 hello 資料表的所有實體，其中 hello **PartitionKey** （客戶的最後一個名稱） 的值為"Smith":</span><span class="sxs-lookup"><span data-stu-id="b78bb-247">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a all entities where hello **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="b78bb-248">在迴圈中，呼叫 hello **CloudTable.ExecuteQuerySegmented**傳入 hello 上一個步驟中的 hello 您具現化的查詢物件的方法。</span><span class="sxs-lookup"><span data-stu-id="b78bb-248">Within a loop, call hello **CloudTable.ExecuteQuerySegmented** method passing hello query object you instantiated in hello previous step.</span></span>  <span data-ttu-id="b78bb-249">hello **CloudTable.ExecuteQuerySegmented**方法會傳回**TableContinuationToken**物件-當**null** -表示沒有多個實體tooretrieve。</span><span class="sxs-lookup"><span data-stu-id="b78bb-249">hello **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities tooretrieve.</span></span> <span data-ttu-id="b78bb-250">Hello 迴圈內使用另一個迴圈 tooiterate over hello 傳回實體。</span><span class="sxs-lookup"><span data-stu-id="b78bb-250">Within hello loop, use another loop tooiterate over hello returned entities.</span></span> <span data-ttu-id="b78bb-251">在下列程式碼範例的 hello，每個傳回的實體會加入 tooa 清單。</span><span class="sxs-lookup"><span data-stu-id="b78bb-251">In hello following code example, each returned entity is added tooa list.</span></span> <span data-ttu-id="b78bb-252">一次 hello 迴圈結束，hello 清單會傳遞 tooa 檢視顯示：</span><span class="sxs-lookup"><span data-stu-id="b78bb-252">Once hello loop ends, hello list is passed tooa view for display:</span></span> 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. <span data-ttu-id="b78bb-253">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="b78bb-253">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b78bb-254">在 [hello**加入檢視**] 對話方塊中，輸入**GetPartition** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-254">On hello **Add View** dialog, enter **GetPartition** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b78bb-255">開啟`GetPartition.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="b78bb-255">Open `GetPartition.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="b78bb-256">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="b78bb-256">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b78bb-257">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b78bb-257">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="b78bb-258">執行 hello 應用程式，並選取**取得分割區**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="b78bb-258">Run hello application, and select **Get Partition** toosee results similar toohello following screen shot:</span></span>
  
    ![取得資料分割](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="b78bb-260">刪除實體</span><span class="sxs-lookup"><span data-stu-id="b78bb-260">Delete an entity</span></span>

<span data-ttu-id="b78bb-261">本節說明如何 toodelete 資料表中的實體。</span><span class="sxs-lookup"><span data-stu-id="b78bb-261">This section illustrates how toodelete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b78bb-262">本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)，並使用來自資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-262">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="b78bb-263">開啟 hello`TablesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="b78bb-263">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="b78bb-264">新增名為 **DeleteEntity** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="b78bb-265">在 hello **DeleteEntity**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b78bb-265">Within hello **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b78bb-266">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="b78bb-266">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="b78bb-267">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="b78bb-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="b78bb-268">取得**CloudTable**物件，代表您要從中刪除 hello 實體參考 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="b78bb-268">Get a **CloudTable** object that represents a reference toohello table from which you are deleting hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="b78bb-269">建立刪除作業物件，其採用衍生自 **TableEntity** 的實體物件。</span><span class="sxs-lookup"><span data-stu-id="b78bb-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="b78bb-270">在此情況下，我們使用 hello **CustomerEntity**類別和 hello 區段中顯示資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)。</span><span class="sxs-lookup"><span data-stu-id="b78bb-270">In this case, we use hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="b78bb-271">hello 實體的**ETag**必須設定 tooa 有效的值。</span><span class="sxs-lookup"><span data-stu-id="b78bb-271">hello entity's **ETag** must be set tooa valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="b78bb-272">執行 hello 刪除作業。</span><span class="sxs-lookup"><span data-stu-id="b78bb-272">Execute hello delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="b78bb-273">傳遞顯示 hello 結果 toohello 檢視。</span><span class="sxs-lookup"><span data-stu-id="b78bb-273">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="b78bb-274">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="b78bb-274">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b78bb-275">在 [hello**加入檢視**] 對話方塊中，輸入**DeleteEntity** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="b78bb-275">On hello **Add View** dialog, enter **DeleteEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b78bb-276">開啟`DeleteEntity.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="b78bb-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. <span data-ttu-id="b78bb-277">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="b78bb-277">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b78bb-278">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b78bb-278">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="b78bb-279">執行 hello 應用程式，並選取**刪除實體**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="b78bb-279">Run hello application, and select **Delete entity** toosee results similar toohello following screen shot:</span></span>
  
    ![取得單一](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="b78bb-281">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b78bb-281">Next steps</span></span>
<span data-ttu-id="b78bb-282">檢視有關將資料儲存在 Azure 中的其他選項的詳細功能指南 toolearn。</span><span class="sxs-lookup"><span data-stu-id="b78bb-282">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="b78bb-283">開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b78bb-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="b78bb-284">開始使用 Azure 佇列儲存體和 Visual Studio 已連線的服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b78bb-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-queues.md)
