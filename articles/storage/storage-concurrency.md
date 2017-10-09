---
title: "aaaManaging Microsoft Azure 儲存體中的並行存取"
description: "Toomanage 的並行存取如何 hello Blob、 佇列、 表格和檔案服務"
services: storage
documentationcenter: 
author: jasontang501
manager: tadb
editor: tysonn
ms.assetid: cc6429c4-23ee-46e3-b22d-50dd68bd4680
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: jasontang501
ms.openlocfilehash: 277fbbb880906da6be67b2267ed5c8e457455bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-concurrency-in-microsoft-azure-storage"></a>管理 Microsoft Azure 儲存體中的並行存取
## <a name="overview"></a>概觀
現代以網際網路為基礎的應用程式通常會有多個使用者同時檢視及更新資料。 這需要仔細的相關說明的可預測的 tooprovide 遇到 tootheir 一般使用者、 應用程式開發人員 toothink，特別是針對案例多位使用者可以更新其中 hello 相同資料。 開發人員通常會考量三個主要的資料並行存取策略：  

1. 開放式並行存取 – 應用程式執行更新會做為其更新的一部分確認如果 hello 之後資料已經變更 hello 應用程式上次讀取資料。 例如，如果兩個檢視的 wiki 頁面的使用者進行更新 toohello 相同頁面上則 hello wiki 平台必須確定該 hello 第二個更新不會覆寫第一個更新 hello – 和兩個使用者了解它們的更新是否已成功。 此策略最常用在 Web 應用程式中。
2. 封閉式並行存取 – 尋找 tooperform 更新應用程式將會鎖定 hello 鎖定釋放，直到更新 hello 資料時，防止其他使用者的物件。 例如，在只有 hello 主要將在何處執行更新的主/從資料複寫案例 hello 主要會通常保存的獨佔鎖定一段時間 hello 資料 tooensure 任何人都可以更新它。
3. 最後一個的寫入者獲勝 – 可讓任何 update 作業 tooproceed，而不驗證 hello 應用程式第一次讀取 hello 資料，因此是否其他應用程式已更新 hello 資料的方法。 此策略 （或缺乏型式策略） 通常用於資料分割的方式會有多個使用者會存取 hello 沒有可能性的位置相同的資料。 在處理暫時性資料串流的情況中，也可以利用此策略。  

本文章提供如何 hello Azure 儲存體的平台開發提供簡化第一級支援所有三個這些並行策略的概觀。  

## <a name="azure-storage--simplifies-cloud-development"></a>Azure 儲存體 – 簡化雲端開發
hello Azure 儲存體服務支援所有的三種策略，雖然它是特殊中其能力 tooprovide 的完整支援開放式和封閉式並行存取，因為它是設計的 tooembrace 強式一致性模型以確保，當hello 儲存體服務認可資料插入或更新的作業的所有進一步存取 toothat 資料會看到最新版本更新的 hello。 使用最終一致性模型的儲存體平台都有之間由一位使用者執行寫入時的延遲和其他使用者，因此複雜順序 tooprevent 不一致，從用戶端應用程式的開發 hello 更新時可以看到資料使用者的影響。  

此外 tooselecting 適當的並行策略開發人員也應該知道的儲存體的平台會變更 – 特別變更 toohello 相同的物件不同的交易之間的隔離。 hello Azure 儲存體服務會使用快照集隔離 tooallow 讀取與寫入作業的單一資料分割內同時作業 toohappen。 不同於其他隔離等級，快照集隔離保證所有讀取都看到 hello 資料的一致快照集，即使在進行更新 – 基本上藉由更新交易在處理時，傳回 hello 最後認可的值。  

## <a name="managing-concurrency-in-blob-storage"></a>管理 Blob 儲存體中的並行存取
您可以選擇 toouse 是開放式或封閉式並行存取模型 toomanage 存取 tooblobs 和中的容器 hello blob 服務。 如果您未明確指定策略上次寫入 wins 是 hello 預設值。  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>Blob 和容器的開放式並行存取
hello 儲存體服務會指派儲存的識別項 tooevery 物件。 此識別碼會在每次對物件執行更新作業時更新。 toohello 用戶端，使用 hello HTTP 通訊協定中定義的 hello （實體標記） 的 ETag 標頭的 HTTP GET 回應的一部分時，會傳回 hello 識別項。 使用者執行這類物件上的更新可以傳送 hello 以及更新才會在符合特定條件 – hello 條件在此情況下會需要 hello 儲存體 」 If-match"標頭的條件式標頭 tooensure 原始的 ETag服務 tooensure hello hello hello 更新要求中指定的 ETag 為 hello 與 hello 儲存體服務中儲存相同的值。  

hello 這個程序概述如下所示：  

1. 擷取 hello 儲存體服務中的 blob，hello 回應包含 HTTP ETag 標頭的值，識別 hello hello 儲存體服務中的 hello 物件的目前版本。
2. 當您更新 hello blob 時，包括您在步驟 1 中 hello 中收到 hello ETag 值**If-match** hello 要求您傳送 toohello 服務的條件式標頭。
3. hello 服務會比較 hello 要求中的 hello 目前的 ETag 值 hello blob 的 hello ETag 值。
4. 如果 hello 目前的 ETag 值 hello blob 是不同的版本，比在 hello hello ETag **If-match** hello 要求，hello 服務中的條件式標頭會傳回 412 錯誤 toohello 用戶端。 這表示 toohello 用戶端 hello 用戶端擷取它之後，另一個處理序已更新 hello blob。
5. 如果 hello 目前的 ETag 值 hello blob 是 hello 與相同的版本 hello ETag 在 hello **If-match** hello 要求，hello 服務中的條件式標頭執行 hello 要求的作業和更新 hello 目前 hello blob 的 ETag 值tooshow 一旦建立新的版本。  

hello 下列 C# 程式碼片段 （使用用戶端儲存庫 4.2.0 hello） 示範如何的簡單範例 tooconstruct **If-match AccessCondition** hello 存取 hello 之屬性的已將 blob 的 ETag 值為基礎先前擷取或插入。 然後它會使用 hello **AccessCondition**物件時就更新 hello blob: hello **AccessCondition**物件加入 hello **If-match**標頭 toohello 要求。 如果另一個處理序已更新 hello blob，hello blob 服務會傳回 HTTP 412 （先決條件失敗） 的狀態訊息。 您可以在此處下載 hello 完整的範例：[使用 Azure 儲存體管理並行](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)。  

```csharp
// Retrieve hello ETag from hello newly created blob
// Etag is already populated as UploadText should cause a PUT Blob call
// toostorage blob service which returns hello etag in response.
string orignalETag = blockBlob.Properties.ETag;

// This code simulates an update by a third party.
string helloText = "Blob updated by a third party.";

// No etag, provided so orignal blob is overwritten (thus generating a new etag)
blockBlob.UploadText(helloText);
Console.WriteLine("Blob updated. Updated ETag = {0}",
blockBlob.Properties.ETag);

// Now try tooupdate hello blob using hello orignal ETag provided when hello blob was created
try
{
    Console.WriteLine("Trying tooupdate blob using orignal etag toogenerate if-match access condition");
    blockBlob.UploadText(helloText,accessCondition:
    AccessCondition.GenerateIfMatchCondition(orignalETag));
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
    {
        Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
        // TODO: client can decide on how it wants toohandle hello 3rd party updated content.
    }
    else
        throw;
}  
```

hello 儲存體服務也支援其他的條件式標頭例如**如果修改自**，**如果不想修改自**和**如果 If-none-Match**以及組合類別。 如需詳細資訊，請參閱 MSDN 上的 [為 Blob 服務作業指定條件式標頭](http://msdn.microsoft.com/library/azure/dd179371.aspx) 。  

hello 下表摘要說明接受下列條件式標頭的 hello 容器作業**If-match** hello 要求，而且傳回以 hello 回應的 ETag 值。  

| 作業 | 傳回容器 ETag 值 | 接受條件式標頭 |
|:--- |:--- |:--- |
| 建立容器 |是 |否 |
| 取得容器屬性 |是 |否 |
| 取得容器中繼資料 |是 |否 |
| 設定容器中繼資料 |是 |是 |
| 取得容器 ACL |是 |否 |
| 設定容器 ACL |是 |是 (*) |
| 刪除容器 |否 |是 |
| 租用容器 |是 |是 |
| 列出 Blob |否 |否 |

（*） hello 定義的權限 SetContainerACL 快取中，更新 toothese 權限會一致的 toopropagate 哪些期間更新便無法保證 toobe 30 秒。  

hello 下表摘要說明接受下列條件式標頭的 hello blob 作業**If-match** hello 要求，而且傳回以 hello 回應的 ETag 值。

| 作業 | 傳回 ETag 值 | 接受條件式標頭 |
|:--- |:--- |:--- |
| 放置 Blob |是 |是 |
| 取得 Blob |是 |是 |
| 取得 Blob 屬性 |是 |是 |
| 設定 Blob 屬性 |是 |是 |
| 取得 Blob 中繼資料 |是 |是 |
| 設定 Blob 中繼資料 |是 |是 |
| 租用 Blob (*) |是 |是 |
| 快照 Blob |是 |是 |
| 複製 Blob |是 |是 (針對來源及目的地 Blob) |
| 中止複製 Blob |否 |否 |
| 刪除 Blob |否 |是 |
| 放置區塊 |否 |否 |
| 放置區塊清單 |是 |是 |
| 取得區塊清單 |是 |否 |
| 放置頁面 |是 |是 |
| 取得頁面範圍 |是 |是 |

(*)租用 Blob 不會變更 blob 上的 hello ETag。  

### <a name="pessimistic-concurrency-for-blobs"></a>Blob 的封閉式並行存取
toolock 專供 blob，您可以取得[租用](http://msdn.microsoft.com/library/azure/ee691972.aspx)在其上。 當您取得租用時，指定您需要多久 hello 租用： 這可以是 15 too60 秒的時間或無限量 tooan 獨佔鎖定。 您可以更新，以及您可以釋放任何租用完與其有限租用 tooextend。 hello blob 服務會在到期時，會自動釋放有限的租用。  

/ 共用讀取、 獨佔寫入啟用不同的同步處理策略 toobe 支援，包括獨佔寫入租用獨佔讀取和寫入的共用 / 獨佔讀取。 其中存在租用 hello 儲存體服務會強制執行獨佔寫入 （put、 設定和刪除作業） 但是確保讀取作業的專用性需要所有的用戶端應用程式一次租用識別碼和該只有一部用戶端使用的 hello 開發人員 tooensure具有有效的租用識別碼。 未包含租用識別碼的讀取作業將會導致共用讀取。  

hello 下列 C# 程式碼片段顯示 30 秒的 blob 上取得獨佔租用及更新 hello blob 的內容 hello，再放開 hello 租用的範例。 如果已經有有效的租用 hello blob 上嘗試 tooacquire 新租用時，hello blob 服務會傳回 「 HTTP (409) 衝突 」 的狀態結果。 使用以下的程式碼片段 hello **AccessCondition** hello 儲存體服務要求 tooupdate hello blob 時，物件 tooencapsulate hello 租用資訊。  您可以在此處下載 hello 完整的範例：[使用 Azure 儲存體管理並行](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)。

```csharp
// Acquire lease for 15 seconds
string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

// Update blob using lease. This operation will succeed
const string helloText = "Blob updated";
var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
blockBlob.UploadText(helloText, accessCondition: accessCondition);
Console.WriteLine("Blob updated using an exclusive lease");

//Simulate third party update tooblob without lease
try
{
    // Below operation will fail as no valid lease provided
    Console.WriteLine("Trying tooupdate blob without valid lease");
    blockBlob.UploadText("Update without lease, will fail");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
    else
        throw;
}  
```

如果您嘗試在租用的 blob 上的寫入作業而不需傳遞 hello 租用識別碼，hello 要求 412 錯誤而失敗。 請注意，如果 hello 租用到期之前呼叫 hello **UploadText**方法，但仍會傳遞 hello 租用識別碼，hello 要求也會因**412**錯誤。 如需管理到期的租用時間與租用識別碼的詳細資訊，請參閱 hello[租用 Blob](http://msdn.microsoft.com/library/azure/ee691972.aspx) REST 文件。  

hello 下列 blob 作業可以使用租用 toomanage 封閉式並行存取：  

* 放置 Blob
* 取得 Blob
* 取得 Blob 屬性
* 設定 Blob 屬性
* 取得 Blob 中繼資料
* 設定 Blob 中繼資料
* 刪除 Blob
* 放置區塊
* 放置區塊清單
* 取得區塊清單
* 放置頁面
* 取得頁面範圍
* 快照 Blob - 若有租用存在，租用識別碼則是選用的
* 複製 Blob-hello 目的地 blob 上是否有租用需要租用識別碼
* 中止複製 Blob-hello 目的地 blob 上是否有無限期租用需要租用識別碼
* 租用 Blob  

### <a name="pessimistic-concurrency-for-containers"></a>容器的封閉式並行存取
租用容器上的啟用相同的同步處理策略 toobe 支援在 blob 的 hello (獨佔寫入 / 共用讀取、 獨佔寫入 / 獨佔讀取和寫入的共用 / 獨佔唯讀) 但是不同於 blob hello 儲存體服務只會強制專用性在刪除作業。 toodelete 具有作用中租用的容器，用戶端必須包含 hello 與 hello 刪除要求的作用中租用識別碼。 所有其他容器作業在租用的容器上成功但不包括 hello 租用識別碼在此情況下它們共用作業。 如果更新 (放置或設定) 或讀取作業需要獨佔性，則開發人員應確定所有的用戶端都使用同一個租用識別碼，並確定同一時間只有一個用戶端具有有效的租用識別碼。  

hello 下列容器作業可以使用租用 toomanage 封閉式並行存取：  

* 刪除容器
* 取得容器屬性
* 取得容器中繼資料
* 設定容器中繼資料
* 取得容器 ACL
* 設定容器 ACL
* 租用容器  

如需詳細資訊，請參閱：  

* [指定 Blob 服務作業的條件式標頭](http://msdn.microsoft.com/library/azure/dd179371.aspx)
* [租用容器](http://msdn.microsoft.com/library/azure/jj159103.aspx)
* [租用 Blob ](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-hello-table-service"></a>Hello 表格服務中的 < 管理並行存取
hello 表格服務會使用開放式並行存取檢查作為 hello 預設行為，當您使用與 hello blob 服務，必須明確選擇 tooperform 開放式並行存取檢查不同的實體。 hello 其他 hello 資料表和 blob 服務之間的差異是，您可以只管理的實體 hello 並行行為而與 hello blob 服務中，您可以管理的容器和 blob 的 hello 並行。  

toouse 開放式並行存取以及 toocheck 如果另一個處理序修改實體，因為從 hello 資料表儲存體服務中擷取，您可以使用 hello 表格服務會傳回實體時，您會收到 hello ETag 值。 hello 這個程序概述如下所示：  

1. 擷取從 hello 資料表儲存體服務的實體，hello 回應包含 ETag 值，識別 hello 與 hello 儲存體服務中該實體相關聯的目前識別項。
2. 當您更新 hello 實體時，包括您在步驟 1 中強制 hello 中收到 hello ETag 值**If-match** hello 傳送 toohello 服務的要求標頭。
3. hello 服務會比較 hello 要求中的 hello 目前的 ETag 值 hello 實體的 hello ETag 值。
4. 如果 hello 目前的 ETag 值 hello 實體中強制 hello hello ETag 不同**If-match** hello 要求，hello 服務中的標頭會傳回 412 錯誤 toohello 用戶端。 這表示 toohello 用戶端 hello 用戶端擷取它之後，另一個處理序已更新 hello 實體。
5. 如果 hello 目前的 ETag 值 hello 實體是 hello 相同 hello 強制在 hello ETag **If-match**標頭中的 hello 要求或 hello **If-match**標頭包含 hello 的萬用字元 （*） hello 服務執行 hello 要求的作業和更新 hello hello 實體 tooshow 已更新過的目前的 ETag 值。  

請注意，不同於 hello blob 服務，hello 表格服務需要 hello 用戶端 tooinclude **If-match**更新要求中的標頭。 不過，很可能 tooforce 無條件更新 （最後一個寫入器 wins 策略），並略過的並行存取檢查，如果 hello 用戶端設定 hello **If-match**標頭 toohello 萬用字元 （*） hello 要求中的。  

下列 C# 程式碼片段的 hello 顯示 customer 實體可能是先前建立或擷取需要更新的電子郵件地址。 hello 初始插入或擷取作業存放區 hello ETag 值以 hello 客戶物件、 且由於 hello 範例使用 hello 相同物件執行個體時，它會執行 hello 取代作業時，會自動傳送 hello ETag 值後 toohello 表格服務，啟用 hello 服務 toocheck 並行違規。 如果另一個處理序已更新資料表儲存體中的 hello 實體，hello 服務會傳回 HTTP 412 （先決條件失敗） 的狀態訊息。  您可以在此處下載 hello 完整的範例：[使用 Azure 儲存體管理並行](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)。

```csharp
try
{
    customer.Email = "updatedEmail@contoso.org";
    TableOperation replaceCustomer = TableOperation.Replace(customer);
    customerTable.Execute(replaceCustomer);
    Console.WriteLine("Replace operation succeeded.");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == 412)
        Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
    else
        throw;
}  
```

tooexplicitly 停用 hello 並行存取檢查，您應該設定的 hello **ETag** hello 屬性**員工**物件太"*"之前執行 hello 取代作業。  

```csharp
customer.ETag = "*";  
```

hello 下表摘要說明如何 hello 資料表實體作業會使用 ETag 值：

| 作業 | 傳回 ETag 值 | 需要 If-Match 要求標頭 |
|:--- |:--- |:--- |
| 查詢實體 |是 |否 |
| 插入實體 |是 |否 |
| 更新實體 |是 |是 |
| 合併實體 |是 |是 |
| 刪除實體 |否 |是 |
| 插入或取代實體 |是 |否 |
| 插入或合併實體 |是 |否 |

請注意該 hello**插入或取代實體**和**插入或合併實體**operations*不*執行任何並行存取檢查，因為其不會傳送的 ETag 值 toohello表格服務。  

一般而言，使用資料表的開發人員在開發可擴充的應用程式時，應該會採用開放式並行存取。 如果封閉式鎖定所需的其中一個方法的開發人員可以採取時存取資料表的每個資料表的指定之 blob tooassign 試 tootake hello blob 上的租用之前 hello 資料表上運作。 這種方法需要具備 hello 應用程式 tooensure 所有資料存取權的路徑取得 hello 租用先前 toooperating hello 資料表上的。 您也應注意 hello 最小的租用時間是 15 秒，需要仔細考慮延展性。  

如需詳細資訊，請參閱：  

* [實體上的作業](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-hello-queue-service"></a>Hello 佇列服務中的 < 管理並行存取
其中一個案例是以並行 hello 佇列服務的考量是其中多個用戶端時，會從佇列擷取訊息。 從 hello 佇列擷取訊息時，hello 回應包括 hello 訊息和 pop receipt 值，也就是必要的 toodelete hello 訊息。 hello 訊息不會自動刪除從 hello 佇列，但已擷取之後，就不可見的 tooother 用戶端 hello hello visibilitytimeout 參數所指定的時間間隔。 擷取 hello 訊息的 hello 用戶端預期的 toodelete hello 訊息之後便已被處理，而之前 hello 時間所指定 hello TimeNextVisible 的 hello 回應，計算出 hello visibilitytimeout hello 值為基礎的項目參數。 visibilitytimeout hello 值會加入 toohello 時間的 hello 訊息擷取 TimeNextVisible toodetermine hello 值。  

hello 佇列服務沒有支援開放式或封閉式並行存取，這個處理從佇列擷取訊息的原因用戶端應該確定等冪的方式處理訊息。 「最後寫入為準」策略可用於更新作業，例如 SetQueueServiceProperties、SetQueueMetaData、SetQueueACL 和 UpdateMessage。  

如需詳細資訊，請參閱：  

* [佇列服務 REST API](http://msdn.microsoft.com/library/azure/dd179363.aspx)
* [取得訊息](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-hello-file-service"></a>Hello 檔案服務中的 < 管理並行存取
hello 檔案服務可以使用兩個不同的通訊協定端點 – SMB 和 REST 來存取。 hello REST 服務沒有設定鎖定的開放式或封閉式鎖定的支援，所有更新都會都依循的最後一個寫入器 wins 策略。 掛接檔案共用的 SMB 用戶端可以利用檔案系統鎖定機制 toomanage 存取 tooshared 檔案 – 包括 hello 能力 tooperform 封閉式鎖定。 當 SMB 用戶端開啟檔案時，它會指定 hello 檔案存取和共用模式。 設定檔案存取選項的 「 寫入 」 或 「 讀取/寫入 」 以及 「 無 」 的檔案共用模式，會導致鎖定由 SMB 用戶端 hello 檔案會在關閉之前的 hello 檔案。 如果 SMB 用戶端之 hello 檔案鎖定的檔案會執行 REST 作業 hello REST 服務會傳回狀態碼 409 （衝突） 和錯誤碼 SharingViolation。  

當 SMB 用戶端開啟檔案以進行刪除時，會將標示 hello 檔案為暫止刪除，直到所有其他 SMB 用戶端上該檔案的開啟控制代碼已關閉。 在檔案標示為「擱置刪除」時，任何對該檔案的 REST 作業都將傳回狀態碼 409 (衝突) 和錯誤碼 SMBDeletePending。 因為可能的 hello SMB 用戶端 tooremove hello 暫止刪除旗標先前 tooclosing hello 檔案，不會傳回狀態碼 404 （找不到）。 換句話說，狀態碼 404 （找不到） 只應該已經移除 hello 檔案時。 請注意，當檔案處於 SMB 暫止刪除狀態，它將不會包含在結果清單檔案的 hello。也請注意，hello REST 刪除的檔案和 REST 刪除目錄作業會以不可分割方式認可，而且不會產生暫止刪除狀態。  

如需詳細資訊，請參閱：  

* [管理檔案鎖定](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>摘要和後續步驟
hello Microsoft Azure 儲存體服務已設計 toomeet hello hello 最複雜的線上應用程式需求而不未強制開發人員 toocompromise 或思考關鍵的設計假設例如並行存取，以及資料的一致性，它們都是 tootake針對授與。  

對於 hello 完成範例應用程式中這篇部落格參考：  

* [使用 Azure 儲存體管理並行存取 - 範例應用程式](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

如需 Azure 儲存體的詳細資訊，請參閱：  

* [Microsoft Azure 儲存體首頁](https://azure.microsoft.com/services/storage/)
* [簡介 tooAzure 儲存體](storage-introduction.md)
* [Blob](storage-dotnet-how-to-use-blobs.md)、[資料表](storage-dotnet-how-to-use-tables.md)、[佇列](storage-dotnet-how-to-use-queues.md)及[檔案](storage-dotnet-how-to-use-files.md)的儲存體入門
* 儲存體架構 – [Azure 儲存體：具有高度一致性的高可用性雲端儲存體服務](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

