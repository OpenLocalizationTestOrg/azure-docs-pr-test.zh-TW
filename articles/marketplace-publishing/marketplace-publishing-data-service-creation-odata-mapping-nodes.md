---
title: "aaaGuide toocreating 資料服務的 hello Marketplace |Microsoft 文件"
description: "Toocreate、 認證和部署資料服務的方式的詳細的指示購買 hello Azure Marketplace 上。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 107baab2-5828-4158-abdf-59a580c80d37
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: e3d88412389d43d104662dc4434363b6ad9475f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-nodes-schema-for-mapping-an-existing-web-service-tooodata-through-csdl"></a>了解對應現有 web 服務 tooOData 透過 CSDL 結構描述的 hello 節點
> [!IMPORTANT]
> 目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。 如果您有商務 una aplicación SaaS 希望 toopublish AppSource 上，您可以找到更多資訊[這裡](https://appsource.microsoft.com/partners)。 如果您的 IaaS 應用程式或開發人員服務您會像在 Azure Marketplace toopublish 中，您可以找到更多資訊[這裡](https://azure.microsoft.com/marketplace/programs/certified/)。
>
>

本文件將有助於釐清對應的 OData 通訊協定 tooCSDL hello 節點結構。 請務必 toonote hello 節點結構是良好的 XML 格式。 因此，設計 OData 對應時，根、父和子結構描述皆適用。

## <a name="ignored-elements"></a>忽略的元素
hello 如下 hello 高等級的 CSDL 元素 （XML 節點），不會成為 toobe hello hello web 服務的中繼資料匯入期間由 hello Azure Marketplace 的後端。 它們可以存在，但會被忽略。

| 元素 | Scope |
| --- | --- |
| 使用元素 |hello 節點、 子節點及所有屬性 |
| 文件元素 |hello 節點、 子節點及所有屬性 |
| ComplexType |hello 節點、 子節點及所有屬性 |
| 關聯元素 |hello 節點、 子節點及所有屬性 |
| 擴充的屬性 |hello 節點、 子節點及所有屬性 |
| EntityContainer |只有 hello 下列屬性會被忽略：*擴充*和*AssociationSet* |
| 結構描述 |只有 hello 下列屬性會被忽略：*命名空間* |
| FunctionImport |只有 hello 下列屬性會被忽略：*模式*（假設 ln 的預設值） |
| EntityType |只有 hello 下列子節點都會被忽略：*金鑰*和*PropertyRef* |

hello 以下描述 hello 變更 （新增和忽略項目） toohello 詳細資料中的各種 CSDL XML 節點。

## <a name="functionimport-node"></a>FunctionImport 節點
FunctionImport 節點代表一個 URL （進入點） 會公開服務 toohello 使用者。 hello 節點可讓您說明如何定址 hello URL、 哪些參數可用 toohello 使用者以及如何提供這些參數。

這個節點的詳細資料可在 [這裡][MSDNFunctionImportLink](https://msdn.microsoft.com/library/cc716710.aspx) 找到

hello 如下 hello 其他屬性 （或新增項目 tooattributes） 公開 hello FunctionImport 節點：

**d:BaseUri** -hello 可公開的 tooMarketplace hello REST 資源的 URI 範本。 Marketplace 使用 hello REST web 服務的 hello 範本 tooconstruct 的查詢。 hello 與 URI 範本包含預留位置的 {parameterName}，hello 表單中的 hello 參數的 parameterName 所在 hello hello 參數名稱。 例如 apiVersion={apiVersion}.
允許參數 tooappear 做為 URI 參數，或是 hello URI 路徑的一部分。 萬一 hello 外觀 hello 路徑中的 hello 它們永遠都是強制性 （不能標示為可為 null）。 *範例：* `d:BaseUri="http://api.MyWeb.com/Site/{url}/v1/visits?start={start}&amp;end={end}&amp;ApiKey=3fadcaa&amp;Format=XML"`

**名稱**-hello hello 名稱匯入函式。  不能是 hello 與 hello CSDL 中其他已定義的名稱相同。  例如 Name="GetModelUsageFile"

**EntitySet** *（選擇性）* -如果 hello 函式傳回的實體類型集合、 hello hello 值**EntitySet**必須所屬 hello 實體集 toowhich hello 集合。 否則，hello **EntitySet**屬性都不能使用。 *範例：* `EntitySet="GetUsageStatisticsEntitySet"`

**ReturnType** *（選擇性）* -指定 hello hello URI 所傳回的元素類型。  請勿使用這個屬性，如果 hello 函式不傳回值。 hello 下面是支援的 hello 類型：

* **Collection (<Entity type name>)**：指定已定義之實體類型的集合。 hello 名稱會出現在 hello hello EntityType 節點名稱屬性。 範例為 Collection(WXC.HourlyResult)。
* **原始 (<mime type>)**： 指定未經處理的文件/blob 傳回 toohello 使用者。 範例為 Raw(image/jpeg)。其他範例：

  * ReturnType="Raw(text/plain)"
  * ReturnType="Collection(sage.DeleteAllUsageFilesEntity)"*

**d:Paging** -指定如何處理分頁的 hello REST 資源。 hello 大 braches 內可用值的參數，例如頁面 = {$page} （& s) itemsperpage 不可以 = {$size} hello 可用選項有：

* **None：** 沒有分頁可用
* **Skip：** 分頁透過邏輯 “skip” 和 “take” (上方) 表示。 略過跳透過 M 項目，並採取，然後傳回 hello 下一步 N 個元素。 參數值：$skip
* **Take:** Take 傳回 hello 下一步 N 項目。 參數值：$take
* **PageSize：** 分頁透過邏輯頁面和大小 (每頁項目數) 表示。 頁面代表 hello 傳回的目前頁面。 參數值：$page
* **大小：**大小代表 hello 傳回每一頁的項目數目。 參數值：$size

**d:AllowedHttpMethods** *（選擇性）* -指定的動詞命令由 hello REST 資源。 此外，會限制可接受的動詞命令 toohello 指定值。  預設值 = POST。  *範例：* `d:AllowedHttpMethods="GET"` hello 選項如下：

* **GET:**通常使用 tooreturn 資料
* **POST:**通常使用 tooinsert 新的資料
* **PUT:**通常使用 tooupdate 資料
* **DELETE:**用 toodelete 資料

其他子節點 （hello CSDL 文件未涵蓋） hello FunctionImport 節點內為：

**d:RequestBody** *（選擇性）* -hello 要求主體是使用 hello 要求的 tooindicate 必須傳送主體 toobe。 參數可以指定在 hello 要求主體中。 它們是以大括號括住，例如 {parameterName}。 這些參數對應使用者輸入到 hello 主體所傳送的 hello toohello 內容提供者的服務。 hello requestBody 項目有具有 httpMethod 名稱的屬性。 hello 屬性可讓兩個值：

* **POST:** HTTP POST hello 要求時使用
* **GET:** hello 要求為 HTTP GET 使用

    範例：

        `<d:RequestBody d:httpMethod="POST">
        <![CDATA[
        <req1:Request xmlns:r1="http://schemas.mysite.com//generic/requests/1" Version="1.0">
        <req1:Query>{Query}</req1:Query><req1:AppId>D453474</req1:AppId>
        <req:DestinationSchemas><req1:Schema>Generic.RequestResponse[1.0]</req1:Schema>
        </req1:DestinationSchemas>
        </req1: Request>
        ]]>
        </d:RequestBody>`

**d:Namespaces**和**d:Namespace** -此節點會描述 hello hello hello 函式匯入 （URI 端點） 所傳回的 XML 中所定義的命名空間。 hello hello 後端服務所傳回的 XML 可能包含任意數目的命名空間所傳回之 toodifferentiate hello 內容。 **這些命名空間，如果在 d:Map 或 d:Match XPath 查詢中使用的所有需要 toobe 列出。** hello d:Namespaces 節點包含一組/份 d:Namespace 節點。 每個列出 hello 後端服務回應中所使用的一個命名空間。 hello 下面是 hello d:Namespace 節點 hello 屬性：

* **d:Prefix:** hello XML 結果傳回 hello 服務，例如 f:FirstName、 f:LastName，f 所在 hello 前置詞中所見 hello hello 命名空間中，前置詞。
* **d:Uri:** hello hello hello 結果文件中使用的命名空間的完整 URI。 它代表 hello 值 hello 前置詞是解決的 tooat 執行階段。

**d:ErrorHandling** *(選用)* - 此節點包含錯誤處理的條件。 每個 hello 條件被驗證 hello hello 內容提供者的服務所傳回的結果。 如果條件符合 hello 提議 HTTP 錯誤碼 toohello 使用者頁面時，會傳回錯誤訊息。

**d:ErrorHandling** *（選擇性）*和**d:Condition** *（選擇性）* -條件節點所擁有一個簽入 hello 結果所傳回的條件hello 內容提供者的服務。 hello 如下 hello**必要**屬性：

* **d:Match:**會驗證是否存在於 hello 內容提供者指定的節點/值的 XPath 運算式的輸出 XML。 hello XPath 針對 hello 輸出執行，並應傳回 true，如果 hello 條件因相符項目或 false。
* **d:HttpStatusCode:** hello Marketplace 應 hello 案例 hello 條件比對中傳回的 HTTP 狀態碼。 Marketplace signalizes 錯誤 toohello 使用者透過 HTTP 狀態碼。 可在 http://en.wikipedia.org/wiki/HTTP_status_code 取得 HTTP 狀態碼清單
* **d:ErrorMessage:** hello 是 toohello – 以 hello HTTP 狀態碼-傳回的使用者的錯誤訊息。 這應該是易懂的錯誤訊息，其中沒有包含任何機密資料。

**d:Title** *（選擇性）* -可讓您描述 hello 標題的 hello 函式。 來自 hello title hello 值

* hello 選用的對應屬性 (xpath) 會指定 toofind hello 標題 hello 回應 hello 服務要求從傳回的位置。
* -或者-指定 hello 節點的值為 hello 標題。

**d:Rights** *（選擇性）* -hello 權限 （例如著作權） 與 hello 函式相關聯。 來自 hello hello 權限的值：

* hello 選用的對應屬性 (xpath) 會指定從 hello 服務要求傳回 toofind hello 回應 hello 權限的位置。
* -或者-指定 hello 節點的值為 hello 權限。

**d:Description** *（選擇性）* -簡短 hello 函式的描述。 來自 hello 描述 hello 值

* hello 選用的對應屬性 (xpath) 會指定 toofind hello 描述 hello 回應 hello 服務要求從傳回的位置。
* -或者-hello 描述指定為 hello 節點的值。

**d:EmitSelfLink** - *請參閱上述範例「透過傳回之資料「分頁」的 FunctionImport」*

**d:EncodeParameterValue** -tooOData 選擇性擴充功能

**d:QueryResourceCost** -tooOData 選擇性擴充功能

**d:Map** -tooOData 選擇性擴充功能

**d:Headers** -tooOData 選擇性擴充功能

**d:Headers** -tooOData 選擇性擴充功能

**d:Value** -tooOData 選擇性擴充功能

**d:HttpStatusCode** -tooOData 選擇性擴充功能

**d:ErrorMessage** -tooOData 選擇性擴充功能

## <a name="parameter-node"></a>參數節點
此節點代表一個公開為 hello URI 範本的一部分的參數 / 要求 hello FunctionImport 節點中已指定的主體。

Hello 「 參數項目 」 節點的相關詳細資料很有幫助文件頁面位於[這裡](http://msdn.microsoft.com/library/ee473431.aspx)(使用 hello**其他版本**下拉式 tooselect 如果必要 tooview hello 文件的不同版本)。 *範例：* `<Parameter Name="Query" Nullable="false" Mode="In" Type="String" d:Description="Query" d:SampleValues="Rudy Duck" d:EncodeParameterValue="true" MaxLength="255" FixedLength="false" Unicode="false" annotation:StoreGeneratedPattern="Identity"/>`

| 參數屬性 | 必要 | 值 |
| --- | --- | --- |
| 名稱 |是 |hello hello 參數名稱。 區分大小寫！  Hello BaseUri 大小寫須相符。 **範例：** `<Property Name="IsDormant" Type="Byte" />` |
| 類型 |是 |hello 參數類型。 hello 值必須是**EDMSimpleType**或 hello 模型 hello 範圍內的複雜型別。 如需詳細資訊，請參閱「6 種支援的參數/屬性類型」。  (區分大小寫！ 第一個字元是大寫，其他都是小寫)。另請參閱 [概念模型型別 (CSDL)][MSDNParameterLink](http://msdn.microsoft.com/library/bb399548.aspx)。 **範例：** `<Property Name="LimitedPartnershipID " Type="Int32" />` |
| Mode |否 |**在**、 外或 InOut 取決於 hello 參數是否為輸入、 輸出或輸入/輸出參數。 (只有 “IN” 適用於 Azure Marketplace)。**範例：**`<Parameter Name="StudentID" Mode="In" Type="Int32" />` |
| MaxLength |否 |hello 上限 hello 參數的長度。 **範例：** `<Property Name="URI" Type="String" MaxLength="100" FixedLength="false" Unicode="false" />` |
| Precision |否 |hello 參數 hello 有效位數。 **範例：** `<Property Name="PreviousDate" Type="DateTime" Precision="0" />` |
| 調整 |否 |hello 小數位數 hello 參數。 **範例：** `<Property Name="SICCode" Type="Decimal" Precision="10" Scale="0" />` |

hello 下面是已加入 toohello CSDL 規格的 hello 屬性：

| 參數屬性 | 說明 |
| --- | --- |
| **d:Regex** *(選用)* |Regex 陳述式使用 hello 參數 toovalidate hello 輸入的值。 如果 hello 輸入的值不符合 hello 陳述式 hello 值被拒絕。 這可讓 toospecify 另一組可能的值，例如: ^ [0-9] +？ $ tooonly 允許數字。 **範例︰**`<Parameter Name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters" d:SampleValues="George |
| **d:Enum** *(選用)* |管道分隔有效 hello 參數的值的清單。 hello hello 值型別必須 hello 參數 toomatch hello 定義型別。 範例：`english |
| **d:Nullable** *(選用)* |允許定義參數是否可為 null。 hello 預設值是:，則為 true。 不過，會公開為 hello URI 範本中的 hello 路徑之一部份的參數不可為 null。 當 hello 屬性設定為這些參數 – toofalse hello 使用者輸入會被覆寫。 **範例：** `<Parameter Name="BikeType" Type="String" Mode="In" Nullable="false"/>` |
| **d:SampleValue** *(選用)* |Hello UI 中的附註 toohello 用戶端為範例值 toodisplay。  很可能 tooadd 數個值利用垂直線分隔清單，也就是 ' |

## <a name="entitytype-node"></a>EntityType 節點
這個節點代表 hello Marketplace toohello 終端使用者從傳回的型別之一。 它也包含從 hello 輸出傳回 toohello 使用者的 hello 內容提供者的服務 toohello 值所傳回的 hello 對應。

此節點之詳細資料會在找到[這裡](http://msdn.microsoft.com/library/bb399206.aspx)(使用 hello**其他版本**下拉式 tooselect 如果必要 tooview hello 文件的不同版本。)

| 屬性名稱 | 必要 | 值 |
| --- | --- | --- |
| 名稱 |是 |hello hello 實體型別名稱。 **範例：** `<EntityType Name="ListOfAllEntities" d:Map="//EntityModel">` |
| BaseType |否 |hello 是 hello hello 所定義的實體類型的基底類型的另一個實體類型的名稱。 **範例：** `<EntityType Name="PhoneRecord" BaseType="dqs:RequestRecord">` |

hello 下面是已加入 toohello CSDL 規格的 hello 屬性：

**d:Map** -針對 hello 服務輸出執行 XPath 運算式。 hello 此處的假設是 hello 服務輸出將包含一組重複的項目，例如 ATOM 摘要是一組重複的項目節點。 其中每一個重複節點都包含一筆記錄。 指定在 hello 個別中重複節點 hello 內容提供者的服務結果 toopoint 保存 hello 個別記錄值則 hello XPath。 範例輸出 hello 服務：

        `<foo>
          <bar> … content … </bar>
          <bar> … content … </bar>
          <bar> … content … </bar>
        </foo>`

會 /foo/bar hello XPath 運算式，因為每個 hello 列節點為 hello 重複輸出中 hello 節點和它包含 hello toohello 使用者傳回的實際內容。

**Key** - Marketplace 會忽略此屬性。 REST 型 Web 服務通常不會公開主要金鑰。

## <a name="property-node"></a>屬性節點
這個節點包含一個 hello 記錄屬性。

此節點之詳細資料會在找到[http://msdn.microsoft.com/library/bb399546.aspx](http://msdn.microsoft.com/library/bb399546.aspx) (使用 hello**其他版本**下拉式 tooselect 如果必要 tooview hello 文件的不同版本。)*範例：* `<EntityType Name="MetaDataEntityType" d:Map="/MyXMLPath">
        <Property Name="Name"     Type="String" Nullable="true" d:Map="./Service/Name" d:IsPrimaryKey="true" DefaultValue=”Joe Doh” MaxLength="25" FixedLength="true" />
        ...
        </EntityType>`

| AttributeName | 必要 | 值 |
| --- | --- | --- |
| 名稱 |是 |hello hello 屬性名稱。 |
| 類型 |是 |hello hello 屬性值類型。 hello 屬性值類型必須是**EDMSimpleType**或複雜類型 （以完整限定的名稱） 的 hello 模型的範圍內。 如需詳細資訊，請參閱概念模型類型 (CSDL)。 |
| Nullable |否 |**True** (hello 預設值) 或**False**根據 hello 屬性是否可以有 null 值。 注意： 在 hello 的 CSDL 版本以 hello [http://schemas.microsoft.com/ado/2006/04/edm](http://schemas.microsoft.com/ado/2006/04/edm)命名空間，複雜類型屬性必須有可為 Null ="False"。 |
| DefaultValue |否 |hello hello 屬性的預設值。 |
| MaxLength |否 |hello hello 屬性值的最大長度。 |
| FixedLength |否 |**True**或**False**根據 hello 屬性值是否會儲存為 fiexed 長度字串。 |
| Precision |否 |是指 toohello hello 數值的數字 tooretain 數目上限。 |
| 調整 |否 |小數位數 tooretain hello 數值的最大數目。 |
| Unicode |否 |**True**或**False**根據 hello 屬性值是否會儲存為 Unicode 字串。 |
| Collation |否 |字串，指定定序順序 toobe 用 hello 資料來源中的 hello。 |
| ConcurrencyMode |否 |**無**(hello 預設值) 或**固定**。 如果設定太 hello 值**固定**，hello 屬性值將會使用開放式並行存取檢查。 |

hello 下面是已加入 toohello CSDL 規格的 hello 額外屬性：

**d:Map** -針對 hello 服務執行的 XPath 運算式輸出，並擷取 hello 輸出的一個屬性。 指定 XPath hello 是相對 toohello 重複 hello EntityType 節點的 XPath 中已選取的節點。 它也是靜態的資源包括在每個 hello 絕對 XPath tooallow 輸出節點，例如著作權陳述式中 hello 原始服務輸出，但應該會出現在每個 hello hello OData 中的資料列之後僅找到類似的可能 toospecify輸出。 從 hello 服務的範例：

        `<foo>
          <bar>
           <baz0>… value …</baz0>
           <baz1>… value …</baz1>
           <baz2>… value …</baz2>
          </bar>
        </foo>`

hello XPath 運算式將./bar/baz0 tooget hello baz0 節點從 hello 內容提供者的服務。

**d:CharMaxLength** -字串類型，您可以指定 hello 最大長度。 請參閱 DataService CSDL 範例

**d:IsPrimaryKey** -指出 hello 資料行是否為 hello hello 資料表/檢視表中的主索引鍵。 請參閱 DataService CSDL 範例。

**d:isExposed** -決定是否公開 hello 資料表結構描述 (通常是 true)。 請參閱 DataService CSDL 範例

**d:IsView** *(選用)* - 如果這是根據檢視，而不是資料表，則為 true。  請參閱 DataService CSDL 範例

**d:Tableschema** - 請參閱 DataService CSDL 範例

**d:ColumnName** -hello hello 資料表/檢視表中的 hello 資料行名稱。  請參閱 DataService CSDL 範例

**d:IsReturned** -為 hello 布林值，決定是否 hello 服務公開 （expose） 此值 toohello 用戶端。  請參閱 DataService CSDL 範例

**d:IsQueryable** -為 hello 決定 hello 資料行是否可以使用中資料庫查詢的布林值。   請參閱 DataService CSDL 範例

**d:OrdinalPosition** -hello 資料行的數值位置的外觀，x、 hello 表格或 hello 檢視，其中 x 是從 1 toohello hello 資料表中資料行數目。  請參閱 DataService CSDL 範例

**d:DatabaseDataType** -hello hello 資料庫，也就是 SQL 資料類型中的 hello 資料行的資料類型。 請參閱 DataService CSDL 範例

## <a name="supported-parametersproperty-types"></a>支援的參數/屬性類型
hello 下面是支援的 hello 型別參數和屬性。 (區分大小寫)

| 基本類型 | 說明 |
| --- | --- |
| Null |代表 hello 不存在的值 |
| Boolean |代表二進位值邏輯的 hello 數學概念 |
| 位元組 |不帶正負號的 8 位元整數值 |
| DateTime |代表範圍從西元 1753 年 1 月 1 日午夜 12:00:00 到西元 9999 年 12 月 31 日下午 11:59:59 的日期和時間 |
| 十進位 |代表精確度和小數位數固定的數值。 此類型可以描述的數值範圍是從負 10 ^255 + 1 toopositive 10 ^255-1 |
| Double |代表具有 15 位數精確度的浮點數，可以代表近似範圍從 ± 2.23e -308 到 ± 1.79e +308 的值。 **使用小到期 tooExel 匯出問題** |
| 單一 |代表具有 7 位數精確度的浮點數，可以代表近似範圍從 ± 1.18e -38 到 ± 3.40e +38 的值。 |
| Guid |代表 16 位元組 (128 位元) 的唯一識別碼值 |
| Int16 |代表帶正負號的 16 位元整數值 |
| Int32 |代表帶正負號的 32 位元整數值 |
| Int64 |代表帶正負號的 64 位元整數值 |
| String |代表固定或可變長度的字元資料 |

## <a name="see-also"></a>另請參閱
* 如果您有興趣了解 hello 整體 OData 對應程序及目的閱讀此文章[資料服務 OData 對應](marketplace-publishing-data-service-creation-odata-mapping.md)tooreview 定義、 結構和指示。
* 如果您有興趣檢視範例，請閱讀這篇文章[資料服務 OData 對應範例](marketplace-publishing-data-service-creation-odata-mapping-examples.md)toosee 範例程式碼，並了解程式碼語法和內容。
* 規定路徑發行閱讀本文資料服務 toohello Azure Marketplace tooreturn toohello[資料服務的發行指導](marketplace-publishing-data-service-creation.md)。
