---
title: "aaaData Factory Azure 複本精靈 |Microsoft 文件"
description: "深入了解如何 toouse hello 資料 Factory Azure 複本精靈支援的資料來源 toosinks toocopy 資料。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 188b3ae15f937b84a58aec1b979347ac8090abf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-copy-wizard"></a>Azure Data Factory 複製精靈
hello Azure 資料 Factory 複製精靈減輕 hello 的擷取資料，通常是在端對端資料整合案例中的第一個步驟的程序。 當經過 hello Azure 資料 Factory 複製精靈，您不需要 toounderstand 任何 JSON 定義連結的服務、 資料集和管線。 hello 精靈會自動建立管線 toocopy 資料，從 hello 選取的資料來源 toohello 選取目的地。 此外，hello 複製精靈可協助您 toovalidate hello 資料內嵌在 hello 階段撰寫的。 這可以節省時間，特別當您會擷取資料的 hello 第一次 hello 資料來源。 toostart hello 複製精靈中，按一下 hello**將資料複製**的 data factory 的 hello 首頁上並排顯示。

![複製精靈](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a>針對巨量資料設計
此精靈可讓您從各種來源 toodestinations tooeasily 移動資料以分鐘為單位。 您瀏覽 hello 精靈之後，具有複製活動的管線會自動為您建立，以及相依的 Data Factory 實體 （連結的服務和資料集）。 不不需要的 toocreate hello 管線的任何額外的步驟。   

![選取資料來源](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> 如需逐步指示 toocreate 範例管線 toocopy 資料從 Azure blob tooan Azure SQL Database 的資料表，請參閱 hello[複製精靈教學課程](data-factory-copy-data-wizard-tutorial.md)。
>
>

hello 精靈被設計大型的資料，請注意，從 hello 開始，並且支援各種不同的資料和物件類型。 您可以撰寫 Data Factory 管線，移動數百個資料夾、檔案或資料表。 hello 精靈支援自動資料預覽、 擷取結構描述和對應，以及資料篩選。

## <a name="automatic-data-preview"></a>自動資料預覽
您可以在 hello 資料是您想要預覽 hello 選取的資料來源中的順序 toovalidate hello 資料的一部分 toocopy。 此外，如果 hello 來源資料是文字檔案中，複製精靈 hello 剖析 hello 文字檔案 toolearn hello 資料列和資料行分隔符號和結構描述自動。

![檔案格式設定](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>結構描述擷取和對應
hello 結構描述的輸入資料可能不符合輸出資料，在某些情況下 hello 結構描述。 在此案例中，您需要 toomap hello 來源結構描述 toocolumns 從 hello 目的地結構描述中的資料行。

> [!TIP]
> 當複製資料的 SQL Server 或 Azure SQL Database 到 Azure SQL 資料倉儲，如果 hello 資料表不存在於 hello 目的地存放區，Data Factory 支援自動建立資料表使用來源的結構描述。 進一步了解從[從 Azure SQL 資料倉儲使用 Azure Data Factory 中移動資料 tooand](./data-factory-azure-sql-data-warehouse-connector.md)。
>

Hello 目的結構描述中，使用下拉式清單 tooselect hello 來源結構描述 toomap tooa 資料行中的資料行。 hello 複製精靈會嘗試 toounderstand 您的資料行對應的模式。 它適用於的 hello 相同模式 toohello 其餘部分的 hello 資料行，因此，您不需要 tooselect 每個 hello 資料行個別 toocomplete hello 結構描述對應。 如果您想要的話，您可以使用 hello 下拉式清單 toomap hello 資料行一個覆寫這些對應。 hello 模式會變成更精確，因為您將多個資料行的對應。 hello 複製精靈不斷地更新 hello 模式，最後到達 hello 右模式 hello 資料行對應您想要 tooachieve。     

![結構描述對應](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>篩選資料
您可以篩選來源資料 tooselect 只有 hello 資料需要複製 toobe toohello 接收資料存放區。 篩選可降低 hello hello 資料 toobe 複製的 toohello 接收的資料儲存和因此增強 hello 輸送量 hello 複製作業的磁碟區。 它提供彈性方式 toofilter 資料關聯式資料庫中的使用 hello SQL 查詢語言，或使用 Azure blob 資料夾中檔案[Data Factory 函式和變數](data-factory-functions-variables.md)。   

### <a name="filtering-of-data-in-a-database"></a>篩選資料庫中的資料
hello 下列螢幕擷取畫面顯示 SQL 查詢使用 hello`Text.Format`函式和`WindowStart`變數。

![驗證運算式](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>篩選 Azure Blob 資料夾中的資料
您可以在 hello 資料夾路徑 toocopy 資料由決定在執行階段為基礎的資料夾中使用變數[系統變數](data-factory-functions-variables.md#data-factory-system-variables)。 支援的 hello 變數是： **{year}**， **{month}**， **{day}**， **{小時}**， **{分鐘}**，和**{自訂}**。 例如︰inputfolder/{year}/{month}/{day}。

假設您有輸入 hello 遵循格式中的資料夾：

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

按一下 hello**瀏覽**按鈕**檔案或資料夾**，瀏覽這些資料夾 tooone (比方說，2016年-> 03-> 01-> 02)，按一下**選擇**。 您應該會看到`2016/03/01/02`hello 文字方塊中。 現在，取代**2016年**與**{year}**， **03**與**{month}**， **01**與**{day}**，和**02**與**{小時}**，並按 hello  **索引標籤**索引鍵。 您應該會看到這些四個變數的下拉式清單 tooselect hello 格式：

![使用系統變數](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Hello 下列螢幕擷取畫面所示，您也可以使用**自訂**變數和任何[支援格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx)。 tooselect 資料夾與該結構中，使用 hello**瀏覽**按鈕第一次。 然後取代的值為**{自訂}**，並按 hello  **索引標籤**金鑰 toosee hello 文字方塊中，您可以在這裡輸入 hello 格式字串。     

![使用自訂變數](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a>排程選項
您可以執行 hello 複製作業一次，或根據排程 （每小時、 每天，依此類推）。 這兩個選項可以用於 hello 範圍的環境，包括在內部部署、 雲端和本機桌面複製 hello 連接器。

一次性複製作業可讓從來源 tooa 目的地的資料移動一次。 它適用於 toodata 任何大小和任何支援的格式。 排程的 hello 複製可讓您 toocopy 資料上規定的循環。 您可以使用 （例如重試、 逾時和警示） 的豐富設定 tooconfigure hello 排程複製。

![排程屬性](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>後續步驟
使用複製活動與 hello 資料 Factory 複製精靈 toocreate 管線快速逐步解說，請參閱[教學課程： 建立管線中使用 hello 複製精靈](data-factory-copy-data-wizard-tutorial.md)。
