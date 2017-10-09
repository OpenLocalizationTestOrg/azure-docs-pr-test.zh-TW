---
title: "aaaAzure CDN 規則引擎功能 |Microsoft 文件"
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
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Azure CDN 規則引擎功能
本主題列出的詳細的描述 hello 可用功能的 Azure 內容傳遞網路 (CDN)[規則引擎](cdn-rules-engine.md)。

規則的 hello 第三個部分是 hello 功能。 一個功能可定義 hello 類型的動作將會套用 toohello 類型的一組符合條件所識別的要求。

## <a name="access"></a>Access

這些功能是設計的 toocontrol 存取 toocontent。


名稱 | 目的
-----|--------
拒絕存取 | 判斷所有要求是否已遭拒絕且含有 [403 禁止] 回應。
權杖驗證 | 決定是否權杖型驗證會套用的 tooa 要求。
權杖驗證拒絕代碼 | 決定時，會傳回 tooa 使用者要求遭到拒絕因為 tooToken 型驗證的回應 hello 型別。
權杖驗證會忽略 URL 的大小寫 | 判斷透過權杖型驗證所做的 URL 比較是否會區分大小寫。
權杖驗證參數 | 決定是否應該重新命名 hello 權杖型驗證查詢字串參數。

### <a name="deny-access"></a>拒絕存取
**目的**：判斷所有要求是否已遭拒且含有 [403 禁止] 回應。

值 | 結果
------|-------
已啟用| 會導致滿足 hello 403 禁止回應以拒絕比對準則 toobe 的所有要求。
已停用| 還原 hello 預設行為。 hello 預設行為是回應的 tooallow hello 原始伺服器 toodetermine hello 類型將傳回。

**預設行為**：已停用

> [!TIP]
   > 這項功能的其中一個可能的使用是 tooassociate 它具有要求標頭比對條件 tooblock 存取 tooHTTP 推薦者 」 使用內嵌連結 tooyour 內容。

### <a name="token-auth"></a>權杖驗證
**用途：**判斷權杖型驗證是否會套用的 tooa 要求。

如果已啟用權杖型驗證，則採用提供加密的權杖，且必須符合該語彙基元指定 toohello 需求的唯一要求。

hello 加密金鑰，將會使用的 tooencrypt 和解密的語彙基元值取決於主索引鍵和權杖驗證頁面上的備份金鑰選項。 請記住，加密金鑰是特定平台的。

值 | 結果
------|---------
已啟用 | 保護 hello 要求使用權杖型驗證的內容。 只接受來自用戶端且可提供有效權杖並符合其需求的要求。 FTP 交易會從權杖型驗證中排除。
已停用| 還原 hello 預設行為。 hello 預設行為是 tooallow 您權杖為基礎的驗證組態 toodetermine 是否要求將會受到保護。

**預設行為：**已停用。

###<a name="token-auth-denial-code"></a>權杖驗證拒絕代碼
**用途：**判斷 hello 回應時，會傳回 tooa 使用者要求遭到拒絕因為 tooToken 為基礎的驗證類型。

hello 可用的回應碼如下所示。

回應碼|回應名稱|說明
----------------|-----------|--------
301|已永久移動|此狀態碼會重新導向位置標頭中指定的未經授權的使用者 toohello URL。
302|已找到|此狀態碼會重新導向位置標頭中指定的未經授權的使用者 toohello URL。 此狀態碼是 hello 執行重新導向的業界標準方法。
307|暫時重新導向|此狀態碼會重新導向位置標頭中指定的未經授權的使用者 toohello URL。
401|未經授權|此狀態碼結合 WWW 驗證回應標頭可讓您 tooprompt 用於驗證的使用者。
403|禁止|這是 hello 標準 403 禁止狀態訊息未經授權的使用者會看到當嘗試 tooaccess 受保護的內容。
404|找不到檔案|此狀態碼表示 hello HTTP 用戶端可以 toocommunicate 與 hello 伺服器，但找不到內容的 hello 要求。

#### <a name="url-redirection"></a>URL 重新導向

此功能支援 URL 重新導向 tooa 使用者定義的 URL 時設定的 tooreturn 3xx 狀態碼。 藉由執行下列步驟的 hello，您可以指定這個使用者定義的 URL:

1. 選取 hello 權杖驗證拒絕程式碼功能的 3xx 回應碼。
2. 從 [選用標頭名稱] 選項中選取 [位置]。
3. 選擇性標頭值選項 toohello 集所需的 URL。

如果未針對 3xx 狀態碼定義 URL，然後 hello 3xx 狀態碼的標準回應頁面將會傳回 toohello 使用者。

URL 重新導向只適用於 3xx 回應碼。

[選用標頭值] 選項支援英數字元、引號和空格。

#### <a name="authentication"></a>驗證

回應 tooan 未經授權之要求的權杖型驗證所保護的內容時，此功能支援 hello 功能 tooinclude WWW 驗證標頭。 Www-authenticate 標頭已設定太 「 基本 」 組態中，如果 hello 未經授權的使用者將會提示帳戶認證。

上述組態的 hello 可藉由執行下列步驟的 hello:

1. 選取 「 401 」 做為 hello 回應 hello 權杖驗證拒絕程式碼功能程式碼。
2. 從 [選用標頭名稱] 選項中選取 [WWW-Authenticate]。
3. 將選擇性標頭值選項設定為太 「 基本。 」

WWW-Authenticate 標頭只適用於 401 回應碼。

### <a name="token-auth-ignore-url-case"></a>權杖驗證會忽略 URL 的大小寫
**目的：**判斷透過權杖型驗證所做的 URL 比較是否會區分大小寫。

這項功能會受到 hello 參數如下：

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

有效值為：

值|結果
---|----
已啟用|時，讓我們的邊緣伺服器 tooignore 案例比較權杖型驗證參數的 Url。
已停用|還原 hello 預設行為。 hello 預設行為是讓 URL 權杖驗證 toobe 區分大小寫的比較。

**預設行為：**已停用。
 
### <a name="token-auth-parameter"></a>權杖驗證參數
**用途：**決定是否應該重新命名 hello 權杖型驗證查詢字串參數。

重要資訊：

- [值] 選項定義可能會指定權杖的 hello 查詢字串參數名稱。
- [值] 選項無法設定得 「 ec_token。 」
- 請確定 [值] 選項只有在定義該 hello 名稱 
- 包含有效的 URL 字元。

值|結果
----|----
已啟用|[值] 選項定義 hello 查詢字串參數名稱應該要定義語彙基元。
已停用|語彙基元可指定為 hello 要求 URL 中未定義的查詢字串參數。

**預設行為：**已停用。 語彙基元可指定為 hello 要求 URL 中未定義的查詢字串參數。

## <a name="caching"></a>快取

這些功能是設計的 toocustomize 何時及如何快取的內容。

名稱 | 目的
-----|--------
頻寬參數 | 判斷是否將會使用頻寬節流設定參數 (例如 ec_rate 和 ec_prebuf)。
頻寬節流設定 | 我們的邊緣伺服器所提供的 hello 回應 hello 頻寬節流同時間。
略過快取 | 決定 hello 要求是否可以利用我們的快取技術。
Cache-Control 標頭處理 | 控制項 hello hello 邊緣伺服器所產生的快取控制標頭，外部 Max-age 功能正在作用中時。
快取索引鍵查詢字串 | 決定 hello 快取索引鍵是否會包含或排除與要求相關聯的查詢字串參數。
快取索引鍵重寫 | 重寫 hello 快取索引鍵與要求相關聯。
完成快取填滿 | 判斷在要求於 Edge Server 上產生部分快取遺失時會發生什麼事。
壓縮檔案類型 | Hello 伺服器上定義 hello 將壓縮的檔案格式。
預設的內部最大壽命 | 決定 hello 預設保留時間上限的間隔 edge server tooorigin 伺服器快取重新驗證。
Expires 標頭處理 | 控制項的邊緣伺服器 hello Expires 標頭產生 hello 外部 Max-age 功能正在作用中時。
外部最大壽命 | 決定瀏覽器 tooedge 伺服器快取重新驗證的 hello 最大時間間隔。
強制執行內部最大壽命 | 決定 edge server tooorigin 伺服器快取重新驗證的 hello 最大時間間隔。
H.264 支援 (HTTP 漸進式下載) | 決定 hello H.264 種檔案格式，可能會使用的 toostream 內容。
接受 No-Cache 要求 | 決定是否轉寄 HTTP 用戶端的無快取要求將會是 toohello 原始伺服器。
忽略原始的 No-Cache | 判斷我們的 CDN 是否將忽略原始伺服器所提供的特定指示詞。
忽略無法滿足的範圍 | 決定時，會傳回 tooclients 要求會產生 416 的範圍無法滿足的要求狀態碼的 hello 回應。
內部最大過時 | 控制多久的時間超過快取的資產可能會提供服務的 hello 正常的到期時間的邊緣伺服器 hello 邊緣伺服器時無法 toorevalidate hello hello 來源伺服器的快取的資產。
部分快取共用 | 判斷要求是否可以產生部分快取的內容。
預先驗證快取的內容 | 在快取內容的 TTL 到期之前，判斷其是否適用進行早期重新驗證。
重新整理零位元組的快取檔案 | 判斷如何透過我們的 Edge Server 來處理 HTTP 用戶端對於 0 位元組快取資產的要求。
設定可快取的狀態碼 | 定義 hello 組可能會導致快取內容的狀態碼。
發生錯誤時傳遞過時的內容 | 判斷是否已過期期間快取重新驗證，或擷取 hello hello 客戶原始伺服器要求內容時，發生錯誤時，將會傳遞快取的內容。
在重新驗證時過期 | 藉由使用我們的邊緣伺服器 tooserve 過時的用戶端 toohello 要求者重新驗證時，可以改善效能。
註解 | hello 註解功能可讓規則中新增附註 toobe。

###<a name="bandwidth-parameters"></a>頻寬參數
**目的：**判斷是否將使用頻寬節流設定參數 (例如 ec_rate 和 ec_prebuf)。

頻寬節流參數判斷 hello 資料傳輸速率為用戶端的要求是否會限制的 tooa 自訂速率。

值|結果
--|--
已啟用|可讓我們的邊緣伺服器 toohonor 頻寬節流的要求。
已停用|讓我們的邊緣伺服器 tooignore 頻寬節流參數。 hello 要求內容系統將會正常處理 （亦即，不含頻寬節流設定）。

**預設行為：**已啟用。

###<a name="bandwidth-throttling"></a>頻寬節流設定
**用途：**流速 hello hello 回應我們的邊緣伺服器所提供的頻寬。

這兩個下列選項的 hello 必須定義的 tooproperly 設定頻寬節流設定。

選項|說明
--|--
每秒 KB 數|設定此選項 toohello 最大頻寬 (每秒 Kb) 可能會使用的 toodeliver hello 回應。
Prebuf 秒|設定此選項 toohello 秒數，我們的邊緣伺服器會等到節流的頻寬。 這段期間，不受限制的 hello 用途是頻寬的 tooprevent 媒體播放 」 發生間斷或緩衝到期 toobandwidth 節流的問題。

**預設行為：**已停用。

###<a name="bypass-cache"></a>略過快取
**用途：**決定 hello 要求是否可以利用我們的快取技術。

值|結果
--|--
已啟用|即使 hello 內容先前快取，在 edge 伺服器上，會導致透過 toohello 原始伺服器的所有要求 toofall。
已停用|根據其回應標頭中定義的 toohello 快取原則 toocache 資產導致邊緣伺服器。

**預設行為：**

- **HTTP 大型︰**已停用

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a>Cache-Control 標頭處理
**用途：**外部 Max-age 功能正在作用中時，控制 hello 產生快取控制標頭的 hello 邊緣伺服器。

hello tooplace hello 外部 Max-age 和中的 hello 快取控制標頭處理功能，是這種設定的最簡單方式 tooachieve hello 相同的陳述式。

值|結果
--|--
覆寫|可確保會進行下列動作的 hello:<br/> -會覆寫 hello 原始伺服器所產生的快取控制標頭。 <br/>-加入 hello 外部 Max-age 功能 toohello 回應所產生的快取控制標頭。
傳遞|可確保 hello 外部 Max-age 功能所產生的快取控制標頭會永遠不會加入 toohello 回應。 <br/> Hello 原始伺服器就會產生快取控制標頭，它會通過 toohello 使用者。 <br/> 如果快取控制標頭，則此選項將不會產生 hello 原始伺服器原因 hello 回應標頭 toonot 可能包含快取控制標頭。
如果遺失則加入|如果快取控制標頭不來自 hello 原始伺服器，此選項會新增 hello 外部 Max-age 功能所產生的快取控制標頭。 若要確保會為所有資產指派 Cache-Control 標頭，此選項非常有用。
移除| 此選項可確保快取控制標頭不含 hello 標頭的回應。 如果已指派給快取控制標頭，它將會移除從 hello 標頭回應。

**預設行為：**覆寫。

###<a name="cache-key-query-string"></a>快取索引鍵查詢字串
**目的：**判斷快取索引鍵是否將包含或排除與要求相關聯的查詢字串參數。

重要資訊：

- 指定一或多個查詢字串參數名稱。 每個參數名稱都應以單一空格分隔。
- 這項功能會決定是否將包含或排除 hello 快取索引鍵的查詢字串參數。 以下提供每個選項的其他資訊。

類型|說明
--|--
 包含|  指出指定的每個參數應該併入 hello 快取索引鍵。 系統將針對每個要求產生唯一的快取索引鍵，其中包含此功能中所定義之查詢字串參數的唯一值。 
 全部包含  |表示，將會建立包含唯一的查詢字串每個要求 tooan 資產的唯一快取索引鍵。 不通常建議這種設定，因為它可能會導致快取點擊 tooa 小比例。 這會增加 hello 負載 hello 原始伺服器，因為它會包含 tooserve 更多的要求。 此設定會複製 hello 快取行為稱為 「 唯一快取"查詢字串快取 頁面上。 
 排除 | 表示該只有 hello 可讓您指定參數將會排除 hello 快取索引鍵。 所有其他的查詢字串參數將會包含在 hello 快取索引鍵。 
 全部排除  |表示所有查詢字串參數將會都排除 hello 快取索引鍵。 此設定會複製 hello 預設快取行為，也稱為 「 標準快取 」 用在查詢字串快取 頁面上。 

hello 冪 HTTP 規則引擎可讓您在此實作查詢字串快取 toocustomize hello 方式。 例如，您可以指定查詢字串快取只會在特定位置或檔案類型上執行。

如果您想要 tooduplicate hello 查詢字串快取行為稱為 「 無快取"查詢字串快取 頁面上，您將需要 toocreate 包含 URL 查詢萬用字元比對條件和略過快取功能的規則。 hello URL 查詢萬用字元比對條件應該設定 tooan 星號 （*）。

#### <a name="sample-scenarios"></a>範例案例

此功能的範例使用方式如下所示。 範例要求和 hello 預設快取索引鍵如下所示。

- **範例要求︰**http://wpc.0001.&lt;網域&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01
- **預設的快取索引鍵︰**/800001/Origin/folder/asset.htm

##### <a name="include"></a>包含

範例組態：

- **類型︰**包括
- **參數︰**語言

這種設定會產生下列查詢字串參數快取索引鍵的 hello:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>全部包含

範例組態：

- **類型︰**全部包括

這種設定會產生下列查詢字串參數快取索引鍵的 hello:

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>排除

範例組態：

- **類型︰**排除
- **參數︰**工作階段識別碼的使用者識別碼

這種設定會產生下列查詢字串參數快取索引鍵的 hello:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>全部排除

範例組態：

- **類型︰**全部排除

這種設定會產生下列查詢字串參數快取索引鍵的 hello:

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a>快取索引鍵重寫
**用途：**撰寫 hello 快取索引鍵與要求相關聯。

快取索引鍵是識別快取的 hello 基於資產的 hello 相對路徑。 換句話說，我們的伺服器會檢查根據 tooits 路徑其快取索引鍵所定義的資產的快取版本。

設定這項功能，藉由定義兩個 hello 下列選項：

選項|說明
--|--
原始路徑| 定義 hello 相對路徑 toohello 類型的要求將會重新寫入其快取索引鍵。 相對路徑可藉由選取基底原始路徑，然後定義規則運算式模式來定義。
新路徑|定義 hello hello 新快取金鑰的相對路徑。 相對路徑可藉由選取基底原始路徑，然後定義規則運算式模式來定義。 此相對路徑可以透過 HTTP 變數 hello 使用動態建構
**預設行為：**要求的快取索引鍵由 hello 要求 URI。

###<a name="complete-cache-fill"></a>完成快取填滿
**目的：**判斷在要求於 Edge Server 上產生部分快取遺失時會發生什麼事。

部分快取遺漏說明 hello 未完全下載的 tooan 邊緣伺服器資產的快取狀態。 如果 edge server 僅部分快取資產，然後 hello 資產的下一個要求將會轉送一次 toohello 原始伺服器。
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
部分快取遺失通常發生於使用者中止下載之後，或發生於只要求使用 HTTP 範圍要求的資產。 這項功能是最適合用於大型的資產，使用者將不通常它們從下載開始 toofinish （例如，視訊）。 如此一來，hello HTTP 大型平台上預設會啟用這項功能。 所有其他平台上則會加以停用。

建議 tooleave hello 預設組態對於 hello HTTP 大型平台，因為它會減少您客戶的原始伺服器上的 hello 負載，而且增加 hello 速度的客戶會下載您的內容。

Toohello 追蹤哪一個快取設定的方式，因為這項功能不能關聯以下列比對條件 hello： 邊緣 Cname、 常值要求標頭、 要求標頭萬用字元、 URL 查詢常值，和 URL 查詢萬用字元。

值|結果
--|--
已啟用|還原 hello 預設行為。 hello 預設行為是 tooforce hello edge server tooinitiate hello 資產的背景擷取從 hello 原始伺服器。 在那之後，hello 資產將會在 hello 邊緣伺服器的本機快取。
已停用|防止邊緣伺服器 hello 資產執行背景擷取。 這表示該 hello 下次要求該地區該資產便會將 edge server toorequest 從 hello 客戶原始伺服器。

**預設行為：**已啟用。

###<a name="compress-file-types"></a>壓縮檔案類型
**用途：** hello 伺服器上定義 hello 將壓縮的檔案格式。

您可以使用檔案格式的網際網路媒體類型 (亦即，內容類型) 來指定檔案格式。 網際網路媒體類型為平台無關的中繼資料，可讓特定資產我們伺服器 tooidentify hello 檔案格式。 以下提供常用的網際網路媒體類型清單。

網際網路媒體類型|說明
--|--
text/plain|純文字檔案
text/html| HTML 檔案
text/css|階層式樣式表 (CSS)
application/x-javascript|Javascript
application/javascript|Javascript
重要資訊：

- 使用單一空格來分隔每個網際網路媒體類型，藉以指定多個類型。 
- 此功能將只會壓縮大小小於 1 MB 的資產。 我們的伺服器將不會壓縮較大型的資產。
- 諸如影像、視訊和音訊媒體資產 (例如 JPG、MP3、MP4 等) 之類的特定類型內容均已壓縮。 這些類型資產上的額外壓縮將不會顯著降低檔案大小。 因此，建議您不要在這些類型的資產上啟用壓縮。
- 不支援萬用字元 (例如星號)。
- 再新增此功能 tooa 規則，請確定 tooset 壓縮頁面上的此規則將套用的 hello 平台 toowhich 壓縮已停用的選項。

###<a name="default-internal-max-age"></a>預設的內部最大壽命
**用途：**判斷 hello 預設保留時間上限的間隔 edge server tooorigin 伺服器快取重新驗證。 換句話說，hello 邊緣伺服器之前，所經歷的時間量會檢查快取的資產是否符合儲存在 hello 原始伺服器上的 hello 資產。

重要資訊：

- 只有原始伺服器未在 Cache-Control 或 Expires 標頭中指派最大壽命指示時，此動作才會針對來自該原始伺服器的回應加以執行。
- 此動作將不會針對未被視為可快取的資產加以執行。
- 此動作不會影響瀏覽器 tooedge 伺服器快取 revalidations。 這種 revalidations 取決於快取控制或 Expires 標頭傳送 toohello 瀏覽器，可以使用外部 Max-age 功能自訂。
- hello 此動作結果並沒有顯著的影響 hello 回應標頭和邊緣伺服器適用於您的內容，從傳回的 hello 內容，但是它可能有傳送的邊緣伺服器 tooyour 原始伺服器的重新驗證流量的 hello 量影響。
- 以下列方式設定此功能：
    - 選取用於預設內部的保留時間上限的 hello 狀態碼。
    - 指定的整數值，然後選取 hello 所需的時間單位 （也就是，秒、 分鐘、 小時等等）。 此值會定義 hello 預設內部的最大時間間隔。

- 設定 hello 時間單位太 「 關閉 」 將會指派預設內部保留時間上限的間隔要求沒有被指派其 Cache-control 或 Expires 標頭中的保留時間上限指示為 7 天。
- Toohello 追蹤哪一個快取設定的方式，因為這項功能無法關聯以 hello 下列比對條件： 
    - Edge 
    - Cname
    - 要求標頭常值
    - 要求標頭萬用字元
    - 要求方法
    - URL 查詢常值
    - URL 查詢萬用字元

**預設值：**7 天

###<a name="expires-header-treatment"></a>Expires 標頭處理
**用途：**外部 Max-age 功能正在作用中時，控制 hello 產生 Expires 標頭的邊緣伺服器。

hello tooplace hello 外部 Max-age 和中的 hello 到期標頭處理功能，這種設定是最簡單的方式 tooachieve hello 相同的陳述式。

值|結果
--|--
覆寫|可確保會進行下列動作的 hello:<br/>-會覆寫 hello 原始伺服器所產生的 Expires 標頭。<br/>-加入 hello 外部 Max-age 功能 toohello 回應所產生的 Expires 標頭。
傳遞|可確保 Expires 標頭所產生的 hello 外部 Max-age 功能永遠不會新增 toohello 回應。 <br/> Hello 原始伺服器就會產生 Expires 標頭，它會通過 toohello 使用者。 <br/>如果 hello 原始伺服器不會產生 Expires 標頭，則此選項可能的原因 hello 回應標頭 toonot 可能包含 Expires 標頭。
如果遺失則加入| 如果 Expires 標頭不來自 hello 原始伺服器，此選項會新增 hello 外部 Max-age 功能所產生的 Expires 標頭。 若要確保會為所有資產指派 Expires 標頭，此選項非常有用。
移除| 可確保 Expires 標頭不含 hello 標頭的回應。 如果已指派給 Expires 標頭，它將會移除從 hello 標頭回應。

**預設行為：**覆寫

###<a name="external-max-age"></a>外部最大壽命
**用途：**瀏覽器 tooedge 伺服器快取重新驗證判斷 hello 最大時間間隔。 換句話說，新版本的邊緣伺服器從資產可以檢查 hello 瀏覽器之前，所經歷的時間量。

啟用這項功能將會產生快取的控制項： 最大的保留期限和到期標頭從我們的邊緣伺服器並將它們傳送 toohello HTTP 用戶端。 根據預設，這些標頭會覆寫所建立的 hello 原始伺服器。 不過，快取控制標頭的處理方式，而到期標頭處理功能可能會使用的 tooalter 這種行為。

重要資訊：

- 此動作不會影響 edge server tooorigin 伺服器快取 revalidations。 這種 revalidations 會取決於收到 hello 原始伺服器，從快取-控制項/Expires 標頭，而且可以自訂預設內部 Max-age 與 Force 內部 Max-age 功能。
- 設定指定整數值，然後選取 hello 所需的時間單位 （也就是，秒、 分鐘、 小時等） 的這項功能。
- 設定此功能 tooa 負值會導致我們的邊緣伺服器 toosend 快取的控制項： 沒有-快取和設定在 hello 截止時間過去的每個回應 toohello 瀏覽器。 HTTP 用戶端並不會快取 hello 回應，雖然這項設定不會影響我們的邊緣伺服器的能力 toocache hello 回應 hello 原始伺服器。
- 設定 hello 時間單位太 「 關閉 」 將會停用這項功能。 使用 hello 回應 hello 原始伺服器的快取的快取-控制項/Expires 標頭會傳遞 toohello 瀏覽器。

**預設行為：**關閉

###<a name="force-internal-max-age"></a>強制執行內部最大壽命
**用途：** edge server tooorigin 伺服器快取重新驗證判斷 hello 最大時間間隔。 換句話說，hello 邊緣伺服器之前，所經歷的時間量可以檢查快取的資產是否符合儲存在 hello 原始伺服器上的 hello 資產。

重要資訊：

- 這項功能將會覆寫 Cache-control 或 Expires 標頭產生從來源伺服器中定義的 hello 最大時間間隔。
- 這項功能不會影響瀏覽器 tooedge 伺服器快取 revalidations。 Revalidations 這些類型由 Cache-control 或 Expires 標頭傳送 toohello 瀏覽器。
- 這項功能並沒有顯著的影響，在 edge server toohello 要求者所傳遞的 hello 回應。 不過，它可能會重新驗證流量從我們的邊緣伺服器 toohello 原始伺服器傳送的 hello 量影響。
- 以下列方式設定此功能：
    - 選取會套用內部的最大年齡 hello 狀態碼。
    - 指定整數值，然後選取 hello 所需的時間單位 （也就是，秒、 分鐘、 小時等等）。 這個值定義 hello 要求的最大時間間隔。

- 設定 hello 時間單位太 「 關閉 」 時停用此功能。 內部的最大時間間隔將不會指派 toorequested 資產。 如果 hello 原始的標頭不包含快取的指示，然後 hello 資產會快取，根據 toohello 預設內部 Max-age 功能中的使用中設定。
- Toohello 追蹤哪一個快取設定的方式，因為這項功能無法關聯以 hello 下列比對條件： 
    - Edge 
    - Cname
    - 要求標頭常值
    - 要求標頭萬用字元
    - 要求方法
    - URL 查詢常值
    - URL 查詢萬用字元

**預設行為：**關閉

###<a name="h264-support-http-progressive-download"></a>H.264 支援 (HTTP 漸進式下載)
**用途：** H.264 判斷 hello 種檔案格式，可能會使用的 toostream 內容。

重要資訊：

- 在 [副檔名] 選項中，定義一組允許的 H.264 副檔名 (以空格分隔)。 檔案副檔名選項會覆寫 hello 預設行為。 在設定此選項時包括這些副檔名，藉以保有 MP4 和 F4V 支援。 
- 請確定 tooinclude 句號時指定每個檔案的副檔名 (例如.mp4.f4v)。

**預設行為︰**HTTP 漸進式下載預設支援 MP4 和 F4V 媒體。

###<a name="honor-no-cache-request"></a>接受 No-Cache 要求
**用途：**決定 HTTP 用戶端的無快取要求是否會轉送 toohello 原始伺服器。

無快取要求發生於 hello HTTP 用戶端會傳送快取的控制項： 沒有-快取和/或 Pragma:no-hello HTTP 要求中的快取標頭。

值|結果
--|--
已啟用|允許 HTTP 用戶端的無快取要求 toobe 轉送的 toohello 原始伺服器，並 hello 原始伺服器將會傳回 hello 回應標頭和透過 hello 邊緣伺服器 hello 主體回復 toohello HTTP 用戶端。
已停用|還原 hello 預設行為。 hello 預設行為是從轉遞 toohello 原始伺服器的 tooprevent 無快取要求。

對所有的生產流量很高建議 tooleave 這項功能預設為停用狀態。 否則，原始伺服器將未受防護的重新整理網頁時不小心可能會觸發多無快取要求的使用者或 hello 從許多熱門的媒體播放程式的自動程式化 toosend 無快取標頭與每個視訊的要求。 儘管如此，這個功能便相當有用 tooapply toocertain 非生產臨時或順序 tooallow 全新內容 toobe 中測試的目錄，視取自 hello 原始伺服器。

將報告轉寄 toobe tooan 原始伺服器，因為 toothis 功能 TCP_Client_Refresh_Miss 允許要求的 hello 快取狀態。 快取狀態報告，可用於在 hello 核心報告模組中，提供依快取狀態的統計資訊。 這可讓您 tootrack hello 數目以及 tooan 原始伺服器，因為 toothis 功能正在轉送的要求百分比。

**預設行為：**已停用。

###<a name="ignore-origin-no-cache"></a>忽略原始的 No-Cache
**用途：**決定是否我們 CDN 將會忽略下列指示詞從來源伺服器提供服務的 hello:

- Cache-Control: private
- Cache-Control: no-store
- Cache-Control: no-cache
- Pragma: no-cache

重要資訊：

- 設定這項功能所定義的狀態碼將會忽略指示詞上方 hello 以空格分隔的清單。
- hello 一組有效狀態碼，這項功能是： 200、 203、 300、 301、 302、 305、 307、 400、 401、 402、 403、 404、 405、 406、 407、 408、 409、 410、 411、 412、 413、 414、 415、 416、 417、 500、 501、 502、 503、 504 和 505。
- 停用此功能，以設定 tooa 空白值。
- Toohello 追蹤哪一個快取設定的方式，因為這項功能無法關聯以 hello 下列比對條件： 
    - Edge 
    - Cname
    - 要求標頭常值
    - 要求標頭萬用字元
    - 要求方法
    - URL 查詢常值
    - URL 查詢萬用字元

**預設行為：**的預設行為是 toohonor hello 上述指示詞。

###<a name="ignore-unsatisfiable-ranges"></a>忽略無法滿足的範圍 
**用途：**決定時，會傳回 tooclients 要求會產生 416 的範圍無法滿足的要求狀態碼的 hello 回應。

根據預設，hello 指定位元組範圍要求無法滿足 edge server，而且如果範圍要求標頭欄位沒有指定時，會傳回此狀態碼。

值|結果
-|-
已啟用|可防止從 416 的範圍無法滿足的要求狀態碼回應 tooan 無效的位元組範圍要求我們邊緣伺服器。 我們的伺服器會傳送 hello 要求的資產而傳回 200 確定 hello 用戶端。
已停用|還原 hello 預設行為。 hello 預設行為是 toohonor 416 的範圍無法滿足的要求狀態碼。

**預設行為：**已停用。

###<a name="internal-max-stale"></a>內部最大過時
**用途：**控制多久過去的 hello 正常的到期時間，可能會從邊緣伺服器提供的快取的資產，hello 邊緣伺服器時無法 toorevalidate hello 快取資產 hello 原始伺服器。

一般來說，當資產的保留時間上限已逾期，hello 邊緣伺服器會傳送重新驗證要求 toohello 原始伺服器。 hello 原始伺服器將會再回應 304 不修改成 hello 邊緣為伺服器提供全新租用 hello 快取資產，或以其他方式與 200 [確定] 以提供更新版的 hello 快取資產 hello 邊緣伺服器。

如果 hello 邊緣伺服器無法 tooestablish hello 原始伺服器的連線嘗試重新驗證時，然後此內部的最大過時功能可控制是否，以及多久，hello 邊緣伺服器可能會繼續 tooserve hello 現在過時資產。

請注意，此時間間隔內啟動 hello 資產的最大期限過期時，不會在 hello 失敗的重新驗證，就會發生。 因此，在可提供資產不成功的重新驗證的 hello 最長為 hello 的保留時間上限加上最大過時的 hello 組合所指定的時間量。 例如，如果資產快取的 9:00 過時 max 15 分鐘、 30 分鐘的最大存留期與失敗的重新驗證嘗試在 9:44 會導致使用者接收 hello 過時快取資產，而 9:46 失敗的重新驗證嘗試會導致hello 終端使用者接收 504 閘道逾時。

針對這項功能已被取代快取所設定的任何值的控制項： 必須-重新驗證，或是快取-控制： proxy-重新驗證從 hello 原始伺服器收到的標頭。 如果任一這些標頭收到 hello 原始伺服器從一開始快取資產時，hello 邊緣伺服器將不會提供過時的快取的資產。 在這種情況下，如果 hello 邊緣伺服器時，無法與 hello 原點 toorevalidate hello 資產的最大時間間隔已過期，然後 hello 邊緣伺服器會傳回 504 閘道逾時。

重要資訊：

- 以下列方式設定此功能：
    - 選取會套用最大過時 hello 狀態碼。
    - 指定的整數值，然後選取 hello 所需的時間單位 （也就是，秒、 分鐘、 小時等等）。 此值會定義 hello 內部 max 過時，將會套用。

- 設定 hello 時間單位太 「 關閉 」 將會停用這項功能。 系統將不會在快取的資產超過一般到期時間之後為其提供服務。
- Toohello 追蹤哪一個快取設定的方式，因為這項功能無法關聯以 hello 下列比對條件： 
    - Edge 
    - Cname
    - 要求標頭常值
    - 要求標頭萬用字元
    - 要求方法
    - URL 查詢常值
    - URL 查詢萬用字元

**預設行為：**2 分鐘

###<a name="partial-cache-sharing"></a>部分快取共用
**目的：**判斷要求是否可以產生部分快取的內容。

Hello 要求完整快取內容之前，此部分快取可能則是使用的 toofulfill 新要求該內容。

值|結果
-|-
已啟用|要求可以產生部分快取的內容。
已停用|要求只會產生完整快取版的 hello 要求內容。

**預設行為：**已停用。

###<a name="prevalidate-cached-content"></a>預先驗證快取的內容
**目的：**在快取內容的 TTL 到期之前，判斷其是否適用進行早期重新驗證。

定義 hello 一段時間的 hello 先前 toohello 到期要求內容的 TTL 期間會很適合早期重新驗證。

重要資訊：

- Hello 快取內容的 TTL 過期後選取 「 關閉 」 hello 時間單位為需要重新驗證 tootake 位置。 不應指定時間，且將會予以忽略。

**預設行為：**關閉。 重新驗證快取的內容 TTL 過期的 hello 之後，可能只會發生。

###<a name="refresh-zero-byte-cache-files"></a>重新整理零位元組的快取檔案
**目的：**判斷如何透過 Edge Server 來處理 HTTP 用戶端對於 0 位元組快取資產的要求。

有效值為：

值|結果
--|--
已啟用|Edge server toore 提取 hello 資產，讓從 hello 原始伺服器。
已停用|還原 hello 預設行為。 hello 預設行為是 tooserve 向上收到要求時有效的快取資產。
不需要此功能即可進行正確的快取和內容傳遞，但此功能可能有助於解決這個問題。 比方說，在來源伺服器上的動態內容產生器不小心造成位元組 0 回應傳送 toohello 邊緣伺服器。 我們的 Edge Server 通常會快取這些類型的回應。 如果您知道對於這類內容而言，0 位元組的回應絕對不是有效的回應， 

如需這類的內容，然後這項功能可避免這些類型的資產提供 tooyour 用戶端。

**預設行為：**已停用。

###<a name="set-cacheable-status-codes"></a>設定可快取的狀態碼
**用途：**定義 hello 組可能會導致快取內容的狀態碼。

根據預設，只會針對 [200 確定] 回應啟用快取。

定義以空格分隔組 hello 預期的狀態碼。

重要資訊：

- 另請啟用 [忽略原始的 No-Cache] 功能。 如果未啟用該功能，則可能不會快取非 [200 確定] 的回應。
- hello 一組有效狀態碼，這項功能是： 203、 300、 301、 302、 305、 307、 400、 401、 402、 403、 404、 405、 406、 407、 408、 409、 410、 411、 412、 413、 414、 415、 416、 417、 500、 501、 502、 503、 504 和 505。
- 這項功能不能使用的 toodisable 產生 200 OK 狀態碼的回應的快取。

**預設行為︰**只會針對產生 [200 確定] 狀態碼的回應啟用快取。
###<a name="stale-content-delivery-on-error"></a>發生錯誤時傳遞過時的內容
**目的：** 

判斷是否已過期期間快取重新驗證，或擷取 hello hello 客戶原始伺服器要求內容時，發生錯誤時，將會傳遞快取的內容。

值|結果
-|-
已啟用|連接 tooan 原始伺服器期間發生錯誤時，過時的內容會提供 toohello 要求者。
已停用|hello 原始伺服器的錯誤將會轉送 toohello 要求者。

**預設行為：**已停用

###<a name="stale-while-revalidate"></a>在重新驗證時過期
**用途：**藉由使用我們的邊緣伺服器 tooserve 過時內容 toohello 要求者重新驗證時，可以改善效能。

重要資訊：

- 這項功能的 hello 行為有所不同相應 toohello 選取的時間單位。
    - **時間單位：**指定的時間長度，然後選取時間單位 （例如秒、 分鐘、 小時等等） tooallow 過時內容傳遞。 此類型的安裝程式允許 hello CDN tooextend hello 段期間內，可能會傳遞內容之前需要驗證，根據下列公式 toohello:**TTL** + **過時時重新驗證時間** 
    - **關閉：**選取 「 關閉 」 toorequire 重新驗證的要求之前可能會提供過時的內容。
        - 請勿指定時間長度，因為它不適用且將會遭到忽略。

**預設行為：**關閉。 重新驗證 hello 要求可以提供內容之前，必須先完成。

###<a name="comment"></a>註解
**用途：**允許規則中新增附註 toobe。

這項功能的其中一個使用 tooprovide hello 一般用途的規則上的其他資訊或特定原因符合條件或功能已加入 toohello 規則。

重要資訊：

- 您最多可以指定 150 個字元。
- 請確定 tooonly 使用英數字元。
- 這項功能不會影響 hello 規則的 hello 行為。 它只是用的 tooprovide 疑難排解 hello 規則時，可協助您可以提供位置資訊供未來參考或的區域。
 
## <a name="headers"></a>headers

這些功能是設計的 tooadd、 修改或刪除 hello 要求或回應的標頭。

名稱 | 目的
-----|--------
Age 回應標頭 | 決定是否將傳送 toohello 要求者的 hello 回應中包含的 Age 回應標頭。
偵錯快取回應標頭 | 決定是否回應可能包括 hello 偵錯 EC 月 X 日回應標頭提供 hello hello 要求資產的快取原則的相關資訊。
修改用戶端要求標頭 | 覆寫、附加或刪除要求的標頭。
修改用戶端回應標頭 | 覆寫、附加或刪除回應的標頭。
設定用戶端 IP 自訂標頭 | 可讓 toobe 加入的 toohello 要求 hello hello 提出要求的用戶端 IP 位址做為自訂要求標頭。

###<a name="age-response-header"></a>Age 回應標頭
**目的**： 決定是否要 Age 回應標頭包含在 hello 傳送回應 toohello 要求者。
值|結果
--|--
已啟用 | hello Age 回應標頭將包含在傳送 toohello 要求者的 hello 回應中。
已停用 | hello Age 回應標頭將排除 hello 回應傳送 toohello 要求者。

**預設行為**：已停用。

###<a name="debug-cache-response-headers"></a>偵錯快取回應標頭
**用途：**決定是否回應可能會包含提供 hello hello 要求資產的快取原則的相關資訊的偵錯 EC 月 X 日回應標頭。

偵錯快取的回應標頭會包含在 hello 回應 hello 下列都為 true 時：

- hello 偵錯快取的回應標頭功能已啟用在 hello 所要的要求。
- 上述要求 hello 定義偵錯快取的回應標頭會包含在 hello 回應 hello 組。

偵錯快取的回應標頭可能會要求包含下列標頭的 hello 和 hello hello 要求中所需的指示詞：

X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_

**範例：**

X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

值|結果
-|-
已啟用|偵錯快取回應標頭的要求將傳回包含 X-EC-Debug 標頭的回應。
已停用|偵錯 EC 月 X 日回應標頭將排除 hello 回應。

**預設行為：**已停用。

###<a name="modify-client-response-header"></a>修改用戶端回應標頭
**目的︰**每個要求都會包含一組說明其本身的 [要求標頭]()。 此功能可以：

- 附加或覆寫 hello 分派 tooa 要求標頭的值。 如果 hello 指定的要求標頭不存在，然後這項功能會將它 toohello 要求。
- 刪除 hello 要求的要求標頭。

轉送 tooan 原始伺服器的要求將會反映這項功能所做的 hello 變更。

要求標頭上，可以執行其中一個 hello 下列動作：

選項|說明|範例
-|-|-
Append|hello 指定 hello 現有的要求標頭值的 toend 不會加入值。|**要求標頭值 (用戶端)：**Value1 <br/> **要求標頭值 (HTTP 規則引擎)：**Value2 <br/>**新的要求標頭值：**Value1Value2
覆寫|標頭的值會設定 toohello hello 要求指定的值。|**要求標頭值 (用戶端)：**Value1 <br/>**要求標頭值 (HTTP 規則引擎)：**Value2 <br/>**新的要求標頭值：**Value2 <br/>
刪除|刪除 hello 指定的要求標頭。|**要求標頭值 (用戶端)：**Value1 <br/> **修改用戶端要求標頭設定：**刪除 hello 要求標頭有問題。 <br/>**結果：** hello 可讓您指定的要求標頭不會轉送 toohello 原始伺服器。

重要資訊：

- 請確定在 [名稱] 選項中指定的 hello 值完全相符的 hello 所要的要求標頭。
- 案例不會列入 hello 目的標頭用來識別的帳戶。 例如，任何下列快取控制標頭名稱變化的 hello 可以使用的 tooidentify 它：
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- 請確定 tooonly 指定標頭名稱時，使用英數字元、 虛線或底線。
- 刪除標頭讓它從轉遞 tooan 原始伺服器，我們的邊緣伺服器。
- hello 下列標頭是保留字，無法修改這項功能：
    - forwarded
    - 主機
    - via
    - 警告
    - x-forwarded-for
    - 以「x-ec」開頭的所有標頭名稱都會保留。

###<a name="modify-client-response-header"></a>修改用戶端回應標頭
每個回應都包含一組說明其本身的 [回應標頭]()。 此功能可以：

- 附加或覆寫 hello 分派 tooa 回應標頭的值。 如果 hello 指定的要求標頭不存在，然後這項功能會將它加入 toohello 回應。
- 刪除 hello 回應的回應標頭。

根據預設，回應標頭值是由原始伺服器和 Edge Server 所定義。

回應標頭上，可以執行其中一個 hello 下列動作：

選項|說明|範例
-|-|-
Append|hello 指定 hello 現有的要求標頭值的 toend 不會加入值。|**回應標頭值 (用戶端)：**Value1 <br/> **回應標頭值 (HTTP 規則引擎)：**Value2 <br/>**新的回應標頭值：**Value1Value2
覆寫|標頭的值會設定 toohello hello 要求指定的值。|**回應標頭值 (用戶端)：**Value1 <br/>**回應標頭值 (HTTP 規則引擎)：**Value2 <br/>**新的回應標頭值：**Value2 <br/>
刪除|刪除 hello 指定的要求標頭。|**要求標頭值 (用戶端)：**Value1 <br/> **修改用戶端要求標頭設定：**刪除 hello 回應標頭有問題。 <br/>**結果：** hello 指定回應標頭不會轉送 toohello 要求者。

重要資訊：

- 請確定在 [名稱] 選項中指定的 hello 值完全相符的 hello 所需的回應標頭。 
- 案例不會列入 hello 目的標頭用來識別的帳戶。 例如，任何下列快取控制標頭名稱變化的 hello 可以使用的 tooidentify 它：
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- 刪除標頭讓它從轉遞 toohello 要求者。
- hello 下列標頭是保留字，無法修改這項功能：
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

###<a name="set-client-ip-custom-header"></a>設定用戶端 IP 自訂標頭
**用途：**新增 IP 位址 toohello 要求識別 hello 要求的用戶端的自訂標頭。

標頭名稱選項定義 hello hello hello 用戶端的 IP 位址的儲存位置的自訂要求標頭名稱。

這項功能可讓客戶透過自訂要求標頭的用戶端 IP 位址時的來源伺服器 toofind。 如果 hello 要求從快取服務，然後 hello 原始伺服器將不會收到通知的 hello 用戶端的 IP 位址。 因此，建議將此功能與 ADN 或不會快取的資產搭配使用。

請確定該 hello 指定的標頭名稱不符合 hello 下列任何一項：

- 標準要求標頭名稱。 您可以在 [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) 中找到標準標頭名稱清單。
- 保留的標頭名稱：
    - forwarded-for
    - 主機
    - vary
    - via
    - 警告
    - x-forwarded-for
    - 以「x-ec」開頭的所有標頭名稱都會保留。
 
## <a name="logs"></a>記錄檔

這些功能都是設計的 toocustomize hello 資料儲存在原始記錄檔。

名稱 | 目的
-----|--------
自訂記錄欄位 1 | 決定 hello 格式和 hello 內容將會指派 toohello 原始記錄檔中的自訂記錄欄位。
記錄查詢字串 | 決定是否將儲存的查詢字串以及存取記錄檔中的 hello URL。

###<a name="custom-log-field-1"></a>自訂記錄欄位 1
**用途：**決定 hello 格式和 hello 內容將會指派 toohello 原始記錄檔中的自訂記錄欄位。

hello 這個自訂欄位背後的主要用途是 tooallow 您 toodetermine 哪些要求和回應標頭值會儲存在記錄檔。

根據預設，hello 自訂記錄檔的欄位稱為 「 x-ec_custom-1"。 不過，您可以自訂 hello 這個欄位的名稱從[未經處理的記錄檔設定 頁面]()。

hello 格式，您應該使用 toospecify 要求和回應標頭的定義如下。

標頭類型|格式|範例
-|-|-
要求標頭|%{[RequestHeader]()}[i]() | %{Accept-Encoding}i <br/> {Referer}i <br/> %{Authorization}i
回應標頭|%{[ResponseHeader]()}[o]()| %{Age}o <br/> %{Content-Type}o <br/> %{Cookie}o

重要資訊：

- 自訂記錄欄位可包含標頭欄位和純文字的任意組合。
- 這個欄位的有效字元包括 hello 下列： 英數字元 (也就是 0-9、 a 到 z、 和 A-Z)、 連字號、 冒號、 分號、 所有格符號、 逗號、 句號、 底線、 等號、 括號、 方括號和空格。 hello 百分比符號和大括號時，便只允許使用 toospecify 標頭欄位。
- 每個指定的標頭欄位的 hello 拼字必須符合 hello 所需的要求/回應標頭名稱。
- 如果您想要 toospecify 多個標頭，則建議您使用分隔符號 tooindicate 每個標頭。 例如，您可以針對每個標頭使用縮寫。 範例語法如下所示。
    - AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o 

**預設值：** -

###<a name="log-query-string"></a>記錄查詢字串
**用途：**決定是否要儲存的查詢字串以及存取記錄檔中的 hello URL。

值|結果
-|-
已啟用|存取記錄檔中記錄 Url 時，可讓 hello 的查詢字串的儲存體。 如果 URL 未包含查詢字串，則此選項將不會有任何作用。
已停用|還原 hello 預設行為。 存取記錄檔中記錄 Url 時，hello 預設行為是 tooignore 查詢字串。

**預設行為：**已停用。

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a>來源

這些功能是設計的 toocontrol hello CDN 與來源伺服器的通訊方式。

名稱 | 目的
-----|--------
Keep-Alive 要求的最大值 | 它已關閉之前，請定義 hello 保持連線的要求數目上限。
Proxy 特定的標頭 | 定義 hello 組會從邊緣伺服器 tooan 原始伺服器轉送的 CDN 專屬要求標頭。


###<a name="maximum-keep-alive-requests"></a>Keep-Alive 要求的最大值
**用途：**定義 hello 保持連線的要求數目上限之前它已關閉。

強烈建議您不要設定 hello tooa 低值時，要求的數目上限，並可能導致效能變差。

重要資訊：

- 將此值指定為整數。
- 不包含逗號或句號中指定的 hello 值。

**預設值︰**10,000 個要求

###<a name="proxy-special-headers"></a>Proxy 特定的標頭
**用途：**定義 hello 組[CDN 特定要求標頭]()，將會轉送從 edge server tooan 原始伺服器。

重要資訊：

- 這項功能中定義的每個 CDN 專屬要求標頭會轉送 tooan 原始伺服器。
- 防止 CDN 專屬的要求標頭，藉由移除此清單從轉遞 tooan 原始伺服器。

**預設行為：**所有[CDN 特定要求標頭]()轉送 toohello 原始伺服器。

## <a name="specialty"></a>特殊性

這些功能提供的進階功能僅可供進階使用者使用。

名稱 | 目的
-----|--------
可快取的 HTTP 方法 | 決定 hello 組可以快取在我們的網路的其他 HTTP 方法。
可快取的要求主體大小 | 定義判斷是否可以快取 POST 回應 hello 臨界值。

###<a name="cacheable-http-methods"></a>可快取的 HTTP 方法
**用途：**決定 hello 組可以快取在我們的網路的其他 HTTP 方法。

重要資訊：

- 此功能假設應一律快取 GET 回應。 如此一來，hello GET HTTP 方法應該不會包含設定這項功能時。
- 這項功能僅支援 hello POST HTTP 方法。 將此功能設定為：POST，藉以啟用 POST 回應快取 
- 根據預設，只會快取主體小於 14 Kb 的要求。 您可以使用可快取的要求主體大小功能來設定 hello 要求主體大小上限。

**預設行為︰**只會快取 GET 回應。

###<a name="cacheable-request-body-size"></a>可快取的要求主體大小

**用途：**定義 hello 臨界值，以判斷是否可以快取 POST 回應。

此臨界值是藉由指定要求主體大小上限來決定。 系統將不會快取包含較大要求主體的要求。

重要資訊：

- 只有在 POST 回應適合用來快取時，才適用此功能。 若要啟用 POST 要求快取使用 hello 可快取 HTTP 方法的功能。
- hello 要求主體會列入考量：
    - x-www-form-urlencoded 值
    - 確保唯一的快取索引鍵
- 定義大型的要求主體大小上限可能會影響資料傳遞效能。
    - **建議值：**14 Kb
    - **最小值︰**1 Kb

**預設行為︰**14 Kb
 
## <a name="url"></a>URL

這些功能可讓要求 toobe 重新導向，或重寫 tooa 不同的 URL。

名稱 | 目的
-----|--------
遵循重新導向 | 判斷要求是否可以在 hello 客戶原始伺服器所傳回的位置標頭中定義的重新導向的 toohello 主機名稱。
[URL 重新導向] | 將要求重新導向透過 hello 位置標頭。
URL 重寫  | 重寫 hello 要求 URL。

###<a name="follow-redirects"></a>遵循重新導向
**用途：**決定要求是否可為客戶原始伺服器所傳回之位置標頭中定義的重新導向的 toohello 主機名稱。

重要資訊：

- 要求只能重新導向的 tooedge Cname 對應 toohello 相同的平台。

值|結果
-|-
已啟用|要求可重新導向。
已停用|要求將不會重新導向。

**預設行為：**已停用。
###<a name="url-redirect"></a>[URL 重新導向]
**目的：**透過位置標頭來將要求重新導向。

這項功能的 hello 組態設定需要設定下列選項的 hello:

選項|說明
-|-
代碼|選取將會傳回 toohello 要求者的 hello 回應程式碼。
來源與模式| 這些設定定義識別 hello 可能會重新導向的要求類型的要求 URI 模式。 只有其 URL 符合這兩個 hello 下列準則的要求會被重新導向： <br/> <br/> **來源︰**(或內容存取點) 選取識別原始伺服器的相對路徑。 這是 hello"/XXXX/ 」 一節和端點名稱。 <br/> **來源 (模式)︰**必須定義依相對路徑識別要求的模式。 這個規則運算式模式必須定義會直接啟動 hello 先前選取的內容存取點 （如上述） 之後的路徑。 <br/> -請確定上述定義 hello 要求 URI 準則 （亦即，來源和模式） 不定義這項功能的任何比對條件相衝突。 <br/> -請確定 toospecify 模式。 使用空白的值為 hello 模式只會符合 hello 選取的來源伺服器 (例如 http://cdn.mydomain.com/) 要求 toohello 根資料夾。
目的地| 定義 hello URL toowhich hello 上方要求會被重新導向。 <br/> 使用下列方式來動態建構此 URL： <br/> - 規則運算式模式 <br/>- HTTP 變數 <br/> 替換圖樣 hello 目的地使用 $ 擷取 hello 來源模式中的 hello 值_n_ 其中 _n_  hello 順序它擷取識別值。 例如，$1 代表 hello hello 來源模式，而 $2 代表 hello 第二個值所擷取的第一個值。 <br/> 
它強烈建議 toouse 絕對 URL。 hello 使用相對的 URL 可能會重新導向 CDN Url tooan 無效的路徑。

**範例案例**

在此範例中，我們將示範如何 tooredirect 邊緣解析 toothis CNAME URL 基底 CDN URL: http://marketing.azureedge.net/brochures

限定要求將會是基底邊緣 CNAME 的 URL 重新導向的 toothis: http://cdn.mydomain.com/resources

此 URL 重新導向可能透過 hello 下列組態來完成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**重點︰**

- hello URL 重新導向功能可定義 hello 要求會被重新導向的 Url。 如此一來，就不需要額外的比對條件。 雖然 hello 比對條件定義為 「 永遠 」，只會要求該點 toohello"冊"hello"marketing"客戶來源上的資料夾會被重新導向。 
- 所有相符的要求將會定義目的地選項中的 CNAME 的 URL 重新導向的 toohello 邊緣。 
    - 範例案例 1： 
        - 範例要求 (CDN URL)：http://marketing.azureedge.net/brochures/widgets.pdf 
        - 要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/widgets.pdf  
    - 範例案例 2： 
        - 範例要求 (Edge CNAME URL)：http://marketing.mydomain.com/brochures/widgets.pdf 
        - 要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/widgets.pdf 範例案例
    - 範例案例 3： 
        - 範例要求 (Edge CNAME URL)：http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - 要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- hello 要求配置 （%{配置}） 的變數已在目的地選項可用。 這可確保該 hello 要求的配置會重新導向之後維持不變。
- hello hello 要求中所擷取的 URL 區段是附加的 toohello"$1"。 透過新的 URL
 
###<a name="url-rewrite"></a>URL 重寫
**用途：**重寫 hello 要求 URL。

重要資訊：

- 這項功能的 hello 組態設定需要設定下列選項的 hello:

選項|說明
-|-
 來源與模式 | 這些設定定義識別 hello 可能重寫的要求類型的要求 URI 模式。 只有其 URL 符合這兩個 hello 下列準則的要求將會重新寫入： <br/>     - **來源 (或內容存取點)：**選取識別原始伺服器的相對路徑。 這是 hello"/XXXX/ 」 一節和端點名稱。 <br/> - **來源 (模式)︰**必須定義依相對路徑識別要求的模式。 這個規則運算式模式必須定義會直接啟動 hello 先前選取的內容存取點 （如上述） 之後的路徑。 <br/> 請確定 hello 要求 URI （亦即，來源和模式） 所定義準則上面沒有與這項功能所定義的 hello 符合任何的條件衝突。 請確定 toospecify 模式。 使用空白的值為 hello 模式只會符合 hello 選取的來源伺服器 (例如 http://cdn.mydomain.com/) 要求 toohello 根資料夾。 
 目的地  |定義 hello 相對 URL 將來重新撰寫上面要求 toowhich hello: <br/>    1.選取可識別原始伺服器的內容存取點。 <br/>    2.使用下列方式來定義相對路徑： <br/>        - 規則運算式模式 <br/>        - HTTP 變數 <br/> <br/> 替換圖樣 hello 目的地使用 $ 擷取 hello 來源模式中的 hello 值_n_ 其中 _n_  hello 順序它擷取識別值。 例如，$1 代表 hello hello 來源模式，而 $2 代表 hello 第二個值所擷取的第一個值。 
 這項功能可讓我們的邊緣伺服器 toorewrite hello URL 而不需執行傳統的重新導向。 這表示該 hello 要求者會收到的 hello 相同的回應程式碼，因為如果有要求 hello 重寫 URL。

**範例案例 1**

在此範例中，我們將示範如何 tooredirect 邊緣解析 toothis CNAME URL 基底 CDN URL: http://marketing.azureedge.net/brochures/

限定要求將會是基底邊緣 CNAME 的 URL 重新導向的 toothis: http://MyOrigin.azureedge.net/resources/

此 URL 重新導向可能透過 hello 下列組態來完成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**範例案例 2**

在此範例中，我們將示範如何 tooredirect 邊緣 CNAME URL 從大寫 toolowercase 使用規則運算式。

此 URL 重新導向可能透過 hello 下列組態來完成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**重點︰**

- hello URL 重寫功能可定義 hello 要求將會重寫的 Url。 如此一來，就不需要額外的比對條件。 雖然 hello 比對條件定義為 「 永遠 」，只會要求該點 toohello"冊"hello"marketing"客戶來源上的資料夾將會重新寫入。

- hello hello 要求中所擷取的 URL 區段是附加的 toohello"$1"。 透過新的 URL



###<a name="compatibility"></a>相容性

這項功能，包括它可以套用的 tooa 要求之前，必須符合的準則相符的。 順序 tooprevent 設定衝突的比對準則，這項功能是與 hello 下列比對條件不相容：

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


## <a name="next-steps"></a>後續步驟
* [規則引擎參考 (英文)](cdn-rules-engine-reference.md)
* [規則引擎條件式運算式 (英文)](cdn-rules-engine-reference-conditional-expressions.md)
* [規則引擎比對條件](cdn-rules-engine-reference-match-conditions.md)
* [覆寫使用 hello 規則引擎的預設 HTTP 行為](cdn-rules-engine.md)
* [Azure CDN 概觀](cdn-overview.md)
