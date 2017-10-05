---
title: "開始使用 Azure 資料表儲存體和 Visual Studio 已連線的服務 (ASP.NET) | Microsoft Docs"
description: "在使用 Visual Studio 已連線的服務連接到儲存體帳戶之後，如何在 Visual Studio ASP.NET 專案中開始使用 Azure 資料表儲存體"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: d9cb32483d3f582bbeb0ccc6a204a8b6d9ea5c96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="cded8-103">開始使用 Azure 資料表儲存體和 Visual Studio 已連線的服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="cded8-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="cded8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="cded8-104">Overview</span></span>

<span data-ttu-id="cded8-105">Azure 資料表儲存體可讓您儲存大量的結構化資料。</span><span class="sxs-lookup"><span data-stu-id="cded8-105">Azure Table storage enables you to store large amounts of structured data.</span></span> <span data-ttu-id="cded8-106">此服務是一個 NoSQL 資料存放區，接受來自 Azure 雲端內外經過驗證的呼叫。</span><span class="sxs-lookup"><span data-stu-id="cded8-106">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="cded8-107">Azure 資料表很適合儲存結構化、非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="cded8-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="cded8-108">本教學課程說明如何使用 Azure 表格儲存體實體撰寫一些常見案例的 ASP.NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="cded8-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="cded8-109">這些案例包括建立資料表，以及新增、查詢和刪除資料表實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="cded8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cded8-110">Prerequisites</span></span>

* [<span data-ttu-id="cded8-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cded8-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="cded8-112">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="cded8-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="cded8-113">建立 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="cded8-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="cded8-114">在 [方案總管] 中，用滑鼠右鍵按一下 [控制器]，然後從內容功能表中選取 [新增] > [控制器]。</span><span class="sxs-lookup"><span data-stu-id="cded8-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![將控制器新增至 ASP.NET MVC 應用程式](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="cded8-116">在 [Add Scaffold] 對話方塊中，按一下 [MVC 5 Controller - Empty]然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cded8-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![指定 MVC 控制器類型](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="cded8-118">在 [新增控制器] 對話方塊中，將控制器命名為 TablesController，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cded8-118">On the **Add Controller** dialog, name the controller *TablesController*, and select **Add**.</span></span>

    ![命名 MVC 控制器](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="cded8-120">將下列 using 指示詞新增至 `TablesController.cs` 檔案：</span><span class="sxs-lookup"><span data-stu-id="cded8-120">Add the following *using* directives to the `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="cded8-121">建立模型類別</span><span class="sxs-lookup"><span data-stu-id="cded8-121">Create a model class</span></span>

<span data-ttu-id="cded8-122">本文中的許多範例使用 **TableEntity**衍生的類別，稱為 **CustomerEntity**。</span><span class="sxs-lookup"><span data-stu-id="cded8-122">Many of the examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="cded8-123">下列步驟會引導您宣告這個類別做為模型類別︰</span><span class="sxs-lookup"><span data-stu-id="cded8-123">The following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="cded8-124">在 [方案總管] 中，用滑鼠右鍵按一下 [模型]，然後從內容功能表中選取 [新增] > [類別]。</span><span class="sxs-lookup"><span data-stu-id="cded8-124">In the **Solution Explorer**, right-click **Models**, and, from the context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="cded8-125">在 [新增項目] 對話方塊中，將類別命名為 **CustomerEntity**。</span><span class="sxs-lookup"><span data-stu-id="cded8-125">On the **Add New Item** dialog, name the class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="cded8-126">開啟 `CustomerEntity.cs` 檔案，並新增下列 using 指示詞：</span><span class="sxs-lookup"><span data-stu-id="cded8-126">Open the `CustomerEntity.cs` file, and add the following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="cded8-127">修改類別，以便在完成時，這個類別會如下列程式碼所示宣告。</span><span class="sxs-lookup"><span data-stu-id="cded8-127">Modify the class so that, when finished, the class is declared as in the following code.</span></span> <span data-ttu-id="cded8-128">類別使用客戶名字作為資料列索引鍵、並使用姓氏作為資料分割索引鍵的，宣告一個稱為 **CustomerEntity** 的實體類別。</span><span class="sxs-lookup"><span data-stu-id="cded8-128">The class declares an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

## <a name="create-a-table"></a><span data-ttu-id="cded8-129">建立資料表</span><span class="sxs-lookup"><span data-stu-id="cded8-129">Create a table</span></span>

<span data-ttu-id="cded8-130">下列步驟說明如何建立資料表：</span><span class="sxs-lookup"><span data-stu-id="cded8-130">The following steps illustrate how to create a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="cded8-131">本章節假設您已完成[設定開發環境](#set-up-the-development-environment)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="cded8-131">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="cded8-132">開啟 `TablesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="cded8-132">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="cded8-133">新增名為 **CreateTable** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="cded8-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="cded8-134">在 **CreateTable** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cded8-134">Within the **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="cded8-135">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="cded8-135">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="cded8-136">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="cded8-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="cded8-137">取得 **CloudTable** 物件，代表所需資料表名稱的參考。</span><span class="sxs-lookup"><span data-stu-id="cded8-137">Get a **CloudTable** object that represents a reference to the desired table name.</span></span> <span data-ttu-id="cded8-138">**CloudTableClient.GetTableReference** 方法不會進行對表格儲存體的要求。</span><span class="sxs-lookup"><span data-stu-id="cded8-138">The **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="cded8-139">無論資料表是否存在都會傳回參考。</span><span class="sxs-lookup"><span data-stu-id="cded8-139">The reference is returned whether or not the table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="cded8-140">呼叫 **CloudTable.CreateIfNotExists** 方法來建立資料表 (如果尚不存在)。</span><span class="sxs-lookup"><span data-stu-id="cded8-140">Call the **CloudTable.CreateIfNotExists** method to create the table if it does not yet exist.</span></span> <span data-ttu-id="cded8-141">如果容器不存在且已成功建立，則 **CloudTable.CreateIfNotExists** 方法會傳回 **true**。</span><span class="sxs-lookup"><span data-stu-id="cded8-141">The **CloudTable.CreateIfNotExists** method returns **true** if the table does not exist, and is successfully created.</span></span> <span data-ttu-id="cded8-142">否則，會傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="cded8-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="cded8-143">使用資料表的名稱更新 **ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="cded8-143">Update the **ViewBag** with the name of the table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="cded8-144">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [資料表]，然後從內容功能表中選取 [新增] > [檢視]。</span><span class="sxs-lookup"><span data-stu-id="cded8-144">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="cded8-145">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **CreateTable**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cded8-145">On the **Add View** dialog, enter **CreateTable** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="cded8-146">開啟 `CreateTable.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="cded8-146">Open `CreateTable.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="cded8-147">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="cded8-147">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="cded8-148">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="cded8-148">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="cded8-149">執行應用程式，並選取 **Create table** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="cded8-149">Run the application, and select **Create table** to see results similar to the following screen shot:</span></span>
  
    ![建立資料表](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="cded8-151">如前所述，僅當資料表不存在且已建立時，**CloudTable.CreateIfNotExists** 方法才會傳回 **true**。</span><span class="sxs-lookup"><span data-stu-id="cded8-151">As mentioned previously, the **CloudTable.CreateIfNotExists** method returns **true** only when the table doesn't exist and is created.</span></span> <span data-ttu-id="cded8-152">因此，如果您在資料表已存在時執行應用程式，此方法會傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="cded8-152">Therefore, if you run the app when the table exists, the method returns **false**.</span></span> <span data-ttu-id="cded8-153">若要多次執行應用程式，您必須先刪除資料表後，才能再次執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="cded8-153">To run the app multiple times, you must delete the table before running the app again.</span></span> <span data-ttu-id="cded8-154">可以透過完成 **CloudTable.Delete** 方法來刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="cded8-154">Deleting the table can be done via the **CloudTable.Delete** method.</span></span> <span data-ttu-id="cded8-155">您也可以使用 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)或 [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)來刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="cded8-155">You can also delete the table using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="cded8-156">將實體加入至資料表</span><span class="sxs-lookup"><span data-stu-id="cded8-156">Add an entity to a table</span></span>

<span data-ttu-id="cded8-157">使用衍生自 **TableEntity** 的自訂類別，將實體對應至 C\# 物件。</span><span class="sxs-lookup"><span data-stu-id="cded8-157">*Entities* map to C\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="cded8-158">若要將實體新增至資料表，請建立一個類別來定義實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="cded8-158">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="cded8-159">在本節中，您將了解如何定義一個使用客戶名字作為資料列索引鍵、並使用姓氏作為資料分割索引鍵的實體類別。</span><span class="sxs-lookup"><span data-stu-id="cded8-159">In this section, you'll see how to define an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="cded8-160">實體的資料分割索引鍵和資料列索引鍵共同唯一識別資料表中的實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-160">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="cded8-161">查詢具有相同分割區索引鍵的實體，其速度快於查詢具有不同分割區索引鍵的實體，但使用不同的資料分割索引鍵可提供更佳的延展性或平行作業。</span><span class="sxs-lookup"><span data-stu-id="cded8-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="cded8-162">應該儲存在資料表服務中的任何屬性，都必須是公開設定和擷取值之支援類型的公用屬性。</span><span class="sxs-lookup"><span data-stu-id="cded8-162">For any property that should be stored in the table service, the property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="cded8-163">實體類別必須宣告公用的無參數建構函式。</span><span class="sxs-lookup"><span data-stu-id="cded8-163">The entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="cded8-164">本章節假設您已完成[設定開發環境](#set-up-the-development-environment)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="cded8-164">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="cded8-165">開啟 `TablesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="cded8-165">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="cded8-166">新增下列指示詞，以便 `TablesController.cs` 檔案中的程式碼可以存取 **CustomerEntity** 類別︰</span><span class="sxs-lookup"><span data-stu-id="cded8-166">Add the following directive so that the code in the `TablesController.cs` file can access the **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="cded8-167">新增名為 **AddEntity** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="cded8-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="cded8-168">在 **AddEntity** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cded8-168">Within the **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="cded8-169">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="cded8-169">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="cded8-170">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="cded8-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="cded8-171">取得 **CloudTable** 物件，其代表您要新增新實體的資料表之參考。</span><span class="sxs-lookup"><span data-stu-id="cded8-171">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="cded8-172">具現化及初始化 **CustomerEntity** 類別。</span><span class="sxs-lookup"><span data-stu-id="cded8-172">Instantiate and initialize the **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="cded8-173">建立 **TableOperation** 物件，以插入客戶實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-173">Create a **TableOperation** object that inserts the customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="cded8-174">呼叫 **CloudTable.Execute** 方法以執行插入作業。</span><span class="sxs-lookup"><span data-stu-id="cded8-174">Execute the insert operation by calling the **CloudTable.Execute** method.</span></span> <span data-ttu-id="cded8-175">您可以檢查 **TableResult.HttpStatusCode** 屬性，以確認作業的結果。</span><span class="sxs-lookup"><span data-stu-id="cded8-175">You can verify the result of the operation by inspecting the **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="cded8-176">狀態碼 2xx 表示已成功處理用戶端所要求的動作。</span><span class="sxs-lookup"><span data-stu-id="cded8-176">A status code of 2xx indicates the action requested by the client was processed successfully.</span></span> <span data-ttu-id="cded8-177">例如，成功插入新實體會造成 HTTP 狀態碼 204，這表示已成功處理作業且伺服器未傳回任何內容。</span><span class="sxs-lookup"><span data-stu-id="cded8-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that the operation was successfully processed and the server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="cded8-178">使用資料表名稱以及插入作業的結果更新 **ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="cded8-178">Update the **ViewBag** with the table name, and the results of the insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="cded8-179">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [資料表]，然後從內容功能表中選取 [新增] > [檢視]。</span><span class="sxs-lookup"><span data-stu-id="cded8-179">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="cded8-180">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **AddEntity**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cded8-180">On the **Add View** dialog, enter **AddEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="cded8-181">開啟 `AddEntity.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="cded8-181">Open `AddEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="cded8-182">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="cded8-182">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="cded8-183">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="cded8-183">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="cded8-184">執行應用程式，並選取 **Add entity** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="cded8-184">Run the application, and select **Add entity** to see results similar to the following screen shot:</span></span>
  
    ![新增實體](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="cded8-186">您可以確認實體是由章節[取得單一實體](#get-a-single-entity)中的步驟所新增。</span><span class="sxs-lookup"><span data-stu-id="cded8-186">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="cded8-187">您也可以使用 [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)檢視資料表中的所有實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-187">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-to-a-table"></a><span data-ttu-id="cded8-188">將一批實體新增至資料表</span><span class="sxs-lookup"><span data-stu-id="cded8-188">Add a batch of entities to a table</span></span>

<span data-ttu-id="cded8-189">除了能夠[一次將一個實體新增至一個資料表](#add-an-entity-to-a-table)，您也可以分批新增實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-189">In addition to being able to [add an entity to a table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="cded8-190">在批次中新增實體可減少程式碼與 Azure 資料表服務之間的來回行程次數。</span><span class="sxs-lookup"><span data-stu-id="cded8-190">Adding entities in batch reduces the number of round-trips between your code and the Azure table service.</span></span> <span data-ttu-id="cded8-191">下列步驟說明如何使用單一插入作業將多個實體新增至資料表：</span><span class="sxs-lookup"><span data-stu-id="cded8-191">The following steps illustrate how to add multiple entities to a table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="cded8-192">本章節假設您已完成[設定開發環境](#set-up-the-development-environment)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="cded8-192">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="cded8-193">開啟 `TablesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="cded8-193">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="cded8-194">新增名為 **AddEntity** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="cded8-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="cded8-195">在 **AddEntity** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cded8-195">Within the **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="cded8-196">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="cded8-196">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="cded8-197">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="cded8-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="cded8-198">取得 **CloudTable** 物件，其代表您要新增新實體的資料表之參考。</span><span class="sxs-lookup"><span data-stu-id="cded8-198">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="cded8-199">根據[將實體新增至資料表](#add-an-entity-to-a-table)章節中呈現的 **CustomerEntity** 模型類別具現化某些客戶物件。</span><span class="sxs-lookup"><span data-stu-id="cded8-199">Instantiate some customer objects based on the **CustomerEntity** model class presented in the section, [Add an entity to a table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="cded8-200">取得 **TableBatchOperation** 物件。</span><span class="sxs-lookup"><span data-stu-id="cded8-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="cded8-201">將實體新增至批次插入作業物件。</span><span class="sxs-lookup"><span data-stu-id="cded8-201">Add entities to the batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="cded8-202">呼叫 **CloudTable.ExecuteBatch** 方法以執行批次插入作業。</span><span class="sxs-lookup"><span data-stu-id="cded8-202">Execute the batch insert operation by calling the **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="cded8-203">**CloudTable.ExecuteBatch** 方法會傳回一份 **TableResult** 物件，可以檢查其中每個 **TableResult** 物件來判定各項操作的成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="cded8-203">The **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined to determine the success or failure of each individual operation.</span></span> <span data-ttu-id="cded8-204">例如，將清單傳遞到檢視，讓檢視顯示每個作業的結果。</span><span class="sxs-lookup"><span data-stu-id="cded8-204">For this example, pass the list to a view and let the view display the results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="cded8-205">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [資料表]，然後從內容功能表中選取 [新增] > [檢視]。</span><span class="sxs-lookup"><span data-stu-id="cded8-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="cded8-206">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **AddEntity**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cded8-206">On the **Add View** dialog, enter **AddEntities** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="cded8-207">開啟 `AddEntities.cshtml` 並加以修改，以便其如下列所示。</span><span class="sxs-lookup"><span data-stu-id="cded8-207">Open `AddEntities.cshtml`, and modify it so that it looks like the following.</span></span>

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

1. <span data-ttu-id="cded8-208">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="cded8-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="cded8-209">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="cded8-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="cded8-210">執行應用程式，並選取 **Add entity** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="cded8-210">Run the application, and select **Add entities** to see results similar to the following screen shot:</span></span>
  
    ![新增實體](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="cded8-212">您可以確認實體是由章節[取得單一實體](#get-a-single-entity)中的步驟所新增。</span><span class="sxs-lookup"><span data-stu-id="cded8-212">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="cded8-213">您也可以使用 [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)檢視資料表中的所有實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-213">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="cded8-214">取得單一實體</span><span class="sxs-lookup"><span data-stu-id="cded8-214">Get a single entity</span></span>

<span data-ttu-id="cded8-215">本節將說明如何使用實體的資料列索引鍵和資料分割索引鍵，從資料表取得單一實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-215">This section illustrates how to get a single entity from a table using the entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="cded8-216">本節假設您已完成[設定開發環境](#set-up-the-development-environment)中的步驟，並使用來自[將一批實體新增至資料表](#add-a-batch-of-entities-to-a-table)的資料。</span><span class="sxs-lookup"><span data-stu-id="cded8-216">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="cded8-217">開啟 `TablesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="cded8-217">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="cded8-218">新增名為 **GetSingle** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="cded8-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="cded8-219">在 **GetSingle** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cded8-219">Within the **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="cded8-220">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="cded8-220">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="cded8-221">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="cded8-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="cded8-222">取得 **CloudTable** 物件，其代表您要擷取實體的資料表之參考。</span><span class="sxs-lookup"><span data-stu-id="cded8-222">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="cded8-223">建立擷取作業物件，其採用衍生自 **TableEntity** 的實體物件。</span><span class="sxs-lookup"><span data-stu-id="cded8-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="cded8-224">第一個參數是 partitionKey，而第二個參數是 rowKey。</span><span class="sxs-lookup"><span data-stu-id="cded8-224">The first parameter is the *partitionKey*, and the second parameter is the *rowKey*.</span></span> <span data-ttu-id="cded8-225">使用[將一批實體新增至資料表](#add-a-batch-of-entities-to-a-table)一節中顯示的 **CustomerEntity** 類別和資料，下列程式碼片段可查詢資料表中是否有 *partitionKey* 值為 "Smith" 且 rowKey 值為 "Ben"的 **CustomerEntity** 實體：</span><span class="sxs-lookup"><span data-stu-id="cded8-225">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="cded8-226">執行擷取作業。</span><span class="sxs-lookup"><span data-stu-id="cded8-226">Execute the retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="cded8-227">將結果傳遞至顯示的檢視。</span><span class="sxs-lookup"><span data-stu-id="cded8-227">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="cded8-228">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [資料表]，然後從內容功能表中選取 [新增] > [檢視]。</span><span class="sxs-lookup"><span data-stu-id="cded8-228">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="cded8-229">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **GetSingle**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cded8-229">On the **Add View** dialog, enter **GetSingle** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="cded8-230">開啟 `GetSingle.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="cded8-230">Open `GetSingle.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="cded8-231">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="cded8-231">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="cded8-232">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="cded8-232">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="cded8-233">執行應用程式，並選取 **Get Single** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="cded8-233">Run the application, and select **Get Single** to see results similar to the following screen shot:</span></span>
  
    ![取得單一](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="cded8-235">取得資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="cded8-235">Get all entities in a partition</span></span>

<span data-ttu-id="cded8-236">如[將實體加入至資料表](#add-an-entity-to-a-table)章節中所述，資料分割和資料列索引鍵的組合唯一識別資料表中的實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-236">As mentioned in the section, [Add an entity to a table](#add-an-entity-to-a-table), the combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="cded8-237">相較於查詢具有不同資料分割索引鍵的實體，查詢具有相同資料分割索引鍵的實體速度會較快。</span><span class="sxs-lookup"><span data-stu-id="cded8-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="cded8-238">本節將說明如何從指定的資料分割中查詢所有實體的資料表。</span><span class="sxs-lookup"><span data-stu-id="cded8-238">This section illustrates how to query a table for all the entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="cded8-239">本節假設您已完成[設定開發環境](#set-up-the-development-environment)中的步驟，並使用來自[將一批實體新增至資料表](#add-a-batch-of-entities-to-a-table)的資料。</span><span class="sxs-lookup"><span data-stu-id="cded8-239">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="cded8-240">開啟 `TablesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="cded8-240">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="cded8-241">新增名為 **GetPartition** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="cded8-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="cded8-242">在 **GetPartition** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cded8-242">Within the **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="cded8-243">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="cded8-243">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="cded8-244">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="cded8-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="cded8-245">取得 **CloudTable** 物件，其代表您要擷取實體的資料表之參考。</span><span class="sxs-lookup"><span data-stu-id="cded8-245">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="cded8-246">具現化 **TableQuery** 物件，以在 **Where** 子句中指定查詢。</span><span class="sxs-lookup"><span data-stu-id="cded8-246">Instantiate a **TableQuery** object specifying the query in the **Where** clause.</span></span> <span data-ttu-id="cded8-247">使用 **CustomerEntity** 類別和[將資料表新增至實體批次](#add-a-batch-of-entities-to-a-table)章節中顯示的資料，下列程式碼片段會查詢所有實體的資料表，其中 **PartitionKey** (客戶的姓氏) 的值為 "Smith":</span><span class="sxs-lookup"><span data-stu-id="cded8-247">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a all entities where the **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="cded8-248">在迴圈內呼叫 **CloudTable.ExecuteQuerySegmented** 方法，以傳遞您在上一個步驟中具現化的查詢物件。</span><span class="sxs-lookup"><span data-stu-id="cded8-248">Within a loop, call the **CloudTable.ExecuteQuerySegmented** method passing the query object you instantiated in the previous step.</span></span>  <span data-ttu-id="cded8-249">**CloudTable.ExecuteQuerySegmented** 方法會傳回 **TableContinuationToken** 物件 - 若為 **null**，表示再也沒有要擷取的實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-249">The **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities to retrieve.</span></span> <span data-ttu-id="cded8-250">在迴圈內，使用另一個迴圈來逐一查看所傳回的實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-250">Within the loop, use another loop to iterate over the returned entities.</span></span> <span data-ttu-id="cded8-251">在下列程式碼範例中，每個傳回的實體都會新增至清單。</span><span class="sxs-lookup"><span data-stu-id="cded8-251">In the following code example, each returned entity is added to a list.</span></span> <span data-ttu-id="cded8-252">一旦迴圈結束後，清單會傳遞至檢視顯示︰</span><span class="sxs-lookup"><span data-stu-id="cded8-252">Once the loop ends, the list is passed to a view for display:</span></span> 

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

1. <span data-ttu-id="cded8-253">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [資料表]，然後從內容功能表中選取 [新增] > [檢視]。</span><span class="sxs-lookup"><span data-stu-id="cded8-253">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="cded8-254">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **GetPartition**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cded8-254">On the **Add View** dialog, enter **GetPartition** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="cded8-255">開啟 `GetPartition.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="cded8-255">Open `GetPartition.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="cded8-256">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="cded8-256">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="cded8-257">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="cded8-257">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="cded8-258">執行應用程式，並選取 **Get Partition** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="cded8-258">Run the application, and select **Get Partition** to see results similar to the following screen shot:</span></span>
  
    ![取得資料分割](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="cded8-260">刪除實體</span><span class="sxs-lookup"><span data-stu-id="cded8-260">Delete an entity</span></span>

<span data-ttu-id="cded8-261">本節說明如何從資料表刪除實體。</span><span class="sxs-lookup"><span data-stu-id="cded8-261">This section illustrates how to delete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="cded8-262">本節假設您已完成[設定開發環境](#set-up-the-development-environment)中的步驟，並使用來自[將一批實體新增至資料表](#add-a-batch-of-entities-to-a-table)的資料。</span><span class="sxs-lookup"><span data-stu-id="cded8-262">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="cded8-263">開啟 `TablesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="cded8-263">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="cded8-264">新增名為 **DeleteEntity** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="cded8-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="cded8-265">在 **DeleteEntity** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cded8-265">Within the **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="cded8-266">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="cded8-266">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="cded8-267">取得 **CloudTableClient** 物件，代表表格服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="cded8-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="cded8-268">取得 **CloudTable** 物件，其代表您要刪除實體的資料表之參考。</span><span class="sxs-lookup"><span data-stu-id="cded8-268">Get a **CloudTable** object that represents a reference to the table from which you are deleting the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="cded8-269">建立刪除作業物件，其採用衍生自 **TableEntity** 的實體物件。</span><span class="sxs-lookup"><span data-stu-id="cded8-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="cded8-270">在此案例中，我們使用[將一批實體新增至資料表](#add-a-batch-of-entities-to-a-table)一節中出現的 **CustomerEntity** 類別和資料。</span><span class="sxs-lookup"><span data-stu-id="cded8-270">In this case, we use the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="cded8-271">實體的 **ETag** 必須設為有效的值。</span><span class="sxs-lookup"><span data-stu-id="cded8-271">The entity's **ETag** must be set to a valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="cded8-272">執行刪除作業。</span><span class="sxs-lookup"><span data-stu-id="cded8-272">Execute the delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="cded8-273">將結果傳遞至顯示的檢視。</span><span class="sxs-lookup"><span data-stu-id="cded8-273">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="cded8-274">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [資料表]，然後從內容功能表中選取 [新增] > [檢視]。</span><span class="sxs-lookup"><span data-stu-id="cded8-274">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="cded8-275">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **DeleteEntity**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cded8-275">On the **Add View** dialog, enter **DeleteEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="cded8-276">開啟 `DeleteEntity.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="cded8-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="cded8-277">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="cded8-277">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="cded8-278">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="cded8-278">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="cded8-279">執行應用程式，並選取 **Delete entity** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="cded8-279">Run the application, and select **Delete entity** to see results similar to the following screen shot:</span></span>
  
    ![取得單一](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="cded8-281">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cded8-281">Next steps</span></span>
<span data-ttu-id="cded8-282">如需了解 Azure 中的其他資料儲存選項，請檢視更多功能指南。</span><span class="sxs-lookup"><span data-stu-id="cded8-282">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="cded8-283">開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="cded8-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="cded8-284">開始使用 Azure 佇列儲存體和 Visual Studio 已連線的服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="cded8-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
