---
title: "Microsoft Azure 儲存體使用 Python aaaClient 端加密 |Microsoft 文件"
description: "hello Python 的 Azure 儲存體用戶端程式庫支援用戶端加密您的 Azure 儲存體應用程式最高的安全性。"
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 3a52b64f93daf85a55308f8a4bee9c98b2315d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Microsoft Azure 儲存體的用戶端 Python 加密
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>概觀
hello [Python 的 Azure 儲存體用戶端程式庫](https://pypi.python.org/pypi/azure-storage)支援 tooAzure 存放裝置，將上傳和下載 toohello 用戶端時解密資料之前加密用戶端應用程式內的資料。

> [!NOTE]
> hello Azure 儲存體 Python 程式庫為預覽狀態。
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>加密和解密透過 hello 信封技術
加密和解密的 hello 處理程序遵循 hello 信封技術。

### <a name="encryption-via-hello-envelope-technique"></a>加密透過 hello 信封技術
透過 hello 信封技術的加密方式 hello 下列方法：

1. hello Azure 儲存體用戶端程式庫產生的內容加密金鑰 (CEK)，這是一次性單次使用對稱金鑰。
2. 使用此 CEK 加密使用者資料。
3. hello CEK 然後再包裝 （加密） 使用 hello 金鑰的加密金鑰 (KEK)。 hello KEK 索引鍵的識別項所識別，而且可以是對稱的金鑰組或對稱金鑰，本機管理。
   hello 儲存體用戶端程式庫本身完全不需要存取 tooKEK。 hello 程式庫會叫用 hello 金鑰包裝演算法所提供的 hello KEK。 使用者可以選擇 toouse 為金鑰包裝/解除包裝成為必要的自訂提供者。
4. hello 加密的資料是然後上傳 toohello Azure 儲存體服務。 hello 包裝的金鑰，以及一些額外的加密中繼資料儲存為 （blob) 上的中繼資料，或與 hello 加密資料 （訊息排入佇列和資料表實體） 插補。

### <a name="decryption-via-hello-envelope-technique"></a>透過 hello 信封技術解密
解密透過 hello 信封技術的運作方式在 hello 下列方法：

1. hello 用戶端程式庫會假設該 hello 使用者在本機管理 hello 金鑰的加密金鑰 (KEK)。 hello 使用者不需要 tooknow hello 特定金鑰用於加密。 相反地，索引鍵的解決器，解析不同的金鑰識別碼 tookeys，可以設定和使用。
2. hello 用戶端程式庫下載 hello 加密資料，以及儲存在 hello 服務任何加密內容。
3. 未包裝 （解密） 使用 hello 金鑰的加密金鑰 (KEK) 則 hello 包裝的內容加密金鑰 (CEK)。 以下同樣地，hello 用戶端程式庫並沒有存取 tooKEK。 只要叫用 hello 自訂提供者的解除包裝的演算法。
4. hello 內容加密金鑰 (CEK) 是則會使用 toodecrypt hello 加密使用者資料。

## <a name="encryption-mechanism"></a>加密機制
hello 儲存體用戶端程式庫會使用[AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard)順序 tooencrypt 使用者資料。 具體來說，就是 [加密區塊鏈結 (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 模式搭配 AES。 每個服務的運作方式稍有不同，我們將在這裡討論每個服務。

### <a name="blobs"></a>Blob
hello 用戶端程式庫目前支援整個 blob 只的加密。 當使用者使用 hello 時，特別是，支援加密**建立*** 方法。 針對下載項目同時支援完整與範圍下載，也提供上傳與下載的平行處理。

在加密期間，會產生 16 個位元組，以及隨機內容加密金鑰 (CEK) 為 32 個位元組，隨機初始化向量 (IV) hello 用戶端程式庫，並將其執行 hello 使用這項資訊的 blob 資料的信封加密中。 hello 包裝 CEK 和一些額外的加密中繼資料會然後儲存 blob 中繼資料以及 hello hello 服務上加密的 blob。

> [!WARNING]
> 如果您要編輯或上傳您自己的 hello blob 的中繼資料，您會需要 tooensure 此中繼資料會保留。 如果您上傳新的中繼資料，如果沒有這個中繼資料，hello 包裝的 CEK、 IV 和其他中繼資料將會遺失且 hello blob 內容永遠不會將可擷取一次。
> 
> 

加密的 blob 下載牽涉到擷取的 hello 整個 blob 使用 hello hello 內容**取得*** 便利的方法。 hello 包裝的 CEK 解除包裝，且與 hello IV 一起使用 （儲存為 blob 中繼資料在此情況下） tooreturn hello 解密資料 toohello 使用者。

下載任意範圍 (**取得*** 具有範圍參數的方法傳入) 在 hello 加密的 blob 會包括調整 hello 順序 tooget 少量可用的其他資料中的使用者所提供的範圍toosuccessfully 解密 hello 要求範圍。

區塊 Blob 和分頁 Blob 只可以使用這種配置加密/解密。 目前不支援加密附加 Blob。

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
3. hello 包裝 CEK 和一些額外的加密中繼資料會儲存為兩個額外的保留屬性。 hello 先保留屬性 (\_ClientEncryptionMetadata1) 是保存 hello IV、 版本和包裝的金鑰資訊的字串屬性。 hello 第二個保留的屬性 (\_ClientEncryptionMetadata2) 是保留加密的 hello 屬性的 hello 資訊的二進位屬性。 hello 這個第二個屬性中的資訊 (\_ClientEncryptionMetadata2) 本身經過加密。
4. Toothese 其他保留所需的內容加密，因為使用者可能現在有只 250 的自訂屬性，而不是 252。 hello hello 實體的大小總計必須小於 1MB。
   
   請注意，只有字串屬性可以加密。 如果其他屬性類型 toobe 加密，它們必須轉換的 toostrings。 hello 加密字串 hello 服務上儲存為二進位屬性，而它們會轉換後 toostrings （原始字串，不具有類型 EdmType.STRING EntityProperties） 解密之後。
   
   對於資料表，此外 toohello 加密原則，使用者必須指定 hello 屬性 toobe 加密。 這可藉由在 hello 類型組 tooEdmType.STRING TableEntity 物件中任一儲存這些屬性，並將加密 hello tableservice 物件上的設定 tootrue 或設定 hello encryption_resolver_function。 加密解析程式是函式，接受資料分割索引鍵、資料列索引鍵和屬性名稱，然後傳回布林值，指出是否應該加密該屬性。 在加密期間，是否應該加密屬性，同時寫入 toohello 網路 hello 用戶端程式庫時，會使用此資訊 toodecide。 hello 委派也提供 hello 可能性的邏輯屬性加密的方式。 (例如，如果 X，則加密屬性 A，否則加密屬性 A 和 B。)請注意，就是不必要的 tooprovide 讀取或查詢實體時此資訊。

### <a name="batch-operations"></a>批次作業
加密原則適用於 tooall hello 批次中的資料列。 hello 用戶端程式庫在內部將會產生新的隨機 IV 和每個資料列的隨機 CEK hello 批次中。 使用者也可以選擇 tooencrypt 不同的屬性，針對每個作業 hello 批次中在 hello 加密解析程式中定義此行為。
如果批次透過 hello tableservice batch() 方法建立為內容管理員，hello tableservice 加密原則會自動套用的 toohello 批次。 藉由呼叫 hello 建構函式明確地建立批次時，如果 hello 加密原則必須傳遞為參數和 hello 存留期的 hello 批次未修改的左。
請注意到使用 hello 批次 （在認可使用 hello tableservice 加密原則的 hello 批次的 hello 階段不會加密實體） 的加密原則的 hello 批次插入時，會加密實體。

### <a name="queries"></a>查詢
tooperform 查詢作業，您必須指定索引鍵的解析程式所能 tooresolve 所有 hello hello 結果集中的索引鍵。 如果 hello 查詢結果中包含的實體不能是解析的 tooa 提供者，hello 用戶端程式庫會擲回錯誤。 對於執行伺服器端投影的任何查詢，hello 用戶端程式庫會將加入 hello 特殊加密中繼資料屬性 (\_ClientEncryptionMetadata1 和\_ClientEncryptionMetadata2) 預設 toohello 所選取的資料行.

> [!IMPORTANT]
> 使用用戶端加密時，請留意以下重點：
> 
> * 當從進行讀取或寫入 tooan 加密 blob、 使用完整的 blob 上傳的命令和範圍/整個 blob 下載命令。 避免撰寫 tooan 加密的 blob，使用通訊協定的作業，例如將區塊、 放置區塊清單、 撰寫網頁或清除的頁面。否則，您可能會破壞 hello 加密的 blob，並使它無法讀取。
> * 對於資料表，存在類似的條件約束。 能謹慎 toonot 更新加密內容，而無須更新 hello 加密中繼資料。
> * 如果您在 hello 加密的 blob 上設定中繼資料，您可能會覆寫 hello 加密相關中繼資料所需來解密，因為設定中繼資料不是加總。 快照集也是如此。在為加密的 Blob 建立快照集時，請避免指定中繼資料。 如果必須設定中繼資料，是確定 toocall hello **get_blob_metadata**方法的第一個 tooget hello 目前的加密中繼資料和中繼資料在設定時，避免並行寫入。
> * 啟用 hello **require_encryption** hello 服務只應搭配加密資料的使用者物件上的旗標。 如需詳細資訊請參閱下方內容。
> 
> 

hello 儲存體用戶端程式庫預期 hello 提供 KEK 和索引鍵的解析程式 tooimplement hello 下列介面。 [Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/) 支援尚未推出，並會在完成時整合到此程式庫。

## <a name="client-api--interface"></a>用戶端 API / 介面
Hello 使用者已建立儲存體服務物件 (也就是 blockblobservice) 之後，可能會指派值 toohello 欄位構成加密原則： key_encryption_key，key_resolver_function，和 require_encryption。 使用者可以僅提供 KEK、僅提供解析程式，或是兩者皆提供。 key_encryption_key 是 hello 基本金鑰，用來識別索引鍵的識別項和類型，提供用來包裝/解除包裝的 hello 邏輯。 key_resolver_function hello 解密程序期間會使用的 tooresolve 索引鍵。 它會傳回指定金鑰識別碼的有效 KEK。 這會提供使用者 hello 能力 toochoose 之間的多個位置中受管理的多個索引鍵。

hello KEK 必須實作下列 hello 方法 toosuccessfully 加密資料：

* wrap_key(cek)： 包裝 hello 指定 CEK （位元組） 使用 hello 使用者選擇的演算法。 傳回 hello 的已包裝金鑰。
* get_key_wrap_algorithm()： 傳回 hello 演算法會使用 toowrap 索引鍵。
* get_kid()： 針對這個 KEK 的傳回 hello 字串索引鍵識別碼。
  hello KEK 必須實作下列方法 toosuccessfully 解密資料的 hello:
* unwrap_key （cek，演算法）： hello 傳回解除包裝的 hello 形式指定 CEK 使用 hello 字串指定的演算法。
* get_kid()：傳回此 KEK 的字串金鑰識別碼。

hello 索引鍵的解析程式必須至少實作可在指定索引鍵的識別碼，傳回 hello 對應 KEK 實作 hello 介面上述的方法。 只有這個方法是 toobe 指派 toohello key_resolver_function 屬性在 hello 服務物件。

* 用於加密，hello 索引鍵永遠且沒有金鑰 hello 情況下會導致錯誤。
* 解密：
  
  * 如果指定 tooget hello 索引鍵，則會叫用 hello 索引鍵的解析程式。 如果指定 hello 解析程式，但是沒有 hello 之金鑰識別碼的對應，會擲回錯誤。
  * 如果未指定解析程式，但指定的索引鍵，hello 金鑰可用如果其識別項所需的 hello 與金鑰識別碼相符。 如果 hello 識別碼不符合，則會擲回錯誤。
    
    hello azure.storage.samples 加密範例<fix URL>示範更詳細的端對端案例，適用於 blob、 佇列和資料表。
      Hello KEK 和索引鍵的解析程式的範例實作，提供 hello 範例檔案中 KeyWrapper 和 KeyResolver 分別。

### <a name="requireencryption-mode"></a>RequireEncryption 模式
使用者可以針對所有上傳和下載都必須加密的作業模式，從中選擇啟用。 在此模式中，嘗試 tooupload 資料，而不會加密 hello 服務的加密原則或下載資料不會失敗 hello 用戶端上。 hello **require_encryption**旗標上 hello 服務物件控制這個行為。

### <a name="blob-service-encryption"></a>Blob 服務加密
Hello blockblobservice 物件上設定 hello 加密原則欄位。 所有其他項目將 hello 用戶端程式庫在內部進行處理。

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>佇列服務加密
Hello queueservice 物件上設定 hello 加密原則欄位。 所有其他項目將 hello 用戶端程式庫在內部進行處理。

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>資料表服務加密
此外 toocreating 加密原則和設定要求的選項，您必須指定**encryption_resolver_function**上 hello **tableservice**，或使用加密屬性上設定 hellohello EntityProperty。

### <a name="using-hello-resolver"></a>使用 hello 解析程式

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>使用屬性
如上面所述，屬性可能會標示為加密儲存在 EntityProperty 物件中，並設定 hello 加密欄位。

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>加密和效能
請注意，加密您的儲存體資料會造成額外的效能負擔。 hello 必須產生金鑰和 IV，hello 內容本身必須經過加密、 和其他中繼資料必須格式化，並且上傳內容。 這項負擔會根據 hello 所加密的資料數量而有所不同。 我們建議客戶一定要在開發期間測試其應用程式的效能。

## <a name="next-steps"></a>後續步驟
* 下載 hello [Java PyPi 套件的 Azure 儲存體用戶端程式庫](https://pypi.python.org/pypi/azure-storage)
* 下載 hello [Python 從原始程式碼 GitHub 的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-python)
