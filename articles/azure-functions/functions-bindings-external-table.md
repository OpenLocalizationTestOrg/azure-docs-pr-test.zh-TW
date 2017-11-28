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
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="e1ea6-103">Azure Functions 外部資料表繫結 (預覽)</span><span class="sxs-lookup"><span data-stu-id="e1ea6-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="e1ea6-104">本文將說明如何 toomanipulate SaaS 提供者 （例如 Sharepoint、 Dynamics） 在您的函式與內建繫結上的表格式資料。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-104">This article shows how toomanipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="e1ea6-105">Azure Functions 支援外部資料表的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="e1ea6-106">API 連線</span><span class="sxs-lookup"><span data-stu-id="e1ea6-106">API Connections</span></span>

<span data-ttu-id="e1ea6-107">資料表繫結利用外部的應用程式開發介面連接 tooauthenticate 與第 3 個合作對象 SaaS 提供者。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-107">Table bindings leverage external API connections tooauthenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="e1ea6-108">指派的繫結時您可以建立新的應用程式開發介面連接或使用現有的應用程式開發介面連接內 hello 相同的資源群組</span><span class="sxs-lookup"><span data-stu-id="e1ea6-108">When assigning a binding you can either create a new API connection or use an existing API connection within hello same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="e1ea6-109">支援的 API 連線 (資料表)</span><span class="sxs-lookup"><span data-stu-id="e1ea6-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="e1ea6-110">連接器</span><span class="sxs-lookup"><span data-stu-id="e1ea6-110">Connector</span></span>|<span data-ttu-id="e1ea6-111">觸發程序</span><span class="sxs-lookup"><span data-stu-id="e1ea6-111">Trigger</span></span>|<span data-ttu-id="e1ea6-112">輸入</span><span class="sxs-lookup"><span data-stu-id="e1ea6-112">Input</span></span>|<span data-ttu-id="e1ea6-113">輸出</span><span class="sxs-lookup"><span data-stu-id="e1ea6-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="e1ea6-114">DB2</span><span class="sxs-lookup"><span data-stu-id="e1ea6-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="e1ea6-115">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-115">x</span></span>|<span data-ttu-id="e1ea6-116">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-116">x</span></span>
|[<span data-ttu-id="e1ea6-117">Dynamics 365 for Operations (英文)</span><span class="sxs-lookup"><span data-stu-id="e1ea6-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="e1ea6-118">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-118">x</span></span>|<span data-ttu-id="e1ea6-119">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-119">x</span></span>
|[<span data-ttu-id="e1ea6-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="e1ea6-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="e1ea6-121">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-121">x</span></span>|<span data-ttu-id="e1ea6-122">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-122">x</span></span>
|[<span data-ttu-id="e1ea6-123">Dynamics NAV (英文)</span><span class="sxs-lookup"><span data-stu-id="e1ea6-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="e1ea6-124">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-124">x</span></span>|<span data-ttu-id="e1ea6-125">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-125">x</span></span>
|[<span data-ttu-id="e1ea6-126">Google 試算表</span><span class="sxs-lookup"><span data-stu-id="e1ea6-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="e1ea6-127">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-127">x</span></span>|<span data-ttu-id="e1ea6-128">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-128">x</span></span>
|[<span data-ttu-id="e1ea6-129">Informix</span><span class="sxs-lookup"><span data-stu-id="e1ea6-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="e1ea6-130">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-130">x</span></span>|<span data-ttu-id="e1ea6-131">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-131">x</span></span>
|[<span data-ttu-id="e1ea6-132">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="e1ea6-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="e1ea6-133">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-133">x</span></span>|<span data-ttu-id="e1ea6-134">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-134">x</span></span>
|[<span data-ttu-id="e1ea6-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="e1ea6-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="e1ea6-136">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-136">x</span></span>|<span data-ttu-id="e1ea6-137">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-137">x</span></span>
|[<span data-ttu-id="e1ea6-138">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="e1ea6-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="e1ea6-139">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-139">x</span></span>|<span data-ttu-id="e1ea6-140">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-140">x</span></span>
|[<span data-ttu-id="e1ea6-141">Common Data Service (英文)</span><span class="sxs-lookup"><span data-stu-id="e1ea6-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="e1ea6-142">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-142">x</span></span>|<span data-ttu-id="e1ea6-143">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-143">x</span></span>
|[<span data-ttu-id="e1ea6-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="e1ea6-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="e1ea6-145">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-145">x</span></span>|<span data-ttu-id="e1ea6-146">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-146">x</span></span>
|[<span data-ttu-id="e1ea6-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="e1ea6-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="e1ea6-148">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-148">x</span></span>|<span data-ttu-id="e1ea6-149">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-149">x</span></span>
|[<span data-ttu-id="e1ea6-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e1ea6-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="e1ea6-151">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-151">x</span></span>|<span data-ttu-id="e1ea6-152">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-152">x</span></span>
|[<span data-ttu-id="e1ea6-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="e1ea6-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="e1ea6-154">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-154">x</span></span>|<span data-ttu-id="e1ea6-155">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-155">x</span></span>
|<span data-ttu-id="e1ea6-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="e1ea6-156">UserVoice</span></span>||<span data-ttu-id="e1ea6-157">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-157">x</span></span>|<span data-ttu-id="e1ea6-158">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-158">x</span></span>
|<span data-ttu-id="e1ea6-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="e1ea6-159">Zendesk</span></span>||<span data-ttu-id="e1ea6-160">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-160">x</span></span>|<span data-ttu-id="e1ea6-161">x</span><span class="sxs-lookup"><span data-stu-id="e1ea6-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="e1ea6-162">外部資料表連線也可以用在 [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) 中</span><span class="sxs-lookup"><span data-stu-id="e1ea6-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="e1ea6-163">建立 API 連線：逐步解說</span><span class="sxs-lookup"><span data-stu-id="e1ea6-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="e1ea6-164">建立函數 > 自訂函數 ![建立自訂函數](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="e1ea6-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="e1ea6-165">案例 `Experimental` > `ExternalTable-CSharp` 範本 > 建立新的 `External Table connection`
![選擇資料表輸入範本](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="e1ea6-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="e1ea6-166">選擇您的 SaaS 提供者 > 選擇/建立連線 ![設定 SaaS 連線](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="e1ea6-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="e1ea6-167">選取您的應用程式開發介面連接 > 建立 hello 函式![建立資料表函式](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="e1ea6-167">Select your API connection > create hello function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="e1ea6-168">選取 `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="e1ea6-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="e1ea6-169">設定 hello 連接 toouse 目標資料表。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-169">Configure hello connection toouse your target table.</span></span> <span data-ttu-id="e1ea6-170">這些設定會依 SaaS 提供者不同而有所差異。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="e1ea6-171">它們會在下方的[資料來源設定](#datasourcesettings)中說明
![設定資料表](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="e1ea6-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="e1ea6-172">使用量</span><span class="sxs-lookup"><span data-stu-id="e1ea6-172">Usage</span></span>

<span data-ttu-id="e1ea6-173">此範例會連接 tooa 資料表識別碼、 LastName 和 FirstName 資料行與名為"Contact"。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-173">This example connects tooa table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="e1ea6-174">hello 程式碼會列出 hello 資料表中的 hello 連絡人實體與記錄檔 hello 名字和姓氏。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-174">hello code lists hello Contact entities in hello table and logs hello first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="e1ea6-175">繫結</span><span class="sxs-lookup"><span data-stu-id="e1ea6-175">Bindings</span></span>
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
<span data-ttu-id="e1ea6-176">`entityId` 針對資料表繫結必須為空白。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="e1ea6-177">`ConnectionAppSettingsKey`識別儲存 hello API 連接字串 hello 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-177">`ConnectionAppSettingsKey` identifies hello app setting that stores hello API connection string.</span></span> <span data-ttu-id="e1ea6-178">hello 應用程式設定會自動建立時新增應用程式開發介面中 hello 連接整合 UI。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-178">hello app setting is created automatically when you add an API connection in hello integrate UI.</span></span>

<span data-ttu-id="e1ea6-179">表格式連接器會提供資料集，每個資料集皆包含資料表。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="e1ea6-180">hello hello 預設資料集名稱是"default"。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-180">hello name of hello default data set is “default.”</span></span> <span data-ttu-id="e1ea6-181">以下列出 hello 標題的資料集和各種 SaaS 提供者中的資料表：</span><span class="sxs-lookup"><span data-stu-id="e1ea6-181">hello titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="e1ea6-182">連接器</span><span class="sxs-lookup"><span data-stu-id="e1ea6-182">Connector</span></span>|<span data-ttu-id="e1ea6-183">Dataset</span><span class="sxs-lookup"><span data-stu-id="e1ea6-183">Dataset</span></span>|<span data-ttu-id="e1ea6-184">資料表</span><span class="sxs-lookup"><span data-stu-id="e1ea6-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="e1ea6-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="e1ea6-185">**SharePoint**</span></span>|<span data-ttu-id="e1ea6-186">網站</span><span class="sxs-lookup"><span data-stu-id="e1ea6-186">Site</span></span>|<span data-ttu-id="e1ea6-187">SharePoint 清單</span><span class="sxs-lookup"><span data-stu-id="e1ea6-187">SharePoint List</span></span>
|<span data-ttu-id="e1ea6-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="e1ea6-188">**SQL**</span></span>|<span data-ttu-id="e1ea6-189">資料庫</span><span class="sxs-lookup"><span data-stu-id="e1ea6-189">Database</span></span>|<span data-ttu-id="e1ea6-190">資料表</span><span class="sxs-lookup"><span data-stu-id="e1ea6-190">Table</span></span> 
|<span data-ttu-id="e1ea6-191">**Google 試算表**</span><span class="sxs-lookup"><span data-stu-id="e1ea6-191">**Google Sheet**</span></span>|<span data-ttu-id="e1ea6-192">試算表</span><span class="sxs-lookup"><span data-stu-id="e1ea6-192">Spreadsheet</span></span>|<span data-ttu-id="e1ea6-193">工作表</span><span class="sxs-lookup"><span data-stu-id="e1ea6-193">Worksheet</span></span> 
|<span data-ttu-id="e1ea6-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="e1ea6-194">**Excel**</span></span>|<span data-ttu-id="e1ea6-195">Excel 檔案</span><span class="sxs-lookup"><span data-stu-id="e1ea6-195">Excel file</span></span>|<span data-ttu-id="e1ea6-196">工作表</span><span class="sxs-lookup"><span data-stu-id="e1ea6-196">Sheet</span></span> 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="e1ea6-197">C# 中的使用方式</span><span class="sxs-lookup"><span data-stu-id="e1ea6-197">Usage in C#</span></span> #

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

<span data-ttu-id="e1ea6-198"><!--
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
## 資料來源設定</span><span class="sxs-lookup"><span data-stu-id="e1ea6-198"><!--
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
<a name="datasourcesettings"></a>
## Data Source Settings</span></span>

### <a name="sql-server"></a><span data-ttu-id="e1ea6-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e1ea6-199">SQL Server</span></span>

<span data-ttu-id="e1ea6-200">hello toocreate 指令碼，並填入 hello Contact 資料表低於。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-200">hello script toocreate and populate hello Contact table is below.</span></span> <span data-ttu-id="e1ea6-201">dataSetName 為 "default"。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="e1ea6-202">Google 試算表</span><span class="sxs-lookup"><span data-stu-id="e1ea6-202">Google Sheets</span></span>
<span data-ttu-id="e1ea6-203">在 Google 文件中，建立具有名為 `Contact` 之工作表的試算表。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="e1ea6-204">hello 連接器無法使用 hello 試算表的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-204">hello connector cannot use hello spreadsheet display name.</span></span> <span data-ttu-id="e1ea6-205">hello 內部名稱 （粗體） 需要 toobe 做 dataSetName，例如： `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** 加入 hello 資料行名稱`Id`， `LastName`， `FirstName` toohello 第一次資料列，然後上填入資料後續的資料列。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-205">hello internal name (in bold) needs toobe used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add hello column names `Id`, `LastName`, `FirstName` toohello first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="e1ea6-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="e1ea6-206">Salesforce</span></span>
<span data-ttu-id="e1ea6-207">dataSetName 為 "default"。</span><span class="sxs-lookup"><span data-stu-id="e1ea6-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1ea6-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1ea6-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
