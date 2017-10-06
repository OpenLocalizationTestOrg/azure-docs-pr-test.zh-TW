---
title: "在您的 Logic Apps aaaAdd hello DB2 連接器 |Microsoft 文件"
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
ms.openlocfilehash: d836c61231d3c9cfdb30ff9c40a48b1718f3ffb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-db2-connector"></a>開始使用 hello DB2 連接器
Microsoft connector for DB2 連接儲存在 IBM DB2 資料庫中的 Logic Apps tooresources。 此連接器會包括 Microsoft 用戶端 toocommunicate 遠端 DB2 伺服器電腦與跨 TCP/IP 網路。 這包括雲端資料庫，例如 IBM Bluemix dashDB 或 IBM DB2 for Windows Azure 的虛擬化，以執行，並在內部部署資料庫時使用 hello 在內部部署資料閘道。 請參閱 hello[支援清單](connectors-create-api-db2.md#supported-db2-platforms-and-versions)的 IBM DB2 平台和版本 （在本主題中）。

hello DB2 連接器支援下列資料庫作業的 hello:

* 列出資料庫資料表
* 使用 SELECT 讀取一個資料列
* 使用 SELECT 讀取所有資料列
* 使用 INSERT 加入一個資料列
* 使用 UPDATE 變更一個資料列
* 使用 DELETE 移除一個資料列

本主題說明如何在邏輯應用程式 tooprocess toouse hello 連接器資料庫作業。

toolearn 進一步了解邏輯應用程式，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="available-actions"></a>可用動作
hello DB2 連接器支援下列邏輯應用程式動作的 hello:

* GetTables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>列出資料表
建立邏輯應用程式的任何作業包括透過 hello Microsoft Azure 入口網站中執行的許多步驟。

在 hello 邏輯 app 中，您可以加入動作 toolist 資料表 DB2 資料庫中。 hello 動作會指示 hello 連接器 tooprocess DB2 結構描述陳述式，例如`CALL SYSIBM.SQLTABLES`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 hello **Azure 開始面板**，選取 **+**  （加號） **Web + 行動**，，然後**邏輯應用程式**。
2. 輸入 hello**名稱**，例如`Db2getTables`，**訂用帳戶**，**資源群組**，**位置**，和**應用程式服務計劃**。 選取**Pin toodashboard**，然後選取**建立**。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 hello**邏輯應用程式的設計工具**，選取**空白 LogicApp**在 hello**範本**清單。
2. 在 hello**觸發程序**清單中，選取**循環**。 
3. 在 hello**循環**觸發程序，選取**編輯**，選取**頻率**下拉式 tooselect**天**，然後設定 hello **間隔**tootype **7**。  
4. 選取 hello **+ 新增步驟**方塊，並選取**將動作加入**。
5. 在 hello**動作**清單中，輸入`db2`hello 中**搜尋更多動作**編輯方塊中，然後選取  **DB2-Get 資料表 （預覽）**。
   
   ![](./media/connectors-create-api-db2/Db2connectorActions.png)  
6. 在 hello **DB2-Get 資料表**設定窗格中，選取**核取方塊**tooenable**連接透過內部部署資料閘道**。 請注意，從雲端 tooon 內部部署的 hello 設定變更。
   
   * 輸入值**伺服器**，hello 形式的地址或別名冒號連接埠號碼。 例如，輸入 `ibmserver01:50000`。
   * 輸入 [資料庫] 的值。 例如，輸入 `nwind`。
   * 選取 [驗證] 的值。 例如，選取 [基本] 。
   * 輸入 [使用者名稱] 的值。 例如，輸入 `db2admin`。
   * 輸入 [密碼] 的值。 例如，輸入 `Password1`。
   * 選取 [閘道] 的值。 例如，選取 [datagateway01] 。
7. 選取 [建立]，然後選取 [儲存]。 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)
8. 在 hello **Db2getTables**刀鋒視窗中的，內 hello**所有執行**清單下**摘要**，選取 hello 第一個列出的項目 （最新的執行）。
9. 在 hello**邏輯應用程式執行**刀鋒視窗中，選取**執行詳細資料**。 在 hello**動作**清單中，選取**Get_tables**。 請參閱 hello 值**狀態**，應該**Succeeded**。 選取 hello**輸入連結**tooview hello 輸入。 選取 hello**輸出連結**，檢視 hello 輸出之後，它應該包含的資料表清單。
   
   ![](./media/connectors-create-api-db2/Db2connectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>建立 hello 連線
此連接器支援連線 toodatabases 裝載內部部署和 hello 雲端中使用 hello 下列連接屬性。 

| 屬性 | 說明 |
| --- | --- |
| 伺服器 |必要。 接受代表 TCP/IP 位址或別名的字串值，其採用 IPv4 或 IPv6 格式，後面接著 (以冒號分隔) TCP/IP 連接埠編號。 |
| 資料庫 |必要。 接受代表 DRDA 關聯式資料庫名稱 (RDBNAM) 的字串值。 DB2 for z/OS 接受 16 個位元組的字串 (資料庫也稱為 IBM DB2 for z/OS 位置)。 DB2 for i5/OS 接受 18 個位元組的字串 (資料庫也稱為 IBM DB2 for i 關聯式資料庫)。 DB2 for LUW 接受 8 個位元組的字串。 |
| 驗證 |選用。 接受清單項目值 (基本或 Windows (kerberos))。 |
| username |必要。 接受字串值。 DB2 for z/OS 接受 8 個位元組的字串。 DB2 for i 接受 10 個位元組的字串。 DB2 for Linux 或 UNIX 接受 8 個位元組的字串。 DB2 for Windows 接受 30 個位元組的字串。 |
| password |必要。 接受字串值。 |
| gateway |必要。 接受代表 hello 在內部部署資料閘道定義 tooLogic 應用程式內 hello 儲存群組的清單項目值。 |

## <a name="create-hello-on-premises-gateway-connection"></a>建立 hello 內部部署閘道連接
此連接器可以存取使用 hello 在內部部署閘道的內部部署 DB2 資料庫。 如需詳細資訊，請參閱閘道主題。 

1. 在 hello**閘道**設定窗格中，選取**核取方塊**tooenable**透過閘道連接**。 請注意，從雲端 tooon 內部部署的 hello 設定變更。
2. 輸入值**伺服器**，hello 形式的地址或別名冒號連接埠號碼。 例如，輸入 `ibmserver01:50000`。
3. 輸入 [資料庫] 的值。 例如，輸入 `nwind`。
4. 選取 [驗證] 的值。 例如，選取 [基本] 。
5. 輸入 [使用者名稱] 的值。 例如，輸入 `db2admin`。
6. 輸入 [密碼] 的值。 例如，輸入 `Password1`。
7. 選取 [閘道] 的值。 例如，選取 [datagateway01] 。
8. 選取**建立**toocontinue。 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>建立 hello 雲端連線
此連接器可以存取雲端 DB2 資料庫。 

1. 在 hello**閘道**設定窗格中，保留 hello**核取方塊**（過） 已停用**透過閘道連接**。 
2. 輸入 [連線名稱] 的值。 例如，輸入 `hisdemo2`。
3. 輸入值**DB2 伺服器名稱**，hello 形式的地址或別名冒號連接埠號碼。 例如，輸入 `hisdemo2.cloudapp.net:50000`。
4. 輸入 [DB2 資料庫名稱] 的值。 例如，輸入 `nwind`。
5. 輸入 [使用者名稱] 的值。 例如，輸入 `db2admin`。
6. 輸入 [密碼] 的值。 例如，輸入 `Password1`。
7. 選取**建立**toocontinue。 
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>使用 SELECT 擷取所有資料列
您可以定義邏輯應用程式動作 toofetch 所有資料列，在 DB2 資料表。 這會指示 hello 連接器 tooprocess DB2 SELECT 陳述式，例如`SELECT * FROM AREA`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 hello **Azure 開始面板**，選取 **+**  （加號） **Web + 行動**，，然後**邏輯應用程式**。
2. 輸入 hello**名稱**，例如`Db2getRows`，**訂用帳戶**，**資源群組**，**位置**，和**應用程式服務計劃**。 選取**Pin toodashboard**，然後選取**建立**。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 hello**邏輯應用程式的設計工具**，選取**空白 LogicApp**在 hello**範本**清單。
2. 在 hello**觸發程序**清單中，選取**循環**。 
3. 在 hello**循環**觸發程序，選取**編輯**，選取**頻率**下拉式 tooselect**天**，然後選取**間隔**tootype **7**。 
4. 選取 hello **+ 新增步驟**方塊，並選取**將動作加入**。
5. 在 hello**動作**清單中，輸入`db2`hello 中**搜尋更多動作**編輯方塊中，然後選取  **DB2-取得資料列 （預覽）**。
6. 在 hello**取得資料列 （預覽）**動作選取**變更連接**。
7. 在 hello**連線**設定窗格中，選取**建立新**。 
   
    ![](./media/connectors-create-api-db2/Db2connectorNewConnection.png)
8. 在 hello**閘道**設定窗格中，保留 hello**核取方塊**（過） 已停用**透過閘道連接**。
   
   * 輸入 [連線名稱] 的值。 例如，輸入 `HISDEMO2`。
   * 輸入值**DB2 伺服器名稱**，hello 形式的地址或別名冒號連接埠號碼。 例如，輸入 `HISDEMO2.cloudapp.net:50000`。
   * 輸入 [DB2 資料庫名稱] 的值。 例如，輸入 `NWIND`。
   * 輸入 [使用者名稱] 的值。 例如，輸入 `db2admin`。
   * 輸入 [密碼] 的值。 例如，輸入 `Password1`。
9. 選取**建立**toocontinue。
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)
10. 在 hello**資料表名稱**清單中，選取 hello**向下箭號**，然後選取**區域**。
11. （選擇性） 選取**Show advanced 選項**toospecify 查詢選項。
12. 選取 [ **儲存**]。 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsTableName.png)
13. 在 hello **Db2getRows**刀鋒視窗中的，內 hello**所有執行**清單下**摘要**，選取 hello 第一個列出的項目 （最新的執行）。
14. 在 hello**邏輯應用程式執行**刀鋒視窗中，選取**執行詳細資料**。 在 hello**動作**清單中，選取**Get_rows**。 請參閱 hello 值**狀態**，應該**Succeeded**。 選取 hello**輸入連結**tooview hello 輸入。 選取 hello**輸出連結**，檢視 hello 輸出之後，它應該包含的資料列清單。
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>使用 INSERT 加入一個資料列
您可以定義邏輯應用程式動作 tooadd 一個資料列中的 DB2 資料表。 這個動作會指示 hello 連接器 tooprocess DB2 INSERT 陳述式，例如`INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 hello **Azure 開始面板**，選取 **+**  （加號） **Web + 行動**，，然後**邏輯應用程式**。
2. 輸入 hello**名稱**，例如`Db2insertRow`，**訂用帳戶**，**資源群組**，**位置**，和**應用程式服務計劃**。 選取**Pin toodashboard**，然後選取**建立**。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 hello**邏輯應用程式的設計工具**，選取**空白 LogicApp**在 hello**範本**清單。
2. 在 hello**觸發程序**清單中，選取**循環**。 
3. 在 hello**循環**觸發程序，選取**編輯**，選取**頻率**下拉式 tooselect**天**，然後選取**間隔**tootype **7**。 
4. 選取 hello **+ 新增步驟**方塊，並選取**將動作加入**。
5. 在 hello**動作**清單中，輸入**db2** hello 中**搜尋更多動作**編輯方塊中，然後選取  **DB2-插入資料列 （預覽）**。
6. 在 hello **DB2-插入資料列 （預覽）**動作選取**變更連接**。 
7. 在 [hello**連線**組態] 窗格中，選取連線。 例如，選取 [hisdemo2] 。
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. 在 hello**資料表名稱**清單中，選取 hello**向下箭號**，然後選取**區域**。
9. 輸入所有必要資料行 (請見紅色星號) 的值。 例如，針對 [AREAID] 輸入 `99999`、輸入 `Area 99999`，以及針對 [REGIONID] 輸入 `102`。 
10. 選取 [ **儲存**]。
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowValues.png)
11. 在 hello **Db2insertRow**刀鋒視窗中的，內 hello**所有執行**清單下**摘要**，選取 hello 第一個列出的項目 （最新的執行）。
12. 在 hello**邏輯應用程式執行**刀鋒視窗中，選取**執行詳細資料**。 在 hello**動作**清單中，選取**Get_rows**。 請參閱 hello 值**狀態**，應該**Succeeded**。 選取 hello**輸入連結**tooview hello 輸入。 選取 hello**輸出連結**，檢視 hello 輸出之後，應該包括 hello 新的資料列。
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>使用 SELECT 擷取一個資料列
您可以定義邏輯應用程式動作 toofetch 一個資料列中的 DB2 資料表。 這個動作會指示 hello 連接器 tooprocess DB2 選取 WHERE 陳述式，例如`SELECT FROM AREA WHERE AREAID = '99999'`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 hello **Azure 開始面板**，選取 **+**  （加號） **Web + 行動**，，然後**邏輯應用程式**。
2. 輸入 hello**名稱**（例如："**Db2getRow**")、[訂用帳戶]、[資源群組]、[位置] 和 [App Service 方案]。 選取**Pin toodashboard**，然後選取**建立**。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 hello**邏輯應用程式的設計工具**，選取**空白 LogicApp**在 hello**範本**清單。 
2. 在 hello**觸發程序**清單中，選取**循環**。 
3. 在 hello**循環**觸發程序，選取**編輯**，選取**頻率**下拉式 tooselect**天**，然後選取**間隔**tootype **7**。 
4. 選取 hello **+ 新增步驟**方塊，並選取**將動作加入**。
5. 在 hello**動作**清單中，輸入**db2** hello 中**搜尋更多動作**編輯方塊中，然後選取  **DB2-取得資料列 （預覽）**。
6. 在 hello**取得資料列 （預覽）**動作選取**變更連接**。 
7. 在 [hello**連線**設定] 窗格中，選取現有的連接。 例如，選取 [hisdemo2] 。
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. 在 hello**資料表名稱**清單中，選取 hello**向下箭號**，然後選取**區域**。
9. 輸入所有必要資料行 (請見紅色星號) 的值。 例如，針對 [AREAID] 輸入 `99999`。 
10. （選擇性） 選取**Show advanced 選項**toospecify 查詢選項。
11. 選取 [ **儲存**]。 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowValues.png)
12. 在 hello **Db2getRow**刀鋒視窗中的，內 hello**所有執行**清單下**摘要**，選取 hello 第一個列出的項目 （最新的執行）。
13. 在 hello**邏輯應用程式執行**刀鋒視窗中，選取**執行詳細資料**。 在 hello**動作**清單中，選取**Get_rows**。 請參閱 hello 值**狀態**，應該**Succeeded**。 選取 hello**輸入連結**tooview hello 輸入。 選取 hello**輸出連結**，檢視 hello 輸出之後，它應該包含資料列。
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>使用 UPDATE 變更資料列
您可以定義邏輯應用程式動作 toochange 一個資料列中的 DB2 資料表。 這個動作會指示 hello 連接器 tooprocess DB2 UPDATE 陳述式中，例如`UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 hello **Azure 開始面板**，選取 **+**  （加號） **Web + 行動**，，然後**邏輯應用程式**。
2. 輸入 hello**名稱**，例如`Db2updateRow`，**訂用帳戶**，**資源群組**，**位置**，和**應用程式服務計劃**。 選取**Pin toodashboard**，然後選取**建立**。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 hello**邏輯應用程式的設計工具**，選取**空白 LogicApp**在 hello**範本**清單。
2. 在 hello**觸發程序**清單中，選取**循環**。 
3. 在 hello**循環**觸發程序，選取**編輯**，選取**頻率**下拉式 tooselect**天**，然後選取**間隔**tootype **7**。 
4. 選取 hello **+ 新增步驟**方塊，並選取**將動作加入**。
5. 在 hello**動作**清單中，輸入**db2** hello 中**搜尋更多動作**編輯方塊中，然後選取  **DB2-更新資料列 （預覽）**。
6. 在 hello **DB2-更新資料列 （預覽）**動作選取**變更連接**。 
7. 在 [hello**連線**設定] 窗格中，選取 tooselect 現有的連接。 例如，選取 [hisdemo2] 。
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. 在 hello**資料表名稱**清單中，選取 hello**向下箭號**，然後選取**區域**。
9. 輸入所有必要資料行 (請見紅色星號) 的值。 例如，針對 [AREAID] 輸入 `99999`、輸入 `Updated 99999`，以及針對 [REGIONID] 輸入 `102`。 
10. 選取 [ **儲存**]。 
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowValues.png)
11. 在 hello **Db2updateRow**刀鋒視窗中的，內 hello**所有執行**清單下**摘要**，選取 hello 第一個列出的項目 （最新的執行）。
12. 在 hello**邏輯應用程式執行**刀鋒視窗中，選取**執行詳細資料**。 在 hello**動作**清單中，選取**Get_rows**。 請參閱 hello 值**狀態**，應該**Succeeded**。 選取 hello**輸入連結**tooview hello 輸入。 選取 hello**輸出連結**，檢視 hello 輸出之後，應該包括 hello 新的資料列。
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>使用 DELETE 移除一個資料列
您可以定義邏輯應用程式動作 tooremove 一個資料列中的 DB2 資料表。 這個動作會指示 hello 連接器 tooprocess DB2 刪除陳述式，例如`DELETE FROM AREA WHERE AREAID = '99999'`。

### <a name="create-a-logic-app"></a>建立邏輯應用程式
1. 在 hello **Azure 開始面板**，選取 **+**  （加號） **Web + 行動**，，然後**邏輯應用程式**。
2. 輸入 hello**名稱**，例如`Db2deleteRow`，**訂用帳戶**，**資源群組**，**位置**，和**應用程式服務計劃**。 選取**Pin toodashboard**，然後選取**建立**。

### <a name="add-a-trigger-and-action"></a>新增觸發程序和動作
1. 在 hello**邏輯應用程式的設計工具**，選取**空白 LogicApp**在 hello**範本**清單。 
2. 在 hello**觸發程序**清單中，選取**循環**。 
3. 在 hello**循環**觸發程序，選取**編輯**，選取**頻率**下拉式 tooselect**天**，然後選取**間隔**tootype **7**。 
4. 選取 hello **+ 新增步驟**方塊，並選取**將動作加入**。
5. 在 hello**動作**清單中，選取**db2** hello 中**搜尋更多動作**編輯方塊中，然後選取  **DB2-刪除資料列 （預覽）**。
6. 在 hello **DB2-刪除資料列 （預覽）**動作選取**變更連接**。 
7. 在 [hello**連線**設定] 窗格中，選取現有的連接。 例如，選取 [hisdemo2] 。
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. 在 hello**資料表名稱**清單中，選取 hello**向下箭號**，然後選取**區域**。
9. 輸入所有必要資料行 (請見紅色星號) 的值。 例如，針對 [AREAID] 輸入 `99999`。 
10. 選取 [ **儲存**]。 
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowValues.png)
11. 在 hello **Db2deleteRow**刀鋒視窗中的，內 hello**所有執行**清單下**摘要**，選取 hello 第一個列出的項目 （最新的執行）。
12. 在 hello**邏輯應用程式執行**刀鋒視窗中，選取**執行詳細資料**。 在 hello**動作**清單中，選取**Get_rows**。 請參閱 hello 值**狀態**，應該**Succeeded**。 選取 hello**輸入連結**tooview hello 輸入。 選取 hello**輸出連結**，檢視 hello 輸出之後，應該包括 hello 刪除資料列。
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowOutputs.png)

## <a name="supported-db2-platforms-and-versions"></a>支援的 DB2 平台和版本
此連接器支援下列 IBM DB2 平台和版本，以及 IBM DB2 相容的產品 (例如 IBM Bluemix dashDB) 支援分散式關聯式資料庫架構 (DRDA) SQL Access Manager (SQLAM) 版本 10 和 11 hello:

* IBM DB2 for z/OS 11.1
* IBM DB2 for z/OS 10.1
* IBM DB2 for i 7.3
* IBM DB2 for i 7.2
* IBM DB2 for i 7.1
* IBM DB2 for LUW 11
* IBM DB2 for LUW 10.5

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/db2/)。 

## <a name="next-steps"></a>後續步驟
[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。 瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。

