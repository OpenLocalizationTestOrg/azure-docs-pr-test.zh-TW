---
title: "aaaData 目錄開發人員概念 |Microsoft 文件"
description: "透過在 Azure 資料目錄概念模型中，介紹 toohello 重要概念 hello 目錄 REST API。"
services: data-catalog
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
tags: 
ms.assetid: 89de9137-a0a4-40d1-9f8d-625acad31619
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: d0b1628ff6c31458cb650efef852244f0c139b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-developer-concepts"></a>Azure 資料目錄開發人員概念
Microsoft **Azure 資料目錄** 是全面管理的雲端服務，能夠進行資料來源探索，以及讓群眾外包資料來源中繼資料。 開發人員可以使用透過其 REST Api 的 hello 服務。 了解 hello 概念 hello 服務中實作是很重要的開發人員 toosuccessfully 整合**Azure 資料目錄**。

## <a name="key-concepts"></a>重要概念
hello **Azure 資料目錄**概念模型根據四個重要概念： hello**目錄**，**使用者**，**資產**，和**註解**。

![概念][1]

*圖 1 - Azure 資料目錄簡易概念模型*

### <a name="catalog"></a>目錄
A**目錄**是 hello 最上層容器的所有 hello 組織所儲存的中繼資料。 每個 Azure 帳戶只能一個 **目錄** 。 類別目錄會繫結的 tooan Azure 訂用帳戶，但只有一個**目錄**可由任何給定的 Azure 帳戶，即使帳戶可以有多個訂用帳戶。

目錄包含**使用者**和**資產**。

### <a name="users"></a>使用者
使用者是有權限 tooperform 動作的安全性主體 （搜尋 hello 類別目錄、 新增、 編輯或移除項目等） hello 目錄中。

一個使用者可能扮演多個不同的角色。 在角色上的資訊，請參閱 hello 區段角色和授權。

可加入個別的使用者和安全性群組。

Azure 資料目錄使用 Azure Active Directory 來管理身分識別和存取權。 每個類別目錄的使用者必須是 hello Active Directory hello 帳戶的成員。

### <a name="assets"></a>Assets
**目錄** 包含資料資產。 **資產**是 hello 單位受 hello 類別目錄的資料粒度。

hello 資料粒度的資產會因資料來源。 對於 SQL Server 或 Oracle 資料庫，資產可以是資料表或檢視。 對於 SQL Server Analysis Services，資產可以是量值、維度或關鍵效能指標 (KPI)。 對於 SQL Server Reporting Services，資產是報表。

**資產**hello 事您新增或移除從類別目錄。 它是您從取回的結果的 hello 單位**搜尋**。

**資產** 由其名稱、位置和類型，以及進一步描述它的註解所組成。

### <a name="annotations"></a>註解
註解是代表資產中繼資料的項目。

註解的範例為描述、標籤、結構描述、文件等等。Hello 資產型別和註解類型的完整清單位於 hello Asset 物件模型區段。

## <a name="crowdsourcing-annotations-and-user-perspective-multiplicity-of-opinion"></a>群眾外包註解和使用者觀點 (多樣性意見)
Azure 資料目錄的重要層面是其支援的中繼資料的 hello crowdsourcing hello 系統中。 相對於的 tooa wiki 方法 – 其中只會有一個意見和 hello 最後寫入者獲勝，hello Azure 資料目錄模型可讓多個意見 toolive hello 系統中的並排顯示。

這個方法反映 hello 真實世界的企業資料的位置不同的使用者可以有不同的檢視方塊指定之資產：

* 資料庫管理員可能會提供大量 ETL 作業的服務等級合約或 hello 可用的處理 視窗的相關資訊
* 資料管理人都可提供適用於 hello 商務程序 toowhich hello 資產的相關資訊，或 hello 商務的 hello 分類已套用 tooit
* 財務分析師可能會提供結束期間的報告工作期間使用 hello 資料的相關資訊

toosupport 此範例中，– hello DBA、 hello 資料服務員和 hello 分析師 – 每個使用者可以加入描述 tooa 單一資料表 hello 目錄中已註冊。 所有描述會都維護 hello 系統中，而且在 hello Azure 資料目錄入口網站會顯示所有說明。

此模式是套用的 toomost hello 中的項目 hello 物件模型，因此 hello JSON 承載中的物件類型通常是屬性的陣列，您預期有單一值。

例如下 hello 資產, 根是描述物件的陣列。 hello 陣列屬性是名為 「 描述 」。 描述物件有一個屬性，也就是描述。 hello 模式是每個型別描述取得描述物件的使用者建立 hello hello 使用者所提供的值。

hello UX 就可以選擇如何 toodisplay hello 組合。 有三種不同的顯示模式。

* hello 最簡單的模式是 [全部顯示]。 在此模式中，所有 hello 物件會都顯示在清單檢視中。 hello Azure 資料目錄入口網站 UX 使用此模式的描述。
* 另一種模式是「合併」。 在這種模式的 hello 不同使用者的所有 hello 值會都合併在一起，以移除重複項目。 在 hello Azure 資料目錄入口網站 UX 此模式的範例包括 hello 標記和專家屬性。
* 第三種模式為「最後寫入者為準」。 在此模式中，只有 hello 最新輸入的顯示值。 friendlyName 是這種模式的一個例子。

## <a name="asset-object-model"></a>資產物件模型
Hello 重要概念 > 一節中引入，hello **Azure 資料目錄**物件模型包括項目，這可以是資產或註解。 項目具有選用或必要的屬性。 某些屬性會套用 tooall 項目。 某些屬性會套用 tooall 資產。 某些屬性會套用 toospecific 資產類型。

### <a name="system-properties"></a>系統屬性
<table><tr><td><b>屬性名稱</b></td><td><b>資料類型</b></td><td><b>註解</b></td></tr><tr><td>timestamp</td><td>DateTime</td><td>hello 最後一個時間 hello 項目已修改。 這個欄位是 hello 伺服器所產生，在插入項目和每次更新項目。 hello 這個屬性的值會被忽略的輸入上的發行作業。</td></tr><tr><td>id</td><td>Uri</td><td>Hello 項目 （唯讀） 的絕對 url。 它是 hello hello 項目的唯一可定址 URI。  hello 這個屬性的值會被忽略的輸入上的發行作業。</td></tr><tr><td>類型</td><td>String</td><td>hello hello 資產 （唯讀） 類型。</td></tr><tr><td>etag</td><td>String</td><td>字串對應 toohello 版本時執行作業之更新 hello 目錄中的項目可以用於開放式並行存取控制的 hello 項目。 "*"可以是使用的 toomatch 任何值。</td></tr></table>

### <a name="common-properties"></a>通用屬性
這些屬性會套用 tooall 根資產型別及所有的註解型別。

<table>
<tr><td><b>屬性名稱</b></td><td><b>資料類型</b></td><td><b>註解</b></td></tr>
<tr><td>fromSourceSystem</td><td>Boolean</td><td>表示項目的資料是衍生自來源系統 (例如 SQL Server Database、Oracle Database) 或由使用者所撰寫。</td></tr>
</table>

### <a name="common-root-properties"></a>通用根屬性
<p>
這些屬性會套用 tooall 根資產型別。

<table><tr><td><b>屬性名稱</b></td><td><b>資料類型</b></td><td><b>註解</b></td></tr><tr><td>名稱</td><td>String</td><td>名稱，衍生自 hello 資料來源位置資訊</td></tr><tr><td>dsl</td><td>DataSourceLocation</td><td>可唯一描述 hello 資料來源，而且是其中一個的 hello hello 資產識別碼。 (請參閱＜雙重識別＞一節)。  hello 結構的 hello dsl 因 hello 通訊協定和來源類型。</td></tr><tr><td>dataSource</td><td>DataSourceInfo</td><td>Hello 的資產類型的詳細資料。</td></tr><tr><td>lastRegisteredBy</td><td>SecurityPrincipal</td><td>描述 hello 最近已登錄使用者這項資產。  包含 hello hello 使用者 (hello upn) 的唯一識別碼和顯示名稱 （lastName 和 firstName）。</td></tr><tr><td>containerId</td><td>String</td><td>Hello 容器資產 hello 資料來源的識別碼。 Hello 容器型別不支援這個屬性。</td></tr></table>

### <a name="common-non-singleton-annotation-properties"></a>一般的非單一註解屬性
這些屬性會套用 tooall 非單一註解類型 (允許 toobe 註解每個資產的多個)。

<table>
<tr><td><b>屬性名稱</b></td><td><b>資料類型</b></td><td><b>註解</b></td></tr>
<tr><td>key</td><td>String</td><td>使用者指定之索引鍵可唯一識別在 hello 目前集合中的 hello 註解。 hello 金鑰長度不能超過 256 個字元。</td></tr>
</table>

### <a name="root-asset-types"></a>根資產類型
根資產類型都是這些型別代表 hello 各種類型的資料可以在 hello 目錄中註冊的資產。 對於每個根型別中，沒有檢視，其中描述資產和 hello 檢視中包含的附註。 發行資產使用 REST API 時，檢視表名稱應使用在 hello 對應 {view_name} url 區段中。

<table><tr><td><b>資產類型 (檢視名稱)</b></td><td><b>其他屬性</b></td><td><b>資料類型</b></td><td><b>允許的註解</b></td><td><b>註解</b></td></tr><tr><td>資料表 ("tables")</td><td></td><td></td><td>說明<p>FriendlyName<p>Tag<p>結構描述<p>ColumnDescription<p>ColumnTag<p> 專家<p>預覽<p>AccessInstruction<p>TableDataProfile<p>ColumnDataProfile<p>ColumnDataClassification<p>文件<p></td><td>資料表代表任何表格式資料。  例如：SQL 資料表、SQL 檢視、Analysis Services 表格式資料表、Analysis Services 多維度的維度、Oracle 資料表等等。   </td></tr><tr><td>量值 ("measures")</td><td></td><td></td><td>說明<p>FriendlyName<p>Tag<p>專家<p>AccessInstruction<p>文件<p></td><td>此類型代表 Analysis Services 量值。</td></tr><tr><td></td><td>measure</td><td>資料欄</td><td></td><td>中繼資料描述 hello 量值</td></tr><tr><td></td><td>isCalculated </td><td>Boolean</td><td></td><td>指定是否 hello 量值或未計算。</td></tr><tr><td></td><td>measureGroup</td><td>String</td><td></td><td>量值的實體容器</td></tr><td>KPI ("kpis")</td><td></td><td></td><td>說明<p>FriendlyName<p>Tag<p>專家<p>AccessInstruction<p>文件</td><td></td></tr><tr><td></td><td>measureGroup</td><td>String</td><td></td><td>量值的實體容器</td></tr><tr><td></td><td>goalExpression</td><td>String</td><td></td><td>MDX 數值運算式或傳回 hello hello KPI 目標值的計算。</td></tr><tr><td></td><td>valueExpression</td><td>String</td><td></td><td>傳回 hello KPI hello 實際值的 MDX 數值運算式。</td></tr><tr><td></td><td>statusExpression</td><td>String</td><td></td><td>表示時間的指定點的 hello KPI hello 狀態 MDX 運算式。</td></tr><tr><td></td><td>trendExpression</td><td>String</td><td></td><td>評估一段時間的 hello hello KPI 值的 MDX 運算式。 hello 趨勢可以是任何以時間為基礎的準則，可用於特定商務內容。</td>
<tr><td>報表 ("reports")</td><td></td><td></td><td>說明<p>FriendlyName<p>Tag<p>專家<p>AccessInstruction<p>文件<p></td><td>此類型代表 SQL Server Reporting Services 報表 </td></tr><tr><td></td><td>assetCreatedDate</td><td>String</td><td></td><td></td></tr><tr><td></td><td>assetCreatedBy</td><td>String</td><td></td><td></td></tr><tr><td></td><td>assetModifiedDate</td><td>String</td><td></td><td></td></tr><tr><td></td><td>assetModifiedBy</td><td>String</td><td></td><td></td></tr><tr><td>容器 ("containers")</td><td></td><td></td><td>說明<p>FriendlyName<p>Tag<p>專家<p>AccessInstruction<p>文件<p></td><td>此類型代表其他資產 (例如 SQL database、Azure Blob 容器或 Analysis Services 模型) 的容器 。</td></tr></table>

### <a name="annotation-types"></a>註解類型
註解型別代表類型的中繼資料可指派 tooother hello 目錄中的型別。

<table>
<tr><td><b>註解類型 (巢狀檢視名稱)</b></td><td><b>其他屬性</b></td><td><b>資料類型</b></td><td><b>註解</b></td></tr>

<tr><td>描述 ("descriptions")</td><td></td><td></td><td>此屬性包含資產的描述。 Hello 系統的每個使用者可以新增自己的描述。  只有該使用者可以編輯 hello 描述物件。  （系統管理員和資產擁有者可以刪除 hello 描述物件，但無法再進行編輯）。 hello 系統會分別維護使用者的描述。  因此是陣列的每個資產 （一個用於每個使用者具有提問加法 toopossibly 包含資訊的其中一個衍生自 hello 資料來源中的 hello 資產的相關知識） 上的描述。</td></tr>
<tr><td></td><td>說明</td><td>字串</td><td>Hello 資產的簡短描述 （2-3 行）</td></tr>

<tr><td>標籤 ("tags")</td><td></td><td></td><td>這個屬性會定義資產的標籤。 Hello 系統的每個使用者可以加入多個資產標記。  標記物件的建立者 hello 使用者可以編輯它們。  （系統管理員和資產擁有者可以刪除 hello 標記物件，但無法再進行編輯）。 hello 系統會分別維護使用者的標記。  因此每個資產上都會有 Tag 物件的陣列。</td></tr>
<tr><td></td><td>tag</td><td>字串</td><td>標記描述 hello 資產。</td></tr>

<tr><td>FriendlyName ("friendlyName")</td><td></td><td></td><td>此屬性包含資產的易記名稱。 FriendlyName 單一註解-只有一個 FriendlyName 可以加入 tooan 資產。  建立連 FriendlyName 物件 hello 使用者可以編輯它。 （系統管理員和資產擁有者可以刪除 hello FriendlyName 物件，但無法再進行編輯）。 hello 系統會分別維護使用者的易記名稱。</td></tr>
<tr><td></td><td>friendlyName</td><td>字串</td><td>Hello 資產的好記的名稱。</td></tr>

<tr><td>結構描述 ("schema")</td><td></td><td></td><td>hello 結構描述會描述 hello hello 資料結構。  它會列出 hello （資料行、 屬性、 欄位等） 的屬性名稱、 類型以及其他中繼資料。  所有衍生自 hello 資料來源這項資訊。  Schema 是單一註解 - 資產只能新增一個 Schema。</td></tr>
<tr><td></td><td>columns</td><td>Column[]</td><td>資料行物件的陣列。 它們衍生自 hello 資料來源的資訊描述 hello 資料行。</td></tr>

<tr><td>ColumnDescription ("columnDescriptions")</td><td></td><td></td><td>此屬性包含資料行的描述。  Hello 系統的每個使用者可以加入自己的多個資料行 （最多每一個資料行） 的說明。 ColumnDescription 物件的建立者 hello 使用者可以編輯它們。  （系統管理員和資產擁有者可以刪除 hello ColumnDescription 物件，但無法再進行編輯）。 hello 系統會分別維護這些使用者的資料行描述。  因此會在每個資產上 ColumnDescription 物件的陣列 （其中每個資料行的每位使用者都有貢獻 hello 資料行的相關知識此外 toopossibly 包含資訊的其中一個衍生自 hello 資料來源）。  hello ColumnDescription 是鬆散結合的 toohello 結構描述，因此它可取得不同步。hello ColumnDescription 可能會描述不存在於 hello 結構描述中的資料行。  它是最多 toohello 寫入器 tookeep 描述和結構描述的同步。 hello 資料來源可能也會有資料行描述資訊以及執行 hello 工具時建立的其他 ColumnDescription 物件。</td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>hello hello 這項描述是指的資料行名稱。</td></tr>
<tr><td></td><td>說明</td><td>String</td><td>簡短描述 （2-3 行） 的 hello 資料行。</td></tr>

<tr><td>ColumnTag ("columnTags")</td><td></td><td></td><td>此屬性包含資料行的標籤。 Hello 系統的每個使用者可以新增特定資料行的多個標記，而且可以加入多個資料行的標記。 ColumnTag 物件的建立者 hello 使用者可以編輯它們。 （系統管理員和資產擁有者可以刪除 hello ColumnTag 物件，但無法再進行編輯）。 hello 系統會分別維護這些使用者的資料行標籤。  因此每個資產上都會有 ColumnTag 物件的陣列。  hello ColumnTag 是鬆散結合的 toohello 結構描述，因此可以取得不同步。hello ColumnTag 可能會描述不存在於 hello 結構描述中的資料行。  它是最多 toohello 寫入器 tookeep 資料行標籤和同步的結構描述。</td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>hello hello 此標記是指的資料行名稱。</td></tr>
<tr><td></td><td>tag</td><td>String</td><td>標記描述 hello 資料行。</td></tr>

<tr><td>專家 ("experts")</td><td></td><td></td><td>此屬性包含的使用者會被視為 hello 資料集中的專家。 hello 專家 opinions(descriptions) 泡泡 toohello 的頂端 hello UX 列出說明時。 每個使用者可以指定自己的專家。 只有該使用者可以編輯 hello 專家物件。 （系統管理員和資產擁有者可以刪除 hello 專家物件，但無法再進行編輯）。</td></tr>
<tr><td></td><td>expert</td><td>SecurityPrincipal</td><td></td></tr>

<tr><td>預覽 ("previews")</td><td></td><td></td><td>hello 預覽包含 hello 前 20 個資料列之資料的 hello 資產的快照集。 預覽只對某些資產類型才有意義 (對資料表有意義，但對量值沒有意義)。</td></tr>
<tr><td></td><td>preview</td><td>object[]</td><td>代表資料行的物件陣列。  每個物件具有對應 tooa hello 資料列的資料行的值資料行的屬性。</td></tr>

<tr><td>AccessInstruction ("accessInstructions")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>mimeType</td><td>字串</td><td>hello hello 內容的 mime 類型。</td></tr>
<tr><td></td><td>內容</td><td>字串</td><td>hello tooget toothis 資料資產的存取方式的指示。 hello 內容可能是 URL、 電子郵件地址或一組的指示。</td></tr>

<tr><td>TableDataProfile ("tableDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>numberOfRows</td></td><td>int</td><td>hello 資料集中的資料列的 hello 數目</td></tr>
<tr><td></td><td>size</td><td>long</td><td>hello 大小，以位元組為單位的 hello 資料集。  </td></tr>
<tr><td></td><td>schemaModifiedTime</td><td>字串</td><td>已修改 hello 最後一個階段 hello 結構描述</td></tr>
<tr><td></td><td>dataModifiedTime</td><td>字串</td><td>已修改 hello 最後一個時間 hello 資料集 （資料已加入、 修改或刪除）</td></tr>

<tr><td>ColumnsDataProfile ("columnsDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columns</td></td><td>ColumnDataProfile[]</td><td>資料行資料設定檔的陣列。</td></tr>

<tr><td>ColumnDataClassification ("columnDataClassifications")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>hello hello 這個分類是指的資料行名稱。</td></tr>
<tr><td></td><td>分類</td><td>String</td><td>此資料行中的 hello 資料 hello 分類。</td></tr>

<tr><td>文件 ("documentation")</td><td></td><td></td><td>指定的資產只能有一個相關聯的文件。</td></tr>
<tr><td></td><td>mimeType</td><td>字串</td><td>hello hello 內容的 mime 類型。</td></tr>
<tr><td></td><td>內容</td><td>字串</td><td>hello 文件內容。</td></tr>

</table>

### <a name="common-types"></a>常見的類型
一般類型可用來當作 hello 類型的屬性，但不是項目。

<table>
<tr><td><b>一般類型</b></td><td><b>屬性</b></td><td><b>資料類型</b></td><td><b>註解</b></td></tr>
<tr><td>DataSourceInfo</td><td></td><td></td><td></td></tr>
<tr><td></td><td>sourceType</td><td>字串</td><td>描述 hello 類型的資料來源。  例如︰SQL Server、Oracle 資料庫等。  </td></tr>
<tr><td></td><td>objectType</td><td>字串</td><td>描述 hello hello 資料來源中的物件類型。 例如：SQL Server 的資料表、檢視。</td></tr>

<tr><td>DataSourceLocation</td><td></td><td></td><td></td></tr>
<tr><td></td><td>protocol</td><td>string</td><td>必要。 描述與 hello 資料來源使用通訊協定 toocommunicate。 例如：適用於 SQl Server 的 "tds"、適用於 Oracle 的 "oracle" 等等。請參閱太[資料來源參考規格-DSL 結構](data-catalog-dsr.md)hello 目前支援的通訊協定的清單。</td></tr>
<tr><td></td><td>位址</td><td>字典<string, object></td><td>必要。 位址是一組是使用的 tooidentify hello 資料來源所參考的資料特定 toohello 通訊協定。 hello 位址資料範圍 tooa 特定通訊協定，也就是說，它不需要知道 hello 通訊協定無意義。</td></tr>
<tr><td></td><td>驗證</td><td>string</td><td>選用。 hello 驗證配置用於 toocommunicate hello 資料來源。 例如：windows、oauth 等等。</td></tr>
<tr><td></td><td>connectionProperties</td><td>字典<string, object></td><td>選用。 其他資訊 tooconnect tooa 資料來源。</td></tr>

<tr><td>SecurityPrincipal</td><td></td><td></td><td>hello 後端不會執行任何驗證的 AAD 針對提供的屬性在發行期間。</td></tr>
<tr><td></td><td>upn</td><td>string</td><td>使用者的唯一電子郵件地址。 如果未提供 objectId 或 「 lastRegisteredBy"屬性，否則為選擇性的 hello 內容中，必須指定。</td></tr>
<tr><td></td><td>objectId</td><td>Guid</td><td>使用者或安全性群組 AAD 身分識別。 選用。 如果未提供 upn 則必須指定，否則為選擇性。</td></tr>
<tr><td></td><td>firstName</td><td>string</td><td>使用者的名字 (用於顯示)。 選用。 Hello"lastRegisteredBy"屬性內容中才有效。 在為 "roles"、"permissions" 和 "experts" 提供安全性主體時則不能指定。</td></tr>
<tr><td></td><td>lastName</td><td>string</td><td>使用者的姓氏 (用於顯示)。 選用。 Hello"lastRegisteredBy"屬性內容中才有效。 在為 "roles"、"permissions" 和 "experts" 提供安全性主體時則不能指定。</td></tr>

<tr><td>資料欄</td><td></td><td></td><td></td></tr>
<tr><td></td><td>名稱</td><td>字串</td><td>Hello 資料行或屬性的名稱。</td></tr>
<tr><td></td><td>類型</td><td>字串</td><td>hello 資料行或屬性的資料類型。 hello 可允許的類型取決於資料 sourceType 的 hello 資產。  僅支援一部分類型。</td></tr>
<tr><td></td><td>maxLength</td><td>int</td><td>hello hello 資料行或屬性所允許的長度上限。 衍生自資料來源。 只適用於 toosome 來源類型。</td></tr>
<tr><td></td><td>precision</td><td>byte</td><td>hello 資料行或屬性的 hello 有效位數。 衍生自資料來源。 只適用於 toosome 來源類型。</td></tr>
<tr><td></td><td>isNullable</td><td>Boolean</td><td>Hello 資料行是否允許 toohave null 值。 衍生自資料來源。 只適用於 toosome 來源類型。</td></tr>
<tr><td></td><td>expression</td><td>字串</td><td>如果 hello 值是導出資料行，此欄位會包含 hello 值的 hello 運算式。 衍生自資料來源。 只適用於 toosome 來源類型。</td></tr>

<tr><td>ColumnDataProfile</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName </td><td>字串</td><td>hello hello 資料行名稱</td></tr>
<tr><td></td><td>類型 </td><td>字串</td><td>hello hello 資料行類型</td></tr>
<tr><td></td><td>Min </td><td>字串</td><td>hello hello 資料集中的最小值</td></tr>
<tr><td></td><td>max </td><td>字串</td><td>hello hello 資料集中的最大值</td></tr>
<tr><td></td><td>avg </td><td>double</td><td>hello 資料集中的 hello 平均值</td></tr>
<tr><td></td><td>stdev </td><td>double</td><td>hello hello 資料集的標準差</td></tr>
<tr><td></td><td>nullCount </td><td>int</td><td>hello hello 資料集中的 null 值計數</td></tr>
<tr><td></td><td>distinctCount  </td><td>int</td><td>hello hello 資料集中的相異值計數</td></tr>


</table>

## <a name="asset-identity"></a>資產身分識別
Azure 資料目錄使用 「 通訊協定 」，並從 hello DataSourceLocation"dsl"屬性 toogenerate 身分識別的 hello 資產，也就是使用的 tooaddress hello"address"屬性包的識別屬性 hello hello 目錄內的資產。
例如，hello"tds 」 通訊協定具有識別屬性 「 伺服器 」，「 資料庫 」、 「 結構描述 」 和 「 物件 」。 hello 通訊協定和 hello 識別屬性的 hello 組合都使用的 toogenerate hello 身分識別的 hello SQL Server 資料表資產。
Azure 資料目錄提供數個內建資料來源通訊協定，列在 [資料來源參考規格 - DSL 結構](data-catalog-dsr.md)中。
hello 一組支援的通訊協定可以擴充以程式設計方式 （請參閱 tooData 目錄 REST API 參考）。 Hello 類別目錄的系統管理員可以註冊自訂資料來源通訊協定。 hello 以下表格說明 hello 所需的內容 tooregister 自訂通訊協定。

### <a name="custom-data-source-protocol-specification"></a>自訂資料來源通訊協定規格
<table>
<tr><td><b>類型</b></td><td><b>屬性</b></td><td><b>資料類型</b></td><td><b>註解</b></td></tr>

<tr><td>DataSourceProtocol</td><td></td><td></td><td></td></tr>
<tr><td></td><td>namespace</td><td>字串</td><td>hello 通訊協定的 hello 命名空間。 命名空間必須是從 1 too255 字元，包含以點 （.） 分隔的一個或多個非空白部分。 每個部分必須是從 1 too255 字元、 以字母開頭並只能包含字母和數字。</td></tr>
<tr><td></td><td>名稱</td><td>字串</td><td>hello hello 通訊協定名稱。 名稱必須從 1 too255 個字元、 以字母開頭且只能包含字母、 數字與 hello 虛線 （-） 字元。</td></tr>
<tr><td></td><td>identityProperties</td><td>DataSourceProtocolIdentityProperty[]</td><td>身分識別屬性清單必須包含至少一個，但不超過 20 個屬性。 例如: 「 伺服器 」、 「 資料庫 」、 「 結構描述 」、 「 物件 」 是 hello"tds 」 通訊協定的識別內容。</td></tr>
<tr><td></td><td>identitySets</td><td>DataSourceProtocolIdentitySet[]</td><td>身分識別集合的清單。 定義代表有效資產身分識別的身分識別屬性集合。 必須包含至少一個，但不超過 20 個集合。 例如：{「伺服器」、「資料庫」、「結構描述」和「物件」} 是 "tds" 通訊協定的身分識別集合，它會定義 Sql Server 資料表資產的身分識別。</td></tr>

<tr><td>DataSourceProtocolIdentityProperty</td><td></td><td></td><td></td></tr>
<tr><td></td><td>名稱</td><td>字串</td><td>hello hello 屬性名稱。 名稱必須介於 1 too100 字元之字母開頭，且只能包含字母和數字。</td></tr>
<tr><td></td><td>類型</td><td>字串</td><td>hello hello 屬性類型。 支援的值："bool"、"boolean"、"byte"、"guid"、"int"、"integer"、"long"、"string"、"url"</td></tr>
<tr><td></td><td>ignoreCase</td><td>布林</td><td>表示使用屬性的值時，是否應忽略大小寫。 只能對具有 "string" 類型的屬性指定。 預設值為 false。</td></tr>
<tr><td></td><td>urlPathSegmentsIgnoreCase</td><td>bool[]</td><td>指出是否應該忽略 hello url 路徑的每個區段的大小寫。 只能對具有 "url" 類型的屬性指定。 預設值為 [false]。</td></tr>

<tr><td>DataSourceProtocolIdentitySet</td><td></td><td></td><td></td></tr>
<tr><td></td><td>名稱</td><td>字串</td><td>hello hello 識別集名稱。</td></tr>
<tr><td></td><td>屬性</td><td>string[]</td><td>hello 的併入這個身分識別的身分識別屬性集清單。 它不能包含重複項目。 Hello"identityProperties"hello 通訊協定清單中，必須定義識別集所參考的每一個屬性。</td></tr>

</table>

## <a name="roles-and-authorization"></a>角色和授權
Microsoft Azure 資料目錄對資產和註解的 CRUD 作業提供授權功能。

## <a name="key-concepts"></a>重要概念
hello Azure 資料目錄會使用兩種授權機制：

* 以角色為基礎的授權
* 以權限為基礎的授權

### <a name="roles"></a>角色
有 3 個角色：**系統管理員**、**擁有者**和**參與者**。  每個角色都有其範圍和權限，在 hello 下表將摘要說明。

<table><tr><td><b>角色</b></td><td><b>範圍</b></td><td><b>權限</b></td></tr><tr><td>系統管理員</td><td>類別目錄 （資產/中所有註解 hello 目錄）</td><td>Read Delete ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>擁有者</td><td>每個資產 (根項目)</td><td>Read Delete ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>參與者</td><td>每個個別的資產和註解</td><td>讀取更新刪除 ViewRoles 附註： hello 著作權所有，並會撤銷如果 hello 權限讀取 hello 項目撤銷 hello 參與者</td></tr></table>

> [!NOTE]
> **讀取**，**更新**，**刪除**， **ViewRoles**權限，也適用 tooany 項目 （資產或註解） 時**: 0-請求**， **ChangeOwnership**， **ChangeVisibility**， **ViewPermissions**都適用 toohello 根資產。
> 
> **刪除**tooan 項目，以及任何子項目和其下的單一項目，適用於權限。 例如，刪除資產時，也會刪除該資產的任何註解。
> 
> 

### <a name="permissions"></a>權限
權限是存取控制項目的清單。 每個存取控制項目指派權限 tooa 安全性主體。 權限只能指定資產 （也就是根項目），並套用 toohello 資產和任何子項目。

Hello 期間**Azure 資料目錄**預覽，只**讀取**支援 hello 權限清單 tooenable 案例 toorestrict 可視性資產的權限。

任何已驗證的使用者具有預設**讀取**以滑鼠右鍵 hello 目錄中的任何項目的可見性會限制除非 toohello 組中 hello 權限的主體。

## <a name="rest-api"></a>REST API
**PUT**和**POST**檢視項目會要求使用的 toocontrol 角色和權限可以是： 在加法 tooitem 承載中，您可以指定兩個系統屬性**角色**和**權限**。

> [!NOTE]
> **權限**只適用 tooa 根項目。
> 
> **擁有者**角色僅適用於 tooa 根項目。
> 
> 根據預設，當 hello 目錄中建立項目時其**參與者**設定 toohello 目前已驗證的使用者。 如果項目應該是可更新所有人，**參與者**應該設定太&lt;Everyone&gt;特殊的安全性主體在 hello**角色**屬性項目時第一次發行 （請參閱下列範例 toohello）。 **參與者**無法變更並保持 hello 相同期間的項目存留期間 (即使**管理員**或**擁有者**沒有 hello 右 toochange hello **參與者**)。 hello 的 hello hello 明確設定支援的值**參與者**是&lt;Everyone&gt;:**參與者**只能是使用者建立項目或&lt;Everyone&gt;。
> 
> 

### <a name="examples"></a>範例
**設定得參與者&lt;Everyone&gt;發佈項目時。**
特殊安全性主體 &lt;Everyone&gt; 具有 objectId "00000000-0000-0000-0000-000000000201"。
  **POST** https://api.azuredatacatalog.com/catalogs/default/views/tables/?api-version=2016-03-30

> [!NOTE]
> 某些 HTTP 用戶端實作可能會自動重新發出回應 tooa 302 從 hello 伺服器中的要求，但通常刪除從 hello 要求的授權標頭。 由於 hello 授權標頭是必要的 toomake 要求 tooAzure 資料目錄，您必須確定重新發出指定 Azure 資料目錄的要求 tooa 重新導向位置時，仍然會提供 hello 授權標頭。 hello 下列程式碼範例示範使用 hello.NET HttpWebRequest 物件。
> 
> 

**內文**

    {
        "roles": [
            {
                "role": "Contributor",
                "members": [
                    {
                        "objectId": "00000000-0000-0000-0000-000000000201"
                    }
                ]
            }
        ]
    }

  **派擁有者，並限制現有根項目的可見性**：**PUT** https://api.azuredatacatalog.com/catalogs/default/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30

    {
        "roles": [
            {
                "role": "Owner",
                "members": [
                    {
                        "objectId": "c4159539-846a-45af-bdfb-58efd3772b43",
                        "upn": "user1@contoso.com"
                    },
                    {
                        "objectId": "fdabd95b-7c56-47d6-a6ba-a7c5f264533f",
                        "upn": "user2@contoso.com"
                    }
                ]
            }
        ],
        "permissions": [
            {
                "principal": {
                    "objectId": "27b9a0eb-bb71-4297-9f1f-c462dab7192a",
                    "upn": "user3@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            },
            {
                "principal": {
                    "objectId": "4c8bc8ce-225c-4fcf-b09a-047030baab31",
                    "upn": "user4@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            }
        ]
    }

> [!NOTE]
> PUT 中，您不需要 toospecify hello 主體中的項目裝載： PUT 可以是使用的 tooupdate 只是角色和/或權限。
> 
> 

<!--Image references-->
[1]: ./media/data-catalog-developer-concepts/concept2.png
