---
title: "aaaUsing 共用存取簽章 (SAS) 在 Azure 儲存體 |Microsoft 文件"
description: "了解 toouse 共用存取簽章 (SAS) toodelegate 存取 tooAzure 存放裝置資源，包括 blob、 佇列、 表格和檔案。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 53e06c78fbfdaa5fd209add719995ef2a6bc8f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>使用共用存取簽章 (SAS)

共用的存取簽章 (SAS) 為您提供儲存體帳戶中的方式 toogrant 有限存取 tooobjects tooother 用戶端，而不會讓您的帳戶金鑰。 在本文中，我們提供 hello SAS 模型的概觀、 檢閱 SAS 最佳作法，以及查看一些範例。

使用 SAS 除了這裡所呈現的額外的程式碼範例，請參閱[開始使用.NET 的 Azure Blob 儲存體](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)hello 的其他範例和[Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?service=storage)程式庫。 您可以下載 hello 範例應用程式並加以執行，或瀏覽 hello GitHub 上的程式碼。

## <a name="what-is-a-shared-access-signature"></a>共用存取簽章為何？
共用的存取簽章提供儲存體帳戶中的委派的存取 tooresources。 透過 SAS，您可以授與用戶端存取 tooresources 在儲存體帳戶，而不需要共用您的帳戶金鑰。 這是在您的應用程式-SAS 中使用共用的存取簽章的 hello 重點是安全的方式 tooshare 您的儲存體資源，而不會危害您的帳戶金鑰。

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

SAS 可讓您更精確地控制存取您授與擁有 hello SAS，其中包括 tooclients hello 類型：

* hello 的 hello 透過 SAS 有效間隔，包括 hello 開始時間和 hello 到期時間。
* hello hello SAS 所授與權限。 例如，blob 的 SAS 可能會授與讀取和寫入權限 toothat blob，但刪除權限。
* 選擇性的 IP 位址或 IP 位址範圍從中接受 Azure 儲存體 hello SAS。 例如，您可以指定屬於 tooyour 組織某個範圍的 IP 位址。
* hello 通訊協定的 Azure 儲存體將會接受 hello SAS。 您可以使用此使用 HTTPS 的選擇性參數 toorestrict 存取 tooclients。

## <a name="when-should-you-use-a-shared-access-signature"></a>使用共用存取簽章的時機？
當您想 tooprovide 存取 tooresources 中不具備儲存體帳戶的存取金鑰將儲存體帳戶 tooany 用戶端時，您可以使用 SAS。 儲存體帳戶包含主要和次要存取金鑰，這兩種授與系統管理存取權 tooyour 帳戶和其中的所有資源都。 這些金鑰的公開會開啟您帳戶 toohello 的可能性惡意或疏忽使用。 共用的存取簽章提供安全的替代方案，可讓用戶端 tooread、 寫入和刪除資料中根據 toohello 權限已明確授與您，儲存體帳戶，而不需要帳戶金鑰。

其中一個 SAS，是實用的常見案例是的服務使用者讀取和寫入其本身資料 tooyour 儲存體帳戶的位置。 在儲存體帳戶儲存使用者資料的案例中，典型的設計模式有兩種：

1. 用戶端通過前端 Proxy 服務 (執行驗證) 來上傳與下載資料。 此前端 proxy 服務有 hello 好處是允許的商務規則驗證，但對於大量的資料或大量的交易中，建立可調整 toomatch 要求的服務可能是昂貴或困難。

  ![案例圖表︰前端 Proxy 服務][sas-storage-fe-proxy-service]

1. 輕量型的服務驗證 hello 用戶端，視需要並接著會產生 SAS。 一旦 hello 用戶端收到 hello SAS，他們可以存取儲存體帳戶資源，直接與 hello 定義 hello SAS 而且 hello 間隔 hello SAS 所允許的權限。 hello SAS 可降低 hello 需要路由透過 hello 前端 proxy 服務的所有資料。

  ![案例圖表︰SAS 提供者服務][sas-storage-provider-service]

許多實際服務可能會混合運用這兩種方法。 例如，某些資料可能會處理並驗證透過 hello 前端 proxy，而其他資料是儲存和/或直接使用 SAS 讀取。

此外，您將需要 toouse SAS tooauthenticate hello 來源中的物件在某些情況下複製作業：

* 當您複製 blob tooanother blob 存在於不同的儲存體帳戶中時，您必須使用 SAS tooauthenticate hello 來源 blob。 您可以選擇使用 SAS tooauthenticate hello 目的地 blob 以及。
* 當您複製檔案 tooanother 檔案位於不同的儲存體帳戶中時，您必須使用 SAS tooauthenticate hello 原始程式檔。 您可以選擇使用 SAS tooauthenticate hello 目的地檔案。
* 當您複製 blob tooa 檔案或檔案 tooa blob 時，您必須使用 SAS tooauthenticate hello 來源物件，即使 hello 來源和目的地的物件位於 hello 相同儲存體帳戶。

## <a name="types-of-shared-access-signatures"></a>共用存取簽章的類型
您可建立兩種類型的共用存取簽章：

* **服務 SAS。** hello 服務 SAS 委派存取 tooa 資源中其中一個 hello 存放服務： hello Blob、 佇列、 資料表或檔案服務。 請參閱[建構服務 SAS](https://msdn.microsoft.com/library/dn140255.aspx)和[Service SAS 範例](https://msdn.microsoft.com/library/dn140256.aspx)如需建構 hello 服務 SAS 權杖的深入資訊。
* **帳戶 SAS。** hello SAS 授權帳戶存取 tooresources 中一或多個 hello 儲存體服務。 所有透過 SAS 服務可用的 hello 作業也會提供透過 SAS 的帳戶。 此外，與 hello 帳戶 SAS，您可以將委派存取 toooperations 適用於提供服務，例如 tooa **Get/Set 服務內容**和**取得 Service Stats**。您也可以委派存取 tooread、 寫入和刪除 blob 容器、 資料表、 佇列和服務的 SAS 不允許的檔案共用上的作業。 請參閱[建構帳戶 SAS](https://msdn.microsoft.com/library/mt584140.aspx)如需建構 hello 帳戶 SAS 權杖的深入資訊。

## <a name="how-a-shared-access-signature-works"></a>共用存取簽章的運作方式
共用的存取簽章是帶正負號的 URI 指向 tooone 或更多的儲存體資源，並含有包含一組特殊的查詢參數的語彙基元。 hello 語彙基元指出 hello 用戶端如何存取 hello 的資源。 Hello 查詢參數，其中 hello 簽章、 是建構自 hello SAS 參數和使用 hello 帳戶金鑰進行簽署。 Azure 儲存體 tooauthenticate hello SAS 會使用此簽章。

SAS URI、 顯示 hello 資源 URI 和 hello SAS 權杖的範例如下：

![SAS URI 的元件][sas-storage-uri]

hello SAS 權杖是一個字串 hello 產生*用戶端*端 (請參閱 hello [SAS 範例](#sas-examples)> 一節的程式碼範例)。 SAS 權杖產生 hello 儲存體用戶端程式庫，例如，不會追蹤 Azure 儲存體以任何方式。 您可以建立無限的數量的 SAS 權杖 hello 用戶端。

當用戶端提供的 SAS URI tooAzure 儲存體做為要求的一部分時，hello 服務會檢查 hello SAS 參數和簽章 tooverify 是適用於驗證 hello 要求。 如果 hello 服務會確認該 hello 簽章有效，會驗證 hello 要求。 否則，hello 要求被拒絕，錯誤碼 403 （禁止）。

## <a name="shared-access-signature-parameters"></a>共用存取簽章參數
hello 帳戶 SAS 和服務的 SAS 權杖包含一些常見的參數，而也不使用一些參數的不同。

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>一般 tooaccount SAS 參數和服務的 SAS 權杖
* **Api 版本**指定 hello 儲存體服務版本 toouse tooexecute hello 要求的選擇性參數。
* **服務版本**指定 hello 儲存體服務版本 toouse tooauthenticate hello 要求的必要的參數。
* **開始時間。** 這是 hello 的 hello SAS 生效的時間。 hello 共用的存取簽章的開始時間是選擇性的。 如果省略開始時間，hello SAS 就是立即生效。 hello 開始時間必須以 UTC （國際標準時間），具有特殊的 UTC 指示項 ("Z")，例如`1994-11-05T13:15:30Z`。
* **到期時間。** 這是 hello 時間過後 hello SAS 已不再有效。 最佳做法建議您為 SAS 指定過期時間，或將它與預存存取原則建立關聯。 hello 到期時間必須以 UTC （國際標準時間），具有特殊的 UTC 指示項 ("Z")，例如`1994-11-05T13:15:30Z`（將詳細說明）。
* **權限。** hello hello SAS 上指定的權限表示 hello 用戶端可以針對使用 hello SAS hello 儲存體資源執行哪些作業。 帳戶 SAS 和服務 SAS 的可用權限不同。
* **IP。** 指定的 IP 位址或 IP 位址範圍 Azure 外部的選擇性參數 (參閱 hello[路由工作階段設定狀態](../expressroute/expressroute-workflows.md#routing-session-configuration-state)的 Express Route) 從哪些 tooaccept 要求。
* **通訊協定。** 選擇性參數指定 hello 通訊協定，允許的要求。 可能的值為 HTTPS 和 HTTP (`https,http`)，這只是 hello 預設值或 HTTPS (`https`)。 請注意，僅 HTTP 是不允許的值。
* **簽章。** hello 簽章從 hello 建構其他參數指定做為部分權杖，然後再加密。 它已用 tooauthenticate hello SAS。

### <a name="parameters-for-a-service-sas-token"></a>服務 SAS 權杖的參數
* **儲存體資源。** 可以委派對服務 SAS 存取的儲存體資源包括：
  * 容器和 Blob
  * 檔案共用及檔案
  * 佇列
  * 資料表和資料表實體範圍。

### <a name="parameters-for-an-account-sas-token"></a>帳戶 SAS 權杖的參數
* **一或多個服務。** SA 帳戶可以委派存取 tooone 或多個 hello 儲存體服務。 例如，您可以建立委派存取 toohello Blob 和檔案服務的帳戶 SAS。 或者，您可以建立一個 SAS，委派存取 tooall 四項服務 （Blob、 佇列、 表格和檔案）。
* **儲存體資源類型。** Tooone 或存放裝置資源，而非特定資源的多個類別，適用於 SAS 的帳戶。 您可以建立帳戶 SAS toodelegate 存取：
  * 服務層級 Api，稱為針對 hello 儲存體帳戶的資源。 範例包括**取得/設定服務屬性**、**取得服務統計資料**和**列出容器/佇列/資料表/共用**。
  * 容器層級 Api，其會針對每個服務呼叫 hello 容器物件： blob 容器、 佇列、 資料表和檔案共用。 範例包括**建立/刪除容器**、**建立/刪除佇列**、**建立/刪除資料表**、**建立/刪除共用**和**列出 Blob/檔案和目錄**。
  * 物件層級 API，針對 Blob、佇列訊息、資料表實體和檔案呼叫。 例如，**放置 Blob**、**查詢實體**、**取得訊息**和**建立檔案**。

## <a name="examples-of-sas-uris"></a>SAS URI 的範例

### <a name="service-sas-uri-example"></a>服務 SAS URI 範例

以下是提供的 SAS URI 讀取和寫入權限 tooa blob 服務的範例。 hello 資料表細分 hello URI toounderstand 的每個部分看出何影響 toohello SA:

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| 名稱 | SAS 部分 | 說明 |
| --- | --- | --- |
| Blob URI |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |hello hello blob 位址。 請注意，我們強烈建議您使用 HTTPS。 |
| 儲存體服務版本 |`sv=2015-04-05` |儲存體服務 2012年-02-12 版和更新版本中，這個參數會指出 hello 版本 toouse。 |
| 開始時間 |`st=2015-04-29T22%3A18%3A26Z` |以 UTC 時間指定。 如果您想 hello SAS toobe 有效立即，省略 hello 開始時間。 |
| 過期時間 |`se=2015-04-30T02%3A23%3A26Z` |以 UTC 時間指定。 |
| 資源 |`sr=b` |hello 資源是 blob。 |
| 權限 |`sp=rw` |hello hello SAS 授與的權限包括 Read (r)，和寫入 (w)。 |
| IP 範圍 |`sip=168.1.5.60-168.1.5.70` |hello 的 IP 位址範圍將會接受要求。 |
| 通訊協定 |`spr=https` |僅允許使用 HTTPS 的要求。 |
| 簽章 |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |使用 tooauthenticate 存取 toohello blob。 hello 簽章是計算字串簽章和金鑰使用 hello SHA256 演算法，並編碼使用 Base64 編碼的 HMAC。 |

### <a name="account-sas-uri-example"></a>帳戶 SAS URI 範例

以下是範例 SA 帳戶的使用 hello hello 權杖相同的一般參數。 由於上面說明了這些參數，在此處將不說明。 只有 hello 參數，為特定 tooaccount SAS 詳述於下表 hello。

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| 名稱 | SAS 部分 | 說明 |
| --- | --- | --- |
| 資源 URI |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |hello Blob 服務端點，使用參數來取得服務屬性 （當使用 GET 呼叫），或設定服務屬性 （當呼叫組）。 |
| 服務 |`ss=bf` |hello SAS 套用 toohello Blob 和檔案服務 |
| 資源類型 |`srt=s` |hello SAS 適用於 tooservice 層級的作業。 |
| 權限 |`sp=rw` |hello 權限授與存取 tooread 和寫入作業。 |

Toohello 服務層級，透過此 SAS 存取作業的權限受到限制是**取得 Blob 服務屬性**（讀取） 和**設定 Blob 服務屬性**（寫入）。 不過，使用不同的資源 URI，hello 相同 SAS 權杖也可能是使用 toodelegate 存取太**取得 Blob 服務統計資料**（讀取）。

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>使用預存存取原則控制 SAS
共用存取簽章可以接受以下兩種格式其中之一：

* **臨機操作 SAS:**當您建立臨機操作 SAS、 hello 開始時間、 到期時間和 hello SAS 的權限會指定在 hello SAS URI （或默示擔保，則開始時間的 hello 案例中）。 這種類型的 SAS 可能會建立為帳戶 SAS 或服務 SAS。
* **與預存的存取原則 SAS:**預存的存取原則定義資源的容器-blob 容器、 資料表、 佇列或檔案共用-和可以是一個或多個共用的存取簽章使用的 toomanage 條件約束。 當您建立 SAS 關聯與預存的存取原則時，hello SAS 會繼承 hello 條件約束-hello 開始時間、 到期時間和權限-hello 預存存取原則的定義。

> [!NOTE]
> 目前，帳戶 SAS 必須是臨機操作 SAS。 帳戶 SAS 尚不支援預存的存取原則。

hello hello 兩個形式之間的差異是很重要的一個重要的案例： 撤銷。 SAS URI 為 URL，因為任何人都可以取得 hello SAS，可以使用它無論原先建立者。 如果已公開發行 SAS，才能使用 hello 世界中的任何人。 SAS 授與存取 tooresources tooanyone 擁有它，直到其中一四項發生：

1. hello 上 hello SAS 達到指定的到期時間。
2. hello hello SAS 為止 （參考的預存的存取原則時，而且如果它會指定到期時間） 所參考的 hello 預存存取原則中指定的到期時間。 這可能是因為 hello 間隔經過之後，或您修改了 hello 預存存取原則與到期時間在 hello 過去，這是其中一種方式 toorevoke hello SAS。
3. hello 預存存取原則參考的 hello SAS 遭到刪除，也就是另一個方式 toorevoke hello SAS。 請注意，如果您完全重新建立 hello 預存存取原則與 hello 相同的名稱，所有現有的 SAS 權杖會一次有效的相應 toohello 權限與原則相關聯該預存的存取 （假設的 hello SAS 未跳過該 hello 到期時間）。 如果您打算 toorevoke hello SAS，是確定 toouse 不同名稱，如果您重新建立與到期時間在未來的 hello hello 存取原則。
4. 重新產生已使用的 toocreate hello SAS 的 hello 帳戶金鑰。 重新產生帳戶金鑰會導致所有應用程式元件使用該金鑰 toofail tooauthenticate 其他有效的帳戶金鑰或 hello 新重新產生的帳戶金鑰在更新之前 toouse 或是 hello。

> [!IMPORTANT]
> 共用的存取簽章 URI 都與 hello 帳戶金鑰的使用的 toocreate hello 簽章，與 hello 預存的存取原則 （如果有的話）。 如果未不指定任何預存的存取原則，則 hello 只方式 toorevoke 共用的存取簽章是 toochange hello 帳戶金鑰。

## <a name="authenticating-from-a-client-application-with-a-sas"></a>使用 SAS 從用戶端應用程式進行驗證
擁有 SAS 的用戶端可以使用 hello SAS tooauthenticate 對儲存體帳戶沒有 hello 帳戶金鑰的要求。 SAS 可以包含在連接字串中，或直接從 hello 適當的建構函式或方法。

### <a name="using-a-sas-in-a-connection-string"></a>在連接字串中使用 SAS
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>在建構函式或方法中使用 SAS
數個 Azure 儲存體用戶端程式庫建構函式和方法多載提供 SAS 參數，讓您可以驗證 SAS 要求 toohello 服務。

例如，以下 SAS URI 是使用的 toocreate 參考 tooa 區塊 blob。 hello SAS 提供 hello 只有 hello 要求所需的認證。 hello 區塊 blob 參考然後用於寫入作業：

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>使用 SAS 時的最佳做法
當您在應用程式中使用共用的存取簽章時，您需要 toobe 注意兩個潛在的風險：

* 如果 SAS 洩漏出去，則取得該 SAS 的任何人都可以使用它，這有可能會洩露您的儲存體帳戶。
* 如果 SAS 提供 tooa 用戶端應用程式到期且 hello 應用程式無法 tooretrieve 新 SAS 從您的服務，可能會減慢 hello 應用程式的功能。

hello 使用共用的存取簽章的下列建議可協助降低這些風險：

1. **一律使用 HTTPS** toocreate 或散發 SAS。 如果 SAS 是透過 HTTP 傳入，而且攔截，執行攔截密碼破解攻擊的攻擊者為可以 tooread hello SAS，，然後使用它，就如同 hello 適合使用者可以擁有，可能洩漏機密資料，或允許的資料損毀 hello惡意的使用者。
2. **可能的話，參考預存存取原則。** 預存存取原則讓您無須 tooregenerate hello 儲存體帳戶金鑰 hello 選項 toorevoke 權限。 這些最在 hello 設定 hello 逾期，未來的 （或無限的），並確定它有定期更新 toomove 遠到未來的 hello。
3. **在臨機操作 SAS 上使用短期的到期時間。** 如此一來，即使 SAS 遭到入侵，亦僅會造成短期影響。 如果您無法參考預存存取原則，此做法格外重要。 Star 逾期時間也會限制 hello 可以藉由限制 hello 時間可用 tooupload tooit 寫入 tooa blob 的資料量。
4. **有 hello SAS 必要時，自動更新用戶端。** 用戶端應該更新 hello SAS hello 到期日重試提供 hello SAS hello 服務無法使用時的順序 tooallow 時間之前。 如果您的 SAS 適用於少量立即 toobe，存留較短的作業都必須是 toobe 期間內完成 hello 到期，則這可能是不必要更新 toobe hello SAS 不正常。 不過，如果您有定期正在透過 SAS 要求的用戶端，然後到期 hello 可能性派上用場。 hello 重要考量是 toobalance hello 需要 hello SAS toobe 存留較短 （如先前所述） 與 hello 用戶端的 hello 需要 tooensure 早期要求更新足夠 （tooavoid 中斷到期 toohello SAS 到期之前 toosuccessful 更新）。
5. **請小心使用 SAS 開始時間。** 如果您設定 hello 開始時間的 SAS 太**現在**，然後 tooclock 誤差 （根據 toodifferent 機器的目前時間的差異），因為失敗可能會觀察到間歇性 hello 第一個幾分鐘的時間。 一般情況下，設定 hello 開始時間 toobe 至少 15 分鐘過去 hello。 或是不進行任何設定，這會針對所有案例立即生效。 hello 相同通常適用於 tooexpiry 時間以及-請記住，您可能會注意到向上 too15 分鐘的時鐘誤差任一方向上的任何要求。 用戶端使用 REST 版本先前 too2012-02-12，hello SAS 未參考的預存的存取原則的最大持續期間是 1 小時，並指定較長的詞彙，比，將會失敗的任何原則。
6. **是特定的 hello 資源 toobe 存取。** 安全性最佳作法是 tooprovide hello 最低必要權限的使用者。 如果使用者只需要讀取權限 tooa 單一實體，然後授與他們 toothat 單一實體讀取權限和不讀取/寫入/刪除存取 tooall 實體。 這也有助於降低 hello 損毀，如果 SAS 遭到入侵，因為 hello SAS hello 指針，攻擊者中的電力較少。
7. **了解您帳戶的任何方式將會被收取費用，包括以 SAS 方式完成的部分。** 如果您提供寫入存取 tooa blob 時，使用者可能選擇 tooupload 200 GB 的 blob。 如果您已獲得它們讀取權限，可能會選擇 toodownload 10 次，在輸出中產生 2 TB 成本為您。 同樣地，提供有限的權限 toohelp 減輕惡意使用者的 hello 潛在動作。 使用這項威脅存留較短的 SAS tooreduce （但留意時鐘誤差 hello 結束時間）。
8. **使用 SAS 驗證寫入資料。** 當用戶端應用程式寫入資料 tooyour 儲存體帳戶時，請注意，可能會有該資料的問題。 如果您的應用程式需要的驗證或授權之前準備好 toouse 資料，您應該在 hello 資料寫入之後，它由您的應用程式之前執行這項驗證。 這種做法也可防止損毀或惡意的資料寫入 tooyour 帳戶的使用者，正確地取得 hello SAS，或是利用遺漏的 SAS 的使用者。
9. **請勿一直使用 SAS。** 有時 hello 與針對儲存體帳戶的特定作業相關聯的風險，勝過 hello 優點的 SAS。 這類作業，建立中介層服務寫入 tooyour 儲存體帳戶之後執行商務規則驗證、 驗證和稽核。 此外，有時也是以其他方式較簡單的 toomanage 存取。 比方說，如果您想 toomake 容器中的所有 blob 公開可讀取，您可以進行 hello 容器為公用，而不是 SAS tooevery 用戶端提供存取。
10. **使用儲存體分析 toomonitor 您的應用程式。** 您可以使用記錄和度量 tooobserve 任何特殊驗證失敗，因為 tooan 中斷您 SAS 提供者服務或 toohello 不小心移除預存的存取原則。 請參閱 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx)如需詳細資訊。

## <a name="sas-examples"></a>SAS 範例
下面是兩種類型共用存取簽章 (帳戶 SAS 和服務 SAS) 的一些範例。

toorun 這些 C# 範例中，您需要下列專案中的 NuGet 套件 tooreference hello:

* [適用於.NET 的 azure 儲存體用戶端程式庫](http://www.nuget.org/packages/WindowsAzure.Storage)，版本 6.x 或更新版本 （toouse 帳戶 SAS）。
* [Azure 資源管理員](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

如需其他範例，示範如何 toocreate 和測試 SAS，請參閱[儲存體的 Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?service=storage)。

### <a name="example-create-and-use-an-account-sas"></a>範例︰建立和使用帳戶 SAS
hello 下列程式碼範例會建立僅適用於 hello Blob 及檔案服務的 SAS 的帳戶，並提供 hello 用戶端權限讀取、 寫入和列出權限 tooaccess 服務層級應用程式開發介面。 hello 帳戶 SAS 會限制 hello 通訊協定 tooHTTPS，因此 hello 要求必須設定成使用 HTTPS。

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

toouse hello 帳戶 SAS tooaccess 服務層級 Api hello Blob 服務、 建構使用 hello SAS Blob 用戶端物件和 hello 儲存體帳戶的 Blob 儲存體端點。

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>範例：建立預存的存取原則
hello 下列程式碼會建立預存的存取原則在容器上。 您可以使用 hello 存取原則 toospecify 條件約束服務 hello 容器上的 SAS 或其 blob。

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>範例︰在容器上建立服務 SAS
下列程式碼的 hello 容器上建立 SAS。 提供現有的預存的存取原則的 hello 名稱，該原則與 hello SAS 相關聯。 如果未不提供任何預存的存取原則，則 hello 程式碼會建立臨機操作 SAS hello 容器上。

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>範例︰在 Blob 上建立服務 SAS
下列程式碼的 hello 的 blob 上建立 SAS。 提供現有的預存的存取原則的 hello 名稱，該原則與 hello SAS 相關聯。 如果未不提供任何預存的存取原則，則 hello 程式碼會建立臨機操作 SAS hello blob 上。

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>結論
共用的存取簽章可用於不應有 hello 帳戶金鑰的 tooyour 儲存體帳戶 tooclients 提供有限的權限。 因此，它們是 hello 安全性模型，使用 Azure 儲存體的任何應用程式不可或缺的一部分。 如果您遵循此處所列的 hello 最佳作法，您可以使用儲存體帳戶中的 SAS tooprovide 更大的彈性存取 tooresources 不會危及應用程式的 hello 安全性。

## <a name="next-steps"></a>後續步驟
* [管理匿名讀取權限 toocontainers 和 blob](storage-manage-access-to-resources.md)
* [使用共用存取簽章來委派存取權](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [資料表與佇列 SAS 簡介](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)

[sas-storage-fe-proxy-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png
[sas-storage-provider-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png
[sas-storage-uri]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png
