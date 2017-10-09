---
title: "串流分析輸出︰儲存體、分析的選項 | Microsoft Docs"
description: "深入了解串流分析資料輸出的選項 (包括使用於分析結果的 Power BI)。"
keywords: "資料轉換, 分析結果, 資料儲存體選項"
services: stream-analytics,documentdb,sql-database,event-hubs,service-bus,storage
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ba6697ac-e90f-4be3-bafd-5cfcf4bd8f1f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 99f8113f0464960e898293397fbe3de90d669857
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-outputs-options-for-storage-analysis"></a>串流分析輸出︰儲存體、分析的選項
當撰寫資料流分析工作，請考慮如何使用 hello 產生的資料。 如何將檢視 hello hello 資料流分析作業的結果，並會在儲存它嗎？

順序 tooenable 各種不同的應用程式模式，在 Azure Stream Analytics 中會有不同的選項，儲存輸出和檢視分析結果。 這會使它輕鬆 tooview 作業輸出，並且可讓您的資料倉儲和其他用途的 hello 耗用量和 hello 作業輸出的儲存體的彈性。 Hello 工作中設定任何輸出必須先建立 hello 作業已啟動，而且流動開始事件。 比方說，如果您使用 Blob 儲存體做為輸出時，hello 作業將不會自動建立儲存體帳戶。 它需要 toobe hello ASA 工作啟動之前，由 hello 使用者所建立。

## <a name="azure-data-lake-store"></a>Azure Data Lake Store
串流分析支援 [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)。 這個儲存體可讓您的作業及探勘分析的任何大小、 類型和擷取速度 toostore 資料。 此外，串流分析需要 toobe 授權 tooaccess hello 資料湖存放區。 有關授權與註冊資料湖存放區 （如有需要） hello toosign hello 的會討論[Data Lake 輸出文件](stream-analytics-data-lake-output.md)。

### <a name="authorize-an-azure-data-lake-store"></a>授權 Azure Data Lake Store
做為輸出 hello Azure 入口網站中選取資料湖存放區時，系統會提示的 tooauthorize 連接 tooan 現有資料湖存放區。  

![授權 Data Lake Store](./media/stream-analytics-define-outputs/06-stream-analytics-define-outputs.png)  

然後填寫 hello Data Lake Store 輸出如下所示為 hello 屬性：

![授權 Data Lake Store](./media/stream-analytics-define-outputs/07-stream-analytics-define-outputs.png)  

hello 下表列出 hello 屬性名稱和其所需的建立輸出資料湖存放區的描述。

<table>
<tbody>
<tr>
<td><B>屬性名稱</B></td>
<td><B>說明</B></td>
</tr>
<tr>
<td>輸出別名</td>
<td>這是用於查詢 toodirect hello 查詢輸出 toothis Data Lake Store 的易記名稱。</td>
</tr>
<tr>
<td>帳戶名稱</td>
<td>hello hello 傳送您的輸出資料湖存放區帳戶名稱。 您將出現的下拉式清單的 Data Lake Store 帳戶登入 toohello 入口網站的 toowhich hello 使用者具有存取權。</td>
</tr>
<tr>
<td>路徑前置詞模式 [<I>選用</I>]</td>
<td>hello 檔案路徑使用 toowrite 內 hello 檔案指定的資料湖存放區帳戶。 <BR>{date}、{time}<BR>範例 1：folder1/logs/{date}/{time}<BR>範例 2：folder1/logs/{date}</td>
</tr>
<tr>
<td>日期格式 [<I>選用</I>]</td>
<td>如果 hello 日期語彙基元不用於 hello 前置詞的路徑，您可以選取組織檔案的 hello 日期格式。 範例：YYYY/MM/DD</td>
</tr>
<tr>
<td>時間格式 [<I>選用</I>]</td>
<td>如果 hello 時間語彙基元 hello 前置詞路徑中，指定組織檔案的 hello 時間格式。 目前僅支援 hello 值是 HH。</td>
</tr>
<tr>
<td>事件序列化格式</td>
<td>輸出資料的序列化格式。 支援 JSON、CSV 和 Avro。</td>
</tr>
<tr>
<td>編碼</td>
<td>若為 CSV 或 JSON 格式，必須指定編碼。 Utf-8 是 hello 此時只支援編碼格式。</td>
</tr>
<tr>
<td>分隔符號</td>
<td>僅適用於 CSV 序列化。 串流分析可支援多種序列化 CSV 資料常用的分隔符號。 支援的值是逗號、分號、空格、索引標籤和分隔號。</td>
</tr>
<tr>
<td>格式</td>
<td>僅適用於 JSON 序列化。 行分隔指定 hello 輸出，將會格式化每個 JSON 物件以新行字元分隔。 陣列指定 hello 輸出將會格式化為 JSON 物件的陣列。</td>
</tr>
</tbody>
</table>

### <a name="renew-data-lake-store-authorization"></a>更新 Data Lake Store 授權
您將需要 toore-驗證 Data Lake Store 帳戶之後您的工作所建立或上次經過驗證,，其密碼已經變更。

![授權 Data Lake Store](./media/stream-analytics-define-outputs/08-stream-analytics-define-outputs.png)  

## <a name="sql-database"></a>SQL Database
[Azure SQL Database](https://azure.microsoft.com/services/sql-database/) 做為資料輸出。 資料流分析工作會在 Azure SQL Database 中撰寫 tooan 現有的資料表。  請注意該 hello 資料表結構描述必須完全符合 hello 欄位和其類型，便會從您的工作輸出。 [Azure SQL 資料倉儲](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)也可以指定做為輸出透過 hello SQL Database 輸出選項 （這是預覽功能）。 hello 下表列出 hello 屬性名稱和描述其建立 SQL Database 輸出。

| 屬性名稱 | 說明 |
| --- | --- |
| 輸出別名 |這是用於查詢 toodirect hello 查詢輸出 toothis 資料庫中的易記名稱。 |
| 資料庫 |hello hello 資料庫傳送您的輸出名稱 |
| 伺服器名稱 |hello SQL Database 伺服器名稱 |
| 使用者名稱 |hello 具有存取 toowrite toohello 資料庫使用者名稱 |
| 密碼 |hello 密碼 tooconnect toohello 資料庫 |
| 資料表 |hello hello 輸出將寫入其中的資料表名稱。 hello 資料表名稱會區分大小寫，並且 hello 這個資料表的結構描述應符合完全 toohello 欄位數目和其所作業輸出要產生的型別。 |

> [!NOTE]
> Hello Azure SQL Database 供應項目目前支援的資料流分析工作輸出。 不過，不支援執行已連結資料庫之 SQL Server 的「Azure 虛擬機器」。 這是主體 toochange 在未來的版本。
> 
> 

## <a name="blob-storage"></a>Blob 儲存體
Blob 儲存體可提供符合成本效益且可延展解決方案 hello 雲端中儲存大量非結構化資料。  如需 Azure Blob 儲存體和其使用方式的簡介，請參閱 hello 文件，網址[toouse 的 Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。

hello 下表列出 hello 屬性名稱和描述來建立 blob 輸出。

<table>
<tbody>
<tr>
<td>屬性名稱</td>
<td>說明</td>
</tr>
<tr>
<td>輸出別名</td>
<td>這是用於查詢 toodirect hello 查詢輸出 toothis blob 儲存體中的易記名稱。</td>
</tr>
<tr>
<td>儲存體帳戶</td>
<td>hello hello 傳送輸出的儲存體帳戶名稱。</td>
</tr>
<tr>
<td>儲存體帳戶金鑰</td>
<td>hello 秘密金鑰與 hello 儲存體帳戶相關聯。</td>
</tr>
<tr>
<td>儲存體容器</td>
<td>容器提供 blob 儲存在 hello Microsoft Azure Blob 服務中的邏輯分組。 當您上傳 blob toohello Blob 服務時，您必須指定該 blob 的容器。</td>
</tr>
<tr>
<td>路徑前置詞模式 [選用]</td>
<td>hello 檔案路徑用 toowrite 您 hello 指定容器內的 blob。<BR>Hello 路徑內，您可以選擇 toouse hello 遵循 2 變數 toospecify hello 頻率 blob 寫入一個或多個執行個體：<BR>{date}、{time}<BR>範例 1：cluster1/logs/{date}/{time}<BR>範例 2：cluster1/logs/{date}</td>
</tr>
<tr>
<td>日期格式 [選用]</td>
<td>如果 hello 日期語彙基元不用於 hello 前置詞的路徑，您可以選取組織檔案的 hello 日期格式。 範例：YYYY/MM/DD</td>
</tr>
<tr>
<td>時間格式 [選用]</td>
<td>如果 hello 時間語彙基元 hello 前置詞路徑中，指定組織檔案的 hello 時間格式。 目前僅支援 hello 值是 HH。</td>
</tr>
<tr>
<td>事件序列化格式</td>
<td>輸出資料的序列化格式。  支援 JSON、CSV 和 Avro。</td>
</tr>
<tr>
<td>編碼</td>
<td>若為 CSV 或 JSON 格式，必須指定編碼。 Utf-8 是 hello 此時只支援編碼格式。</td>
</tr>
<tr>
<td>分隔符號</td>
<td>僅適用於 CSV 序列化。 串流分析可支援多種序列化 CSV 資料常用的分隔符號。 支援的值是逗號、分號、空格、索引標籤和分隔號。</td>
</tr>
<tr>
<td>格式</td>
<td>僅適用於 JSON 序列化。 行分隔指定 hello 輸出，將會格式化每個 JSON 物件以新行字元分隔。 陣列指定 hello 輸出將會格式化為 JSON 物件的陣列。 這個陣列只當 hello 作業停止或資料流分析已移動 toohello 下一個時間範圍將會關閉。 一般情況下，它就是分隔的 JSON，因為它不需要任何特殊處理，而 hello 輸出檔案正在寫入至偏好 toouse 線條。</td>
</tr>
</tbody>
</table>

## <a name="event-hub"></a>事件中樞
[事件中樞](https://azure.microsoft.com/services/event-hubs/) 是具高延展性的發佈-訂閱事件擷取器。 它每秒可以收集數百萬個事件。  Hello 輸出資料流分析工作將會 hello 輸入的另一個資料流處理工作時做為輸出的事件中心使用。

有幾個參數所需的 tooconfigure 事件中心資料流做為輸出。

| 屬性名稱 | 說明 |
| --- | --- |
| 輸出別名 |這是用於查詢 toodirect hello 查詢輸出 toothis 事件中心的易記名稱。 |
| 服務匯流排 命名空間 |服務匯流排命名空間是一個容器，包含一組訊息實體。 建立新的事件中樞時，也會建立服務匯流排命名空間 |
| 事件中樞 |您的事件中樞輸出 hello 名稱 |
| 事件中樞原則名稱 |hello 共用的存取原則，可以建立 hello 事件中樞設定 索引標籤。每一個共用存取原則會有名稱、權限 (由您設定) 和存取金鑰 |
| 事件中樞原則金鑰 |使用 tooauthenticate 存取 toohello 服務匯流排命名空間 hello 共用存取金鑰。 |
| 資料分割索引鍵資料行 [選用] |此資料行包含 hello 事件中樞輸出的資料分割索引鍵。 |
| 事件序列化格式 |輸出資料的序列化格式。  支援 JSON、CSV 和 Avro。 |
| 編碼 |如需 CSV 和 JSON，utf-8 是 hello 此時只支援編碼格式 |
| 分隔符號 |僅適用於 CSV 序列化。 串流分析可支援多種以 CSV 格式序列化資料常用的分隔符號。 支援的值是逗號、分號、空格、索引標籤和分隔號。 |
| 格式 |僅適用於 JSON 類型。 行分隔指定 hello 輸出，將會格式化每個 JSON 物件以新行字元分隔。 陣列指定 hello 輸出將會格式化為 JSON 物件的陣列。 |

## <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com/)可用於做為輸出資料流分析工作 tooprovide 豐富的視覺效果經驗的分析結果。 這項功能可以用於可運作的儀表板、產生報告，以及度量驅動的報告。

### <a name="authorize-a-power-bi-account"></a>授權 Power BI 帳戶
1. 選取 Power BI 時，做為輸出 hello Azure 入口網站中，您將會提示的 tooauthorize，現有的 Power BI 使用者或 toocreate 新的 Power BI 帳戶。  
   
   ![授權 Power BI 使用者](./media/stream-analytics-define-outputs/01-stream-analytics-define-outputs.png)  
2. 如果您尚未擁有帳戶，請建立新帳戶，然後按一下 [立即授權]。  就會呈現類似 hello 下列畫面。  
   
   ![Azure 帳戶 Power BI](./media/stream-analytics-define-outputs/02-stream-analytics-define-outputs.png)  
3. 在此步驟中，提供 hello 工作或學校帳戶授權 hello Power BI 輸出。 如果您尚未註冊 Power BI，請選擇 [立即註冊]。 hello Power BI 所使用的工作或學校帳戶可以不同於 hello 您目前登入的 Azure 訂用帳戶。

### <a name="configure-hello-power-bi-output-properties"></a>設定 hello Power BI 輸出屬性
Hello 驗證 Power BI 帳戶之後，您可以設定您的 Power BI 輸出 hello 屬性。 hello 表是 hello 的屬性名稱的清單，以及其描述 tooconfigure Power BI 輸出。

| 屬性名稱 | 說明 |
| --- | --- |
| 輸出別名 |這是用於查詢 toodirect hello 查詢輸出 toothis power Bi 輸出的易記名稱。 |
| 群組工作區 |您可以選取 tooenable 與其他 Power BI 使用者共用的資料在您的 Power BI 的群組帳戶，或選擇 「 我的工作區 」，若不想讓 toowrite tooa 群組。  更新現有的群組，將需要更新 hello Power BI 驗證。 |
| 資料集名稱 |提供輸出 toouse 需要 hello Power BI 資料集名稱。 |
| 資料表名稱 |提供的 Power BI 輸出的 hello hello 資料集下的資料表名稱。 目前，串流分析工作的 Power BI 輸出中，一個資料集只能有一個資料表 |

如需 Power BI 輸出和儀表板設定逐步解說，請參閱 hello [Azure Stream Analytics 與 Power BI](stream-analytics-power-bi-dashboard.md)發行項。

> [!NOTE]
> 未明確建立 hello 資料集和資料表 hello Power BI 儀表板中。 hello 資料集和資料表就會自動填入時便會啟動 hello 作業和 hello 工作開始提取的輸出放入 Power BI。 請注意，如果 hello 工作查詢不會產生任何結果，hello 資料集，而且不會建立資料表。 也請注意，如果 Power BI 已經有資料集和資料表與 hello 同名 hello 提供一個此資料流分析作業中，hello 現有資料將會覆寫。
> 
> 

### <a name="schema-creation"></a>建立結構描述
Azure Stream Analytics 建立 Power BI 資料集，並代表 hello 使用者資料表，如果不存在。 在其他情況下，新值更新 hello 資料表。目前沒有 hello 限制該只能有一個資料表可以位於資料集內。

### <a name="data-type-conversion-from-asa-toopower-bi"></a>資料類型轉換從 ASA tooPower BI
Azure Stream Analytics 更新在執行階段動態 hello 資料模型，如果 hello 輸出結構描述變更。 所有追蹤資料行名稱變更、 資料行類型變更，與 hello 新增或移除資料行。

下表涵蓋 hello 資料型別轉換，從[資料流分析的資料型別](https://msdn.microsoft.com/library/azure/dn835065.aspx)tooPower BIs[實體資料模型 (EDM) 型別](https://powerbi.microsoft.com/documentation/powerbi-developer-walkthrough-push-data/)如果 POWER BI 資料集和資料表不存在。


從串流分析 | tooPower BI
-----|-----|------------
bigint | Int64
nvarchar(max) | String
datetime | DateTime
float | 兩倍
記錄陣列 | 字串類型、常數值 “IRecord” 或 “IArray”

### <a name="schema-update"></a>更新結構描述
資料流分析會推斷 hello hello 輸出中的事件的第一個集合為基礎的 hello 資料模型結構描述。 之後如有必要，hello 資料模型結構描述就會更新的 tooaccommodate 不一定適合放入 hello 原始結構描述的內送事件。

hello`SELECT *`應該避免查詢 tooprevent 動態結構描述更新，跨資料列。 此外 toopotential 效能的影響，它可能也會導致 indeterminacy 的 hello hello 結果所花費的時間。 需要 Power BI 儀表板上顯示的 toobe hello 完全符合欄位應該選取。 此外，hello 資料值應該符合以 hello 選擇資料類型。


先前/目前 | Int64 | String | DateTime | 兩倍
-----------------|-------|--------|----------|-------
Int64 | Int64 | String | String | 兩倍
兩倍 | 兩倍 | String | String | 兩倍
String | String | String | String |  | String | 
DateTime | String | String |  DateTime | String


### <a name="renew-power-bi-authorization"></a>更新 Power BI 授權
您將需要 toore-驗證 Power BI 帳戶之後您的工作所建立或上次經過驗證,，其密碼已經變更。 如果您的 Azure Active Directory (AAD) 租用戶上設定多重要素驗證 (MFA) 則必須同時 toorenew 每 2 週的 Power BI 授權。 此問題的徵兆是沒有作業輸出和 「 驗證使用者錯誤 」 hello 作業記錄檔中：

  ![Power BI 重新整理權杖錯誤](./media/stream-analytics-define-outputs/03-stream-analytics-define-outputs.png)  

tooresolve 這個問題，請停止程式執行的作業，並移 tooyour Power BI 輸出。  按一下 hello 「 更新授權 」 連結，然後重新啟動您的工作，從 hello 上次停止時間 tooavoid 資料遺失。

  ![Power BI 更新授權](./media/stream-analytics-define-outputs/04-stream-analytics-define-outputs.png)  

## <a name="table-storage"></a>資料表儲存體
[Azure 資料表儲存體](../storage/common/storage-introduction.md)提供高可用性、 可大幅擴充的儲存體，讓應用程式可以自動調整 toomeet 使用者需求。 資料表儲存體是 Microsoft 的 NoSQL 索引鍵/屬性存放區哪一個較少 hello 結構描述上的條件約束，可以利用結構化資料。 Azure 資料表儲存體可以是使用的 toostore 資料持續性和有效率的擷取。

hello 下表列出 hello 屬性名稱和描述其建立之資料表的輸出。

| 屬性名稱 | 說明 |
| --- | --- |
| 輸出別名 |這是使用查詢 toodirect hello 查詢輸出 toothis 資料表儲存體中的易記名稱。 |
| 儲存體帳戶 |hello hello 傳送輸出的儲存體帳戶名稱。 |
| 儲存體帳戶金鑰 |hello 與 hello 儲存體帳戶相關聯的存取金鑰。 |
| 資料表名稱 |hello hello 資料表名稱。 如果不存在，將取得建立 hello 資料表。 |
| 資料分割索引鍵 |hello hello 輸出資料行包含 hello 資料分割索引鍵名稱。 hello 資料分割索引鍵是 hello form hello 第一個實體的主索引鍵一部分的指定資料表中的資料分割的唯一識別碼。 很可能是 up too1 KB 大小的字串值。 |
| 列索引鍵 |hello hello 輸出資料行包含 hello 資料列索引鍵名稱。 hello 資料列索引鍵是給定資料分割內的實體的唯一識別碼。 組件可構成實體主索引鍵的 hello 第二個部分。 hello 資料列索引鍵是字串值，可能是 up too1 KB 的大小。 |
| 批次大小 |hello 批次作業的記錄數目。 通常 hello 預設是足以應付大部分的工作，請參閱 toohello[資料表批次作業規格](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx)如需詳細資訊修改此設定。 |

## <a name="service-bus-queues"></a>服務匯流排佇列
[服務匯流排佇列](https://msdn.microsoft.com/library/azure/hh367516.aspx)第一個方案中提供，第一次出 (FIFO) 訊息傳遞 tooone 或更多的競爭取用者。 一般而言，訊息會預期的 toobe 接收和處理由 hello 接收者 hello 時態順序，在其中加入 toohello 佇列，以及每個訊息是接收並處理一個訊息取用者。

hello 下表列出 hello 屬性名稱和描述其建立之佇列的輸出。

| 屬性名稱 | 說明 |
| --- | --- |
| 輸出別名 |這是用於查詢 toodirect hello 查詢輸出 toothis 服務匯流排佇列的易記名稱。 |
| 服務匯流排 命名空間 |服務匯流排命名空間是一個容器，包含一組訊息實體。 |
| 佇列名稱 |hello hello 服務匯流排佇列名稱。 |
| 佇列原則名稱 |當您建立佇列時，您也可以在 hello 佇列設定 索引標籤上，建立共用的存取原則。每一個共用存取原則會有名稱、權限 (由您設定) 和存取金鑰。 |
| 佇列原則金鑰 |使用 tooauthenticate 存取 toohello 服務匯流排命名空間 hello 共用存取金鑰。 |
| 事件序列化格式 |輸出資料的序列化格式。  支援 JSON、CSV 和 Avro。 |
| 編碼 |如需 CSV 和 JSON，utf-8 是 hello 此時只支援編碼格式 |
| 分隔符號 |僅適用於 CSV 序列化。 串流分析可支援多種以 CSV 格式序列化資料常用的分隔符號。 支援的值是逗號、分號、空格、索引標籤和分隔號。 |
| 格式 |僅適用於 JSON 類型。 行分隔指定 hello 輸出，將會格式化每個 JSON 物件以新行字元分隔。 陣列指定 hello 輸出將會格式化為 JSON 物件的陣列。 |

## <a name="service-bus-topics"></a>服務匯流排主題
服務匯流排佇列則是提供一個 tooone 通訊方法，從 寄件者 tooreceiver [Service Bus 主題](https://msdn.microsoft.com/library/azure/hh367516.aspx)提供對多個表單的通訊。

hello 下表列出 hello 屬性名稱和描述其建立之資料表的輸出。

| 屬性名稱 | 說明 |
| --- | --- |
| 輸出別名 |這是用於查詢 toodirect hello 查詢輸出 toothis 服務匯流排主題中的易記名稱。 |
| 服務匯流排 命名空間 |服務匯流排命名空間是一個容器，包含一組訊息實體。 建立新的事件中樞時，也會建立服務匯流排命名空間 |
| 主題名稱 |主題為傳訊實體，類似 tooevent 中樞與佇列。 變更就會從許多不同的裝置與服務的設計的 toocollect 事件資料流。 建立主題時也會給予其特定名稱。 無法使用 tooa 主題，除非在建立訂閱時，傳送 hello 訊息，因此請確定有一或多個訂閱 hello 主題下 |
| 主題原則名稱 |當您建立主題時，您也可以在 hello 主題設定 索引標籤上，建立共用的存取原則。每一個共用存取原則會有名稱、權限 (由您設定) 和存取金鑰 |
| 主題原則金鑰 |使用 tooauthenticate 存取 toohello 服務匯流排命名空間 hello 共用存取金鑰。 |
| 事件序列化格式 |輸出資料的序列化格式。  支援 JSON、CSV 和 Avro。 |
| 編碼 |若為 CSV 或 JSON 格式，必須指定編碼。 Utf-8 是 hello 此時只支援編碼格式 |
| 分隔符號 |僅適用於 CSV 序列化。 串流分析可支援多種以 CSV 格式序列化資料常用的分隔符號。 支援的值是逗號、分號、空格、索引標籤和分隔號。 |

## <a name="azure-cosmos-db"></a>Azure Cosmos DB
[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) 是完全受管理的 NoSQL 文件資料庫服務，不僅提供透過無結構描述資料進行的查詢和交易、既可預測又可靠的效能，還能讓您進行快速的開發。

下面清單詳細資料 hello 屬性名稱和其描述建立 Azure Cosmos DB 輸出 hello。

* **輸出別名**– ASA 查詢中此輸出別名 toorefer  
* **帳戶名稱**– hello 名稱或端點的 hello Cosmos DB 帳戶的 URI。  
* **帳戶金鑰**– hello hello Cosmos DB 帳戶的共用的存取金鑰。  
* **資料庫**– hello Cosmos DB 資料庫名稱。  
* **集合名稱模式**– hello 集合名稱或其 hello 集合 toobe 使用模式。 可使用 hello {partition} 語彙基元，資料分割會從 0 開始建構 hello 集合名稱格式。 以下是有效的範例輸入：  
  1\) MyCollection – 必須要有一個名為 “MyCollection” 的集合存在。  
  2\) MyCollection{partition} – 這些集合必須存在 – "MyCollection0”、“MyCollection1”、“MyCollection2” 等，依此類推。  
* **資料分割索引鍵** - 選擇性。 只有當您在集合名稱模式中使用 {parition} 語彙基元時，才需要此索引鍵。 hello 輸出使用事件 toospecify hello 機碼中跨集合分割輸出的 hello 欄位名稱。 若為單一集合輸出，則可使用任何任意的輸出欄，例如 PartitionId。  
* **文件識別碼** ：可省略。 使用 toospecify hello 主索引鍵的 insert 或 update 作業所根據的輸出事件中的 hello 欄位 hello 名稱。  


## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
您已經導入了的 tooStream 分析，資料流分析的資料是來自 hello 物聯網的受管理的服務。 toolearn 進一步了解這項服務，請參閱：

* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
