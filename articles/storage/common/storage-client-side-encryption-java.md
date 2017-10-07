---
title: "使用 Java 的 Microsoft Azure 儲存體的 aaaClient 端加密 |Microsoft 文件"
description: "hello for Java 的 Azure 儲存體用戶端程式庫支援最高的安全性應用程式的 Azure 儲存體用戶端加密以及與 Azure 金鑰保存庫的整合。"
services: storage
documentationcenter: java
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 3df49907-554c-404a-9b0c-b3e3269ad04f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: cb40c737b9065005f0f31f654e7e43fd27b923f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-with-java-for-microsoft-azure-storage"></a>Microsoft Azure 儲存體搭配 Java 的用戶端加密和 Azure Key Vault
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>概觀
hello [for Java 的 Azure 儲存體用戶端程式庫](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)支援 tooAzure 存放裝置，將上傳和下載 toohello 用戶端時解密資料之前加密用戶端應用程式內的資料。 hello 程式庫也支援與整合[Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)儲存體帳戶金鑰管理。

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>加密和解密透過 hello 信封技術
加密和解密的 hello 處理程序遵循 hello 信封技術。  

### <a name="encryption-via-hello-envelope-technique"></a>加密透過 hello 信封技術
透過 hello 信封技術的加密方式 hello 下列方法：  

1. hello Azure 儲存體用戶端程式庫產生的內容加密金鑰 (CEK)，這是一次性單次使用對稱金鑰。  
2. 使用此 CEK 加密使用者資料。   
3. hello CEK 然後再包裝 （加密） 使用 hello 金鑰的加密金鑰 (KEK)。 hello KEK 索引鍵的識別項所識別，可非對稱金鑰組或對稱金鑰，可以是本機管理或儲存在 Azure 金鑰保存庫中。  
   hello 儲存體用戶端程式庫本身完全不需要存取 tooKEK。 hello 程式庫會叫用所提供的金鑰保存庫 hello 金鑰包裝演算法。 使用者可以選擇 toouse 為金鑰包裝/解除包裝成為必要的自訂提供者。  
4. hello 加密的資料是然後上傳 toohello Azure 儲存體服務。 hello 包裝的金鑰，以及一些額外的加密中繼資料儲存為 （blob) 上的中繼資料，或與 hello 加密資料 （訊息排入佇列和資料表實體） 插補。

### <a name="decryption-via-hello-envelope-technique"></a>透過 hello 信封技術解密
解密透過 hello 信封技術的運作方式在 hello 下列方法：  

1. hello 用戶端程式庫會假設該 hello 使用者在本機或 Azure 金鑰保存庫中管理 hello 金鑰的加密金鑰 (KEK)。 hello 使用者不需要 tooknow hello 特定金鑰用於加密。 相反地，可以設定並使用索引鍵的解析程式會解析 tookeys 不同索引鍵的識別項。  
2. hello 用戶端程式庫下載 hello 加密資料，以及儲存在 hello 服務任何加密內容。  
3. 未包裝 （解密） 使用 hello 金鑰的加密金鑰 (KEK) 則 hello 包裝的內容加密金鑰 (CEK)。 以下同樣地，hello 用戶端程式庫並沒有存取 tooKEK。 它只會叫用自訂的 hello 或金鑰保存庫提供者的解除包裝的演算法。  
4. hello 內容加密金鑰 (CEK) 是則會使用 toodecrypt hello 加密使用者資料。

## <a name="encryption-mechanism"></a>加密機制
hello 儲存體用戶端程式庫會使用[AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard)順序 tooencrypt 使用者資料。 具體來說，就是 [加密區塊鏈結 (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 模式搭配 AES。 每個服務的運作方式稍有不同，我們將在這裡討論每個服務。

### <a name="blobs"></a>Blob
hello 用戶端程式庫目前支援整個 blob 只的加密。 當使用者使用 hello 時，特別是，支援加密**上傳*** 方法或 hello **openOutputStream**方法。 針對下載，則皆支援完整與範圍下載。  

在加密期間，會產生 16 個位元組，以及隨機內容加密金鑰 (CEK) 為 32 個位元組，隨機初始化向量 (IV) hello 用戶端程式庫，並將其執行 hello 使用這項資訊的 blob 資料的信封加密中。 hello 包裝 CEK 和一些額外的加密中繼資料會然後儲存 blob 中繼資料以及 hello hello 服務上加密的 blob。

> [!WARNING]
> 如果您要編輯或上傳您自己的 hello blob 的中繼資料，您會需要 tooensure 此中繼資料會保留。 如果您上傳新的中繼資料，如果沒有這個中繼資料，hello 包裝的 CEK、 IV 和其他中繼資料將會遺失且 hello blob 內容永遠不會將可擷取一次。
> 
> 

加密的 blob 下載牽涉到擷取的 hello 整個 blob 使用 hello hello 內容**下載*/openInputStream** 便利的方法。 hello 包裝的 CEK 解除包裝，且與 hello IV 一起使用 （儲存為 blob 中繼資料在此情況下） tooreturn hello 解密資料 toohello 使用者。

下載任意範圍 (**downloadRange*** 方法)，在 hello 加密的 blob 包含調整 hello 範圍提供的順序 tooget 使用者少量的額外的資料可以是使用的 toosuccessfully 解密 hello要求的範圍。  

所有 Blob 類型 (區塊 Blob、頁面 Blob 和附加 Blob) 都可以使用此機制進行加密/解密。

### <a name="queues"></a>佇列
因為佇列訊息可以是任何格式，hello 用戶端程式庫會定義包含 hello 訊息文字中的 hello 初始化向量 (IV) 與 hello 加密的內容加密金鑰 (CEK) 的自訂格式。  

在加密期間，hello 用戶端程式庫會產生 16 個位元組，以及隨機 CEK 32 個位元組的隨機 IV，並執行信封加密 hello 佇列的訊息文字使用這項資訊。 hello 包裝 CEK 和一些額外的加密中繼資料接著會加入 toohello 加密的佇列訊息。 這個修改過的訊息 （如下所示） 會儲存在 hello 服務。

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

在解密，hello 包裝的金鑰是擷取自 hello 佇列訊息，而且解除包裝。 hello IV 也是擷取自 hello 佇列訊息，並搭配 hello 解除包裝金鑰 toodecrypt hello 佇列訊息資料。 請注意 hello 的加密中繼資料是小型 （下 500 個位元組），因此它沒有會計 hello 64 KB 限制的佇列訊息，而 hello 影響應該很容易管理。

### <a name="tables"></a>資料表
hello 插入的實體屬性的用戶端程式庫支援加密和取代作業。

> [!NOTE]
> 目前不支援合併。 屬性的子集可能已加密先前使用不同的金鑰，因為只要合併 hello 新內容，並更新 hello 中繼資料會導致資料遺失。 合併 需要進行額外的服務從 hello 服務呼叫 tooread hello 預先存在的實體，或使用每個屬性的新機碼，這兩者都不適用基於效能的考量。
> 
> 

資料表資料加密的運作方式如下：  

1. 使用者指定 hello 屬性 toobe 加密。  
2. hello 用戶端程式庫會產生 16 個位元組的隨機內容加密金鑰 (CEK) 32 個位元組，針對每個實體，以及隨機初始化向量 (IV)，並執行 hello 藉由衍生新的 IV，每個加密的個別屬性 toobe 信封加密屬性。 加密的 hello 屬性會儲存為二進位資料。  
3. hello 包裝 CEK 和一些額外的加密中繼資料會儲存為兩個額外的保留屬性。 hello 第一個保留的屬性 (_ClientEncryptionMetadata1) 是保存 hello IV、 版本和包裝的金鑰資訊的字串屬性。 hello 第二個保留的屬性 (_ClientEncryptionMetadata2) 是保留加密的 hello 屬性的 hello 資訊的二進位屬性。 此第二個屬性 (_ClientEncryptionMetadata2) 中的 hello 資訊本身是加密。  
4. Toothese 其他保留所需的內容加密，因為使用者可能現在有只 250 的自訂屬性，而不是 252。 hello hello 實體的大小總計必須小於 1MB。  
   
   請注意，只有字串屬性可以加密。 如果其他屬性類型 toobe 加密，它們必須轉換的 toostrings。 hello 加密字串 hello 服務上儲存為二進位屬性，而它們會轉換後 toostrings 解密之後。
   
   對於資料表，此外 toohello 加密原則，使用者必須指定 hello 屬性 toobe 加密。 作法是指定 [Encrypt] 屬性 (針對衍生自 TableEntity 的 POCO 實體)，或在要求選項中指定加密解析程式。 加密解析程式是委派，接受資料分割索引鍵、資料列索引鍵和屬性名稱，然後傳回布林值，指出是否應該加密該屬性。 在加密期間，是否應該加密屬性，同時寫入 toohello 網路 hello 用戶端程式庫時，會使用此資訊 toodecide。 hello 委派也提供 hello 可能性的邏輯屬性加密的方式。 (例如，如果 X，則加密屬性 A，否則加密屬性 A 和 B。)請注意，就是不必要的 tooprovide 讀取或查詢實體時此資訊。

### <a name="batch-operations"></a>批次作業
在批次作業中，hello 相同 KEK 會使用於跨所有 hello 資料列中的批次作業因為 hello 用戶端程式庫只允許一個選項物件 （並因此一個原則/KEK） 每個批次作業。 不過，hello 用戶端程式庫會在內部產生新的隨機 IV 和每個資料列的隨機 CEK hello 批次中。 使用者也可以選擇 tooencrypt 不同的屬性，針對每個作業 hello 批次中在 hello 加密解析程式中定義此行為。

### <a name="queries"></a>查詢
tooperform 查詢作業，您必須指定索引鍵的解析程式所能 tooresolve 所有 hello hello 結果集中的索引鍵。 如果 hello 查詢結果中包含的實體不能是解析的 tooa 提供者，hello 用戶端程式庫會擲回錯誤。 為執行伺服器端投影的任何查詢，hello 用戶端程式庫將由預設 toohello 選取資料行加入 hello 的特殊加密中繼資料屬性 （_ClientEncryptionMetadata1 和 _ClientEncryptionMetadata2）。

## <a name="azure-key-vault"></a>Azure 金鑰保存庫
Azure 金鑰保存庫可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和密碼。 使用 Azure 金鑰保存庫時，使用者可以使用受硬體安全模組 (HSM) 保護的金鑰來加密金鑰和密碼 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.PFX 檔案和密碼)。 如需詳細資訊，請參閱 [什麼是 Azure 金鑰保存庫？](../../key-vault/key-vault-whatis.md)。

hello 儲存體用戶端程式庫會使用整個 Azure hello 金鑰保存庫核心程式庫中的順序 tooprovide 通用架構，來管理金鑰。 使用者也會使用 hello 金鑰保存庫延伸模組程式庫的 hello 其他好處。 hello 延伸模組程式庫提供有用的功能，簡單且順暢對稱/RSA 本機和雲端金鑰提供者，以及與彙總快取。

### <a name="interface-and-dependencies"></a>介面和相依性
有三個金鑰保存庫封裝：  

* azure keyvault 核心包含 hello IKey 和 IKeyResolver。 這是不具有相依性的小型封裝。 Java 的 hello 儲存體用戶端程式庫將其定義為相依性。
* azure keyvault 包含 hello 金鑰保存庫 REST 用戶端。  
* azure-keyvault-extensions 包含延伸模組程式碼，其中包含密碼編譯演算法的實作及 RSAKey 和 SymmetricKey。 它相依於 hello 核心和 KeyVault 命名空間並提供功能 toodefine 彙總的解析程式 （當使用者想 toouse 多個索引鍵的提供者） 和快取索引鍵的解析程式。 雖然 hello 儲存體用戶端程式庫不會直接依賴這個封裝，如果使用者想 toouse Azure 金鑰保存庫 toostore 其索引鍵或 toouse hello 金鑰保存庫的擴充功能 tooconsume hello 本機和雲端密碼編譯提供者，它們會需要此封裝。  
  
  金鑰保存庫是專為高價值的主要金鑰而設計，個別金鑰保存庫的節流限制都以此為設計重點。 執行時用戶端加密與金鑰保存庫，hello 慣用的模型會 toouse 對稱主要金鑰儲存為金鑰保存庫中的機密資料，並在本機快取。 使用者必須進行下列 hello:  

1. 建立密碼離線，並將它上傳 tooKey 保存庫。  
2. 參數 tooresolve hello hello 密碼加密的目前版本，並快取這項資訊在本機使用 hello 密碼的基底識別碼。 用於 CachingKeyResolver 快取。使用者是未預期的 tooimplement 自己的快取邏輯。  
3. 建立 hello 加密原則時，使用 hello 快取解析程式做為輸入。
   可以找到有關使用金鑰保存庫的詳細資訊，hello 加密程式碼範例中。 <fix URL>  

## <a name="best-practices"></a>最佳作法
加密已支援只能在 Java 的 hello 儲存體用戶端程式庫中。

> [!IMPORTANT]
> 使用用戶端加密時，請留意以下重點：
> 
> * 當從進行讀取或寫入 tooan 加密 blob、 使用完整的 blob 上傳的命令和範圍/整個 blob 下載命令。 避免撰寫 tooan 加密的 blob，使用通訊協定作業，例如將區塊、 放置區塊清單、 寫入的頁面，清除頁面或附加區塊;否則，您可能會破壞 hello 加密的 blob，並使它無法讀取。
> * 對於資料表，存在類似的條件約束。 能謹慎 toonot 更新加密內容，而無須更新 hello 加密中繼資料。  
> * 如果您在 hello 加密的 blob 上設定中繼資料，您可能會覆寫 hello 加密相關中繼資料所需來解密，因為設定中繼資料不是加總。 快照集也是如此。在為加密的 Blob 建立快照集時，請避免指定中繼資料。 如果必須設定中繼資料，是確定 toocall hello **downloadAttributes**方法的第一個 tooget hello 目前的加密中繼資料和中繼資料在設定時，避免並行寫入。  
> * 啟用 hello **requireEncryption**中應僅適用於加密資料的使用者 hello 預設要求選項旗標。 如需詳細資訊請參閱下方內容。  
> 
> 

## <a name="client-api--interface"></a>用戶端 API / 介面
使用者在建立 EncryptionPolicy 物件時，可以只提供金鑰 (實作 IKey)、只提供者解析程式 (實作 IKeyResolver)，或兩者都提供。 IKey 是 hello 基本金鑰，用來識別索引鍵的識別項和類型，提供用來包裝/解除包裝的 hello 邏輯。 IKeyResolver hello 解密程序期間會使用的 tooresolve 索引鍵。 它定義 ResolveKey 方法，可根據金鑰識別碼傳回 IKey。 這會提供使用者 hello 能力 toochoose 之間的多個位置中受管理的多個索引鍵。

* 用於加密，hello 索引鍵永遠且沒有金鑰 hello 情況下會導致錯誤。  
* 解密：  
  
  * 如果指定 tooget hello 索引鍵，則會叫用 hello 索引鍵的解析程式。 如果指定 hello 解析程式，但是沒有 hello 之金鑰識別碼的對應，會擲回錯誤。  
  * 如果未指定解析程式，但指定的索引鍵，hello 金鑰可用如果其識別項所需的 hello 與金鑰識別碼相符。 如果 hello 識別碼不符合，則會擲回錯誤。  
    
    hello[加密範例](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples)<fix URL>示範更詳細的端對端案例，適用於 blob、 佇列和資料表，以及與金鑰保存庫整合。

### <a name="requireencryption-mode"></a>RequireEncryption 模式
使用者可以針對所有上傳和下載都必須加密的作業模式，從中選擇啟用。 在此模式中，嘗試 tooupload 資料，而不會加密 hello 服務的加密原則或下載資料不會失敗 hello 用戶端上。 hello **requireEncryption**旗標的 hello 要求選項物件控制這個行為。 如果您的應用程式將會加密儲存在 Azure 儲存體中的所有物件，則您可以將 hello **requireEncryption** hello hello 服務用戶端物件的預設要求選項上的屬性。   

例如，使用**CloudBlobClient.getDefaultRequestOptions().setRequireEncryption(true)** toorequire 加密所有的 blob 作業透過該用戶端物件來執行。

### <a name="blob-service-encryption"></a>Blob 服務加密
建立**BlobEncryptionPolicy**物件，並將它設定在 hello 要求選項 (每個應用程式開發介面或使用用戶端層級**DefaultRequestOptions**)。 所有其他項目將 hello 用戶端程式庫在內部進行處理。

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

// Set hello encryption policy on hello request options.
BlobRequestOptions options = new BlobRequestOptions();
options.setEncryptionPolicy(policy);

// Upload hello encrypted contents toohello blob.
blob.upload(stream, size, null, options, null);

// Download and decrypt hello encrypted contents from hello blob.
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
blob.download(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a>佇列服務加密
建立**QueueEncryptionPolicy**物件，並將它設定在 hello 要求選項 (每個應用程式開發介面或使用用戶端層級**DefaultRequestOptions**)。 所有其他項目將 hello 用戶端程式庫在內部進行處理。

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

// Add message
QueueRequestOptions options = new QueueRequestOptions();
options.setEncryptionPolicy(policy);

queue.addMessage(message, 0, 0, options, null);

// Retrieve message
CloudQueueMessage retrMessage = queue.retrieveMessage(30, options, null);
```

### <a name="table-service-encryption"></a>資料表服務加密
此外 toocreating 加密原則和設定要求的選項，您必須指定**EncryptionResolver**中**TableRequestOptions**，或在 hello hello [加密] 屬性實體的 getter 和 setter。

### <a name="using-hello-resolver"></a>使用 hello 解析程式

```java
// Create hello IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create hello encryption policy toobe used for upload and download.
TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

TableRequestOptions options = new TableRequestOptions()
options.setEncryptionPolicy(policy);
options.setEncryptionResolver(new EncryptionResolver() {
    public boolean encryptionResolver(String pk, String rk, String key) {
        if (key == "foo")
        {
            return true;
        }
        return false;
    }
});

// Insert Entity
currentTable.execute(TableOperation.insert(ent), options, null);

// Retrieve Entity
// No need toospecify an encryption resolver for retrieve
TableRequestOptions retrieveOptions = new TableRequestOptions()
retrieveOptions.setEncryptionPolicy(policy);

TableOperation operation = TableOperation.retrieve(ent.PartitionKey, ent.RowKey, DynamicTableEntity.class);
TableResult result = currentTable.execute(operation, retrieveOptions, null);
```

### <a name="using-attributes"></a>使用屬性
如前所述，如果 hello 實體實作 TableEntity，然後 hello 屬性 getter 和 setter 可以以 hello [加密] 屬性，而不是指定 hello 裝飾**EncryptionResolver**。

```java
private string encryptedProperty1;

@Encrypt
public String getEncryptedProperty1 () {
    return this.encryptedProperty1;
}

@Encrypt
public void setEncryptedProperty1(final String encryptedProperty1) {
    this.encryptedProperty1 = encryptedProperty1;
}
```

## <a name="encryption-and-performance"></a>加密和效能
請注意，加密您的儲存體資料會造成額外的效能負擔。 hello 必須產生金鑰和 IV，hello 內容本身必須經過加密、 和其他中繼資料必須格式化，並且上傳內容。 這項負擔會根據 hello 所加密的資料數量而有所不同。 我們建議客戶一定要在開發期間測試其應用程式的效能。

## <a name="next-steps"></a>後續步驟
* 下載 hello [Java Maven 套件的 Azure 儲存體用戶端程式庫](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)  
* 下載 hello[從 GitHub Java 原始碼的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-java)   
* 下載 Java Maven 套件 hello Azure 金鑰保存庫 Maven 程式庫：
  * [核心](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault-core) 封裝
  * [用戶端](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault) 封裝
* 請瀏覽 hello [Azure 金鑰保存庫文件](../../key-vault/key-vault-whatis.md)
