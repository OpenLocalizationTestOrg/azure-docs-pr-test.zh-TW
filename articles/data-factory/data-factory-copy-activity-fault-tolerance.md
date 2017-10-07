---
title: "在 Azure 資料 Factory 複製活動中藉由略過不相容的資料列的 aaaAdd 容錯功能 |Microsoft 文件"
description: "了解如何 tooadd 容錯藉由在複製期間略過不相容的資料列的 Azure 資料 Factory 複製活動中的功能"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>跳過不相容的資料列以在複製活動中新增容錯

Azure Data Factory[複製活動](data-factory-data-movement-activities.md)來源和接收的資料存放區之間複製資料時將您提供兩種方式 toohandle 不相容的資料列：

- 您可以中止和失敗 hello 複製活動不相容的資料時遇到 （預設行為）。
- 您可以繼續 toocopy 所有 hello 加入容錯，並略過不相容的資料列的資料。 此外，您可以在 Azure Blob 儲存體記錄 hello 不相容的資料列。 您可以接著檢查 hello 記錄 toolearn hello hello 失敗原因、 修正 hello 資料 hello 的資料來源，再重試 hello 複製活動。

## <a name="supported-scenarios"></a>支援的案例
複製活動支援三種情節，以偵測、跳過並記錄不相容的資料：

- **Hello 來源資料類型與 hello 接收原生型別之間的不相容**

    例如： 複製資料，從 CSV 檔案中的 Blob 儲存體 tooa SQL 資料庫的結構描述定義，包含三種**INT**類型資料行。 hello CSV 檔案資料列包含數值資料，例如`123,456,789`成功複製 toohello 接收存放區。 不過，hello 資料列包含非數字的值，例如`123,456,abc`被偵測為不相容，所以會略過。

- **Hello hello 來源與 hello 接收器之間的資料行數不相符**

    例如： 複製資料，從 CSV 檔案中的 Blob 儲存體 tooa SQL 資料庫的結構描述定義，包含六個資料行。 hello CSV 檔案包含六個資料行的資料列成功地複製 toohello 接收存放區。 hello CSV 檔案包含的資料列更多或少於六個資料行被偵測為不相容，並略過。

- **撰寫 tooa 關聯式資料庫時的主索引鍵違規**

    例如： 將資料從 SQL server tooa SQL 資料庫複製。 在 hello 接收 SQL 資料庫中，定義主索引鍵，但是沒有這類主索引鍵會定義在 hello 來源 SQL server。 hello 來源檔案中的 hello 重複資料列不能複製的 toohello 接收。 複製活動會將只 hello 第一個資料列的 hello 來源資料複製到 hello 接收。 hello 後續的來源資料列包含重複的 hello 主索引鍵值被偵測為不相容且會略過。

## <a name="configuration"></a>組態
hello 下列範例提供 JSON 定義 tooconfigure 略過複製活動在 hello 不相容的資料列：

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | 啟用或停用在複製期間略過不相容的資料列。 | True<br/>FALSE (預設值) | 否 |
| **redirectIncompatibleRowSettings** | 一組屬性可指定當您想 toolog hello 不相容的資料列。 | &nbsp; | 否 |
| **linkedServiceName** | hello 連結服務的 Azure 儲存體 toostore hello 記錄，其中包含 hello 略過資料列。 | hello 名稱[AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service)或[AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service)連結服務，也就是您想 toouse toostore hello 記錄檔的 toohello 儲存執行個體。 | 否 |
| **路徑** | hello 記錄檔，其中包含 hello hello 路徑略過資料列。 | 指定您想 toouse toolog hello 不相容的資料 hello Blob 儲存體路徑。 如果您未提供路徑，hello 服務會為您建立的容器。 | 否 |

## <a name="monitoring"></a>監視
Hello 複製活動執行完成之後，您可以看到 hello hello [監視] 區段中略過資料列數目：

![監視跳過的不相容資料列](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

如果您設定 toolog hello 不相容的資料列時，您可以找到 hello 記錄檔，在這個路徑： `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` hello 記錄檔，您可以查看 hello 略過的資料列並 hello hello 不相容問題的根本原因。

Hello 原始資料和 hello 對應的錯誤會記錄在 hello 檔。 Hello 記錄檔案內容的範例如下所示：
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解 Azure 資料 Factory 複製活動時，請參閱[使用複製活動移動資料](data-factory-data-movement-activities.md)。
