---
title: "aaaAzure 函式外部資料表繫結 （預覽） |Microsoft 文件"
description: "使用 Azure Functions 中的外部資料表繫結"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a>Azure Functions 外部資料表繫結 (預覽)
本文將說明如何 toomanipulate SaaS 提供者 （例如 Sharepoint、 Dynamics） 在您的函式與內建繫結上的表格式資料。 Azure Functions 支援外部資料表的輸入和輸出繫結。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a>API 連線

資料表繫結利用外部的應用程式開發介面連接 tooauthenticate 與第 3 個合作對象 SaaS 提供者。 

指派的繫結時您可以建立新的應用程式開發介面連接或使用現有的應用程式開發介面連接內 hello 相同的資源群組

### <a name="supported-api-connections-tables"></a>支援的 API 連線 (資料表)

|連接器|觸發程序|輸入|輸出|
|:-----|:---:|:---:|:---:|
|[DB2](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||x|x
|[Dynamics 365 for Operations (英文)](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||x|x
|[Dynamics 365](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[Dynamics NAV (英文)](https://msdn.microsoft.com/library/gg481835.aspx)||x|x
|[Google 試算表](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||x|x
|[Informix](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||x|x
|[Dynamics 365 for Financials](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[MySQL](https://docs.microsoft.com/azure/store-php-create-mysql-database)||x|x
|[Oracle Database](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||x|x
|[Common Data Service (英文)](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||x|x
|[Salesforce](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||x|x
|[SharePoint](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||x|x
|[SQL Server](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||x|x
|[Teradata](http://www.teradata.com/products-and-services/azure/products/)||x|x
|UserVoice||x|x
|Zendesk||x|x


> [!NOTE]
> 外部資料表連線也可以用在 [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) 中

### <a name="creating-an-api-connection-step-by-step"></a>建立 API 連線：逐步解說

1. 建立函數 > 自訂函數 ![建立自訂函數](./media/functions-bindings-storage-table/create-custom-function.jpg)
1. 案例 `Experimental` > `ExternalTable-CSharp` 範本 > 建立新的 `External Table connection`
![選擇資料表輸入範本](./media/functions-bindings-storage-table/create-template-table.jpg)
1. 選擇您的 SaaS 提供者 > 選擇/建立連線 ![設定 SaaS 連線](./media/functions-bindings-storage-table/authorize-API-connection.jpg)
1. 選取您的應用程式開發介面連接 > 建立 hello 函式![建立資料表函式](./media/functions-bindings-storage-table/table-template-options.jpg)
1. 選取 `Integrate` > `External Table`
    1. 設定 hello 連接 toouse 目標資料表。 這些設定會依 SaaS 提供者不同而有所差異。 它們會在下方的[資料來源設定](#datasourcesettings)中說明
![設定資料表](./media/functions-bindings-storage-table/configure-API-connection.jpg)

## <a name="usage"></a>使用量

此範例會連接 tooa 資料表識別碼、 LastName 和 FirstName 資料行與名為"Contact"。 hello 程式碼會列出 hello 資料表中的 hello 連絡人實體與記錄檔 hello 名字和姓氏。

### <a name="bindings"></a>繫結
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
`entityId` 針對資料表繫結必須為空白。

`ConnectionAppSettingsKey`識別儲存 hello API 連接字串 hello 應用程式設定。 hello 應用程式設定會自動建立時新增應用程式開發介面中 hello 連接整合 UI。

表格式連接器會提供資料集，每個資料集皆包含資料表。 hello hello 預設資料集名稱是"default"。 以下列出 hello 標題的資料集和各種 SaaS 提供者中的資料表：

|連接器|Dataset|資料表|
|:-----|:---|:---| 
|**SharePoint**|網站|SharePoint 清單
|**SQL**|資料庫|資料表 
|**Google 試算表**|試算表|工作表 
|**Excel**|Excel 檔案|工作表 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a>C# 中的使用方式 #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings">

</a>
## 資料來源設定

### <a name="sql-server"></a>SQL Server

hello toocreate 指令碼，並填入 hello Contact 資料表低於。 dataSetName 為 "default"。

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a>Google 試算表
在 Google 文件中，建立具有名為 `Contact` 之工作表的試算表。 hello 連接器無法使用 hello 試算表的顯示名稱。 hello 內部名稱 （粗體） 需要 toobe 做 dataSetName，例如： `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** 加入 hello 資料行名稱`Id`， `LastName`， `FirstName` toohello 第一次資料列，然後上填入資料後續的資料列。

### <a name="salesforce"></a>Salesforce
dataSetName 為 "default"。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
