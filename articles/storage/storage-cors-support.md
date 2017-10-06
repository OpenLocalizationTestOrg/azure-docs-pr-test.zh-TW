---
title: "aaaCross 原始資源共用 (CORS) 支援 |Microsoft 文件"
description: "深入了解如何 tooenable hello Microsoft Azure 儲存體服務的 CORS 支援。"
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: carmonm
editor: tysonn
ms.assetid: a0229595-5b64-4898-b8d6-fa2625ea6887
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 2/22/2017
ms.author: cbrooks
ms.openlocfilehash: 0a6ec3bf6999c5faa7f0912dc2a47921aa01d3d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cross-origin-resource-sharing-cors-support-for-hello-azure-storage-services"></a>Hello Azure 儲存體服務的跨原始資源共用 (CORS) 支援
從 2013年-08-15 版開始，hello Azure 儲存體服務支援跨原始資源共用 (CORS) hello Blob、 資料表、 佇列和檔案服務。 CORS 是 HTTP 功能，可讓 web 應用程式執行另一個網域中的下一個網域 tooaccess 資源。 網頁瀏覽器實作稱為安全性限制[相同來源原則](http://www.w3.org/Security/wiki/Same_Origin_Policy)，用於防止網頁呼叫 Api 在不同的網域。CORS 提供安全的方式 tooallow 一個網域 （hello 原始網域） toocall 另一個網域中的應用程式開發介面。 請參閱 hello [CORS 規格](http://www.w3.org/TR/cors/)如 CORS 的詳細資訊。

您可以個別設定 CORS 規則 hello 的每個儲存體服務，藉由呼叫[設定 Blob 服務屬性](https://msdn.microsoft.com/library/hh452235.aspx)，[設定佇列服務屬性](https://msdn.microsoft.com/library/hh452232.aspx)，和[設定表格服務屬性](https://msdn.microsoft.com/library/hh452240.aspx). 一旦您設定 hello hello 服務的 CORS 規則，那麼對 hello 服務發出來自不同網域的適當驗證的要求將不評估的 toodetermine 是否允許根據您指定的 toohello 規則。

> [!NOTE]
> 請注意，CORS 不是一種驗證機制。 啟用 CORS 時，對儲存體資源所提出的任何要求都必須具有適當的驗證簽章，或者必須對公用資源提出。
> 
> 

## <a name="understanding-cors-requests"></a>了解 CORS 要求
來自原始網域的 CORS 要求可能包含兩個不同要求：

* 預檢要求，查詢會在 hello 服務所加諸的 hello CORS 限制。 需要 hello 預檢要求，除非 hello 要求方法[簡單的方法](http://www.w3.org/TR/cors/)，這表示 GET、 HEAD 或 POST。
* hello 實際要求，針對 hello 進行所需的資源。

### <a name="preflight-request"></a>預檢要求
hello 預檢要求會查詢 hello 已 hello 帳戶擁有者建立 hello 儲存體服務的 CORS 限制。 hello 網頁瀏覽器 （或其他使用者代理程式） 選項會將要求傳送包含 hello 要求標頭、 方法和原始網域。 hello 儲存體服務會評估一組預先設定的 CORS 規則來指定哪一個原始網域、 要求方法為基礎的 hello 預期作業和要求標頭可能會針對儲存體資源的實際要求上指定。

如果啟用 hello 服務的 CORS，且 CORS 規則符合預檢要求的 hello，hello 服務會以狀態碼 200 （確定） 回應，並且納入 hello 回應 hello 所需的 Access-control 標頭。

如果 hello 服務未啟用 CORS 或 CORS 規則不符合 hello 預檢要求，hello 服務將會以狀態碼 403 （禁止） 回應。

如果 OPTIONS 要求不包含的 hello hello 必要的 CORS 標頭 （hello 原點和存取控制-要求方法標頭），hello 服務會回應以狀態碼 400 （不正確的要求）。

請注意，預檢要求會評估 hello 服務 （Blob、 佇列和資料表），但不檢查 hello 要求的資源。 hello 帳戶擁有者必須啟用 CORS，為了讓 hello 要求 toosucceed hello 帳戶服務屬性的一部分。

### <a name="actual-request"></a>實際要求
一旦接受 hello 預檢要求，會傳回 hello 回應 hello 瀏覽器會發送 hello 針對 hello 儲存體資源的實際要求。 如果 hello 預檢要求遭到拒絕，請立即 hello 瀏覽器將會拒絕 hello 實際要求。

hello 實際要求會被視為對 hello 儲存體服務的一般要求。 hello 存在 hello Origin 標頭表示 hello 要求是 CORS 要求，並 hello 服務會檢查 hello 比對 CORS 規則。 如果找到相符項目，會加入的 toohello 回應 hello Access-control 標頭，並傳送後 toohello 用戶端。 如果找不到相符項目，不會傳回 hello CORS Access-control 標頭。

## <a name="enabling-cors-for-hello-azure-storage-services"></a>啟用 hello Azure 儲存體服務的 CORS
在 hello 服務層級，會設定 CORS 規則，因此您需要 tooenable 或停用 CORS，每個服務 （Blob、 佇列和表格） 分開。 根據預設，每個服務都會停用 CORS。 tooenable CORS，您需要 tooset hello 適當的服務屬性使用 2013年-08-15 版或更新版本，並將 CORS 規則 toohello 服務屬性。 如需詳細資訊，關於如何 tooenable 或服務及其如何 tooset CORS 規則，請停用 CORS 太參考[設定 Blob 服務屬性](https://msdn.microsoft.com/library/hh452235.aspx)，[設定佇列服務屬性](https://msdn.microsoft.com/library/hh452232.aspx)，和[設定資料表服務屬性](https://msdn.microsoft.com/library/hh452240.aspx)。

以下範例是透過設定服務屬性作業指定的單一 CORS 規則：

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

下面會描述 hello CORS 規則中包含每個項目：

* **AllowedOrigins**： 允許 toomake hello 原始網域透過 CORS 對 hello 儲存體要求服務。 hello 原始網域是要求源自的 hello 的 hello 網域。 請注意 hello 來源必須具有 hello 使用者年齡傳送 toohello 服務的 hello 原始來源區分大小寫完全相符。 您也可以使用 hello 萬用字元 ' *' tooallow 所有原始網域 toomake 透過 CORS 要求。 Hello 上述範例中，在 hello 網域[http://www.contoso.com](http://www.contoso.com)和[http://www.fabrikam.com](http://www.fabrikam.com)可對使用 CORS hello 服務的要求。
* **AllowedMethods**: hello 方法 （HTTP 要求動詞命令） 該 hello 原始網域可能用於 CORS 要求。 Hello 上述範例中，允許使用只有 PUT 和 GET 要求。
* **AllowedHeaders**: hello 要求標頭的 hello 原始網域可在 hello CORS 要求上指定。 Hello 上述範例中，允許開頭 x-ms-中繼資料，x ms-中繼-目標和 x ms-中繼 abc 的所有中繼資料標頭。 請注意該 hello 萬用字元 ' *' 表示 hello 任何標頭開頭指定允許前置詞。
* **ExposedHeaders**: hello 可能 hello 回應 toohello CORS 要求中傳送和 hello 瀏覽器 toohello 要求簽發者所公開的回應標頭。 在上面，hello 瀏覽器的 hello 範例為指示 tooexpose x-ms-中繼，任何標頭開頭。
* **MaxAgeInSeconds**: hello 最大時間量瀏覽器應該快取預檢 OPTIONS 要求 hello。

hello Azure 儲存體服務支援指定帶有前置詞的標頭這兩個 hello **AllowedHeaders**和**ExposedHeaders**項目。 tooallow 標頭的類別，您可以指定相同的前置詞 toothat 類別目錄。 例如，指定 *x-ms-meta** 做為有前置詞的標頭會建立一項規則，可比對開頭為 x-ms-meta 的所有標頭。

hello 下列限制適用於 tooCORS 規則：

* 您可以將每個儲存體服務 （Blob、 資料表和佇列） 的 CORS 規則指定 toofive 組成。
* hello 所有 CORS 規則設定 hello 要求時，排除 XML 標記的大小上限不得超過 2 KB。
* 允許的標頭、 公開的標頭或允許的原始網域的 hello 長度不可超過 256 個字元。
* 允許的標頭和公開的標頭可以是：
  * 常值標頭，即 hello 確切的標頭提供名稱，例如**x ms-中繼-處理**。 可能在 hello 要求中指定最多 64 個常值標頭。
  * 前置詞的標頭，即 hello 標頭的前置詞提供，例如**x ms-中繼資料***。 以這種方式指定前置詞，允許或公開以給定前置詞的 hello 開頭的任何標頭。 可能在 hello 要求中指定兩個帶有前置詞的標頭的最大值。
* 在 hello hello 方法 （或 HTTP 動詞命令） 指定**AllowedMethods**項目必須符合 Azure 儲存體服務 Api 支援 toohello 方法。 支援的方法為 DELETE、GET、HEAD、MERGE、POST、OPTIONS 及 PUT。

## <a name="understanding-cors-rule-evaluation-logic"></a>了解 CORS 規則評估邏輯
儲存體服務收到預檢或實際要求時，它會評估該要求，根據您已建立 hello 服務透過適當設定服務屬性作業 hello hello CORS 規則。 CORS 規則的評估順序 hello hello 的 hello 設定服務屬性作業的要求本文中所設定。

CORS 規則的評估，如下所示：

1. 首先，hello 原始網域的 hello 要求會檢查是否符合列出的 hello 的 hello 網域**AllowedOrigins**項目。 如果 hello 原始網域包含在 hello 清單或允許所有網域包含 hello 萬用字元 ' *'，然後將會繼續評估規則。 如果不包含 hello 原始網域，則 hello 要求會失敗。
2. 接下來，hello 要求 hello 方法 （或 HTTP 動詞命令） 會針對檢查 hello 中所列的 hello 方法**AllowedMethods**項目。 如果 hello 方法包含在 hello 清單中，然後會繼續評估規則。如果沒有，就會 hello 要求失敗。
3. 如果 hello 要求符合原始網域和其方法中的規則，該規則選取的 tooprocess hello 要求並沒有進一步的規則會進行評估。 Hello 要求才會成功之前，不過，任何 hello 要求上指定的標頭會針對檢查 hello 標頭列在 hello **AllowedHeaders**項目。 如果傳送嗨標頭不符合允許的標頭的 hello，hello 要求將會失敗。

因為 hello 規則的處理順序 hello 會出現在 hello 要求主體，最佳做法建議您指定 hello 最嚴格的規則與尊重 tooorigins 第一次在 hello 清單中，以便先評估這些。 指定的規則較不嚴格，例如規則 tooallow 所有來源 – 在 hello hello 清單的結尾。

### <a name="example--cors-rules-evaluation"></a>範例 - CORS 規則評估
hello 下列範例顯示 hello 儲存體服務作業 tooset CORS 規則的部分要求主體。 請參閱[設定 Blob 服務屬性](https://msdn.microsoft.com/library/hh452235.aspx)，[設定佇列服務屬性](https://msdn.microsoft.com/library/hh452232.aspx)，和[設定表格服務屬性](https://msdn.microsoft.com/library/hh452240.aspx)如需建構 hello 要求詳細資料。

```xml
<Cors>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>PUT,HEAD</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>*</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-client-request-id</AllowedHeaders>
    </CorsRule>
</Cors>
```

接下來，請考慮下列 CORS 要求的 hello:

| 要求 |  |  | Response |  |
| --- | --- | --- | --- | --- |
| **方法** |**原始** |**要求標頭** |**規則相符** |**結果** |
| **PUT** |http://www.contoso.com |x-ms-blob-content-type |第一個規則 |成功 |
| **GET** |http://www.contoso.com |x-ms-blob-content-type |第二個規則 |成功 |
| **GET** |http://www.contoso.com |x-ms-client-request-id |第二個規則 |失敗 |

hello 第一個要求符合第一個規則的 hello – hello 原始網域符合允許出處 hello、 hello 方法符合允許的方法，hello 和 hello 標頭符合允許的標頭 – hello，因此成功。

hello 第二個要求不符合 hello 第一個規則，因為 hello 方法不符合 hello 允許方法。 它，不過，與相符 hello 第二個規則，讓它成功。

hello 第三個要求符合 hello 第二個規則在原始網域和方法，因此會不評估任何進一步的規則。 不過，hello *x ms-用戶端的要求識別碼標頭*不允許 hello 第二個規則，因此儘管 hello 事實，hello 語意 hello 第三個規則的允許 toosucceed hello 要求失敗。

> [!NOTE]
> 雖然這個範例會顯示較不嚴格的規則之前更嚴格，一般而言 hello 最佳作法是 toolist hello 最嚴格的規則第一次。
> 
> 

## <a name="understanding-how-hello-vary-header-is-set"></a>了解如何設定 hello Vary 標頭
hello*區分*標頭是一組通知關於 hello 伺服器 tooprocess hello 要求所選取的 hello 準則 hello 瀏覽器或使用者代理程式的要求標頭欄位所組成的標準 HTTP/1.1 標頭。 hello*區分*標頭主要是用於快取，proxy、 瀏覽器及 Cdn 使用它 toodetermine 如何 hello 快取回應。 如需詳細資訊，請參閱 hello hello 規格[Vary 標頭](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)。

當 hello 瀏覽器或其他使用者代理程式會快取 CORS 要求的回應 hello 時，hello 原始網域會快取為允許原始的 hello。 當第二個網域問題 hello 相同儲存體資源的要求，當 hello 快取為作用中、 hello 使用者代理程式會擷取 hello 快取的原始網域。 hello 第二個網域不符合 hello 快取的網域，因此 hello 要求失敗時符合則成功。 在某些情況下，Azure 儲存體設定 hello Vary 標頭太**原點**tooinstruct hello 使用者代理程式 toosend hello 後續 CORS 要求 toohello 服務要求網域與 hello hello 快取來源。

Azure 儲存體設定 hello*區分*標頭太**原點**hello 下列案例中，實際 GET/HEAD 要求：

* 當 hello 原始網域完全符合 hello 允許要求的 CORS 規則所定義的來源。 toobe 完全相符，hello CORS 規則不能包含萬用字元 '*' 字元。
* 沒有規則相符 hello 要求來源，但啟用 hello 儲存體服務的 CORS。

在 hello 其中 GET/HEAD 要求符合允許所有原始網域的 CORS 規則的情況下，hello 回應表示允許所有原始網域，而且 hello 使用者代理程式快取時將會允許來自任何原始網域的後續要求為作用中的 hello 快取。

請注意，使用非 GET/HEAD 方法要求，hello 儲存體服務不會設定 hello Vary 標頭，因為回應 toothese 方法不會快取使用者代理程式。

hello 下表指出 Azure 儲存體如何將回應 tooGET/HEAD 要求根據 hello 先前所述的案例：

| 要求 | 帳戶設定和規則評估的結果 |  |  | Response |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **要求上存在的 Origin 標頭** |**針對此服務指定的 CORS 規則** |**有允許所有原始網域的比對規則存在 (*)** |**有完全符合原始網域的比對規則存在** |**回應包括 Vary 標頭集合 tooOrigin** |**回應包含 Access-Control-Allowed-Origin："*"** |**回應包含 Access-Control-Exposed-Headers** |
| 否 |否 |否 |否 |否 |否 |否 |
| 否 |是 |否 |否 |是 |否 |否 |
| 否 |是 |是 |否 |否 |是 |是 |
| 是 |否 |否 |否 |否 |否 |否 |
| 是 |是 |否 |是 |是 |否 |是 |
| 是 |是 |否 |否 |是 |否 |否 |
| 是 |是 |是 |否 |否 |是 |是 |

## <a name="billing-for-cors-requests"></a>CORS 要求的計費方式
成功的預檢要求會計費，如果您已啟用的任何 hello 您帳戶的儲存體服務的 CORS (透過呼叫[設定 Blob 服務屬性](https://msdn.microsoft.com/library/hh452235.aspx)，[設定佇列服務屬性](https://msdn.microsoft.com/library/hh452232.aspx)，或[設定表格服務屬性](https://msdn.microsoft.com/library/hh452240.aspx))。 toominimize 費用，請考慮設定 hello **MaxAgeInSeconds**項目中將 CORS 規則 tooa 大數值而 hello 使用者代理程式會快取 hello 要求。

未成功的預檢要求將不會列入計費。

## <a name="next-steps"></a>後續步驟
[設定 Blob 服務屬性](https://msdn.microsoft.com/library/hh452235.aspx)

[設定佇列服務屬性](https://msdn.microsoft.com/library/hh452232.aspx)

[設定資料表服務屬性](https://msdn.microsoft.com/library/hh452240.aspx)

[W3C 跨原始資源共用規格](http://www.w3.org/TR/cors/)

