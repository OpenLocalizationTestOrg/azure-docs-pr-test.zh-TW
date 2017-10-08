---
title: "在您的 Logic Apps aaaAdd hello Azure SQL Database 連接器 |Microsoft 文件"
description: "搭配 REST API 參數來使用 Azure SQL Database 連接器的概觀"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a>開始使用 hello Azure SQL Database 連接器
使用 hello Azure SQL Database 連接器，建立為您的組織管理資料在資料表中的工作流程。 

利用 SQL Database，您可以：

* 建置您的工作流程加入新的客戶 tooa 客戶資料庫，或更新訂單 」 資料庫中的訂單。
* 使用動作 tooget 資料列、 插入新資料列，並且甚至刪除。 例如，當有記錄在 Dynamics CRM Online 中建立時 (觸發程序)，則在 Azure SQL Database 插入資料列 (動作)。 

本主題說明您如何 toouse hello 邏輯應用程式中的 SQL Database 連接器及清單也 hello 動作。

toolearn 進一步了解邏輯應用程式，請參閱[為何的 logic apps](../logic-apps/logic-apps-what-are-logic-apps.md)和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="connect-tooazure-sql-database"></a>連接 tooAzure SQL 資料庫
邏輯應用程式可以存取任何服務之前，您先建立*連接*toohello 服務。 連線可讓邏輯應用程式與另一個服務連線。 例如，tooconnect tooSQL 資料庫，您先建立 SQL Database*連接*。 toocreate 連線，您輸入您平常用 tooaccess hello 服務，您所連接的 hello 認證。 因此，在 SQL 資料庫中，輸入您 SQL 資料庫認證 toocreate hello 連接。 

#### <a name="create-hello-connection"></a>建立 hello 連線
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>使用觸發程序
此連接器並沒有任何觸發程序。 使用其他觸發程序 toostart hello 邏輯應用程式，例如循環觸發程序、 HTTP Webhook 觸發程序、 觸發程序適用於其他連接器，等等。 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md) 可提供範例。

## <a name="use-an-action"></a>使用動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

1. 選取加號 hello。 您會看到幾個選擇：**將動作加入**，**加入條件**，或其中一個 hello**詳細**選項。
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. 選擇 [新增動作] 。
3. 在 [hello] 文字方塊中，輸入"sql"tooget 所有 hello 可用動作的清單。
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. 在我們的範例中，選擇 [SQL Server - 取得資料列]。 如果連接已存在，然後選取 hello**資料表名稱**從 hello 下拉式清單，然後輸入 hello**資料列識別碼**想 tooreturn。
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    如果系統提示您輸入 hello 連接資訊，然後輸入 hello 詳細資料 toocreate hello 連接。 [建立 hello 連接](connectors-create-api-sqlazure.md#create-the-connection)本主題說明這些屬性。 
   
   > [!NOTE]
   > 在此範例中，我們會從資料表傳回資料列。 在這個資料列，toosee hello 資料加入另一個使用 hello 資料表中的 hello 欄位建立檔的動作。 比方說，將會使用 hello FirstName 和 LastName 欄位 toocreate hello 雲端儲存體帳戶中的新檔案的 OneDrive 動作。 
   > 
   > 
5. **儲存**您的變更 （hello 工具列的左上的角）。 邏輯應用程式將會儲存，而且可能會自動啟用。

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/sql/)。 

## <a name="next-steps"></a>後續步驟
[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。 瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。

