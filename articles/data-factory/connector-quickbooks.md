---
title: "使用 Azure Data Factory (搶鮮版 (Beta)) 從 QuickBooks 複製資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 管線中的複製活動，將資料從 QuickBooks 複製到支援的接收資料存放區。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/30/2017
ms.author: jingwang
ms.openlocfilehash: 9c3a725d0d0c5091a280c3fb99279757f1e014f1
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="copy-data-from-quickbooks-using-azure-data-factory-beta"></a>使用 Azure Data Factory (搶鮮版 (Beta)) 從 QuickBooks 複製資料

本文概述如何使用 Azure Data Factory 中的「複製活動」，從 QuickBooks 複製資料。 本文是根據[複製活動概觀](copy-activity-overview.md)一文，該文提供複製活動的一般概觀。

> [!NOTE]
> 本文適用於第 2 版的 Data Fatory (目前為預覽版)。 如果您使用第 1 版的 Data Factory 服務，也就是正式推出 (GA) 的版本，請參閱[第 1 版的複製活動](v1/data-factory-data-movement-activities.md)。

> [!IMPORTANT]
> 此連接器目前為搶鮮版 (Beta)。 您可以親身體驗並提供意見反應。 請勿在生產環境中使用它。

## <a name="supported-capabilities"></a>支援的功能

您可以將資料從 QuickBooks 複製到任何支援的接收資料存放區。 如需複製活動所支援作為來源/接收器的資料存放區清單，請參閱[支援的資料存放區](copy-activity-overview.md#supported-data-stores-and-formats)表格。

Azure Data Factory 提供的內建驅動程式可啟用連線，因此使用此連接器您不需要手動安裝任何驅動程式。

此連接器目前僅支援 1.0a，這表示您需要具備一個開發人員帳戶，其中含有在 2017 年 7 月 17 日之前建立的應用程式。

## <a name="getting-started"></a>開始使用

[!INCLUDE [data-factory-v2-connector-get-started-2](../../includes/data-factory-v2-connector-get-started-2.md)]

下列各節提供屬性的相關詳細資料，這些屬性是用來定義 QuickBooks 連接器專屬的 Data Factory 實體。

## <a name="linked-service-properties"></a>連結服務屬性

以下是針對 QuickBooks 已連結服務支援的屬性：

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| type | Type 屬性必須設定為：**QuickBooks** | yes |
| endpoint | QuickBooks 伺服器的端點。 (也就是 quickbooks.api.intuit.com)  | yes |
| companyId | 要授權之 QuickBooks 公司的公司識別碼。  | yes |
| accessToken | 用於 OAuth 1.0 驗證的存取權杖。 您可以選擇將這個欄位標記為 SecureString 以將它安全地儲存在 ADF，或將密碼儲存在 Azure Key Vault；然後在執行複製資料時，讓複製活動從該處提取 - 請參閱[將認證儲存在 Key Vault](store-credentials-in-key-vault.md) 以進一步了解。 | yes |
| accessTokenSecret | 用於 OAuth 1.0 驗證的存取權杖祕密。 您可以選擇將這個欄位標記為 SecureString 以將它安全地儲存在 ADF，或將密碼儲存在 Azure Key Vault；然後在執行複製資料時，讓複製活動從該處提取 - 請參閱[將認證儲存在 Key Vault](store-credentials-in-key-vault.md) 以進一步了解。 | yes |
| useEncryptedEndpoints | 指定是否使用 HTTPS 來加密資料來源端點。 預設值為 true。  | 否 |

**範例：**

```json
{
    "name": "QuickBooksLinkedService",
    "properties": {
        "type": "QuickBooks",
        "typeProperties": {
            "endpoint" : "quickbooks.api.intuit.com",
            "companyId" : "<companyId>",
            "accessToken": {
                 "type": "SecureString",
                 "value": "<accessToken>"
            },
            "accessTokenSecret": {
                 "type": "SecureString",
                 "value": "<accessTokenSecret>"
            },
            "useEncryptedEndpoints" : true
        }
    }
}
```

## <a name="dataset-properties"></a>資料集屬性

如需可用來定義資料集的區段和屬性完整清單，請參閱[資料集](concepts-datasets-linked-services.md)一文。 本節提供 QuickBooks 資料集所支援的屬性清單。

若要從 QuickBooks 複製資料，請將資料集的 type 屬性設定為 **QuickBooksObject**。 在此類型的資料集中，沒有任何其他類型特定的屬性。

**範例**

```json
{
    "name": "QuickBooksDataset",
    "properties": {
        "type": "QuickBooksObject",
        "linkedServiceName": {
            "referenceName": "<QuickBooks linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>複製活動屬性

如需可用來定義活動的區段和屬性完整清單，請參閱[管線](concepts-pipelines-activities.md)一文。 本節提供 QuickBooks 來源所支援的屬性清單。

### <a name="quickbookssource-as-source"></a>將 QuickBooksSource 作為來源

若要從 QuickBooks 複製資料，請將複製活動中的來源類型設定為 **QuickBooksSource**。 複製活動的 **source** 區段支援下列屬性：

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| type | 複製活動來源的 type 屬性必須設定為：**QuickBooksSource** | yes |
| query | 使用自訂 SQL 查詢來讀取資料。 例如：`"SELECT * FROM "Bill" WHERE Id = '123'"`。 | yes |

**範例：**

```json
"activities":[
    {
        "name": "CopyFromQuickBooks",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<QuickBooks input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "QuickBooksSource",
                "query": "SELECT * FROM \"Bill\" WHERE Id = '123' "
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a>後續步驟
如需 Azure Data Factory 中的複製活動所支援作為來源和接收器的資料存放區清單，請參閱[支援的資料存放區](copy-activity-overview.md#supported-data-stores-and-formats)。
