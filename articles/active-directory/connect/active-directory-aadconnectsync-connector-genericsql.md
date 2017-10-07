---
title: "aaaGeneric SQL 連接器 |Microsoft 文件"
description: "本文說明如何 tooconfigure Microsoft 泛型 SQL 連接器。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a>一般 SQL 連接器技術參考
本文說明 hello 泛型 SQL 連接器。 hello 文章適用 toohello 下列產品：

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * 必須使用 Hotfix 4.1.3671.0 或更新版本 [KB3092178](https://support.microsoft.com/kb/3092178)。

MIM2016 和 FIM2010R2，hello 連接器可做為從 hello 下載[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495)。

toosee 在動作中，此連接器，請參閱 「 hello[泛型 SQL Connector 逐步](active-directory-aadconnectsync-connector-genericsql-step-by-step.md)發行項。

## <a name="overview-of-hello-generic-sql-connector"></a>Hello 泛型 SQL 連接器的概觀
hello 泛型 SQL 連接器可讓您使用 ODBC 連接的資料庫系統 toointegrate hello 同步處理服務。  

從高階觀點來看，hello hello 連接器目前版本支援下列功能的 hello:

| 功能 | 支援 |
| --- | --- |
| 連接的資料來源 |hello 連接器僅支援所有的 64 位元 ODBC 驅動程式。 經過 hello 下列測試： <li>Microsoft SQL Server 與 SQL Azure</li><li>IBM DB2 10.x</li><li>IBM DB2 9.x</li><li>Oracle 10 和 11 g</li><li>MySQL 5.x</li> |
| 案例 |<li>物件生命週期管理</li><li>密碼管理</li> |
| 作業 |<li>完整匯入和差異匯入、匯出</li><li>針對匯出：新增、刪除、更新和取代</li><li>設定密碼、變更密碼</li> |
| 結構描述 |<li>動態探索物件和屬性</li> |

### <a name="prerequisites"></a>必要條件
使用 hello 連接器之前，請確定您擁有 hello 同步處理伺服器 hello 下列項目：

* Microsoft .NET 4.5.2 Framework 或更新版本
* 64 位元的 ODBC 用戶端驅動程式

### <a name="permissions-in-connected-data-source"></a>連接的資料來源權限
toocreate 或執行任何支援的 hello 工作一般 SQL 連接器中，您必須具有：

* db_datareader
* db_datawriter

### <a name="ports-and-protocols"></a>連接埠和通訊協定
Hello hello ODBC 驅動程式 toowork 所需的連接埠，請參閱 hello 資料庫供應商的文件。

## <a name="create-a-new-connector"></a>建立新的連接器
tooCreate 一般 SQL 連接器，請在**同步處理服務**選取**管理代理程式**和**建立**。 選取 hello**一般 SQL (Microsoft)**連接器。

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a>連線能力
hello 連接器會使用 ODBC DSN 檔案的連線。 建立 hello DSN 檔案使用**ODBC 資料來源**下 hello [開始] 功能表中找到**系統管理工具**。 在 [hello] 系統管理工具，建立**檔案 DSN**讓它可以提供 toohello 連接器。

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

hello 連線能力畫面第一次為 hello，當您建立新的一般 SQL 連接器。 您必須先 tooprovide hello 下列資訊：

* DSN 檔案路徑
* 驗證
  * 使用者名稱
  * 密碼

hello 資料庫應該支援其中一種驗證方法：

* **Windows 驗證**: hello 驗證資料庫使用 hello Windows 認證 tooverify hello 使用者。 hello 使用者名稱/密碼指定為使用的 tooauthenticate 與 hello 資料庫。 此帳戶需要權限 toohello 資料庫。
* **SQL 驗證**： 資料庫使用 hello 使用者名稱/密碼進行驗證的 hello 定義一個 hello 連線能力畫面 tooconnect toohello 資料庫。 如果您儲存使用者名稱/密碼 hello hello DSN 檔案中，hello hello 連線能力畫面上所提供的認證具有優先順序。
* **Azure SQL Database 驗證**： 如需詳細資訊，請參閱[連接 tooSQL 資料庫使用 Azure Active Directory 驗證](../../sql-database/sql-database-aad-authentication.md)。

**DN 是錨點**: hello DN 如果您選取此選項時，也會當做 hello 錨點屬性使用。 它可以使用的簡單實作，但也有下列限制的 hello:

* 連接器只支援一種物件類型。 因此屬性只能參考的任何參考 hello 相同物件類型。

**匯出型別： 物件取代**： 在匯出期間，當只有某些屬性已變更，匯出 hello 整個物件所有屬性，並取代 hello 現有物件。

### <a name="schema-1-detect-object-types"></a>結構描述 1 (偵測物件類型)
這個頁面上，您將 tooconfigure hello 連接器的方式進行 toofind hello hello 資料庫中的不同物件類型。

每個物件類型會顯示為一個資料分割，並且在 [設定資料分割和階層] 上進一步設定。

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

**物件類型的偵測方法**: hello 連接器支援這些物件類型的偵測方法。

* **固定值**： 您提供的物件類型的 hello 清單，以逗號分隔清單。 例如： `User,Group,Department`。  
  ![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)
* **資料表/檢視/預存程序**： 提供 hello hello 資料表/檢視/預存程序名稱，然後 hello 提供 hello 清單的物件類型的資料行名稱。 如果您使用預存程序，然後也提供參數，格式為 hello **[名稱]: [方向]: [Value]**。 提供每個參數，在不同行 （使用 Ctrl + Enter tooget 新行）。  
  ![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)
* **SQL 查詢**： 此選項可讓您 tooprovide SQL 查詢，以傳回物件類型的單一資料行，例如`SELECT [Column Name] FROM TABLENAME`。 hello 傳回資料行必須是字串類型 (varchar)。

### <a name="schema-2-detect-attribute-types"></a>結構描述 2 (偵測屬性類型)
這個頁面上，您將如何 tooconfigure hello 的屬性名稱和型別將 toobe 偵測到。 hello 組態選項會列出每個 hello 前一頁上偵測到的物件類型。

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

**屬性類型的偵測方法**: hello 連接器支援結構描述 1 畫面中的這些屬性類型偵測方法可搭配每個偵測到的物件類型。

* **資料表/檢視/預存程序**： 提供 hello hello 資料表/檢視/預存程序應使用的 toofind hello 屬性名稱的名稱。 如果您使用預存程序，然後也提供參數，格式為 hello **[名稱]: [方向]: [Value]**。 提供每個參數，在不同行 （使用 Ctrl + Enter tooget 新行）。 toodetect hello 屬性名稱中的多重值屬性，提供以逗號分隔清單的資料表或檢視表。 當父和子資料表具有相同的資料行名稱時，則不支援多重值案例。
* **SQL 查詢**： 此選項可讓您 tooprovide SQL 查詢，以傳回屬性名稱的單一資料行，例如`SELECT [Column Name] FROM TABLENAME`。 hello 傳回資料行必須是字串類型 (varchar)。

### <a name="schema-3-define-anchor-and-dn"></a>結構描述 3 (定義錨點和 DN)
此頁面可讓您 tooconfigure 錨點和 DN 屬性每個偵測到的物件類型。 您可以選取多個屬性 toomake hello 錨點唯一。

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* 不會列出多重值和布林值屬性。
* 相同的屬性無法用於 DN 和 錨點，除非**DN 是錨點**hello 連線能力 頁面上選取。
* 如果**DN 是錨點**選取在 hello 連線能力 頁面上，此頁面需要唯一的 hello DN 屬性。 這個屬性也會用為 hello 錨點屬性。

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a>結構描述 4 (定義屬性類型、參考和方向)
此頁面可讓您 tooconfigure hello 屬性類型，例如整數、 二進位或布林值，以及針對每個屬性的方向。 [結構描述 2]  頁面中的所有屬性都會列出，包括多重值屬性。

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* **資料型別**: toomap hello 屬性型別 toothose 類型已知 hello 同步處理引擎所使用。 hello 預設值是相同的型別在 hello SQL 結構描述中，偵測到的 toouse hello 但無法輕易地偵測 DateTime 和參考。 對於，您需要 toospecify **DateTime**或**參考**。
* **方向**: hello 屬性方向 tooImport、 匯出或 ImportExport，您可以設定。 ImportExport 是預設值。

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

注意：

* 如果屬性型別不是偵測到 hello 連接器，它會使用 hello 字串資料類型。
* **巢狀資料表** 視為一個資料行的資料庫資料表。 Oracle 會 hello 巢狀資料表資料列儲存不依特定順序。 不過，當您擷取 hello 巢狀的資料表至 PL/SQL 變數，hello 資料列會提供從 1 開始的連續註標。 提供陣列存取 tooindividual 資料列。
* **VARRYS** hello 連接器中不支援。

### <a name="schema-5-define-partition-for-reference-attributes"></a>結構描述 5 (定義參考屬性的資料分割)
在此頁面上，您會為所有參考屬性設定屬性所參考的資料分割 (物件類型)。

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

如果您使用**DN 是錨點**，則您必須使用相同的物件型別為其中一個您要從參考 hello 的 hello。 您無法參考其他物件類型。

>[!NOTE]
現在是可選擇的 hello 2017 年 3 月更新中啟動"*"這個選項時所選然後所有可能成員類型將會匯入。

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 自 2017 年 hello"*"也稱為**任何選項**已變更 toosupport 匯入和匯出流程。 如果您想要 toouse 這個選項您多重值的資料表/檢視應該包含 hello 物件類型的屬性。

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> 如果"*"也必須指定 hello hello hello 物件類型資料行名稱，然後選取。</br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

在匯入之後，您會看到類似下面的 toohello 影像：

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a>全域參數
hello 全域參數頁面是使用的 tooconfigure 差異匯入，日期/時間格式和密碼方法。

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



hello 泛型 SQL Connector 支援 hello 差異匯入下列方法：

* **觸發程序**：請參閱 [使用觸發程序產生差異檢視](https://technet.microsoft.com/library/cc708665.aspx)。
* **浮水印**：可以用於任何資料庫的一般方法。 hello 浮水印查詢是根據 hello 資料庫供應商，預先填入。 浮水印資料行必須出現在所用的每個資料表/檢視上。 此資料行必須在插入和更新 toohello 做為資料表和其相依性追蹤 (多重值或子系) 資料表。 同步處理服務與 hello 資料庫伺服器之間的 hello 時鐘必須同步處理。 如果沒有，則可能會省略 hello 差異匯入中的某些項目。  
  限制：
  * 浮水印策略不支援已刪除的物件。
* **快照**：(僅適用於 Microsoft SQL Server) [使用快照產生差異檢視](https://technet.microsoft.com/library/cc720640.aspx)
* **變更追蹤**：(僅適用於 Microsoft SQL Server) [About 變更追蹤](https://msdn.microsoft.com/library/bb933875.aspx)  
  限制：
  * 錨點和 DN 屬性必須是 hello hello 資料表中的所選物件的主索引鍵的一部分。
  * 在使用變更追蹤的匯入和匯出期間內，不支援 SQL 查詢。

**其他參數**： 指定 hello 指出您的資料庫伺服器所在的資料庫伺服器時區。 會使用此值 toosupport hello 各種格式的日期和時間屬性。

hello 連接器一律日期和日期時間以 UTC 格式儲存。 toobe 無法 toocorrectly 轉換 hello 日期和時間值，必須指定 hello 時區 hello 資料庫伺服器以及使用 hello 格式。 hello 格式應該是以.Net 格式表示。

在匯出期間的每個日期時間屬性必須提供 toohello 連接器以 UTC 時間格式。

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

**密碼設定**: hello 連接器提供的密碼同步處理功能和支援設定及變更密碼。

hello 連接器提供兩種 toosupport 密碼同步處理：

* **預存程序**： 此方法需要兩個預存程序 toosupport 集與變更密碼。 輸入新增的所有參數，並變更中的 hello 密碼作業**設定密碼 SP**和**變更密碼 SP**分別依照下列範例中的參數。
  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)
* **密碼延伸模組**： 這個方法會要求密碼延伸模組 DLL (您需要 tooprovide hello 其實作 hello 的延伸模組 DLL 名稱[IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx)介面)。 密碼延伸模組組件必須放在 擴充功能資料夾中，如此 hello 連接器可以載入 hello DLL 在執行階段。
  ![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)

您也可以在 hello tooenable hello 密碼管理**設定副檔名**頁面。
![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)

### <a name="configure-partitions-and-hierarchies"></a>設定資料分割和階層
在 hello 資料分割和階層 頁面上，選取所有物件類型。 每個物件類型都在自己的資料分割中。

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

您也可以覆寫 hello 上定義的 hello 值**連線**或**全域參數**頁面。

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a>設定錨點
此頁面是唯讀的因為已定義 hello 錨點。 hello 選錨點屬性一律會附加與 hello 物件型別 tooensure 則仍會保持唯一的各種物件類型。

![錨點](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a>設定執行步驟參數
Hello hello 連接器上執行設定檔上設定這些步驟。 這些設定進行 hello 匯入及匯出資料的實際工作。

### <a name="full-and-delta-import"></a>完整和差異匯入
一般 SQL 連接器支援使用下列方法的完整和差異匯入：

* 資料表
* 檢視
* 預存程序
* SQL 查詢

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

**資料表/檢視**  
tooimport 多重值的屬性物件，您必須有 tooprovide hello 以逗號分隔的資料表/檢視表名稱**名稱的多重值的資料表/檢視**和個別的聯結條件中 hello**聯結條件**與 hello 父資料表。

範例： 您想 tooimport hello Employee 物件和其所有多重值的屬性。 有兩個資料表：[員工] \(主要資料表) 和 [部門] \(多重值)。
請勿 hello 遵循：

* 在 [資料表/檢視/SP] 中輸入**員工**。
* 在 [多重資料表/檢視名稱] 中輸入 [部門]。
* 輸入 hello 員工 （& s） 中的部門之間的聯結條件**聯結條件**，例如`Employee.DEPTID=Department.DepartmentID`。
  ![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)

**預存程序**  
![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)

* 如果您有太多資料，建議您預存程序與 tooimplement 分頁。
* 您的預存程序 toosupport 分頁，您需要 tooprovide 開始索引 」 和 「 結束索引。 請參閱： [有效地進行大量資料的分頁](https://msdn.microsoft.com/library/bb445504.aspx)。
* 在執行時，會以在 [設定步驟] 頁面上設定的各自頁面大小值取代 @StartIndex 和 @EndIndex。 例如，當 hello 連接器擷取第一頁和 hello 頁面大小設定 500，在這種情況下@StartIndex會是 1 和@EndIndex500。 連接器擷取的後續頁面時，請增加這些值，並變更 hello @StartIndex &@EndIndex值。
* tooexecute 參數化預存程序，提供中的 hello 參數`[Name]:[Direction]:[Value]`格式。 輸入每個參數 （使用 Ctrl + Enter tooget 新行） 的個別行上。
* 一般 SQL 連接器也支援從 Microsoft SQL Server 中連結伺服器的匯入作業。 如果應該從連結的伺服器中的資料表中擷取資訊，則資料表應該 hello 格式提供：`[ServerName].[Database].[Schema].[TableName]`
* 一般 SQL 連接器僅支援在執行步驟資訊和結構描述偵測之間具有類似結構 (包括別名和資料類型) 的物件。 如果 hello 選取從結構描述並提供在執行步驟的詳細資訊的物件不同，則 SQL Connector 是無法 toosupport 這種案例。

**SQL 查詢**  
![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* 不支援多個結果集查詢。
* SQL 查詢支援 hello 分頁，並提供開始索引和結束索引做為變數 toosupport 分頁。

### <a name="delta-import"></a>差異匯入
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

相較於完整匯入，差異匯入設定需要一些更詳細的設定。

* 如果您選擇 hello 觸發程序或快照集的方法 tootrack 差異變更，然後提供在歷程記錄資料表或快照集資料庫**歷程記錄資料表或快照集資料庫名稱**方塊。
* 您也需要 tooprovide 歷程記錄資料表與父資料表之間的聯結條件例如`Employee.ID=History.EmployeeID`
* tootrack hello hello 歷程記錄資料表中的 hello 父資料表上的交易，您必須提供包含 hello 作業資訊 （新增/更新/刪除） 的 hello 資料行名稱。
* 如果您選擇浮水印 tootrack 差異變更，然後提供包含 hello 作業資訊中的 hello 資料行名稱**上限標記資料行名稱**。
* hello**變更類型屬性**資料行是 hello 變更類型的必要項。 此資料行對應 hello 主資料表中發生的變更或多重值資料表 tooa 變更 hello 差異檢視中的類型。 這個資料行可以包含 hello Modify_Attribute 變更類型屬性層級變更或新增、 修改或刪除變更為物件層級變更類型的類型。 如果以外的 hello 預設值新增、 修改或刪除，則您可以定義使用這個選項的值。

### <a name="export"></a>匯出
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

一般 SQL 連接器支援使用下列四種方法的匯出：

* 資料表
* 檢視
* 預存程序
* SQL 查詢

**資料表/檢視**  
如果您選擇 hello 資料表/檢視表選項，hello 連接器會產生 hello 個別查詢 toodo hello 匯出。

**預存程序**  
![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)

如果您選擇 hello 預存程序選項，匯出，需要三個不同預存程序 tooperform Insert/Update/Delete 作業。

* **將預存程序名稱**： 如果任何物件都有 tooconnector hello 個別資料表中插入作業會執行此預存程序。
* **更新預存程序名稱**： 如果任何物件都有 tooconnector hello 個別資料表中的更新，會執行此預存程序。
* **刪除預存程序名稱**： 如果任何物件都有 tooconnector hello 個別資料表中要刪除此預存程序來執行。
* 從 hello 做為參數值 toohello 預存程序的結構描述中所選取的屬性。 例如， `EmployeeName: INPUT: @EmployeeName` （hello 連接器結構描述中選取員工姓名和 hello 連接器進行匯出時取代 hello 個別值）
* toorun 參數化預存程序，提供中的參數`[Name]:[Direction]:[Value]`格式。 輸入每個參數 （使用 Ctrl + Enter tooget 新行） 的個別行上。

**SQL query**  
![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)

如果您選擇 hello SQL 查詢選項，匯出，需要有三個不同查詢 tooperform Insert/Update/Delete 作業。

* **插入查詢**： 如果任何物件都有 tooconnector hello 個別資料表中插入作業會執行此查詢。
* **更新查詢**： 如果任何物件都有 tooconnector hello 個別資料表中更新執行此查詢。
* **刪除查詢**： 如果任何物件都有 tooconnector hello 個別資料表中要刪除此查詢會執行。
* 從當做參數值 toohello 查詢，例如 hello 結構描述中所選取屬性`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`

## <a name="troubleshooting"></a>疑難排解
* 如需如何 tooenable 記錄 tootroubleshoot hello 連接器資訊，請參閱 hello[如何 tooEnable ETW 追蹤連接器](http://go.microsoft.com/fwlink/?LinkId=335731)。
