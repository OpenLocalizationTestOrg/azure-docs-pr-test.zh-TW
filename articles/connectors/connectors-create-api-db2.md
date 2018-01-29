---
title: "在您的 Logic Apps 中新增 DB2 連接器 | Microsoft Docs"
description: "搭配 REST API 參數來使用 DB2 連接器的概觀"
services: 
documentationcenter: 
author: gplarsen
manager: erikre
editor: 
tags: connectors
ms.assetid: 1c6b010c-beee-496d-943a-a99e168c99aa
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: 7ad246ede7e891de42235443c1bc6a90b88ad5ac
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="get-started-with-the-db2-connector"></a>開始使用 DB2 連接器
Microsoft Connector for DB2 可將 Logic Apps 連接至 IBM DB2 資料庫中儲存的資源。 此連接器包含透過 TCP/IP 網路與遠端 DB2 伺服器電腦通訊的 Microsoft 用戶端。 其中包括雲端資料庫 (例如在 Azure 虛擬化中執行的 IBM Bluemix dashDB 或 IBM DB2 for Windows)，以及使用內部部署資料閘道的內部部署資料庫。 請參閱支援的 IBM DB2 平台和版本 [清單](connectors-create-api-db2.md#supported-db2-platforms-and-versions) (本主題結尾處)。

DB2 連接器支援下列資料庫作業：

* 列出資料庫資料表
* 使用 SELECT 讀取一個資料列
* 使用 SELECT 讀取所有資料列
* 使用 INSERT 加入一個資料列
* 使用 UPDATE 變更一個資料列
* 使用 DELETE 移除一個資料列

本主題說明如何在邏輯應用程式中使用連接器來處理資料庫作業。

若要深入了解 Logic Apps，請參閱 [建立邏輯應用程式](../logic-apps/quickstart-create-first-logic-app-workflow.md)。

## <a name="available-actions"></a>可用動作
DB2 連接器支援下列邏輯應用程式動作：

* GetTables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>列出資料表
針對由透過 Microsoft Azure 入口網站執行之許多步驟所組成的任何作業，建立邏輯應用程式。

在邏輯應用程式中，您可以新增動作以列出 DB2 資料庫中的資料表。 此動作會指示連接器來處理 DB2 結構描述陳述式，如 `CALL SYSIBM.SQLTABLES`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 **Azure 開始面板**中，依序選取 **+** (加號)、[Web + 行動] 和 [邏輯應用程式]。
2. 輸入 [名稱]，如 `Db2getTables`、**訂用帳戶**、**資源群組**、**位置**和 **App Service 方案**。 選取 [釘選到儀表板]，然後選取 [建立]。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 [Logic Apps 設計工具] 中，在 [範本] 清單中選取 [空白 LogicApp]。
2. 在**觸發程序**清單中，選取 [週期性]。 
3. 在 [週期性] 觸發程序中，選取 [編輯]，選取 [頻率] 下拉式清單以選取 [天]，然後設定 [間隔] 以輸入 **7**。  
4. 選取 [+ 新增步驟] 方塊，然後再選取 [新增動作]。
5. 在**動作**清單中，於 [搜尋更多動作] 編輯方塊中輸入 `db2`，然後選取 [DB2 - 取得資料表 (預覽)]。
   
   ![](./media/connectors-create-api-db2/Db2connectorActions.png)  
6. 在 [DB2 - 取得資料表] 組態窗格中，選取**核取方塊**以啟用 [透過內部部署資料閘道連接]。 請注意從雲端至內部部署的設定變更。
   
   * 以地址或別名冒號連接埠號碼的格式，輸入 [伺服器] 的值。 例如，輸入 `ibmserver01:50000`。
   * 輸入 [資料庫] 的值。 例如，輸入 `nwind`。
   * 選取 [驗證] 的值。 例如，選取 [基本] 。
   * 輸入 [使用者名稱] 的值。 例如，輸入 `db2admin`。
   * 輸入 [密碼] 的值。 例如，輸入 `Password1`。
   * 選取 [閘道] 的值。 例如，選取 [datagateway01] 。
7. 選取 [建立]，然後選取 [儲存]。 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)
8. 在 [Db2getTables] 刀鋒視窗中，於 [摘要] 之下的 [所有執行] 清單中，選取第一個列出的項目 (最近一次執行)。
9. 在 [邏輯應用程式執行] 刀鋒視窗中，選取 [執行詳細資料]。 選取 [動作] 清單中的 [Get_tables]。 請查看 [狀態] 的值，應該是 [成功]。 選取 [輸入連結]  以檢視輸入。 選取 [輸出連結] 並檢視輸出，其中應包含資料表清單。
   
   ![](./media/connectors-create-api-db2/Db2connectorGetTablesLogicAppRunOutputs.png)

## <a name="create-the-connections"></a>建立連線
此連接器支援使用下列連接屬性來連接裝載於內部和雲端中的資料庫。 

| 屬性 | 說明 |
| --- | --- |
| 伺服器 |必要。 接受代表 TCP/IP 位址或別名的字串值，其採用 IPv4 或 IPv6 格式，後面接著 (以冒號分隔) TCP/IP 連接埠編號。 |
| 資料庫 |必要。 接受代表 DRDA 關聯式資料庫名稱 (RDBNAM) 的字串值。 DB2 for z/OS 接受 16 個位元組的字串 (資料庫也稱為 IBM DB2 for z/OS 位置)。 DB2 for i5/OS 接受 18 個位元組的字串 (資料庫也稱為 IBM DB2 for i 關聯式資料庫)。 DB2 for LUW 接受 8 個位元組的字串。 |
| 驗證 |選用。 接受清單項目值 (基本或 Windows (kerberos))。 |
| username |必要。 接受字串值。 DB2 for z/OS 接受 8 個位元組的字串。 DB2 for i 接受 10 個位元組的字串。 DB2 for Linux 或 UNIX 接受 8 個位元組的字串。 DB2 for Windows 接受 30 個位元組的字串。 |
| password |必要。 接受字串值。 |
| gateway |必要。 接受清單項目值，該值代表對儲存群組內的 Logic Apps 定義的內部部署資料閘道。 |

## <a name="create-the-on-premises-gateway-connection"></a>建立內部部署閘道連線
此連接器可以使用內部部署閘道存取內部部署 DB2 資料庫。 如需詳細資訊，請參閱閘道主題。 

1. 在 [閘道] 組態窗格中，選取**核取方塊**以啟用 [透過閘道連接]。 請注意從雲端至內部部署的設定變更。
2. 以地址或別名冒號連接埠號碼的格式，輸入 [伺服器] 的值。 例如，輸入 `ibmserver01:50000`。
3. 輸入 [資料庫] 的值。 例如，輸入 `nwind`。
4. 選取 [驗證] 的值。 例如，選取 [基本] 。
5. 輸入 [使用者名稱] 的值。 例如，輸入 `db2admin`。
6. 輸入 [密碼] 的值。 例如，輸入 `Password1`。
7. 選取 [閘道] 的值。 例如，選取 [datagateway01] 。
8. 選取 [建立]  繼續作業。 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)

## <a name="create-the-cloud-connection"></a>建立雲端連線
此連接器可以存取雲端 DB2 資料庫。 

1. 在 [閘道] 組態窗格中，讓**核取方塊**停用 (取消選取) [透過閘道連接]。 
2. 輸入 [連線名稱] 的值。 例如，輸入 `hisdemo2`。
3. 以地址或別名冒號連接埠號碼的格式，輸入 [DB2 伺服器名稱] 的值。 例如，輸入 `hisdemo2.cloudapp.net:50000`。
4. 輸入 [DB2 資料庫名稱] 的值。 例如，輸入 `nwind`。
5. 輸入 [使用者名稱] 的值。 例如，輸入 `db2admin`。
6. 輸入 [密碼] 的值。 例如，輸入 `Password1`。
7. 選取 [建立]  繼續作業。 
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>使用 SELECT 擷取所有資料列
您可以定義邏輯應用程式動作，擷取 DB2 資料表中的所有資料列。 此動作會指示連接器來處理 DB2 SELECT 陳述式，如 `SELECT * FROM AREA`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 **Azure 開始面板**中，依序選取 **+** (加號)、[Web + 行動] 和 [邏輯應用程式]。
2. 輸入 [名稱]，如 `Db2getRows`、**訂用帳戶**、**資源群組**、**位置**和 **App Service 方案**。 選取 [釘選到儀表板]，然後選取 [建立]。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 [Logic Apps 設計工具] 中，在 [範本] 清單中選取 [空白 LogicApp]。
2. 在**觸發程序**清單中，選取 [週期性]。 
3. 在 [週期性] 觸發程序中，選取 [編輯]，選取 [頻率] 下拉式清單以選取 [天]，然後選取 [間隔] 以輸入 **7**。 
4. 選取 [+ 新增步驟] 方塊，然後再選取 [新增動作]。
5. 在**動作**清單中，於 [搜尋更多動作] 編輯方塊中輸入 `db2`，然後選取 [DB2 - 取得資料列 (預覽)]。
6. 在 [取得資料列 (預覽)] 動作中，選取 [變更連線]。
7. 在 [連線] 組態窗格中，選取 [新建]。 
   
    ![](./media/connectors-create-api-db2/Db2connectorNewConnection.png)
8. 在 [閘道] 組態窗格中，讓**核取方塊**停用 (取消選取) [透過閘道連接]。
   
   * 輸入 [連線名稱] 的值。 例如，輸入 `HISDEMO2`。
   * 以地址或別名冒號連接埠號碼的格式，輸入 [DB2 伺服器名稱] 的值。 例如，輸入 `HISDEMO2.cloudapp.net:50000`。
   * 輸入 [DB2 資料庫名稱] 的值。 例如，輸入 `NWIND`。
   * 輸入 [使用者名稱] 的值。 例如，輸入 `db2admin`。
   * 輸入 [密碼] 的值。 例如，輸入 `Password1`。
9. 選取 [建立]  繼續作業。
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)
10. 在 [資料表名稱] 清單中，選取**向下箭號**，然後選取 [AREA]。
11. (選擇性) 選取 [顯示進階選項]  來指定查詢選項。
12. 選取 [ **儲存**]。 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsTableName.png)
13. 在 [Db2getRows] 刀鋒視窗中，於 [摘要] 之下的 [所有執行] 清單中，選取第一個列出的項目 (最近一次執行)。
14. 在 [邏輯應用程式執行] 刀鋒視窗中，選取 [執行詳細資料]。 選取 [動作] 清單中的 [Get_rows]。 請查看 [狀態] 的值，應該是 [成功]。 選取 [輸入連結]  以檢視輸入。 選取 [輸出連結] 並檢視輸出，其中應包含資料列清單。
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>使用 INSERT 加入一個資料列
您可以定義邏輯應用程式動作，在 DB2 資料表中新增資料列。 此動作會指示連接器來處理 DB2 INSERT 陳述式，如 `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 **Azure 開始面板**中，依序選取 **+** (加號)、[Web + 行動] 和 [邏輯應用程式]。
2. 輸入 [名稱]，如 `Db2insertRow`、**訂用帳戶**、**資源群組**、**位置**和 **App Service 方案**。 選取 [釘選到儀表板]，然後選取 [建立]。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 [Logic Apps 設計工具] 中，在 [範本] 清單中選取 [空白 LogicApp]。
2. 在**觸發程序**清單中，選取 [週期性]。 
3. 在 [週期性] 觸發程序中，選取 [編輯]，選取 [頻率] 下拉式清單以選取 [天]，然後選取 [間隔] 以輸入 **7**。 
4. 選取 [+ 新增步驟] 方塊，然後再選取 [新增動作]。
5. 在**動作**清單中，於 [搜尋更多動作] 編輯方塊中輸入 **db2**，然後選取 [DB2 - 插入資料列 (預覽)]。
6. 在 [DB2 - 插入資料列 (預覽)] 動作中，選取 [變更連線]。 
7. 在 [連線]  組態窗格中選取連線。 例如，選取 [hisdemo2] 。
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. 在 [資料表名稱] 清單中，選取**向下箭號**，然後選取 [AREA]。
9. 輸入所有必要資料行 (請見紅色星號) 的值。 例如，針對 [AREAID] 輸入 `99999`、輸入 `Area 99999`，以及針對 [REGIONID] 輸入 `102`。 
10. 選取 [ **儲存**]。
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowValues.png)
11. 在 [Db2insertRow] 刀鋒視窗中，於 [摘要] 之下的 [所有執行] 清單中，選取第一個列出的項目 (最近一次執行)。
12. 在 [邏輯應用程式執行] 刀鋒視窗中，選取 [執行詳細資料]。 選取 [動作] 清單中的 [Get_rows]。 請查看 [狀態] 的值，應該是 [成功]。 選取 [輸入連結]  以檢視輸入。 選取 [輸出連結] 並檢視輸出，其中應包含新資料列。
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>使用 SELECT 擷取一個資料列
您可以定義邏輯應用程式動作，擷取 DB2 資料表中的資料列。 此動作會指示連接器來處理 DB2 SELECT WHERE 陳述式，如 `SELECT FROM AREA WHERE AREAID = '99999'`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 **Azure 開始面板**中，依序選取 **+** (加號)、[Web + 行動] 和 [邏輯應用程式]。
2. 輸入**名稱** (例如"**Db2getRow**")、[訂用帳戶]、[資源群組]、[位置] 和 [App Service 方案]。 選取 [釘選到儀表板]，然後選取 [建立]。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 [Logic Apps 設計工具] 中，在 [範本] 清單中選取 [空白 LogicApp]。 
2. 在**觸發程序**清單中，選取 [週期性]。 
3. 在 [週期性] 觸發程序中，選取 [編輯]，選取 [頻率] 下拉式清單以選取 [天]，然後選取 [間隔] 以輸入 **7**。 
4. 選取 [+ 新增步驟] 方塊，然後再選取 [新增動作]。
5. 在**動作**清單中，於 [搜尋更多動作] 編輯方塊中輸入 **db2**，然後選取 [DB2 - 取得資料列 (預覽)]。
6. 在 [取得資料列 (預覽)] 動作中，選取 [變更連線]。 
7. 在 [連線]  組態窗格中選取現有連線。 例如，選取 [hisdemo2] 。
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. 在 [資料表名稱] 清單中，選取**向下箭號**，然後選取 [AREA]。
9. 輸入所有必要資料行 (請見紅色星號) 的值。 例如，針對 [AREAID] 輸入 `99999`。 
10. (選擇性) 選取 [顯示進階選項]  來指定查詢選項。
11. 選取 [ **儲存**]。 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowValues.png)
12. 在 [Db2getRow] 刀鋒視窗中，於 [摘要] 之下的 [所有執行] 清單中，選取第一個列出的項目 (最近一次執行)。
13. 在 [邏輯應用程式執行] 刀鋒視窗中，選取 [執行詳細資料]。 選取 [動作] 清單中的 [Get_rows]。 請查看 [狀態] 的值，應該是 [成功]。 選取 [輸入連結]  以檢視輸入。 選取 [輸出連結] 並檢視輸出，其中應包含資料列。
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>使用 UPDATE 變更資料列
您可以定義邏輯應用程式動作，變更 DB2 資料表中的資料列。 此動作會指示連接器來處理 DB2 UPDATE 陳述式，如 `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 **Azure 開始面板**中，依序選取 **+** (加號)、[Web + 行動] 和 [邏輯應用程式]。
2. 輸入 [名稱]，如 `Db2updateRow`、**訂用帳戶**、**資源群組**、**位置**和 **App Service 方案**。 選取 [釘選到儀表板]，然後選取 [建立]。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 [Logic Apps 設計工具] 中，在 [範本] 清單中選取 [空白 LogicApp]。
2. 在**觸發程序**清單中，選取 [週期性]。 
3. 在 [週期性] 觸發程序中，選取 [編輯]，選取 [頻率] 下拉式清單以選取 [天]，然後選取 [間隔] 以輸入 **7**。 
4. 選取 [+ 新增步驟] 方塊，然後再選取 [新增動作]。
5. 在**動作**清單中，於 [搜尋更多動作] 編輯方塊中輸入 **db2**，然後選取 [DB2 - 更新資料列 (預覽)]。
6. 在 [DB2 - 更新資料列 (預覽)] 動作中，選取 [變更連線]。 
7. 在 [連線]  組態窗格中，選取以選取現有連線。 例如，選取 [hisdemo2] 。
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. 在 [資料表名稱] 清單中，選取**向下箭號**，然後選取 [AREA]。
9. 輸入所有必要資料行 (請見紅色星號) 的值。 例如，針對 [AREAID] 輸入 `99999`、輸入 `Updated 99999`，以及針對 [REGIONID] 輸入 `102`。 
10. 選取 [ **儲存**]。 
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowValues.png)
11. 在 [Db2updateRow] 刀鋒視窗中，於 [摘要] 之下的 [所有執行] 清單中，選取第一個列出的項目 (最近一次執行)。
12. 在 [邏輯應用程式執行] 刀鋒視窗中，選取 [執行詳細資料]。 選取 [動作] 清單中的 [Get_rows]。 請查看 [狀態] 的值，應該是 [成功]。 選取 [輸入連結]  以檢視輸入。 選取 [輸出連結] 並檢視輸出，其中應包含新資料列。
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>使用 DELETE 移除一個資料列
您可以定義邏輯應用程式動作，移除 DB2 資料表中的資料列。 此動作會指示連接器來處理 DB2 DELETE 陳述式，如 `DELETE FROM AREA WHERE AREAID = '99999'`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 **Azure 開始面板**中，依序選取 **+** (加號)、[Web + 行動] 和 [邏輯應用程式]。
2. 輸入 [名稱]，如 `Db2deleteRow`、**訂用帳戶**、**資源群組**、**位置**和 **App Service 方案**。 選取 [釘選到儀表板]，然後選取 [建立]。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 [Logic Apps 設計工具] 中，在 [範本] 清單中選取 [空白 LogicApp]。 
2. 在**觸發程序**清單中，選取 [週期性]。 
3. 在 [週期性] 觸發程序中，選取 [編輯]，選取 [頻率] 下拉式清單以選取 [天]，然後選取 [間隔] 以輸入 **7**。 
4. 選取 [+ 新增步驟] 方塊，然後再選取 [新增動作]。
5. 在**動作**清單中，於 [搜尋更多動作] 編輯方塊中選取 [db2]，然後選取 [DB2 - 刪除資料列 (預覽)]。
6. 在 [DB2 - 刪除資料列 (預覽)] 動作中，選取 [變更連線]。 
7. 在 [連線]  組態窗格中選取現有連線。 例如，選取 [hisdemo2] 。
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. 在 [資料表名稱] 清單中，選取**向下箭號**，然後選取 [AREA]。
9. 輸入所有必要資料行 (請見紅色星號) 的值。 例如，針對 [AREAID] 輸入 `99999`。 
10. 選取 [ **儲存**]。 
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowValues.png)
11. 在 [Db2deleteRow] 刀鋒視窗中，於 [摘要] 之下的 [所有執行] 清單中，選取第一個列出的項目 (最近一次執行)。
12. 在 [邏輯應用程式執行] 刀鋒視窗中，選取 [執行詳細資料]。 選取 [動作] 清單中的 [Get_rows]。 請查看 [狀態] 的值，應該是 [成功]。 選取 [輸入連結]  以檢視輸入。 選取 [輸出連結] 並檢視輸出，其中應包含刪除的資料列。
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowOutputs.png)

## <a name="supported-db2-platforms-and-versions"></a>支援的 DB2 平台和版本
此連接器支援以下 IBM DB2 平台和版本，以及 IBM DB2 相容產品 (例如 IBM Bluemix dashDB)，而這些產品支援分散式關聯資料庫架構 (DRDA) SQL 存取管理員 (SQLAM) 版本 10 和 11：

* IBM DB2 for z/OS 11.1
* IBM DB2 for z/OS 10.1
* IBM DB2 for i 7.3
* IBM DB2 for i 7.2
* IBM DB2 for i 7.1
* IBM DB2 for LUW 11
* IBM DB2 for LUW 10.5

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/db2/)的所有限制。 

## <a name="next-steps"></a>後續步驟
[建立邏輯應用程式](../logic-apps/quickstart-create-first-logic-app-workflow.md)。 請到我們的 [API 清單](apis-list.md)探索 Logic Apps 中其他可用的連接器。

