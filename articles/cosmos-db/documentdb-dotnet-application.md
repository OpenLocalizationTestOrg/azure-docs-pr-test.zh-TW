---
title: "Azure Cosmos DB 的 ASP.NET MVC 教學課程：Web 應用程式開發 | Microsoft Docs"
description: "ASP.NET MVC 教學課程 toocreate MVC web 應用程式使用 Azure Cosmos DB。 您將在託管於 Azure 網站的待辦事項應用程式儲存 JSON 和存取資料 - ASP NET MVC 教學課程逐步解說。"
keywords: "asp.net mvc 教學課程, web 應用程式開發, mvc web 應用程式, asp net mvc 教學課程逐步解說"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395809351"></a>ASP.NET MVC 教學課程：使用 Azure Cosmos DB 進行 Web 應用程式開發
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

toohighlight 如何有效率地，您可以利用 Azure Cosmos DB toostore，與查詢 JSON 文件，這篇文章提供端對端逐步解說顯示如何 toobuild 使用 Azure Cosmos DB 待辦事項應用程式。 hello 工作將會儲存為 Azure Cosmos DB 中的 JSON 文件。

![Hello todo 清單本教學課程-ASP NET MVC 教學課程逐步解說所建立的 MVC web 應用程式的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

本逐步解說會示範如何 toouse hello Azure Cosmos DB 服務 toostore 及存取資料從 Azure 上裝載的 ASP.NET MVC web 應用程式。 如果您想要尋求著重在 Azure Cosmos DB 的教學課程，而且不 hello ASP.NET MVC 元件，請參閱[建置 Azure Cosmos DB C# 主控台應用程式](documentdb-get-started.md)。

> [!TIP]
> 本教學課程假設您先前有過使用 ASP.NET MVC 和 Azure 網站的經驗。 如果您是新 tooASP.NET 或 hello[必要條件工具](#_Toc395637760)，我們建議您下載 hello 完整的範例專案，從[GitHub] [ GitHub]和中的 hello 指示此範例中。 一旦建立它，您可以檢閱此文件 toogain 的深入了解 hello hello hello 專案內容中的程式碼。
> 
> 

## <a name="_Toc395637760"></a>此資料庫教學課程的必要條件
這篇文章中的 hello 指示之前，您應該確定您擁有 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 

    或

    Hello 的本機安裝[Azure Cosmos DB 模擬器](local-emulator.md)。
* [Visual Studio 2017](http://www.visualstudio.com/)。  
* Microsoft Azure SDK for.NET 的 Visual Studio 2017，可透過 hello Visual Studio 安裝程式。

已使用 Microsoft Visual Studio 社群 2017年採取這篇文章中的所有 hello 螢幕擷取畫面。 如果您的系統設定的不同版本很可能您的螢幕和選項都不會完全，符合，但如果符合上述必要條件 hello 應該使用此解決方案。

## <a name="_Toc395637761"></a>步驟 1：建立 Azure Cosmos DB 資料庫帳戶
我們將從建立 Azure Cosmos DB 帳戶開始著手。 如果您已有 Azure Cosmos DB SQL (DocumentDB) 帳戶，或如果您使用 hello Azure Cosmos DB 模擬器本教學課程中，您可以跳過[建立新的 ASP.NET MVC 應用程式](#_Toc395637762)。

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
我們現在會逐步解說如何 toocreate 新的 ASP.NET MVC 應用程式從 hello 從頭。 

## <a name="_Toc395637762"></a>步驟 2：建立新的 ASP.NET MVC 應用程式

1. 在 Visual Studio 中的 hello**檔案**功能表上，點太**新增**，然後按一下**專案**。 hello**新專案** 對話方塊隨即出現。

2. 在 [hello**專案類型**] 窗格中，展開**範本**， **Visual C#**， **Web**，然後選取**ASP.NET Web 應用程式**.

      ![螢幕擷取畫面 hello 新增專案 對話方塊與 hello 反白顯示的 ASP.NET Web 應用程式專案類型](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. 在 [hello**名稱**] 方塊中，輸入 hello 名稱的 hello 專案。 本教學課程使用 hello 名稱"todo"。 如果您選擇 toouse 這以外的項目，然後每當本教學課程參 hello todo 命名空間，您需要 tooadjust hello 提供程式碼範例 toouse 任何您已命名為您的應用程式。 
4. 按一下**瀏覽**toonavigate toohello 資料夾位置，toocreate hello 專案，然後再按一下**確定**。
   
      hello**新的 ASP.NET Web 應用程式** 對話方塊隨即出現。
   
    ![Hello 反白顯示 hello MVC 應用程式範本 [新的 ASP.NET Web 應用程式] 對話方塊的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. 在 hello 範本 窗格中，選取  **MVC**。

6. 按一下**確定**，讓 Visual Studio 執行其動作周圍 scaffolding hello 空白 ASP.NET MVC 範本。 

          
7. 一旦完成 Visual Studio 建立 hello 未定案 MVC 應用程式會有空白的 ASP.NET 應用程式，您可以在本機執行。
   
    我們會略過執行 hello 專案在本機相信我們所有看到的 hello ASP.NET"Hello World"應用程式。 讓我們前往直線 tooadding Azure Cosmos DB toothis 專案並建置應用程式。

## <a name="_Toc395637767"></a>步驟 3： 加入 Azure Cosmos DB tooyour MVC web 應用程式專案
既然我們已經有大部分的 hello ASP.NET MVC 配管，我們需要針對此解決方案，讓我們協助 toohello 真正的目的，本教學課程，加入 Azure Cosmos DB tooour MVC web 應用程式。

1. hello Azure Cosmos DB.NET SDK 會封裝，並以 NuGet 封裝進行散發。 tooget hello Visual Studio 中的 NuGet 封裝，使用 Visual Studio 中的 hello NuGet 套件管理員中的 hello 專案上按一下滑鼠右鍵**方案總管 中**，然後按一下**管理 NuGet 封裝**。
   
    ![Hello 的螢幕擷取畫面以滑鼠右鍵按一下方案總管中，使用 管理 NuGet 封裝的反白顯示 hello web 應用程式專案的選項。](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    hello**管理 NuGet 封裝** 對話方塊隨即出現。
2. 在 hello NuGet**瀏覽**方塊中，輸入***Azure DocumentDB***。 （hello 封裝名稱尚未更新的 tooAzure Cosmos DB。）
   
    從 hello 結果中，安裝 hello **microsoft Microsoft.Azure.DocumentDB**封裝。 這會下載並安裝 hello Azure Cosmos DB 封裝，以及所有相依性，例如 Newtonsoft.Json。 按一下**確定**hello 中**預覽**視窗中，和**我接受**hello 中**授權接受**視窗 toocomplete hello 安裝。
   
    ![Hello 管理 NuGet 封裝 視窗，以 hello Microsoft Azure DocumentDB 用戶端程式庫反白顯示的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      或者，您可以使用 Package Manager Console tooinstall hello 套件 hello。 toodo，請在 hello**工具**功能表上，按一下  **NuGet 套件管理員**，然後按一下 **Package Manager Console**。 在 hello 提示字元中輸入下列 hello。
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. Hello 封裝安裝之後，您的 Visual Studio 方案應該類似下列兩個新的參考加入，Microsoft.Azure.Documents.Client 和 Newtonsoft.Json hello。
   
    ![Hello 兩個參考的螢幕擷取畫面加入 toohello JSON 資料專案在 方案總管](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>步驟 4： 設定 hello ASP.NET MVC 應用程式
現在讓我們加入 hello 模型、 檢視和控制器 toothis MVC 應用程式：

* [新增模型](#_Toc395637764)。
* [新增控制器](#_Toc395637765)。
* [新增檢視](#_Toc395637766)。

### <a name="_Toc395637764"></a>新增 JSON 資料模型
讓我們先建立 hello **M**在 MVC 中，hello 模型。 

1. 在**方案總管] 中**，以滑鼠右鍵按一下 hello**模型**資料夾中，按一下 [**新增**，然後按一下**類別**。
   
      hello**加入新項目** 對話方塊隨即出現。
2. 將您的新類別命名為 **Item.cs**，然後按一下 [新增]。 
3. 在這個新**Item.cs**檔案中，最後將之後 hello hello 面一行加入*使用陳述式*。
   
        using Newtonsoft.Json;
4. 現在，將此程式碼取代 
   
        public class Item
        {
        }
   
    以下列程式碼的 hello。
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    Azure Cosmos DB 中的所有資料都傳送 hello 線上，而且儲存成 JSON。 toocontrol hello 方式將物件序列化/還原序列化，您可以使用的 JSON.NET 的 hello **JsonProperty**屬性示 hello**項目**剛才所建立的類別。 您沒有**有**toodo 這但我想 tooensure 我屬性都會遵循 hello JSON camelCase 命名慣例。 
   
    不只可以您控制 hello 屬性名稱的 hello 格式時進入 JSON，但您可以完全重新命名.NET 屬性我如同以 hello**描述**屬性。 

### <a name="_Toc395637765"></a>新增控制器
會負責 hello **M**，現在讓我們來建立 hello **C**在 MVC 中，控制器類別。

1. 在**方案總管 中**，以滑鼠右鍵按一下 hello**控制站**資料夾中，按一下**新增**，然後按一下**控制器**。
   
    hello**新增 Scaffold**  對話方塊隨即出現。
2. 選取 Web API 5 控制器 - 空，然後按一下新增。
   
    ![Hello 以 hello MVC 5 控制器空反白顯示的選項加入 Scaffold 對話方塊的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. 將新的控制器命名為 **ItemController**
   
    ![Hello [加入控制器] 對話方塊的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    一旦建立 hello 檔案時，Visual Studio 方案看起來應該像 hello 下列 hello 新 ItemController.cs 檔案中與**方案總管 中**。 也會顯示 hello 稍早建立新 Item.cs 檔案。
   
    ![Hello Visual Studio 方案-與 hello 新 ItemController.cs 檔案，並反白顯示 Item.cs 檔案的 [方案總管] 的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    您可以關閉 ItemController.cs，再回來 tooit 更新版本。 

### <a name="_Toc395637766"></a>新增檢視
現在，讓我們來建立 hello **V**在 MVC 中，hello 檢視：

* [新增項目索引檢視](#AddItemIndexView)。
* [新增項目檢視](#AddNewIndexView)。
* [新增編輯項目檢視](#_Toc395888515)。

#### <a name="AddItemIndexView"></a>新增項目索引檢視
1. 在**方案總管] 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下空白的 hello**項目**加入 hello 時為您建立 Visual Studio 的資料夾**ItemController**舊版中，按一下 [**新增**，然後按一下**檢視**。
   
    ![顯示 hello 項目資料夾以反白顯示 hello 加入檢視命令，建立 Visual Studio 方案總管的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. 在 hello**加入檢視**對話方塊方塊中，執行下列 hello:
   
   * 在 hello**檢視名稱**方塊中，輸入***索引***。
   * 在 hello**範本**方塊中，選取***清單***。
   * 在 hello**模型類別**方塊中，選取***項目 (todo。模型）***。
   * 在 hello 版面配置頁面中，輸入***~/Views/Shared/_Layout.cshtml***。
     
   ![螢幕擷取畫面顯示 hello 新增檢視對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. 設定所有這些值之後，按一下 [新增]  ，並讓 Visual Studio 建立新的範本檢視。 一旦完成後，就會開啟 hello cshtml 檔案所建立。 因為我們將 tooit 稍後再回來，我們可以關閉 Visual Studio 中的該檔案。

#### <a name="AddNewIndexView"></a>新增項目檢視
我們建立類似 toohow**項目索引** 檢視中，現在我們將建立新的檢視，來建立新**項目**。

1. 在**方案總管 中**，以滑鼠右鍵按一下 hello**項目**資料夾再按一下**新增**，然後按一下**檢視**。
2. 在 hello**加入檢視**對話方塊方塊中，執行下列 hello:
   
   * 在 hello**檢視名稱**方塊中，輸入***建立***。
   * 在 hello**範本**方塊中，選取***建立***。
   * 在 hello**模型類別**方塊中，選取***項目 (todo。模型）***。
   * 在 hello 版面配置頁面中，輸入***~/Views/Shared/_Layout.cshtml***。
   * 按一下 [新增] 。
   
#### <a name="_Toc395888515"></a>新增編輯項目檢視
最後，會加入一個編輯的最後一個檢視和**項目**在 hello 與之前相同的方式。

1. 在**方案總管 中**，以滑鼠右鍵按一下 hello**項目**資料夾再按一下**新增**，然後按一下**檢視**。
2. 在 hello**加入檢視**對話方塊方塊中，執行下列 hello:
   
   * 在 hello**檢視名稱**方塊中，輸入***編輯***。
   * 在 hello**範本**方塊中，選取***編輯***。
   * 在 hello**模型類別**方塊中，選取***項目 (todo。模型）***。
   * 在 hello 版面配置頁面中，輸入***~/Views/Shared/_Layout.cshtml***。
   * 按一下 [新增] 。

完成之後，關閉所有 Visual Studio 中的 hello cshtml 文件，因為我們將稍後再回來 toothese 檢視。

## <a name="_Toc395637769"></a>步驟 5︰裝設 Azure Cosmos DB
既然已處理 hello 標準的 MVC 動作完成，讓我們來開啟 tooadding hello 程式碼的 Azure Cosmos DB。 

在本節中，我們會將 toohandle hello 後面的程式碼：

* [列出未完成項目](#_Toc395637770)。
* [新增項目](#_Toc395637771)。
* [編輯項目](#_Toc395637772)。

### <a name="_Toc395637770"></a>列出 MVC Web 應用程式中的未完成項目
hello 第一件事 toodo 這裡會加入包含所有 hello 邏輯 tooconnect tooand 使用 Azure Cosmos DB 的類別。 此教學課程中我們將會封裝此呼叫 DocumentDBRepository tooa 儲存機制類別中的所有邏輯。 

1. 在**方案總管 中**hello 專案上按一下滑鼠右鍵、 按一下**新增**，然後按一下**類別**。 Hello 新類別命名**DocumentDBRepository**按一下**新增**。
2. 在新建立的 hello **DocumentDBRepository**類別，然後將 hello 下列*using 陳述式*上方 hello*命名空間*宣告
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    現在，將此程式碼取代 
   
        public class DocumentDBRepository
        {
        }
   
    以下列程式碼的 hello。
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. 我們正在讀取組態中的某些值，因此開啟 hello **Web.config**應用程式的檔案並加入下列行下 hello hello `<AppSettings>` > 一節。
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. 現在，更新 hello 值*端點*和*authKey*使用 hello 金鑰刀鋒視窗中的 hello Azure 入口網站。 使用 hello **URI** hello 做為 hello 端點設定，並使用 hello hello 值的索引鍵 刀鋒視窗從**主索引鍵**，或**次要金鑰**從 hello 做為 hello hello 值的索引鍵 刀鋒視窗authKey 設定。

    會負責裝設 hello Azure Cosmos DB 儲存機制，現在讓我們來新增應用程式邏輯。

1. hello 首先我們要 toobe 無法 toodo 待辦事項清單應用程式與為 toodisplay hello 不完整的項目。  複製並貼上下列程式碼片段中任何位置的 hello hello **DocumentDBRepository**類別。
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. 開啟 hello **ItemController**我們稍早加入並新增下列 hello *using 陳述式*hello 命名空間宣告上方。
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    如果您專案不是"todo"，則您需要使用"todo tooupdate。模型 >。tooreflect hello 專案名稱。
   
    現在，將此程式碼取代
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    以下列程式碼的 hello。
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. 開啟**Global.asax.cs**並加入下列行 toohello hello **Application_Start**方法 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

此時您的解決方案應該能夠 toobuild 沒有發生任何錯誤。

如果您已執行 hello 應用程式現在，您將會進入 toohello **HomeController**和 hello**索引**該控制器的檢視。 這是我們選擇在 hello 開頭 hello MVC 範本專案的 hello 預設行為，但我們不想要 ！ 我們來變更 hello 路由這個 MVC 應用程式 tooalter 這種行為。

開啟***應用程式\_Start\RouteConfig.cs***並找出 hello 行開頭為 「 預設值:"並將它變更為下列 tooresemble hello。

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

這會告訴您擁有 hello URL toocontrol 中未指定值，如果 hello，而是路由行為的 ASP.NET MVC**首頁**，使用**項目**為 hello 控制站及使用者**索引**為 hello 檢視。

現在，如果您要執行 hello 應用程式，它會呼叫您**ItemController**這將會呼叫 toohello 儲存機制類別中，並使用 hello GetItems 方法 tooreturn 所有 hello 不完整的項目 toohello**檢視**\\**項目**\\**索引**檢視。 

如果建置並立即執行此專案，您現在應該會看到如下的內容。    

![Hello todo 清單 web 應用程式建立此資料庫的教學課程的螢幕擷取畫面](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>新增項目
讓我們將某些項目放入資料庫，讓我們有更多超過在空的方格窗格 toolook。

讓我們加入一些程式碼太 Azure Cosmos DB 中的 Azure Cosmos DBRepository 且 ItemController toopersist hello 記錄。

1. 新增下列方法 tooyour hello **DocumentDBRepository**類別。
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   這個方法只會採用傳遞 tooit 的物件，並將它保存在 Azure Cosmos DB。
2. 開啟 hello ItemController.cs 檔案並加入下列程式碼片段 hello 類別內的 hello。 這是 ASP.NET MVC 如何知道哪些 toodo hello**建立**動作。 在此情況下只呈現 hello 相關 Create.cshtml 稍早建立的檢視。
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    我們現在需要某些更多的程式碼，將會接受從 hello hello 提交此控制器中**建立**檢視。
3. 新增 hello 的程式碼 toohello ItemController.cs 類別，此控制站的表單 POST 哪些 toodo 告知 ASP.NET MVC 的下一個區塊。
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    此程式碼會呼叫 toohello DocumentDBRepository 中，並使用 hello CreateItemAsync 方法 toopersist hello 新 todo 項目 toohello 資料庫。 
   
    **安全性注意事項**: hello **ValidateAntiForgeryToken**屬性使用這裡 toohelp 保護此應用程式針對跨站台要求偽造攻擊。 多個 tooit 比只將這個屬性，檢視需要 toowork 與這個防偽語彙基元。 如需有關 hello 主旨，以及如何 tooimplement 這是否正確，請參閱範例[防止跨站台要求偽造][Preventing Cross-Site Request Forgery]。 hello 上所提供的原始程式碼[GitHub] [ GitHub]有 hello 完整實作的。
   
    **安全性注意事項**： 我們也會使用 hello**繫結**hello 方法參數 toohelp 屬性防止過度張貼攻擊。 如需詳細資訊，請參閱 [ASP.NET MVC 中的基本 CRUD 作業][Basic CRUD Operations in ASP.NET MVC]。

這總結 hello 所需的程式碼 tooadd 新項目 tooour 的資料庫。

### <a name="_Toc395637772"></a>編輯項目
沒有為我們的最後一件事 toodo，並且可 tooadd hello 能力 tooedit**項目**hello 資料庫和 toomark 來完成。 hello 編輯檢視已加入 toohello 專案，因此我們只需要 tooadd 部分的程式碼 tooour 控制器和 toohello **DocumentDBRepository**類別一次。

1. 新增下列 toohello hello **DocumentDBRepository**類別。
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    hello 的這些方法的第一個**GetItem**擷取項目從 Azure Cosmos DB 傳遞後 toohello **ItemController**然後在 toohello**編輯**檢視。
   
    hello hello 方法的第二個我們剛才加入取代 hello**文件**在 hello 版的 hello 與 Azure Cosmos DB**文件**hello 從傳入**ItemController**。
2. 新增下列 toohello hello **ItemController**類別。
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    hello 第一個方法會處理 hello Http GET，hello 使用者按一下時 hello**編輯**連結從 hello**索引**檢視。 此方法會提取[**文件**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx)從 Azure Cosmos 資料庫並將其傳遞 toohello**編輯**檢視。
   
    hello**編輯**檢視然後將執行 Http POST toohello **IndexController**。 
   
    我們加入了控制代碼傳遞更新的 hello 物件 tooAzure Cosmos DB toobe hello 第二個方法會保存在 hello 資料庫。

這就是它，是我們需要 toorun 我們的應用程式的所有項目，清單不完整**項目**，加入新**項目**，並編輯**項目**。

## <a name="_Toc395637773"></a>步驟 6： 在本機執行 hello 應用程式
tootest hello 應用程式在本機電腦，請勿 hello 遵循：

1. 在 Visual Studio 中偵錯模式 toobuild hello 應用程式中按 F5。 它應該建置 hello 應用程式，並啟動我們先前看過的 hello 空白格線頁的瀏覽器：
   
    ![Hello todo 清單 web 應用程式建立此資料庫的教學課程的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. 按一下 hello**新建**連結並新增值 toohello**名稱**和**描述**欄位。 保留 hello**已完成**核取方塊取消選取 新否則 hello**項目**將加入已完成狀態中，而且不會出現在 hello 初始清單上。
   
    ![Hello 建立檢視的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. 按一下**建立**而重新導向後 toohello**索引**檢視和您**項目**hello 清單中會出現。
   
    ![Hello 索引檢視的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    一些其他覺得可用 tooadd**項目**tooyour todo 清單。
    
4. 按一下**編輯**下一步 tooan**項目**hello 清單也會採取 toohello**編輯**檢視您可以在其中更新任何屬性的物件，包括 hello **完成**旗標。 如果您將標示 hello**完成**旗標，然後按一下**儲存**，hello**項目**hello 未完成的工作清單中已經移除了。
   
    ![Hello 勾選 hello 已完成方塊索引檢視的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. 一旦測試過 hello 應用程式，請按 Ctrl + F5 toostop 偵錯 hello 應用程式。 您已準備好 toodeploy ！

## <a name="_Toc395637774"></a>步驟 7： 部署的 hello 應用程式 tooAzure 應用程式服務 
既然您已擁有 hello 完整的應用程式可以使用 Azure Cosmos DB 正常運作我們 toodeploy 此 web 應用程式 tooAzure 應用程式服務。  

1. 中的 hello 專案上按一下滑鼠右鍵 toopublish 所有您需要 toodo 這個應用程式是**方案總管 中**按一下**發行**。
   
    ![Hello 方案總管 中的 發佈 選項的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. 在 hello**發行**對話方塊中，按一下  **Microsoft Azure App Service**，然後選取**建立新**toocreate 應用程式服務的設定檔，或是按一下**選取現有**toouse 現有的設定檔。

    ![Visual Studio 中的 [發佈] 對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. 如果您有現有的 Azure App Service 設定檔，請輸入您的訂用帳戶名稱。 使用 hello**檢視**篩選 toosort 由資源群組或資源類型，然後選取您的 Azure 應用程式服務。 
   
    ![Visual Studio 中的 [App Service] 對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. toocreate 新的 Azure 應用程式服務設定檔中，按一下**新建**在 hello**發行** 對話方塊。 在 hello**建立 App Service**  對話方塊中，輸入您的 Web 應用程式名稱和適當的訂用帳戶、 資源群組和應用程式服務方案，然後按一下 **建立**。

    ![Visual Studio 中的 [建立 App Service] 對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

幾秒後，Visual Studio 便會發佈 Web 應用程式並啟動瀏覽器，您可以在瀏覽器中看到您方便好用的應用程式已在 Azure 中執行！



## <a name="_Toc395637775"></a>接續步驟
恭喜！ 您只要建置您的第一個 ASP.NET MVC web 應用程式使用 Azure Cosmos DB 並發佈它 tooAzure。 hello hello 完成應用程式，包括 hello 詳細資料的原始碼和刪除功能未包含在此教學課程可以下載或複製從[GitHub][GitHub]。 因此如果您想要加入該 tooyour 應用程式中，抓取 hello 程式碼，並將它加入 toothis 應用程式。

tooadd 額外的功能 tooyour 應用程式中，檢閱 hello Api 可在 hello [Azure Cosmos DB.NET 程式庫](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)感覺可用 toocontribute toohello Azure Cosmos DB.NET 程式庫上[GitHub][GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
