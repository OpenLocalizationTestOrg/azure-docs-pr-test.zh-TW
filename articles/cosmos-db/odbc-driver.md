---
title: "aaaConnect tooAzure Cosmos DB 使用 BI 分析工具 |Microsoft 文件"
description: "了解如何 toouse hello Azure Cosmos DB ODBC 驅動程式 toocreate 資料表和檢視表，以便正規化的資料可以檢視在 BI 和資料分析的軟體。"
keywords: "odbc, odbc 驅動程式"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 9967f4e5-4b71-4cd7-8324-221a8c789e6b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: e12a70f7805445f09fac01411e4bfbccc9a29c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-cosmos-db-using-bi-analytics-tools-with-hello-odbc-driver"></a>連接 tooAzure Cosmos DB hello ODBC 驅動程式搭配使用 BI 分析工具

hello Azure Cosmos DB ODBC 驅動程式可讓 tooconnect tooAzure Cosmos DB 使用 BI 分析工具，例如 SQL Server Integration Services、 Power BI Desktop 和 Tableau 讓分析，並在那些中建立 Azure Cosmos DB 資料視覺效果解決方案。

hello Azure Cosmos DB ODBC 驅動程式符合 ODBC 3.8，而且支援 ANSI SQL 92 語法。 hello 驅動程式提供豐富的功能 toohelp renormalize Azure Cosmos DB 中的資料。 您可以使用 hello 驅動程式，來表示 Azure Cosmos DB 中的資料做為資料表和檢視表。 hello 驅動程式可讓您針對 hello 資料表和檢視表包括查詢、 插入、 更新和刪除的群組 tooperform SQL 作業。

## <a name="why-do-i-need-toonormalize-my-data"></a>為什麼我需要 toonormalize 我的資料？
Azure Cosmos DB 是 schemaless 資料庫，因此它啟用應用程式 tooiterate 啟用快速開發的應用程式及其資料模型 hello 立即不將它們 tooa 嚴格的結構描述。 單一 Azure Cosmos DB 資料庫可以包含各種結構的 JSON 文件。 這是最適合用於快速應用程式開發，但是當您想 tooanalyze 並建立報表的資料使用資料分析和 BI 工具，hello 資料通常需要 toobe 簡維方式呈現，而且遵守 tooa 特定結構描述。

這是 hello ODBC 驅動程式的運作方式。 藉由使用 hello ODBC 驅動程式，您可以現在重新正規化 Azure Cosmos DB 中的資料到資料表和檢視表 tooyour 資料分析和報告需求。 hello 重新正規化結構描述基礎資料的 hello 造成任何影響，而且不限制開發人員 tooadhere toothem，它們只是可讓您 tooleverage ODBC 相容工具 tooaccess hello 資料。 因此，現在您的 Azure Cosmos DB 資料庫不會只是開發小組的最愛，也會是資料分析師的最愛。

現在可讓開始與 hello ODBC 驅動程式。

## <a id="install"></a>步驟 1： 安裝 hello Azure Cosmos DB ODBC 驅動程式

1. 下載您的環境的 hello 驅動程式：

    * 適用於 64 位元 Windows 的 [Microsoft Azure Cosmos DB ODBC 64-bit.msi](https://aka.ms/documentdb-odbc-64x64)
    * 適用於 32 位元和 64 位元 Windows 的 [Microsoft Azure Cosmos DB ODBC 32x64-bit.msi](https://aka.ms/documentdb-odbc-32x64)
    * 適用於 32 位元 Windows 的 [Microsoft Azure Cosmos DB ODBC 32-bit.msi](https://aka.ms/documentdb-odbc-32x32)

    執行的 hello msi 檔案在本機，哪些啟動 hello **Microsoft Azure Cosmos DB ODBC 驅動程式安裝精靈**。 
2. 完成 hello hello 預設輸入的 tooinstall hello ODBC 驅動程式的安裝精靈。
3. 開啟 hello **ODBC 資料來源管理員**您的電腦上的應用程式，您可以輸入**ODBC 資料來源**hello Windows 在搜尋方塊。 
    您可以確認 hello 驅動程式已安裝，即可 hello**驅動程式** 索引標籤，並確定**Microsoft Azure Cosmos DB ODBC 驅動程式**列。

    ![Azure Cosmos DB ODBC 資料來源管理員](./media/odbc-driver/odbc-driver.png)

## <a id="connect"></a>步驟 2： 連接 tooyour Azure Cosmos DB 資料庫

1. 之後[安裝 hello Azure Cosmos DB ODBC 驅動程式](#install)，在 hello **ODBC 資料來源管理員**視窗中，按一下 **新增**。 您可以建立「使用者 DSN」或「系統 DSN」。 在此範例中，我們會建立「使用者 DSN」。
2. 在 hello**建立新的資料來源**視窗中，選取**Microsoft Azure Cosmos DB ODBC 驅動程式**，然後按一下**完成**。
3. 在 [hello **Azure Cosmos DB ODBC 驅動程式 SDN 安裝**] 視窗中，填入下列 hello: 

    ![Azure Cosmos DB ODBC 驅動程式 DSN 設定視窗](./media/odbc-driver/odbc-driver-dsn-setup.png)
    - **資料來源名稱**: hello ODBC DSN 自己易記名稱。 這個名稱是唯一的 tooyour Azure Cosmos DB 帳戶，因此將其命名適當如果您有多個帳戶。
    - **描述**: hello 資料來源的簡短描述。
    - **主機**：Azure Cosmos DB 帳戶的 URI。 您可以擷取這從 hello Azure 入口網站中的 hello Azure Cosmos DB 金鑰刀鋒視窗中 hello 下列螢幕擷取畫面所示。 
    - **便捷鍵**: hello 的 hello Azure 入口網站中的 hello Azure Cosmos DB 金鑰刀鋒視窗的主要或次要、 讀寫或唯讀金鑰 hello 下列螢幕擷取畫面所示。 我們建議如果 hello DSN 用於唯讀資料處理和報表，使用 hello 唯讀金鑰。
    ![Azure Cosmos DB 金鑰刀鋒視窗](./media/odbc-driver/odbc-driver-keys.png)
    - **加密 存取金鑰**： 選取此機器的 hello 使用者為基礎的 hello 最佳選擇。 
4. 按一下 hello**測試**按鈕 toomake 確定您可以對 tooyour Azure Cosmos DB 帳戶進行連接。 
5. 按一下**進階選項**和集 hello 下列值：
    - **查詢一致性**： 選取 hello[一致性層級](consistency-levels.md)您的作業。 hello 預設值為工作階段。
    - **重試次數**： 輸入 hello 次數 tooretry 作業時，如果沒有完成 hello 初始要求，這是因為 tooservice 節流。
    - **結構描述檔案**：您在這裡有一些選項。
        - 根據預設，保留原狀 （空白），此項目 hello 驅動程式會掃描所有集合 toodetermine hello 結構描述的每個集合的 hello 第一頁資料。 這就是所謂的「集合對應」。 沒有定義結構描述檔案，hello 驅動程式具有 tooperform hello 掃描每個驅動程式工作階段，並可能會導致較高的啟動時間使用 hello DSN 的應用程式。 建議您一律將結構描述檔案與 DSN 產生關連。
        - 如果您已經有結構描述檔案 (可能是一個使用建立 hello[結構描述編輯器](#schema-editor))，您可以按一下**瀏覽**，瀏覽 tooyour 檔案，按一下 **儲存**，然後按一下**確定**。
        - 如果您想 toocreate 新的結構描述，請按一下**確定**，然後按一下**結構描述編輯器**hello 主視窗中。 然後繼續 toohello[結構描述編輯器](#schema-editor)資訊。 在建立 hello 新結構描述檔案時，請記住 toogo 後 toohello**進階選項**視窗 tooinclude hello 新建立的結構描述檔案。

6. 一旦您完成並關閉 hello **Azure Cosmos DB ODBC 驅動程式 DSN 設定** 視窗中，為新的使用者 DSN hello 加入 toohello 使用者 DSN 索引標籤。

    ![新 Azure Cosmos DB ODBC DSN hello 使用者 DSN 索引標籤](./media/odbc-driver/odbc-driver-user-dsn.png)

## <a id="#collection-mapping"></a>步驟 3： 建立使用 hello 集合的對應方法的結構描述定義

您可以使用的取樣方法有兩種：**集合對應**或**資料表分隔符號**。 取樣工作階段可以利用這兩種取樣方法，但是每個集合僅可以使用特定的取樣方法。 hello 執行下列步驟建立 hello 資料的結構描述中使用 hello 集合的對應方法的一個或多個集合。 此取樣方法擷取 hello hello hello 資料集合 toodetermine hello 結構 頁面中的資料。 它調換 hello ODBC 端上的集合物件 tooa 資料表。 同質集合中的 hello 資料時，此取樣方法是有效率且快速。 如果集合包含異質性資料類型，建議使用 hello[資料表分隔符號對應方法](#table-mapping)因為它提供了更強固的取樣方法 toodetermine hello hello 集合中的資料結構。 

1. 完成步驟 1-4。 之後[連接 tooyour Azure Cosmos DB 資料庫](#connect)，按一下 **結構描述編輯器**在 hello **Azure Cosmos DB ODBC 驅動程式 DSN 設定**視窗。

    ![Hello Azure Cosmos DB ODBC 驅動程式 DSN 安裝程式視窗中的結構描述編輯器 按鈕](./media/odbc-driver/odbc-driver-schema-editor.png)
2. 在 hello**結構描述編輯器**視窗中，按一下 **建立新**。
    hello**產生結構描述**hello Azure Cosmos DB 帳號視窗會顯示所有 hello 集合。 
3. 選取一或多個集合 toosample，然後按一下**範例**。 
4. 在 [hello**設計] 檢視中**表示索引標籤、 hello 資料庫、 結構描述和資料表。 在 hello 資料表檢視中，hello 掃描會顯示 hello 組 hello 資料行名稱 （SQL 名稱、 來源名稱） 相關聯的屬性。
    每個資料行，您可以修改 hello 資料行 SQL 名稱、 hello SQL 類型 SQL 的長度 （如果適用），小數位數 （如果適用）、 有效位數 （如果適用） 和可為 Null。
    - 您可以設定**隱藏資料行**太**true**如果您想 tooexclude 該資料行從查詢結果。 資料行標示為隱藏的資料行 = true 不會傳回選取範圍和投影，雖然它們仍是 hello 結構描述的一部分。 例如，您可以隱藏所有開頭為"_"hello Azure Cosmos DB 所需的系統屬性。
    - hello**識別碼**資料行是 hello 無法隱藏，因為它正使用 hello hello 標準化結構描述中的主索引鍵的唯一欄位。 
5. 當您完成定義 hello 結構描述後時，按一下**檔案** | **儲存**，瀏覽 toohello 目錄 toosave hello 結構描述，然後按一下**儲存**。

    如果您想在未來的 hello toouse 這個結構描述的 DSN 中，開啟 hello Azure Cosmos DB ODBC 驅動程式 DSN 設定視窗 （透過 hello ODBC 資料來源管理員)、 按一下 [進階選項]，然後在 hello 結構描述檔案中，巡覽 toohello 儲存結構描述。 儲存結構描述檔案 tooan hello DSN 連接 tooscope toohello 資料和結構描述所定義的結構會修改現有的資料來源名稱。

## <a id="table-mapping"></a>步驟 4： 建立使用 hello 資料表分隔符號的結構描述定義對應方法

您可以使用的取樣方法有兩種：**集合對應**或**資料表分隔符號**。 取樣工作階段可以利用這兩種取樣方法，但是每個集合僅可以使用特定的取樣方法。 

hello 下列步驟建立 hello 資料的結構描述中一個或多個集合使用 hello**資料表分隔符號**對應方法。 當您的集合包含異質資料類型時，建議您使用這個取樣方法。 您可以使用此方法 tooscope hello 取樣 tooa 組屬性和其相對應的值。 例如，如果文件包含"Type"屬性，您可以範圍 hello 取樣 toohello 值，這個屬性。 hello 取樣 hello 最終結果會是一組資料表，每個 hello 針對您指定的類型的值。 例如，類型 = Car 會產生「汽車」資料表，而類型 = Plane 會產生「飛機」資料表。

1. 完成步驟 1-4。 之後[連接 tooyour Azure Cosmos DB 資料庫](#connect)，按一下 **結構描述編輯器**hello Azure Cosmos DB ODBC 驅動程式 DSN 安裝程式視窗中。
2. 在 hello**結構描述編輯器**視窗中，按一下 **建立新**。
    hello**產生結構描述**hello Azure Cosmos DB 帳號視窗會顯示所有 hello 集合。 
3. 選取的集合上 hello**檢視範例** 索引標籤的 hello**對應定義**hello 集合的資料行按一下**編輯**。 接著在 hello**對應定義**視窗中，選取**資料表分隔符號**方法。 然後 hello 遵循：

    a. 在 [hello**屬性**] 方塊中，輸入 hello 名稱的分隔符號屬性。 這是文件中要 tooscope hello 取樣，比方說，縣 （市） 的屬性，然後按 enter 鍵。 

    b. 如果您只想 tooscope hello 取樣 toocertain 值 hello 您剛才輸入的屬性，hello 選取範圍 方塊中，選取 hello 屬性，然後輸入 hello 值**值** 方塊中，例如，Seattle 然後按 enter。 您可以繼續 tooadd 有多個屬性值。 只確定該 hello 正確地輸入值時，選取屬性。

    例如，如果您包含**屬性**值縣 （市），而且您想 toolimit 資料表 tooonly 包含紐約和阿布達比縣 （市） 值的資料列，您會在 hello hello屬性方塊中，和紐約和阿布達比輸入縣（市）**值**方塊。
4. 按一下 [確定] 。 
5. 完成 hello hello 集合的對應定義之後，您想 toosample，在 hello**結構描述編輯器**視窗中，按一下 **範例**。
     每個資料行，您可以修改 hello 資料行 SQL 名稱、 hello SQL 類型 SQL 的長度 （如果適用），小數位數 （如果適用）、 有效位數 （如果適用） 和可為 Null。
    - 您可以設定**隱藏資料行**太**true**如果您想 tooexclude 該資料行從查詢結果。 資料行標示為隱藏的資料行 = true 不會傳回選取範圍和投影，雖然它們仍是 hello 結構描述的一部分。 例如，您可以隱藏開頭為"_"所有的 hello Azure Cosmos DB 所需的系統屬性。
    - hello**識別碼**資料行是 hello 無法隱藏，因為它正使用 hello hello 標準化結構描述中的主索引鍵的唯一欄位。 
6. 當您完成定義 hello 結構描述後時，按一下**檔案** | **儲存**，瀏覽 toohello 目錄 toosave hello 結構描述，然後按一下**儲存**。
7. 在 hello **Azure Cosmos DB ODBC 驅動程式 DSN 設定**視窗中，按一下 * * 進階選項 * *。 然後，在 hello**結構描述檔案**，瀏覽 toohello 儲存結構描述檔案，然後按一下**確定**。 按一下**確定**再次 toosave hello DSN。 此儲存 hello 的結構描述建立 toohello DSN。 

## <a name="optional-creating-views"></a>(選擇性) 建立檢視
您可以定義及 hello 取樣過程中建立檢視。 這些檢視是相等的 tooSQL 的檢視。 它們是唯讀，且會範圍 hello 項目，並定義 Azure Cosmos DB SQL hello 投影。 

toocreate 檢視中的資料，hello**結構描述編輯器**視窗中的，於 hello**檢視定義**資料行中，按一下 **新增**在 hello 集合 toosample hello 資料列。 接著在 hello**檢視定義**視窗中，執行下列 hello:
1. 按一下**新增**，輸入 hello 檢視中，例如 EmployeesfromSeattleView 的名稱，然後按一下**確定**。
2. 在 hello**編輯檢視**視窗中，輸入 Azure Cosmos DB 查詢。 這必須是 Azure Cosmos DB SQL 查詢 (例如 `SELECT c.City, c.EmployeeName, c.Level, c.Age, c.Gender, c.Manager FROM c WHERE c.City = “Seattle”`)，然後按一下確定。

您可以依需求建立多個檢視。 在您完成定義 hello 檢視，您可以再取樣 hello 資料。 

## <a name="step-5-view-your-data-in-bi-tools-such-as-power-bi-desktop"></a>步驟 5：在 BI 工具 (例如 Power BI Desktop) 中檢視資料

您可以使用新 DSN tooconnect DocumentADB 搭配任何 ODBC 相容的工具-這個步驟只會顯示您如何 tooconnect tooPower BI Desktop 並建立 Power BI 視覺效果。

1. 開啟 Power BI Desktop。
2. 按一下 [取得資料]。
3. 在 hello**取得資料**視窗中，按一下 **其他** | **ODBC** | **連接**。
4. 在 hello**從 ODBC**視窗中，您所建立，並按一下選取的 hello 資料來源名稱**確定**。 您可以保留 hello**進階選項**空白項目。
5. 在 hello**存取資料來源使用 ODBC 驅動程式**視窗中，選取**預設或自訂**，然後按一下**連接**。 您不需要 tooinclude hello**認證連接字串屬性**。
6. 在 hello**導覽**視窗中的，hello 左窗格中，展開 hello 資料庫，hello 結構描述，然後選取 hello 資料表。 hello [結果] 窗格包含使用您所建立的 hello 結構描述的 hello 資料。
7. 在 Power BI desktop 中，toovisualize hello 資料檢查 hello 資料表名稱，前面的 hello 方塊，然後按一下**負載**。
8. 在 Power BI Desktop 中的 在 hello 最左側，選取 hello 資料 索引標籤 ![Power BI Desktop 中的 [資料] 索引標籤](./media/odbc-driver/odbc-driver-data-tab.png) tooconfirm 已匯入您的資料。
9. 您現在可以建立 hello 報表 索引標籤上，即可使用 Power BI 的視覺效果![Power BI Desktop 中的報表 索引標籤](./media/odbc-driver/odbc-driver-report-tab.png)，然後按一下**新 Visual**，並自訂您的磚。 如需有關在 Power BI Desktop 中建立視覺效果的詳細資訊，請參閱 [Power BI 中的視覺效果類型](https://powerbi.microsoft.com/documentation/powerbi-service-visualization-types-for-reports-and-q-and-a/)。

## <a name="troubleshooting"></a>疑難排解

如果您收到下列錯誤 hello，請確定 hello**主機**和**便捷鍵**您複製的值 hello Azure 入口網站中的[步驟 2](#connect)是否正確，然後再試一次。 使用方 hello hello 複製按鈕 toohello**主機**和**便捷鍵**hello 免費的 Azure 入口網站 toocopy hello 值錯誤中的值。

    [HY000]: [Microsoft][Azure Cosmos DB] (401) HTTP 401 Authentication Error: {"code":"Unauthorized","message":"hello input authorization token can't serve hello request. Please check that hello expected payload is built as per hello protocol, and check hello key being used. Server used hello following payload toosign: 'get\ndbs\n\nfri, 20 jan 2017 03:43:55 gmt\n\n'\r\nActivityId: 9acb3c0d-cb31-4b78-ac0a-413c8d33e373"}`

## <a name="next-steps"></a>後續步驟

toolearn 深入了解 Azure Cosmos DB，請參閱[什麼是 Azure Cosmos DB？](introduction.md)。
