---
title: "使用 Azure Data Factory 從 Marketo 複製資料 (搶鮮版 (Beta)) | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 管線中的複製活動，將資料從 Marketo 複製到支援的接收資料存放區。"
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
ms.date: 12/15/2017
ms.author: jingwang
ms.openlocfilehash: dc4e8b8682e686abc77f43427615c7069585f327
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="copy-data-from-marketo-using-azure-data-factory-beta"></a>使用 Azure Data Factory 從 Marketo 複製資料 (搶鮮版 (Beta))

本文概述如何使用 Azure Data Factory 中的「複製活動」，從 Marketo 複製資料。 本文是根據[複製活動概觀](copy-activity-overview.md)一文，該文提供複製活動的一般概觀。

> [!NOTE]
> 本文適用於第 2 版的 Data Fatory (目前為預覽版)。 如果您使用第 1 版的 Data Factory 服務，也就是正式推出 (GA) 的版本，請參閱[第 1 版的複製活動](v1/data-factory-data-movement-activities.md)。

> [!IMPORTANT]
> 此連接器目前為搶鮮版 (Beta)。 您可以親身體驗並提供意見反應。 請勿在生產環境中使用它。

## <a name="supported-capabilities"></a>支援的功能

您可以將資料從 Marketo 複製到任何支援的接收資料存放區。 如需複製活動所支援作為來源/接收器的資料存放區清單，請參閱[支援的資料存放區](copy-activity-overview.md#supported-data-stores-and-formats)表格。

Azure Data Factory 提供的內建驅動程式可啟用連線，因此使用此連接器您不需要手動安裝任何驅動程式。

## <a name="getting-started"></a>開始使用

[!INCLUDE [data-factory-v2-connector-get-started-2](../../includes/data-factory-v2-connector-get-started-2.md)]

下列各節提供屬性的相關詳細資料，這些屬性是用來定義 Marketo 連接器專屬的 Data Factory 實體。

## <a name="linked-service-properties"></a>連結服務屬性

以下是針對 Marketo 已連結服務支援的屬性：

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| type | type 屬性必須設定為：**Marketo** | yes |
| endpoint | Marketo 伺服器的端點。 (亦即 123-ABC-321.mktorest.com)  | yes |
| clientId | Marketo 服務的用戶端識別碼。  | yes |
| clientSecret | Marketo 服務的用戶端密碼。 您可以選擇將這個欄位標記為 SecureString 將它安全地儲存在 ADF，或將密碼儲存在 Azure Key Vault，然後在執行複製資料時，讓 ADF 複製活動從該處提取 - 請參閱[將認證儲存在 Key Vault](store-credentials-in-key-vault.md) 以進一步了解。 | yes |
| useEncryptedEndpoints | 指定是否使用 HTTPS 來加密資料來源端點。 預設值為 true。  | 否 |
| useHostVerification | 指定在透過 SSL 連線時，是否要求伺服器憑證中的主機名稱符合伺服器的主機名稱。 預設值為 true。  | 否 |
| usePeerVerification | 指定在透過 SSL 連線時，是否要確認伺服器的身分識別。 預設值為 true。  | 否 |

**範例：**

```json
{
    "name": "MarketoLinkedService",
    "properties": {
        "type": "Marketo",
        "typeProperties": {
            "endpoint" : "123-ABC-321.mktorest.com",
            "clientId" : "<clientId>",
            "clientSecret": {
                 "type": "SecureString",
                 "value": "<clientSecret>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a>資料集屬性

如需可用來定義資料集的區段和屬性完整清單，請參閱[資料集](concepts-datasets-linked-services.md)一文。 本節提供 Marketo 資料集所支援的屬性清單。

若要從 Marketo 複製資料，請將資料集的 type 屬性設定為 **MarketoObject**。 在此類型的資料集中，沒有任何其他類型特定的屬性。

**範例**

```json
{
    "name": "MarketoDataset",
    "properties": {
        "type": "MarketoObject",
        "linkedServiceName": {
            "referenceName": "<Marketo linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>複製活動屬性

如需可用來定義活動的區段和屬性完整清單，請參閱[管線](concepts-pipelines-activities.md)一文。 本節提供 Marketo 來源所支援的屬性清單。

### <a name="marketosource-as-source"></a>將 MarketoSource 作為來源

若要從 Marketo 複製資料，請將複製活動中的來源類型設定為 **MarketoSource**。 複製活動的 **source** 區段支援下列屬性：

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| type | 複製活動來源的 type 屬性必須設定為：**MarketoSource** | yes |
| query | 使用自訂 SQL 查詢來讀取資料。 例如：`"SELECT * FROM Activitiy_Types"`。 | yes |

**範例：**

```json
"activities":[
    {
        "name": "CopyFromMarketo",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Marketo input dataset name>",
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
                "type": "MarketoSource",
                "query": "SELECT top 1000 * FROM Activitiy_Types"
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
