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
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>開始使用 Azure 資料表儲存體和 Visual Studio 已連線的服務 (ASP.NET)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>概觀

Azure 資料表儲存體可讓您 toostore 大量結構化資料。 hello 服務是可接受來自內部和外部 hello Azure 雲端的已驗證的呼叫的 NoSQL 資料存放區。 Azure 資料表很適合儲存結構化、非關聯式資料。

本教學課程會示範 toowrite ASP.NET 為使用 Azure 資料表儲存體實體一些常見案例的程式碼。 這些案例包括建立資料表，以及新增、查詢和刪除資料表實體。 

##<a name="prerequisites"></a>必要條件

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>建立 MVC 控制器 

1. 在 hello**方案總管 中**，以滑鼠右鍵按一下**控制站**，並從 hello 內容功能表中，選取**加入控制器->** 。

    ![加入控制器 tooan ASP.NET MVC 應用程式](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. 在 hello**新增 Scaffold**對話方塊中，選取**MVC 5 控制器空白**，然後選取**新增**。

    ![指定 MVC 控制器類型](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. 在 hello**加入控制器**對話方塊中，名稱 hello 控制器*TablesController*，並選取**新增**。

    ![名稱 hello MVC 控制器](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. 新增下列 hello*使用*指示詞 toohello`TablesController.cs`檔案：

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>建立模型類別

中的 hello 範例的許多發行項使用**TableEntity**-衍生的類別呼叫**CustomerEntity**。 hello 步驟會引導您宣告這個類別做為模型類別：

1. 在 hello**方案總管 中**，以滑鼠右鍵按一下**模型**，並從 hello 內容功能表中，選取**新增類別->** 。

1. 在 hello**加入新項目**對話方塊中，名稱 hello 類別， **CustomerEntity**。

1. 開啟 hello`CustomerEntity.cs`檔並加入下列 hello**使用**指示詞：

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. 修改 hello 類別，以便完成後，請 hello 類別的宣告方式如下列程式碼的 hello 所示。 hello 類別會宣告稱為實體類別**CustomerEntity**使用 hello hello 資料列索引鍵為客戶的名字和姓氏 hello 資料分割索引鍵。

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

## <a name="create-a-table"></a>建立資料表

hello 下列步驟說明如何 toocreate 資料表：

> [!NOTE]
> 
> 本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`TablesController.cs`檔案。

1. 新增名為 **CreateTable** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. 在 hello **CreateTable**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. 取得 **CloudTableClient** 物件，代表表格服務用戶端。
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 取得**CloudTable**物件，表示參考 toohello 所需的資料表名稱。 hello **CloudTableClient.GetTableReference**方法不會針對資料表儲存體的要求。 不論是否 hello 資料表存在，則會傳回 hello 參考。 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. 呼叫 hello **CloudTable.CreateIfNotExists**方法 toocreate hello 資料表如果尚不存在。 hello **CloudTable.CreateIfNotExists**方法會傳回**true**如果 hello 資料表不存在，而且已成功建立。 否則，會傳回 **false**。    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. 更新 hello **ViewBag** hello hello 資料表名稱。

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**CreateTable** hello 檢視名稱，然後選取**新增**。

1. 開啟`CreateTable.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. 執行 hello 應用程式，並選取**建立資料表**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![建立資料表](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    如先前所述，hello **CloudTable.CreateIfNotExists**方法會傳回**true**只當 hello 資料表不存在，而且會建立。 因此，如果 hello 資料表存在時，您可以執行 hello 應用程式，hello 方法會傳回**false**。 toorun hello 應用程式多次，必須刪除 hello 資料表，才能再次執行 hello 應用程式。 正在刪除 hello 資料表可透過 hello **CloudTable.Delete**方法。 您也可以刪除 hello 資料表使用 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)或 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)。  

## <a name="add-an-entity-tooa-table"></a>加入實體 tooa 表

*實體*對應 tooC\#物件使用的自訂類別衍生自**TableEntity**。 tooadd 實體 tooa 資料表，建立一個類別來定義實體的 hello 屬性。 在本節中，您會看到如何使用的實體類別 toodefine hello hello 資料列索引鍵為客戶的名字和姓氏 hello 資料分割索引鍵。 在一起，實體的資料分割和資料列索引鍵可唯一識別 hello 資料表中的 hello 實體。 查詢具有相同分割區索引鍵的實體，其速度快於查詢具有不同分割區索引鍵的實體，但使用不同的資料分割索引鍵可提供更佳的延展性或平行作業。 應該儲存在 hello 表格服務的所有屬性，hello 屬性必須是支援的型別可公開設定和擷取值的公用屬性。
hello 實體類別*必須*宣告公用的無參數建構函式。

> [!NOTE]
> 
> 本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。

1. 開啟 hello`TablesController.cs`檔案。

1. 新增下列指示詞，因此的 hello hello 中的程式碼的 hello`TablesController.cs`檔案可以存取 hello **CustomerEntity**類別：

    ```csharp
    using StorageAspnet.Models;
    ```

1. 新增名為 **AddEntity** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. 在 hello **AddEntity**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. 取得 **CloudTableClient** 物件，代表表格服務用戶端。
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 取得**CloudTable**物件，代表要 tooadd hello 新實體參考 toohello 資料表 toowhich。 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. 具現化，並初始化 hello **CustomerEntity**類別。

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. 建立**TableOperation**插入 hello customer 實體的物件。

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. 執行呼叫 hello hello 插入作業**CloudTable.Execute**方法。 您可以藉由檢查 hello 確認 hello 作業結果的 hello **TableResult.HttpStatusCode**屬性。 2xx 狀態碼表示已成功處理 hello hello 用戶端要求的動作。 例如，成功插入新的實體會導致 HTTP 狀態碼 204，也就是說，hello 作業已成功處理，而且 hello 伺服器未傳回任何內容。

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. 更新 hello **ViewBag** hello 資料表名稱，與 hello 的 hello 插入作業的結果。

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**AddEntity** hello 檢視名稱，然後選取**新增**。

1. 開啟`AddEntity.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. 執行 hello 應用程式，並選取**加入實體**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![新增實體](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    您可以確認 hello 實體已加入 hello 區段中的 hello 步驟[取得單一實體](#get-a-single-entity)。 您也可以使用 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)tooview 所有 hello 出資料表的實體。

## <a name="add-a-batch-of-entities-tooa-table"></a>加入實體 tooa 資料表的批次

中可以加入 toobeing 太[一次新增一個實體 tooa 表](#add-an-entity-to-a-table)，您也可以加入實體批次中。 加入實體批次中可減少您的程式碼與 hello Azure 資料表服務之間的來回的 hello 數目。 hello 下列步驟說明如何 tooadd 多個實體 tooa 資料表具有單一 insert 作業：

> [!NOTE]
> 
> 本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。

1. 開啟 hello`TablesController.cs`檔案。

1. 新增名為 **AddEntity** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. 在 hello **AddEntities**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. 取得 **CloudTableClient** 物件，代表表格服務用戶端。
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 取得**CloudTable**物件，表示會持續 tooadd hello 新實體參考 toohello 資料表 toowhich。 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. 根據 hello 某些客戶物件具現化**CustomerEntity**模型類別 hello 區段中呈現[加入實體 tooa 表](#add-an-entity-to-a-table)。

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. 取得 **TableBatchOperation** 物件。

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. 加入實體 toohello 批次插入作業物件。

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. 執行呼叫 hello hello 批次插入作業**CloudTable.ExecuteBatch**方法。   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. hello **CloudTable.ExecuteBatch**方法會傳回一份**TableResult**物件其中每個**TableResult**物件可以檢查的 toodetermine hello 成功或失敗每個個別作業。 例如，傳遞 hello 清單 tooa 檢視，讓 hello 檢視顯示每個作業的 hello 結果。 
 
    ```csharp
    return View(results);
    ```

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**AddEntities** hello 檢視名稱，然後選取**新增**。

1. 開啟`AddEntities.cshtml`，並使它看起來類似下列 hello 加以修改。

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

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. 執行 hello 應用程式，並選取**加入實體**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![新增實體](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    您可以確認 hello 實體已加入 hello 區段中的 hello 步驟[取得單一實體](#get-a-single-entity)。 您也可以使用 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)tooview 所有 hello 出資料表的實體。

## <a name="get-a-single-entity"></a>取得單一實體

本節說明如何從資料表使用的單一實體 tooget hello 實體的資料列索引鍵和資料分割索引鍵。 

> [!NOTE]
> 
> 本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)，並使用來自資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)。 

1. 開啟 hello`TablesController.cs`檔案。

1. 新增名為 **GetSingle** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. 在 hello **GetSingle**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. 取得 **CloudTableClient** 物件，代表表格服務用戶端。
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 取得**CloudTable**物件，代表擷取 hello 實體參考 toohello 資料表。 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. 建立擷取作業物件，其採用衍生自 **TableEntity** 的實體物件。 hello 第一個參數是 hello *partitionKey*，hello 第二個參數則是 hello *rowKey*。 使用 hello **CustomerEntity**類別和 hello 區段中顯示資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)，下列程式碼片段查詢 hello 資料表 hello **CustomerEntity**實體*partitionKey* "Smith"的值和*rowKey* "Ben"的值：

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. 執行 hello 擷取作業。   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. 傳遞顯示 hello 結果 toohello 檢視。

    ```csharp
    return View(result);
    ```

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**GetSingle** hello 檢視名稱，然後選取**新增**。

1. 開啟`GetSingle.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

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

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. 執行 hello 應用程式，並選取**取得單一**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![取得單一](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>取得資料分割中的所有實體

Hello 區段中所述[加入實體 tooa 表](#add-an-entity-to-a-table)，hello 組合的磁碟分割和資料列索引鍵會唯一識別資料表中的實體。 相較於查詢具有不同資料分割索引鍵的實體，查詢具有相同資料分割索引鍵的實體速度會較快。 本節說明如何 tooquery 所有 hello 實體，從指定的資料分割的資料表。  

> [!NOTE]
> 
> 本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)，並使用來自資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)。 

1. 開啟 hello`TablesController.cs`檔案。

1. 新增名為 **GetPartition** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. 在 hello **GetPartition**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. 取得 **CloudTableClient** 物件，代表表格服務用戶端。
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 取得**CloudTable**物件，代表擷取 hello 實體參考 toohello 資料表。 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. 具現化**TableQuery**物件，指定在 hello hello 查詢**其中**子句。 使用 hello **CustomerEntity**類別和 hello 區段中顯示資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)，hello 下列程式碼片段查詢 hello 資料表的所有實體，其中 hello **PartitionKey** （客戶的最後一個名稱） 的值為"Smith":

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. 在迴圈中，呼叫 hello **CloudTable.ExecuteQuerySegmented**傳入 hello 上一個步驟中的 hello 您具現化的查詢物件的方法。  hello **CloudTable.ExecuteQuerySegmented**方法會傳回**TableContinuationToken**物件-當**null** -表示沒有多個實體tooretrieve。 Hello 迴圈內使用另一個迴圈 tooiterate over hello 傳回實體。 在下列程式碼範例的 hello，每個傳回的實體會加入 tooa 清單。 一次 hello 迴圈結束，hello 清單會傳遞 tooa 檢視顯示： 

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

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**GetPartition** hello 檢視名稱，然後選取**新增**。

1. 開啟`GetPartition.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

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

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. 執行 hello 應用程式，並選取**取得分割區**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![取得資料分割](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>刪除實體

本節說明如何 toodelete 資料表中的實體。

> [!NOTE]
> 
> 本節假設您已完成中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)，並使用來自資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)。 

1. 開啟 hello`TablesController.cs`檔案。

1. 新增名為 **DeleteEntity** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. 在 hello **DeleteEntity**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. 取得 **CloudTableClient** 物件，代表表格服務用戶端。
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 取得**CloudTable**物件，代表您要從中刪除 hello 實體參考 toohello 資料表。 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. 建立刪除作業物件，其採用衍生自 **TableEntity** 的實體物件。 在此情況下，我們使用 hello **CustomerEntity**類別和 hello 區段中顯示資料[加入實體 tooa 資料表的批次](#add-a-batch-of-entities-to-a-table)。 hello 實體的**ETag**必須設定 tooa 有效的值。  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. 執行 hello 刪除作業。   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. 傳遞顯示 hello 結果 toohello 檢視。

    ```csharp
    return View(result);
    ```

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**資料表**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**DeleteEntity** hello 檢視名稱，然後選取**新增**。

1. 開啟`DeleteEntity.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

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

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. 執行 hello 應用程式，並選取**刪除實體**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![取得單一](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>後續步驟
檢視有關將資料儲存在 Azure 中的其他選項的詳細功能指南 toolearn。

  * [開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET)](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [開始使用 Azure 佇列儲存體和 Visual Studio 已連線的服務 (ASP.NET)](../storage/vs-storage-aspnet-getting-started-queues.md)
