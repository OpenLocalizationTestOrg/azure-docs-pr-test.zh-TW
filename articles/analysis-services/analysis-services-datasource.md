---
title: "Azure Analysis Services 中支援的 aaaData 來源 |Microsoft 文件"
description: "說明 Azure Analysis Services 中資料模型支援的資料來源。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2902d7d3c3bcf086419822fa826193bd247bde61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a>Azure Analysis Services 中支援的資料來源
Azure Analysis Services 伺服器支援連接 toodata 來源 hello 雲端和內部部署組織中。 其他支援的資料來源加入所有 hello 時間。 請經常回來查看。 

目前支援下列資料來源的 hello:

| 雲端  |
|---|
| Azure Blob 儲存體*  |
| Azure SQL Database  |
| Azure 資料倉儲 |


| 內部部署  |   |   |   |
|---|---|---|---|
| Access 資料庫  | 資料夾* | Oracle 資料庫  | Teradata 資料庫 |
| Active Directory*  | JSON 文件*  | Postgre SQL 資料庫*  |XML 表格* |
| Analysis Services  | Lines from binary*  | SAP HANA*  |
| 分析平台系統  | MySQL Database  | SAP Business Warehouse*  | |
| Dynamics CRM*  | OData 摘要*  | SharePoint*  |
| Excel 活頁簿  | ODBC 查詢  | SQL Database  |
| Exchange*  | OLE DB  | Sybase 資料庫  |

\* 僅限表格式 1400 模型。 

> [!IMPORTANT]
> Tooon 內部部署資料來源需要連接[在內部部署資料閘道](analysis-services-gateway.md)安裝在您的環境中的電腦上。

## <a name="data-providers"></a>資料提供者

Azure Analysis Services 中的資料模型連接 toocertain 資料來源時，可能需要不同的資料提供者。 在某些情況下，連接使用原生提供者，例如 SQL Server Native Client (SQLNCLI11) toodata 來源的表格式模型可能會傳回錯誤。

Tooa 雲端資料連接的資料模型的來源，例如 Azure SQL Database 中，如果您使用 SQLOLEDB 以外的原生提供者，您可能會看到錯誤訊息： **「 hello 提供者未註冊 'SQLNCLI11.1'。 」** 或者，如果您有 DirectQuery 模型連接 tooon 內部部署資料來源，如果您使用原生提供者可能會看到錯誤訊息： **"建立 OLE DB 資料列集時發生錯誤。Incorrect syntax near 'LIMIT'”** (建立 OLE DB 列集時發生錯誤。'LIMIT' 附近的語法錯誤)。

下列資料來源提供者的 hello 支援 in-memory 或 DirectQuery 資料模型時連接 toodata 來源 hello 雲端或內部部署中：

### <a name="cloud"></a>雲端
| **資料來源** | **In-memory** | **DirectQuery** |
|  --- | --- | --- |
| Azure SQL 資料倉儲 |.NET Framework Data Provider for SQL Server |.NET Framework Data Provider for SQL Server |
| Azure SQL Database |.NET Framework Data Provider for SQL Server |.NET Framework Data Provider for SQL Server | |

### <a name="on-premises-via-gateway"></a>內部部署 (透過閘道)
|**資料來源** | **In-memory** | **DirectQuery** |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 |.NET Framework Data Provider for SQL Server |
| SQL Server |Microsoft OLE DB Provider for SQL Server |.NET Framework Data Provider for SQL Server | |
| SQL Server |.NET Framework Data Provider for SQL Server |.NET Framework Data Provider for SQL Server | |
| Oracle |Microsoft OLE DB Provider for Oracle |Oracle Data Provider for .NET | |
| Oracle |Oracle Data Provider for .NET |Oracle Data Provider for .NET | |
| Teradata |Teradata 的 OLE DB 提供者 |Teradata Data Provider for .NET | |
| Teradata |Teradata Data Provider for .NET |Teradata Data Provider for .NET | |
| 分析平台系統 |.NET Framework Data Provider for SQL Server |.NET Framework Data Provider for SQL Server | |

> [!NOTE]
> 使用內部部署閘道時，請確定已安裝 64 位元提供者。
> 
> 

在移轉內部部署 SQL Server Analysis Services 表格式模型 tooAzure Analysis Services 時，可能需要 toochange hello 提供者。

**toospecify 資料來源提供者**

1. 在 SSDT > **Tabular Model Explorer** (表格式模型總管)  >  資料來源 中，以滑鼠右鍵按一下資料來源連線，然後按一下編輯資料來源。
2. 在**編輯連接**，按一下 [**進階**tooopen hello 進階屬性] 視窗。
3. 在**Set 進階 Properties** > **提供者**，然後選取 hello 適當的提供者。

## <a name="impersonation"></a>模擬
在某些情況下，可能需要 toospecify 不同模擬帳戶。 模擬帳戶可以在 SSDT 或 SSMS 中指定。

對於內部部署資料來源：

* 如果使用 SQL 驗證，模擬應為服務帳戶。
* 如果使用 Windows 驗證，請設定 Windows 使用者/密碼。 對於 SQL Server，In-Memory 資料模型僅支援具有特定模擬帳戶的 Windows 驗證。

對於雲端資料來源：

* 如果使用 SQL 驗證，模擬應為服務帳戶。

## <a name="next-steps"></a>後續步驟
如果您有內部部署資料來源，是確定 tooinstall hello[在內部部署閘道](analysis-services-gateway.md)。   
toolearn 進一步了解管理您的伺服器在 SSDT 或 SSMS，請參閱[管理您的伺服器](analysis-services-manage.md)。

