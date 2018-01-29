---
title: "Azure CDN 規則引擎功能 | Microsoft Docs"
description: "Azure CDN 規則引擎比對條件和功能的參考文件。"
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 858bc1dd2880583a3283522a01c9a48679b76296
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Azure CDN 規則引擎功能
本文列出的詳細的描述可用的功能的 Azure 內容傳遞網路 (CDN)[規則引擎](cdn-rules-engine.md)。

規則的第三個部分是功能。 一個功能可定義一組符合條件所識別的要求的型別套用的動作類型。

## <a name="access-features"></a>存取功能

這些功能是設計來控制內容的存取權。


名稱 | 目的
-----|--------
[拒絕存取 (403)](#deny-access-403) | 判斷所有要求是否已遭拒絕且含有 [403 禁止] 回應。
[權杖驗證](#token-auth) | 決定是否權杖型驗證會套用至要求。
[權杖驗證拒絕程式碼](#token-auth-denial-code) | 決定由於權杖型驗證的要求遭到拒絕時，會傳回給使用者的回應類型。
[語彙基元 Auth 忽略 URL 大小寫](#token-auth-ignore-url-case) | 判斷所做的權杖型驗證的 URL 比較是否區分大小寫。
[權杖驗證參數](#token-auth-parameter) | 判斷是否應將權杖型驗證查詢字串參數重新命名。


## <a name="caching-features"></a>快取功能

這些功能是設計來自訂快取內容的時機和方法。

名稱 | 目的
-----|--------
[頻寬參數](#bandwidth-parameters) | 判斷是否使用頻寬節流參數 （例如，ec_rate 和 ec_prebuf）。
[頻寬節流設定](#bandwidth-throttling) | 節流的頻寬邊緣伺服器所提供的回應。
[略過快取](#bypass-cache) | 決定是否要求應該略過快取。
[快取控制標頭的處理方式](#cache-control-header-treatment) | 控制產生`Cache-Control`邊緣伺服器會在外部 Max-age 功能正在作用中時的標頭。
[快取索引鍵查詢字串](#cache-key-query-string) | 判斷快取索引鍵是否將包含或排除與要求相關聯的佇列字串參數。
[快取索引鍵重寫](#cache-key-rewrite) | 重寫與要求相關聯的快取索引鍵。
[完整快取填滿](#complete-cache-fill) | 判斷在要求於 Edge Server 上產生部分快取遺失時會發生什麼事。
[壓縮檔案類型](#compress-file-types) | 定義將在伺服器上壓縮的檔案格式。
[預設內部 Max-age](#default-internal-max-age) | 判斷 Edge Server 到原始伺服器快取重新驗證之間的預設最大壽命間隔。
[到期標頭的處理方式](#expires-header-treatment) | 控制產生`Expires`標頭的邊緣伺服器外部 Max-age 功能正在作用中時。
[外部 Max-age](#external-max-age) | 判斷瀏覽器到 Edge Server 快取重新驗證之間的最大壽命間隔。
[強制內部 Max-age](#force-internal-max-age) | 判斷 Edge Server 到原始伺服器快取重新驗證之間的最大壽命間隔。
[H.264 支援 （HTTP 漸進式下載）](#h264-support-http-progressive-download) | 判斷可能用於串流處理內容的 H.264 檔案格式類型。
[實行 No Cache 要求](#honor-no-cache-request) | 判斷是否要將 HTTP 用戶端的 no-cache 要求轉送到原始伺服器。
[忽略原點 No Cache](#ignore-origin-no-cache) | 決定是否 CDN 會忽略某些指示詞從來源伺服器提供服務。
[忽略 Unsatisfiable 範圍](#ignore-unsatisfiable-ranges) | 決定當要求產生 416 的範圍無法滿足的要求狀態碼傳回至用戶端的回應。
[內部的最大過時](#internal-max-stale) | 控制當 Edge Server 無法使用原始伺服器重新驗證快取的資產時，從 Edge Server 所提供的快取資產可能會經歷多長的標準到期時間。
[部分快取共用](#partial-cache-sharing) | 判斷要求是否可以產生部分快取的內容。
[Prevalidate 快取的內容](#prevalidate-cached-content) | 在快取內容的 TTL 到期之前，判斷其是否適用進行早期重新驗證。
[重新整理零位元組的快取檔案](#refresh-zero-byte-cache-files) | 決定如何 0 個位元組的快取資產的 HTTP 用戶端的要求由邊緣伺服器。
[設定可快取的狀態碼](#set-cacheable-status-codes) | 定義一組可產生快取內容的狀態碼。
[過時的內容傳遞發生錯誤](#stale-content-delivery-on-error) | 判斷在快取重新驗證期間發生錯誤時，或者在接收到來自客戶原始伺服器的要求內容時，是否要傳遞到期的快取內容。
[過時的指令時](#stale-while-revalidate) | 藉由使用邊緣伺服器提供給要求者的過時用戶端，重新驗證時，可以改善效能。

## <a name="comment-feature"></a>註解功能

這項功能被設計來提供規則中的其他資訊。

名稱 | 目的
-----|--------
[Comment](#comment) | 允許要在規則中加入附註。
 
## <a name="header-features"></a>標頭功能

這些功能是設計來新增、修改或刪除要求或回應的標頭。

名稱 | 目的
-----|--------
[Age 回應標頭](#age-response-header) | 判斷 Age 回應標頭是否將包含於傳送到要求者的回應中。
[偵錯快取的回應標頭](#debug-cache-response-headers) | 決定是否回應可能包括偵錯 EC 月 X 日回應標頭，提供要求資產的快取原則的資訊。
[修改用戶端要求標頭](#modify-client-request-header) | 覆寫、附加或刪除要求的標頭。
[修改用戶端的回應標頭](#modify-client-response-header) | 覆寫、附加或刪除回應的標頭。
[設定用戶端 IP 自訂標頭](#set-client-ip-custom-header) | 允許將要新增到要求的要求用戶端 IP 位址做為自訂要求標頭。


## <a name="logging-features"></a>記錄功能

這些功能是設計來自訂儲存於原始記錄檔中的資料。

名稱 | 目的
-----|--------
[自訂記錄欄位 1](#custom-log-field-1) | 判斷將指派給原始記錄檔中自訂記錄欄位的格式和內容。
[記錄查詢字串](#log-query-string) | 判斷查詢字串以及 URL 是否將一起儲存於存取記錄中。


<!---
## Optimize

These features determine whether a request will undergo the optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied to a request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates the Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied to a request.

If this feature has been enabled, then the following criteria must also be met before the request will be processed by Edge Optimizer:

- The requested content must use an edge CNAME URL.
- The edge CNAME referenced in the URL must correspond to a site whose configuration has been activated in a rule.

This feature requires the ADN platform and the Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that the request is eligible for Edge Optimizer processing.
Disabled|Restores the default behavior. The default behavior is to deliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates the Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and the Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests to the corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs to be performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until the Edge Optimizer – Instantiate Configuration feature that references it is removed from the rule.
- The instantiation of a site configuration does not mean that all requests to the corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If the desired site does not appear in the list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin-features"></a>Origin 功能

這些功能是設計來控制 CDN 與原始伺服器通訊的方式。

名稱 | 目的
-----|--------
[保持運作的最大要求](#maximum-keep-alive-requests) | 判斷在關閉 Keep-Alive 連線之前，適用於該連線的最大要求數目。
[Proxy 特殊標頭](#proxy-special-headers) | 定義將從 Edge Server 轉送到原始伺服器之 CDN 特定的要求標頭組。


## <a name="specialty-features"></a>特殊功能

這些功能適用於進階使用者提供進階的功能。

名稱 | 目的
-----|--------
[快取的 HTTP 方法](#cacheable-http-methods) | 決定其他可快取在網路上的 HTTP 方法集合。
[快取的要求主體大小](#cacheable-request-body-size) | 定義用以判斷是否可快取 POST 回應的臨界值。
[使用者變數](#user-variable) | 僅供內部使用。

 
## <a name="url-features"></a>URL 功能

這些功能可讓要求重新導向至不同的 URL 或重寫為不同的 URL。

名稱 | 目的
-----|--------
[請遵循重新導向](#follow-redirects) | 判斷要求是否可以重新導向至定義於客戶原始伺服器所傳回之位置標頭中的主機名稱。
[重新導向 URL](#url-redirect) | 透過位置標頭將要求重新導向。
[URL 重寫](#url-rewrite)  | 重寫要求 URL。



## <a name="azure-cdn-rules-engine-features-reference"></a>Azure CDN 規則引擎功能參考

---
### <a name="age-response-header"></a>Age 回應標頭
**目的**： 決定是否要傳送給要求者的回應中包含的 Age 回應標頭。
值|結果
--|--
已啟用 | Age 回應標頭包含在傳送給要求者的回應。
已停用 | Age 回應標頭排除在傳送給要求者的回應。

**預設行為**：已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="bandwidth-parameters"></a>頻寬參數
**目的：**判斷是否會使用頻寬節流設定參數 (例如 ec_rate 和 ec_prebuf)。

頻寬節流設定參數會判斷是否要將用戶端要求的資料傳輸速率限制為自訂的速率。

值|結果
--|--
已啟用|可讓邊緣伺服器接受頻寬節流的要求。
已停用|會忽略頻寬節流參數的邊緣伺服器。 通常將會提供要求的內容 (亦即，不需頻寬節流設定)。

**預設行為：**已啟用。
 
[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="bandwidth-throttling"></a>頻寬節流設定
**用途：**節流的頻寬邊緣伺服器所提供的回應。

您必須定義下列這兩個選項，才能正確設定頻寬節流設定。

選項|說明
--|--
每秒 KB 數|將此選項設定為可能用來傳遞回應的最大頻寬 (每秒 KB 數)。
Prebuf 秒|此選項設為的邊緣伺服器頻寬已節流，等待的秒數。 這段不受頻寬限制之期間的用意是防止媒體播放器因為頻寬節流設定而遇到間斷或緩衝處理問題。

**預設行為：**已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="bypass-cache"></a>略過快取
**用途：**決定是否要求應該略過快取。

值|結果
--|--
已啟用|導致所有對原始伺服器的要求都失敗，即使先前已在 Edge Server 上快取內容也一樣。
已停用|導致 Edge Server 會根據其回應標頭中定義的快取原則來快取資產。

**預設行為：**

- **HTTP 大型︰**已停用

<!---
- **ADN:** Enabled

--->

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="cacheable-http-methods"></a>可快取的 HTTP 方法
**用途：**決定可以進行快取在網路的其他 HTTP 方法的集合。

重要資訊：

- 此功能假設應一律快取 GET 回應。 如此一來，在設定此功能時，就不應包含 GET HTTP 方法。
- 此功能支援 POST HTTP 方法。 啟用這項功能將設定為快取的 POST 回應`POST`。
- 根據預設，會快取的要求的主體是小於 14 Kb。 使用 [可快取的要求主體大小] 功能來設定要求主體大小上限。

**預設行為：**只有 GET 回應會快取。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="cacheable-request-body-size"></a>可快取的要求主體大小
**目的：**定義用以判斷是否可快取 POST 回應的臨界值。

此臨界值是藉由指定要求主體大小上限來決定。 系統將不會快取包含較大要求主體的要求。

重要資訊：

- 只有在 POST 回應適合用來快取時，才適用此功能。 使用 [可快取的 HTTP 方法] 功能來啟用 POST 要求快取。
- 已針對下列項目將要求主體納入考量：
    - x-www-form-urlencoded 值
    - 確保唯一的快取索引鍵
- 定義大型的要求主體大小上限可能會影響資料傳遞效能。
    - **建議值：**14 Kb
    - **最小值︰**1 Kb

**預設行為︰**14 Kb

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="cache-control-header-treatment"></a>Cache-Control 標頭處理
**用途：**控制的產生`Cache-Control`邊緣伺服器會在外部 Max-age 功能正在作用中時的標頭。

完成這類型組態的最簡單方式是將 [外部最大壽命] 和 [Cache-Control 標頭處理] 功能放在同一個陳述式中。

值|結果
--|--
覆寫|可確保執行下列動作：<br/> -覆寫`Cache-Control`原始伺服器所產生的標頭。 <br/>-加入`Cache-Control`至回應的外部 Max-age 功能所產生的標頭。
傳遞|可確保`Cache-Control`外部 Max-age 功能所產生的標頭永遠不會加入至回應。 <br/> 如果來源伺服器會產生`Cache-Control`標頭，它也會通過終端使用者。 <br/> 如果來源伺服器不會產生`Cache-Control`標頭，則此選項可能會造成回應標頭未包含`Cache-Control`標頭。
如果遺失則加入|如果`Cache-Control`標頭不來自原始伺服器，則此選項會增加`Cache-Control`外部 Max-age 功能所產生的標頭。 這個選項特別適合用於確保所有資產，會都指派`Cache-Control`標頭。
移除| 此選項可確保`Cache-Control`標頭不含標頭回應。 如果`Cache-Control`已指派標頭，則會從標頭回應中移除。

**預設行為：**覆寫。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="cache-key-query-string"></a>快取索引鍵查詢字串
**目的：**判斷快取索引鍵是否將包含或排除與要求相關聯的查詢字串參數。

重要資訊：

- 指定一或多個查詢字串參數名稱。 每個參數名稱都應以單一空格分隔。
- 此功能會判斷是否要在快取索引鍵中包含查詢字串參數或從中排除。 以下提供每個選項的其他資訊。

類型|說明
--|--
 包含|  指出應該在快取索引鍵中包含每個指定的參數。 系統將針對每個要求產生唯一的快取索引鍵，其中包含此功能中所定義之查詢字串參數的唯一值。 
 全部包含  |指出將針對每個包含唯一查詢字串的資產要求建立唯一的快取索引鍵。 通常不建議使用此類型的組態，因為它可能會導致一小部分的快取命中數。 這將會增加原始伺服器上的負載，因為它必須為更多要求提供服務。 這個組態會複製 [查詢字串快取] 頁面上名為「unique-cache」的快取行為。 
 排除 | 指出只會從快取索引鍵中排除指定的參數。 所有的其他查詢字串參數都將包含於快取索引鍵中。 
 全部排除  |指出將從快取索引鍵中排除所有查詢字串參數。 這個組態會複製 [查詢字串快取] 頁面上名為「standard-cache」的預設快取行為。 

HTTP 規則引擎的強大功能可讓您自訂實作查詢字串快取的行為。 例如，您可以指定查詢字串快取只會在特定位置或檔案類型上執行。

如果您想要複製 [查詢字串快取] 頁面上名為「no-cache」的查詢字串快取行為，則您必須建立規則，其中包含 [URL 查詢萬用字元] 比對條件和 [略過快取] 功能。 [URL 查詢萬用字元] 比對條件應設為星號 (*)。

#### <a name="sample-scenarios"></a>範例案例

下列範例是這項功能的使用方式，會提供範例要求和預設快取金鑰：

- **範例要求︰**http://wpc.0001.&lt;網域&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01
- **預設的快取索引鍵︰**/800001/Origin/folder/asset.htm

##### <a name="include"></a>包含

範例組態：

- **類型︰**包括
- **參數︰**語言

這類型的組態會產生下列查詢字串參數快取索引鍵：

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>全部包含

範例組態：

- **類型︰**全部包括

這類型的組態會產生下列查詢字串參數快取索引鍵：

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>排除

範例組態：

- **類型︰**排除
- **參數︰**工作階段識別碼的使用者識別碼

這類型的組態會產生下列查詢字串參數快取索引鍵：

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>全部排除

範例組態：

- **類型︰**全部排除

這類型的組態會產生下列查詢字串參數快取索引鍵：

    /800001/Origin/folder/asset.htm

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="cache-key-rewrite"></a>快取索引鍵重寫
**目的：**重寫與要求相關聯的快取索引鍵。

快取索引鍵是基於快取目的識別資產的相對路徑。 換句話說，伺服器會檢查其路徑根據資產的快取版本其快取索引鍵所定義。

藉由定義兩個下列選項來設定此功能：

選項|說明
--|--
原始路徑| 定義將重寫快取索引鍵之快取類型的相對路徑。 相對路徑可藉由選取基底原始路徑，然後定義規則運算式模式來定義。
新路徑|定義新快取索引鍵的相對路徑。 相對路徑可藉由選取基底原始路徑，然後定義規則運算式模式來定義。 此相對路徑可使用 HTTP 變數來動態建構
**預設行為︰**要求的快取索引鍵是依要求 URI 來判斷。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="comment"></a>註解
**目的：**能夠在規則中加入附註。

此功能的用途之一是提供一般用途的規則，或是為何要將特定比對條件或功能加入至規則的其他相關資訊。

重要資訊：

- 您最多可以指定 150 個字元。
- 僅使用英數字元。
- 此功能不會影響規則的行為。 這只表示會提供一個區域，讓您可在其中提供資訊以供未來參考之用，或是有助於疑難排解規則的資訊。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="complete-cache-fill"></a>完成快取填滿
**目的：**判斷在要求於 Edge Server 上產生部分快取遺失時會發生什麼事。

部分快取遺失會說明未完全下載至 Edge Server 之資產的快取狀態。 如果只在 Edge Server 上部分快取了資產，則會將該資產的下一個要求再次轉送至原始伺服器。
<!---
This feature is not available for the ADN platform. The typical traffic on this platform consists of relatively small assets. The size of the assets served through these platforms helps mitigate the effects of partial cache misses, since the next request will typically result in the asset being cached on that POP.

--->
部分快取遺失通常發生於使用者中止下載之後，或發生於只要求使用 HTTP 範圍要求的資產。 對於使用者通常不會完整下載的大型資產 (例如，影片) 而言，此功能非常實用。 因此，HTTP 大型平台上預設會啟用此功能。 所有其他平台上則會加以停用。

保留 HTTP 大型的平台的預設組態，因為它可以減少您客戶的原始伺服器上的負載，並增加的速度，您的客戶會下載您的內容。

由於追蹤快取設定的方式，因而導致此功能無法與下列比對條件產生關聯︰Edge Cname、要求標頭常值、要求標頭萬用字元、URL 查詢常值和 URL 查詢萬用字元。

值|結果
--|--
已啟用|還原預設行為。 預設行為是強制 Edge Server 從原始伺服器起始資產的背景擷取。 在那之後，資產將位於 Edge Server 的本機快取中。
已停用|防止 Edge Server 執行資產的背景擷取。 這表示來自該地區中該資產的下一個要求將導致 Edge Server 向客戶原始伺服器要求它。

**預設行為：**已啟用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="compress-file-types"></a>壓縮檔案類型
**目的：**定義將在伺服器上壓縮的檔案格式。

您可以使用檔案格式的網際網路媒體類型 (例如，內容類型) 來指定檔案格式。 網際網路媒體類型為平台無關的中繼資料可讓伺服器識別特定資產的檔案格式。 以下提供常用的網際網路媒體類型清單。

網際網路媒體類型|說明
--|--
text/plain|純文字檔案
text/html| HTML 檔案
text/css|階層式樣式表 (CSS)
application/x-javascript|Javascript
application/javascript|Javascript
重要資訊：

- 使用單一空格來分隔每個網際網路媒體類型，藉以指定多個類型。 
- 此功能將只會壓縮大小小於 1 MB 的資產。 伺服器不會壓縮較大的資產。
- 諸如影片、視訊和音訊媒體資產 (例如，JPG、MP3、MP4 等) 的特定類型內容均已壓縮。 這些類型資產上的額外壓縮將不會顯著降低檔案大小。 因此，建議您不要在這些類型的資產上啟用壓縮。
- 不支援萬用字元 (例如星號)。
- 將此功能新增至規則之前，請確定會針對將套用此規則的平台，在 [壓縮] 頁面上設定 [壓縮已停用] 選項。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="custom-log-field-1"></a>自訂記錄欄位 1
**目的：**判斷將指派給原始記錄檔中自訂記錄欄位的格式和內容。

這個自訂的欄位可讓您判斷哪些要求和回應標頭值會儲存在記錄檔。

根據預設，自訂記錄欄位稱為「x-ec_custom-1」。 不過，您可以自訂這個欄位的名稱從原始記錄檔設定 頁面。

您應該用來指定要求和回應標頭格式設定的定義如下。

標頭類型|格式|範例
-|-|-
要求標頭|%{[RequestHeader]()}[i]() | %{Accept-Encoding}i <br/> {Referer}i <br/> %{Authorization}i
回應標頭|%{[ResponseHeader]()}[o]()| %{Age}o <br/> %{Content-Type}o <br/> %{Cookie}o

重要資訊：

- 自訂記錄欄位可包含標頭欄位和純文字的任意組合。
- 此欄位的有效字元包括下列各項：英數字元 (0-9、a-z 和 A-Z)、連字號、冒號、分號、單引號、逗號、句號、底線、等號、括弧、中括弧和空格。 只有在用於指定標頭欄位時，才能使用百分比符號和大括弧。
- 每個指定標頭欄位的拼字都必須符合所需的要求/回應標頭名稱。
- 如果您想要指定多個標頭，則建議您使用分隔符號來表示每個標頭。 例如，您可以針對每個標頭使用縮寫。 範例語法如下所示。
    - AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o 

**預設值：** -

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="debug-cache-response-headers"></a>偵錯快取回應標頭
**目的：**判斷回應是否會包含 X-EC-Debug 回應標頭，其可在快取原則上提供要求資產的相關資訊。

符合下列兩種情況時，將會在回應中包含偵錯快取回應標頭：

- 已在所需的要求上啟用 [偵錯快取回應標頭] 功能。
- 上述要求會定義一組將包含於回應中的偵錯快取回應標頭。

偵錯快取回應標頭可能是藉由在要求中包含下列標頭和所需指示詞來要求：

X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_

**範例：**

X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

值|結果
-|-
已啟用|偵錯快取回應標頭的要求將傳回包含 X-EC-Debug 標頭的回應。
已停用|X-EC-Debug 回應標頭將會從回應中排除。

**預設行為：**已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="default-internal-max-age"></a>預設的內部最大壽命
**目的：**判斷 Edge Server 到原始伺服器快取重新驗證之間預設的最大壽命間隔。 換句話說，就是 Edge Server 將檢查快取的資產是否符合原始伺服器上儲存的資產之前所經過的時間長度。

重要資訊：

- 這個動作才會進行回應來自原始伺服器的未指派中的保留時間上限指示`Cache-Control`或`Expires`標頭。
- 此動作將不會針對未被視為可快取的資產加以執行。
- 此動作不會影響瀏覽器對 Edge Server 快取重新驗證。 取決於這些類型的 revalidations`Cache-Control`或`Expires`傳送至瀏覽器，可以使用外部 Max-age 功能自訂標頭。
- 此動作的結果對於回應標頭以及針對您的內容從 Edge Server 傳回的內容並無顯著影響，但它可能會影響從 Edge Server 傳送至原始伺服器的重新驗證流量。
- 以下列方式設定此功能：
    - 選取可套用預設內部最大壽命的狀態碼。
    - 指定整數值，然後選取所需的時間單位 (例如，秒、分鐘、小時等)。 此值會定義預設的內部最大壽命間隔。

- 設定為"Off"的時間單位，將會指派預設內部保留時間上限的間隔時間為 7 天要求沒有被指派中的保留時間上限指示其`Cache-Control`或`Expires`標頭。
- 由於追蹤快取設定的行為，因而導致此功能無法與下列比對條件產生關聯： 
    - Edge 
    - Cname
    - 要求標頭常值
    - 要求標頭萬用字元
    - 要求方法
    - URL 查詢常值
    - URL 查詢萬用字元

**預設值：**7 天

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="deny-access-403"></a>拒絕存取 (403)
**目的**：判斷所有要求是否已遭拒且含有 [403 禁止] 回應。

值 | 結果
------|-------
已啟用| 導致所有滿足比對準則的要求遭拒，且具有 [403 禁止] 回應。
已停用| 還原預設行為。 預設行為是讓原始伺服器能夠判斷將傳回的回應類型。

**預設行為**：已停用

> [!TIP]
   > 此功能的可能用法之一是將它關聯至 [要求標頭] 比對條件，以封鎖存取使用內嵌連結連至您內容的 HTTP 推薦者。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="expires-header-treatment"></a>Expires 標頭處理
**用途：**控制的產生`Expires`標頭的邊緣伺服器外部 Max-age 功能正在作用中時。

完成這類型組態的最簡單方式是將 [外部最大壽命] 和 [Expires 標頭處理] 功能放在同一個陳述式中。

值|結果
--|--
覆寫|確保將會進行下列動作：<br/>-覆寫`Expires`原始伺服器所產生的標頭。<br/>-加入`Expires`至回應的外部 Max-age 功能所產生的標頭。
傳遞|可確保`Expires`外部 Max-age 功能所產生的標頭永遠不會加入至回應。 <br/> 如果來源伺服器會產生`Expires`標頭，它會將傳遞至使用者。 <br/>如果來源伺服器不會產生`Expires`標頭，則此選項可能會造成回應標頭未包含`Expires`標頭。
如果遺失則加入| 如果`Expires`標頭不來自原始伺服器，則此選項會增加`Expires`外部 Max-age 功能所產生的標頭。 這個選項特別適合用於確保所有的資產將會指派`Expires`標頭。
移除| 可確保`Expires`標頭不含標頭回應。 如果`Expires`已指派標頭，則會從標頭回應中移除。

**預設行為：**覆寫

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="external-max-age"></a>外部最大壽命
**目的：**判斷瀏覽器到 Edge Server 快取重新驗證之間的最大壽命間隔。 換句話說，就是瀏覽器可以檢查來自 Edge Server 的新版本資產之前所經歷的時間長度。

啟用此功能將會產生`Cache-Control: max-age`和`Expires`邊緣伺服器從標頭並將它們傳送至 HTTP 用戶端。 根據預設，這些標頭將會覆寫原始伺服器所建立的標頭。 不過，可能會使用 [Cache-Control 標頭處理] 和 [Expires 標頭處理] 功能來改變此行為。

重要資訊：

- 此動作不會影響 Edge Server 對原始伺服器的快取重新驗證。 取決於這些類型的 revalidations`Cache-Control`和`Expires`標頭接收來自原始伺服器，並且可以自訂預設內部 Max-age 與 Force 內部 Max-age 功能。
- 指定整數值，然後選取所需的時間單位 (例如，秒、分鐘、小時等)，從而設定此功能。
- 設定為負數值的這項功能會導致要傳送的邊緣伺服器`Cache-Control: no-cache`和`Expires`設定每個回應以瀏覽器與過去的時間。 HTTP 用戶端並不會快取的回應，雖然這項設定不會影響快取來自原始伺服器回應的邊緣伺服器的能力。
- 將時間單位設為「關閉」，即會停用此功能。 `Cache-Control`和`Expires`快取與來源伺服器的回應標頭會傳遞至瀏覽器。

**預設行為：**關閉

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="follow-redirects"></a>遵循重新導向
**目的：**判斷是否可將要求重新導向至定義於客戶原始伺服器所傳回之位置標頭中的主機名稱。

重要資訊：

- 您只能將要求重新導向至對應到相同平台的 Edge CNAME。

值|結果
-|-
已啟用|要求可重新導向。
已停用|要求將不會重新導向。

**預設行為：**已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="force-internal-max-age"></a>強制執行內部最大壽命
**目的：**判斷 Edge Server 到原始伺服器快取重新驗證之間的最大壽命間隔。 換句話說，就是 Edge Server 可以檢查快取的資產是否符合原始伺服器上儲存的資產之前所經過的時間長度。

重要資訊：

- 這項功能將會覆寫中定義的最大時間間隔`Cache-Control`或`Expires`從原始伺服器所產生的標頭。
- 此功能不會影響瀏覽器對 Edge Server 的快取重新驗證。 取決於這些類型的 revalidations`Cache-Control`或`Expires`標頭傳送到瀏覽器。
- 此功能對於由 Edge Server 傳遞給要求者的回應並沒有顯著的影響。 不過，它有影響的邊緣伺服器從傳送至原始伺服器的重新驗證流量。
- 以下列方式設定此功能：
    - 選取將套用內部最大壽命的狀態碼。
    - 指定整數值並選取所需的時間單位 (例如，秒、分鐘、小時等)。 此值會定義要求的最大壽命間隔。

- 將時間單位設為「關閉」，即會停用此功能。 系統不會將內部最大壽命間隔指派給要求的資產。 如果原始標頭未包含快取指示，則將根據 [預設內部最大壽命] 功能的作用中設定來快取資產。
- 由於追蹤快取設定的行為，因而導致此功能無法與下列比對條件產生關聯： 
    - Edge 
    - Cname
    - 要求標頭常值
    - 要求標頭萬用字元
    - 要求方法
    - URL 查詢常值
    - URL 查詢萬用字元

**預設行為：**關閉

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="h264-support-http-progressive-download"></a>H.264 支援 (HTTP 漸進式下載)
**目的：**判斷可能用於串流處理內容的 H.264 檔案格式類型。

重要資訊：

- 在 [副檔名] 選項中，定義一組允許的 H.264 副檔名 (以空格分隔)。 [副檔名] 選項將會覆寫預設行為。 在設定此選項時包括這些副檔名，藉以保有 MP4 和 F4V 支援。 
- 指定每個副檔名 (例如 .mp4 .f4v) 時，務必包含句點。

**預設行為︰**HTTP 漸進式下載預設支援 MP4 和 F4V 媒體。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="honor-no-cache-request"></a>接受 No-Cache 要求
**目的：**判斷是否要將 HTTP 用戶端的 no-cache 要求轉送到原始伺服器。

HTTP 用戶端傳送時發生無快取要求`Cache-Control: no-cache`及/或`Pragma: no-cache`HTTP 要求標頭。

值|結果
--|--
已啟用|允許將 HTTP 用戶端的 no-cache 要求轉送到原始伺服器，而原始伺服器會透過 Edge Server 將回應標頭和主體傳回 HTTP 用戶端。
已停用|還原預設行為。 預設行為是防止將 no-cache 要求轉送到原始伺服器。

針對所有生產環境的流量，強烈建議將此功能保留為其預設的停用狀態。 否則，將無法為原始伺服器提供防護，來防範可能會在重新整理網頁時不小心觸發許多 no-cache 要求的使用者，或者許多已編碼為要透過每個視訊要求傳送 no-cache 標題的熱門媒體播放器。 不過，此功能非常適合用來套用至特定的非生產環境暫存或測試目錄，以便隨時從原始伺服器提取隨最新內容。

將針對因此功能而允許轉送至原始伺服器的要求報告的快取狀態為 TCP_Client_Refresh_Miss。 快取狀態報表 (可在 [核心報告] 模組中取得) 會依快取狀態提供統計資訊。 這讓您能夠追蹤因此功能而轉送至原始伺服器的要求數目和百分比。

**預設行為：**已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="ignore-origin-no-cache"></a>忽略原始的 No-Cache
**用途：**決定 CDN 是否會忽略由來源伺服器的下列指示詞：

- `Cache-Control: private`
- `Cache-Control: no-store`
- `Cache-Control: no-cache`
- `Pragma: no-cache`

重要資訊：

- 定義將忽略上述指示詞的狀態碼清單 (以空格分隔)，藉以設定此功能。
- 以下是此功能的有效狀態碼集合︰200、203、300、301、302、305、307、400、401、402、403、404、405、406、407、408、409、410、411、412、413、414、415、416、417、500、501、502、503、504 和 505。
- 藉由將其設為空白值來停用此功能。
- 由於追蹤快取設定的行為，因而導致此功能無法與下列比對條件產生關聯： 
    - Edge 
    - Cname
    - 要求標頭常值
    - 要求標頭萬用字元
    - 要求方法
    - URL 查詢常值
    - URL 查詢萬用字元

**預設行為︰**預設行為是採用上述指示詞。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="ignore-unsatisfiable-ranges"></a>忽略無法滿足的範圍 
**目的：**判斷在要求產生 [416 無法滿足的要求範圍] 狀態代碼時將傳回用戶端的要求。

根據預設，當 Edge Server 無法滿足指定的位元組範圍要求，且未指定 If-Range 要求標頭欄位時，即會傳回此狀態碼。

值|結果
-|-
已啟用|防止無效的位元組範圍要求以範圍無法滿足的要求狀態碼 416 回應邊緣伺服器。 伺服器會傳遞要求的資產而傳回 200 確定用戶端。
已停用|還原預設行為。 預設行為是接受 [416 無法滿足的要求範圍] 狀態碼。

**預設行為：**已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="internal-max-stale"></a>內部最大過時
**目的：**控制當 Edge Server 無法使用原始伺服器重新驗證快取的資產時，從 Edge Server 所提供的快取資產可能會經歷多長的標準到期時間。

一般來說，當資產的最大壽命時間過期時，Edge Server 會將重新驗證要求傳送至原始伺服器。 原始伺服器接著會使用 [304 未修改] 來回應，以便為 Edge Server 提供所快取資產上的全新租用，或使用 [200 確定] 來提供具備更新快取資產版本的 Edge Server。

如果 Edge Server 在嘗試進行這類重新驗證時無法建立與原始伺服器的連線，則這個 [內部最大過時] 功能就會控制 Edge Server 是否可能要繼續提供現已過時的資產，以及提供多久時間。

請注意，這個時間間隔是從資產的最大壽命到期時開始，而不是從發生失敗的重新驗證時開始。 因此，在未成功重新驗證的情況下可為資產提供服務的最長期間，是由 max-age 加上 max-stale 的組合所指定的時間長度。 比方說，如果資產已快取在 30 分鐘的最大存留期與 15 分鐘的最大過時的 9:00，然後在 9:44 失敗的重新驗證嘗試會導致畷樾簅接收過期的快取的資產，而 9:46 失敗的重新驗證嘗試會導致 en-usd 使用者會接收 504 閘道逾時。

設定這項功能已被取代的任何值`Cache-Control: must-revalidate`或`Cache-Control: proxy-revalidate`來自原始伺服器收到的標頭。 如果在一開始快取資產時從原始伺服器接收到這其中一個標頭，則 Edge Server 將不會為過時的快取資產提供服務。 在這種情況下，如果無法重新驗證與來源時已到期的資產的最大時間間隔，edge server edge server 會傳回 504 閘道逾時錯誤。

重要資訊：

- 以下列方式設定此功能：
    - 選取將套用 max-stale 的狀態碼。
    - 指定整數值，然後選取所需的時間單位 (例如，秒、分鐘、小時等)。 此值可定義將套用的內部 max-stale。

- 將時間單位設為「關閉」，即會停用此功能。 系統將不會在快取的資產超過一般到期時間之後為其提供服務。
- 由於追蹤快取設定的行為，因而導致此功能無法與下列比對條件產生關聯： 
    - Edge 
    - Cname
    - 要求標頭常值
    - 要求標頭萬用字元
    - 要求方法
    - URL 查詢常值
    - URL 查詢萬用字元

**預設行為：**兩分鐘

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="log-query-string"></a>記錄查詢字串
**目的：**判斷查詢字串是否將與 URL 一起儲存於存取記錄中。

值|結果
-|-
已啟用|在存取記錄中記錄 URL 時，允許儲存查詢字串。 如果 URL 未包含查詢字串，則此選項將不會有任何作用。
已停用|還原預設行為。 預設行為是在存取記錄中記錄 URL 時忽略查詢字串。

**預設行為：**已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="maximum-keep-alive-requests"></a>Keep-Alive 要求的最大值
**目的：**判斷在關閉 Keep-Alive 連線之前，適用於該連線的最大要求數目。

強烈建議您不要將要求數目上限設為較低的值，這樣可能會導致效能變差。

重要資訊：

- 將此值指定為整數。
- 請勿在指定的值中包含逗號或句號。

**預設值︰**10,000 個要求

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="modify-client-request-header"></a>修改用戶端要求標頭
**用途：**每個要求中包含一組要求標頭的描述。 此功能可以：

- 附加或覆寫指派給要求標頭的值。 如果指定的要求標頭不存在，則此功能會將其加入至要求。
- 刪除要求的要求標頭。

要轉送到原始伺服器的要求將會反映此功能所做的變更。

您可以在要求標頭上執行下列其中一個動作：

選項|說明|範例
-|-|-
Append|指定的值會新增至現有要求標頭值的結尾。|**要求標頭值 (用戶端)：**Value1 <br/> **要求標頭值 (HTTP 規則引擎)：**Value2 <br/>**新的要求標頭值：**Value1Value2
覆寫|要求標頭值將會設定為指定的值。|**要求標頭值 (用戶端)：**Value1 <br/>**要求標頭值 (HTTP 規則引擎)：**Value2 <br/>**新的要求標頭值：**Value2 <br/>
刪除|刪除指定的要求標頭。|**要求標頭值 (用戶端)：**Value1 <br/> **修改用戶端要求標頭組態：**刪除有問題的要求標頭。 <br/>**結果︰**指定的要求標頭將不會轉送到原始伺服器。

重要資訊：

- 確定 [名稱] 選項中指定的值與所需的要求標頭完全相符。
- 基於識別標頭的目的，不會將大小寫納入考量。 例如，下列變化的任一`Cache-Control`標頭名稱可以用來識別它：
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- 在指定標頭名稱時，僅使用英數字元、連字號或底線。
- 刪除標頭會防止它被轉送到原始伺服器的邊緣伺服器。
- 以下為保留的標頭，且此功能無法加以修改：
    - forwarded
    - host
    - via
    - 警告
    - x-forwarded-for
    - 以「x-ec」開頭的所有標頭名稱都會保留。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="modify-client-response-header"></a>修改用戶端回應標頭
每個回應包含一組回應標頭的描述。 此功能可以：

- 附加或覆寫指派給回應標頭的值。 如果指定的回應標頭不存在，則此功能會將其新增至回應。
- 刪除回應的回應標頭。

根據預設，回應標頭值會定義供來源伺服器和邊緣伺服器。

您可以在回應標頭上執行下列其中一個動作：

選項|說明|範例
-|-|-
Append|指定的值會新增至現有回應標頭值的結尾。|**回應標頭值 (用戶端)：**Value1 <br/> **回應標頭值 (HTTP 規則引擎)：**Value2 <br/>**新的回應標頭值：**Value1Value2
覆寫|回應標頭值將會設定為指定的值。|**回應標頭值 (用戶端)：**Value1 <br/>**回應標頭值 (HTTP 規則引擎)：**Value2 <br/>**新的回應標頭值：**Value2 <br/>
刪除|刪除指定的回應標頭。|**回應標頭值 (用戶端)：**Value1 <br/> **修改用戶端回應標頭組態：**刪除有問題的回應標頭。 <br/>**結果︰**指定的回應標頭將不會轉送給要求者。

重要資訊：

- 確定 [名稱] 選項中指定的值與所需的回應標頭完全相符。 
- 基於識別標頭的目的，不會將大小寫納入考量。 例如，下列變化的任一`Cache-Control`標頭名稱可以用來識別它：
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- 刪除標頭可防止它被轉送到要求者。
- 以下為保留的標頭，且此功能無法加以修改：
    - accept-encoding
    - age
    - connection
    - content-encoding
    - content-length
    - content-range
    - 日期
    - 伺服器
    - trailer
    - transfer-encoding
    - 升級
    - vary
    - via
    - 警告
    - 以「x-ec」開頭的所有標頭名稱都會保留。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="partial-cache-sharing"></a>部分快取共用
**目的：**判斷要求是否可以產生部分快取的內容。

接著可能會使用這個部分快取來滿足該內容的新要求，直到完全快取要求的內容為止。

值|結果
-|-
已啟用|要求可以產生部分快取的內容。
已停用|要求只能產生所要求內容的完整快取版本。

**預設行為：**已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="prevalidate-cached-content"></a>預先驗證快取的內容
**目的：**在快取內容的 TTL 到期之前，判斷其是否適用進行早期重新驗證。

定義在要求內容的 TTL 到期之前的時間長度，而要求的內容在這段期間將適用進行早期驗證。

重要資訊：

- 選取「關閉」做為時間單位，需要在快取內容的 TTL 到期之後進行重新驗證。 不應指定時間，且將會予以忽略。

**預設行為：**關閉。 重新驗證可能只會在快取內容的 TTL 到期之後進行。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="proxy-special-headers"></a>Proxy 特定的標頭
**用途：**定義會從邊緣伺服器轉送到原始伺服器的 CDN 專屬要求標頭的集合。

重要資訊：

- 此功能中定義的每個 CDN 特定要求標頭都將轉送到原始伺服器。
- 從此清單中移除 CDN 特定的要求標頭，藉以防止將其轉送到原始伺服器。

**預設行為：**所有 CDN 專屬要求標頭會都轉寄至原始伺服器。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="refresh-zero-byte-cache-files"></a>重新整理零位元組的快取檔案
**用途：**決定如何處理的 HTTP 用戶端要求的位元組 0 快取資產的邊緣伺服器。

有效值為：

值|結果
--|--
已啟用|會導致 edge server 資產中重新提取來自原始伺服器。
已停用|還原預設行為。 預設行為是根據要求提供有效的快取資產。
不需要此功能即可進行正確的快取和內容傳遞，但此功能可能有助於解決這個問題。 例如，原始伺服器上的動態內容產生器不慎產生了要傳送到 Edge Server 的 0 位元組回應。 這些類型的回應通常會快取的邊緣伺服器。 如果您知道對於這類內容而言，0 位元組的回應絕對不是有效的回應， 

則此功能可防止將這些類型的資產提供給用戶端。

**預設行為：**已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="set-cacheable-status-codes"></a>設定可快取的狀態碼
**目的：**定義一組可產生快取內容的狀態碼。

根據預設，只會針對 [200 確定] 回應啟用快取。

定義一組所需的狀態碼 (以空格分隔)。

重要資訊：

- 啟用 [忽略原始的 No-Cache] 功能。 如果未啟用此功能，可能不會快取非 [200 確定] 的回應。
- 以下是此功能的有效狀態碼集合︰203、300、301、302、305、307、400、401、402、403、404、405、406、407、408、409、410、411、412、413、414、415、416、417、500、501、502、503、504 和 505。
- 此功能無法用來針對產生 [200 確定] 狀態碼的回應停用快取。

**預設行為︰**只會針對產生 [200 確定] 狀態碼的回應啟用快取。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="set-client-ip-custom-header"></a>設定用戶端 IP 自訂標頭
**目的︰**依 IP 位址識別要求用戶端的自訂標頭加入至要求。

標頭名稱選項定義自訂要求標頭儲存用戶端的 IP 位址的名稱。

此功能讓客戶原始伺服器能夠透過自訂要求標頭找出用戶端 IP 位址。 如果是從快取提供要求，則不會將用戶端的 IP 位址告知原始伺服器。 因此，建議將此功能與 ADN 或不會快取的資產搭配使用。

請確定指定的標頭名稱不符合下列任一個名稱：

- 標準要求標頭名稱。 您可以在 [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) 中找到標準標頭名稱清單。
- 保留的標頭名稱：
    - forwarded-for
    - host
    - vary
    - via
    - 警告
    - x-forwarded-for
    - 以「x-ec」開頭的所有標頭名稱都會保留。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="stale-content-delivery-on-error"></a>發生錯誤時傳遞過時的內容
**用途：**判斷發生錯誤時在快取重新驗證期間，或從客戶原始伺服器擷取所要求的內容時，是否會傳遞過期的快取的內容。

值|結果
-|-
已啟用|在原始伺服器連接期間發生錯誤時，會提供給要求者過時的內容。
已停用|來源伺服器的錯誤轉寄給要求者。

**預設行為：**已停用

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="stale-while-revalidate"></a>在重新驗證時過期
**用途：**藉由使用重新驗證時，過時內容提供給要求者的邊緣伺服器可改善效能。

重要資訊：

- 此功能的行為會根據選取的時間單位而不同。
    - **時間單位︰**指定的時間長度，然後選取允許過時內容傳遞的時間單位 (例如，秒、分鐘、小時等)。 這種類型的安裝程式可讓 CDN 根據下列公式，延伸可能要在要求驗證之前傳遞內容的時間長度：**TTL** + **重新驗證時間時過時** 
    - **關閉：**選取「關閉」，以便在可能提供過時內容的要求之前，要求重新驗證。
        - 請勿指定時間長度，因為它不適用且將會遭到忽略。

**預設行為：**關閉。 重新驗證必須在可提供要求的內容之前進行。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="token-auth"></a>權杖驗證
**目的**：判斷是否要將權杖型驗證套用到要求。

如果啟用權杖型驗證，則只會接受提供加密權杖且符合該權杖所指定需求的要求。

加密金鑰是用來加密和解密的語彙基元值取決於主索引鍵和權杖驗證頁面上的備份金鑰選項。 請記住，加密金鑰是特定平台的。

值 | 結果
------|---------
已啟用 | 使用權杖型驗證保護要求的內容。 只接受來自用戶端且可提供有效權杖並符合其需求的要求。 FTP 交易會從權杖型驗證中排除。
已停用| 還原預設行為。 預設行為是讓您的權杖型驗證組態能夠判斷要求是否將會受到保護。

**預設行為：**已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="token-auth-denial-code"></a>權杖驗證拒絕代碼
**目的：**判斷在要求因權杖型驗證而遭到拒絕時將傳回給使用者的回應類型。

以下列出可用的回應碼。

回應碼|回應名稱|說明
----------------|-----------|--------
301|已永久移動|此狀態碼會將未經授權的使用者重新導向至位置標頭中指定的 URL。
302|已找到|此狀態碼會將未經授權的使用者重新導向至位置標頭中指定的 URL。 此狀態碼是執行重新導向的業界標準方法。
307|暫時重新導向|此狀態碼會將未經授權的使用者重新導向至位置標頭中指定的 URL。
401|未經授權|將此狀態碼與 WWW 驗證回應標頭相結合，讓您能夠提示使用者進行驗證。
403|禁止|這是標準的 [403 禁止] 狀態訊息，未經授權的使用者將會在嘗試存取受保護的內容時看見此訊息。
404|找不到檔案|此狀態碼表示 HTTP 用戶端能夠與伺服器通訊，但找不到要求的內容。

#### <a name="url-redirection"></a>URL 重新導向

將此功能設為傳回 3xx 狀態碼時，此功能支援將 URL 重新導向至使用者定義的 URL。 執行下列步驟，即可指定此使用者定義的 URL：

1. 針對 [權杖驗證拒絕代碼] 功能選取 3xx 回應碼。
2. 從 [選用標頭名稱] 選項中選取 [位置]。
3. 將 [選用標頭值] 選項設為所需的 URL。

如果未定義適用於 3xx 狀態碼的 URL，則會將適用於 3xx 狀態碼的標準回應頁面傳回給使用者。

URL 重新導向只適用於 3xx 回應碼。

[選用標頭值] 選項支援英數字元、引號和空格。

#### <a name="authentication"></a>驗證

此功能支援的功能可在針對權杖型驗證所保護的內容回應未經授權的要求時包含 WWW-Authenticate 標頭。 如果您的設定中已將 WWW-Authenticate 標頭設為「basic」，則會提示未經授權的使用者提供帳戶認證。

您可以藉由執行下列步驟來完成上述組態：

1. 針對 [權杖驗證拒絕代碼] 功能選取 [401] 做為回應碼。
2. 從 [選用標頭名稱] 選項中選取 [WWW-Authenticate]。
3. 將 [選用標頭值] 選項設為 [basic]。

WWW-Authenticate 標頭只適用於 401 回應碼。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="token-auth-ignore-url-case"></a>權杖驗證會忽略 URL 的大小寫
**用途：**判斷權杖型驗證所進行的 URL 比較是否區分大小寫。

受此功能影響的參數如下：

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

有效值為：

值|結果
---|----
已啟用|會導致要比較權杖型驗證參數的 Url 時忽略大小寫的邊緣伺服器。
已停用|還原預設行為。 預設行為是在進行權杖型驗證的 URL 比較時會區分大小寫。

**預設行為：**已停用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="token-auth-parameter"></a>權杖驗證參數
**目的：**判斷是否應將權杖型驗證查詢字串參數重新命名。

重要資訊：

- [值] 選項會定義可能要透過其指定權杖的查詢字串參數名稱。
- [值] 選項不能設定為 [ec_token]。
- 確認 [值] 選項中定義的名稱僅包含有效的 URL 字元。

值|結果
----|----
已啟用|[值] 選項會定義應透過其定義權杖的查詢字串參數名稱。
已停用|您可以指定權杖做為要求 URL 中未定義的查詢字串參數。

**預設行為：**已停用。 您可以指定權杖做為要求 URL 中未定義的查詢字串參數。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="url-redirect"></a>[URL 重新導向]
**目的：**透過位置標頭來將要求重新導向。

此功能的組態必須設定下列選項：

選項|說明
-|-
代碼|選取將傳回給要求者的回應碼。
來源與模式| 這些設定會定義要求 URI 模式，此模式會識別可能要重新導向的要求類型。 只會重新導向 URL 符合下列這兩個準則的要求： <br/> <br/> **來源 (或內容存取點)：**選取識別原始伺服器的相對路徑。 這是「/XXXX/」區段和您的端點名稱。 <br/> **來源 (模式)︰**必須定義依相對路徑識別要求的模式。 這個規則運算式模式必須定義一個路徑，該路徑會在先前選取的內容存取點 (請參閱上述內容) 之後直接啟動。 <br/> - 確定先前定義的要求 URI 準則 (亦即，[來源與模式]) 不會與針對此功能所定義的任何比對條件相衝突。 <br/> - 指定模式；如果您是使用空白值作為模式，所有字串都會相符。
目的地| 定義要將上述要求重新導向至其中的 URL。 <br/> 使用下列方式來動態建構此 URL： <br/> - 規則運算式模式 <br/>- HTTP 變數 <br/> 使用 $_n_，將擷取自來源模式的值替代為目的地模式，其中 _n_ 可依擷取的順序來識別值。 例如，$1 表示擷取自來源模式的第一個值，而 $2 代表第二個值。 <br/> 
強烈建議使用絕對 URL。 使用相對 URL 可能會將 CDN URL 重新導向至不正確的路徑。

**範例案例**

此範例中，示範如何將重新導向的邊緣會解析成此基底的 CDN URL 的 CNAME URL: http://marketing.azureedge.net/brochures

符合資格的要求將會重新導向至此基底 Edge CNAME URL：http://cdn.mydomain.com/resources

此 URL 重新導向可透過下列組態來達成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**重點︰**

- [URL 重新導向] 功能會定義將重新導向的要求 URL。 如此一來，就不需要額外的比對條件。 雖然將比對條件定義為 [一律]，但只會重新導向指向 [marketing] 客戶原始伺服器上 [brochures] 資料夾的要求。 
- 所有相符的要求都將重新導向到 [目的地] 選項中所定義的 Edge CNAME URL。 
    - 範例案例 1： 
        - 範例要求 (CDN URL)：http://marketing.azureedge.net/brochures/widgets.pdf 
        - 要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/widgets.pdf  
    - 範例案例 2： 
        - 範例要求 (Edge CNAME URL)：http://marketing.mydomain.com/brochures/widgets.pdf 
        - 要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/widgets.pdf 範例案例
    - 範例案例 3： 
        - 範例要求 (Edge CNAME URL)：http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - 要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- 已在 [目的地] 選項中運用要求配置 (%{scheme}) 變數。 這可確保要求的配置在重新導向之後仍會維持不變。
- 擷取自要求的 URL 區段會透過「$1」附加到新的 URL。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="url-rewrite"></a>URL 重寫
**目的：**重寫要求 URL。

重要資訊：

- 此功能的組態必須設定下列選項：

選項|說明
-|-
 來源與模式 | 這些設定會定義要求 URI 模式，此模式會識別可能要重寫的要求類型。 只會重寫 URL 符合下列這兩個準則的要求： <br/>     - **來源 (或內容存取點)：**選取識別原始伺服器的相對路徑。 這是「/XXXX/」區段和您的端點名稱。 <br/> - **來源 (模式)︰**必須定義依相對路徑識別要求的模式。 這個規則運算式模式必須定義一個路徑，該路徑會在先前選取的內容存取點 (請參閱上述內容) 之後直接啟動。 <br/> - 確認先前定義的要求 URI 準則 (亦即，[來源與模式]) 不會與針對此功能所定義的任何比對條件相衝突。 指定模式；如果您是使用空白值作為模式，所有字串都會相符。 
 目的地  |使用下列方式來定義要將上述要求重寫至其中的相對 URL： <br/>    1.選取可識別原始伺服器的內容存取點。 <br/>    2.使用下列方式來定義相對路徑： <br/>        - 規則運算式模式 <br/>        - HTTP 變數 <br/> <br/> 使用 $_n_，將擷取自來源模式的值替代為目的地模式，其中 _n_ 可依擷取的順序來識別值。 例如，$1 表示擷取自來源模式的第一個值，而 $2 代表第二個值。 
 這項功能可讓要重寫 URL，而不需執行傳統的重新導向的邊緣伺服器。 這表示，如果收到重寫 URL 的要求，要求者將會收到相同的回應碼。

**範例案例 1**

此範例示範如何將重新導向的邊緣會解析成此基底的 CDN URL 的 CNAME URL: http://marketing.azureedge.net/brochures/

符合資格的要求將會重新導向至此基底 Edge CNAME URL：http://MyOrigin.azureedge.net/resources/

此 URL 重新導向可透過下列組態來達成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**範例案例 2**

此範例示範如何將重新導向 CNAME URL 從小寫使用規則運算式的全部大寫的邊緣。

此 URL 重新導向可透過下列組態來達成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**重點︰**

- [URL 重寫] 功能會定義將要重寫的要求 URL。 如此一來，就不需要額外的比對條件。 雖然將比對條件定義為 [一律]，但只會重寫指向 [marketing] 客戶原始伺服器上 [brochures] 資料夾的要求。

- 擷取自要求的 URL 區段會透過「$1」附加到新的 URL。

#### <a name="compatibility"></a>相容性

此功能包括必須符合才能套用到要求的比對準則。 為了防止設定衝突的比對準則，此功能與下列比對條件不相容：

- AS 號碼
- CDN 原點
- 用戶端 IP 位址
- 客戶原點
- 要求配置
- URL 路徑目錄
- URL 路徑的副檔名
- URL 路徑的檔案名稱
- URL 路徑常值
- URL 路徑 Regex
- URL 路徑萬用字元
- URL 查詢常值
- URL 查詢參數
- URL 查詢 Regex
- URL 查詢萬用字元

[回到頁首](#azure-cdn-rules-engine-features)

</br>

---
### <a name="user-variable"></a>使用者變數
**用途：**僅供內部使用。

[回到頁首](#azure-cdn-rules-engine-features)

</br>

## <a name="next-steps"></a>後續步驟
* [規則引擎參考 (英文)](cdn-rules-engine-reference.md)
* [規則引擎條件式運算式 (英文)](cdn-rules-engine-reference-conditional-expressions.md)
* [規則引擎比對條件 (英文)](cdn-rules-engine-reference-match-conditions.md)
* [使用規則引擎覆寫預設的 HTTP 行為](cdn-rules-engine.md)
* [Azure CDN 概觀](cdn-overview.md)
