---
title: "Azure 邏輯應用程式中的 aaaAdd hello Oracle 資料庫連接器 |Microsoft 文件"
description: "在邏輯應用程式中使用 hello Oracle 資料庫連接器"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>開始使用 hello Oracle 資料庫連接器

使用 hello Oracle 資料庫連接器，您建立組織中現有的資料庫使用資料的工作流程。 此連接器可以連線的 tooan 安裝在內部部署 Oracle 資料庫或 Azure 虛擬機器與 Oracle 資料庫。 您可以使用此連接器來：

* 建置您的工作流程加入新的客戶 tooa 客戶資料庫，或更新訂單 」 資料庫中的訂單。
* 使用動作 tooget 資料列、 插入新資料列，並且甚至刪除。 例如，在 Dynamics CRM Online 中建立記錄時 (觸發程序)，就會在 Oracle Database 中插入資料列 (動作)。 

本主題說明如何 toouse hello 邏輯應用程式中的 Oracle 資料庫連接器。

## <a name="prerequisites"></a>必要條件

* 支援的 Oracle 版本： 
    * Oracle 9 和更新版本
    * Oracle 用戶端軟體 8.1.7 和更新版本

* 安裝 hello 在內部部署資料閘道。 [Tooon 內部部署資料連接的 logic apps 從](../logic-apps/logic-apps-gateway-connection.md)清單 hello 步驟。 在內部部署 Oracle 資料庫或以 Oracle DB 安裝 Azure VM 需要的 tooconnect tooan hello 閘道。 

    > [!NOTE]
    > hello 在內部部署資料閘道作為橋接器，並提供在內部部署資料 （不在 hello 雲端的資料） 與您的 logic apps 之間的安全資料傳輸。 hello 相同閘道器可以使用多個服務，與多個資料來源。 因此，您可能只需要 tooinstall hello 閘道一次。

* Hello hello 在內部部署資料閘道的安裝所在的電腦上安裝 Oracle 用戶端 hello。 請務必從 Oracle 的.NET tooinstall hello 64 位元 Oracle 資料提供者：  

  [適用於 Windows x64 的 64 位元 ODAC 12c 版本 4 (12.1.0.2.4)](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > 如果未安裝 hello Oracle 用戶端，嘗試 toocreate 或使用 hello 連線時，也會發生錯誤。 請參閱本主題中的 hello 常見錯誤。


## <a name="add-hello-connector"></a>新增 hello 連接器

> [!IMPORTANT]
> 此連接器並沒有任何觸發程序。 只有動作。 因此當您建立應用程式邏輯，加入另一個觸發程序 toostart 應用程式邏輯，例如**排程-循環**，或**要求 / 回應-回應**。 

1. 在 hello [Azure 入口網站](https://portal.azure.com)，建立空白的邏輯應用程式。

2. 在 hello 啟動邏輯應用程式中，選取 hello**要求 / 回應-要求**觸發程序： 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. 選取 [ **儲存**]。 當您儲存時，系統會自動生產生一個要求 URL。 

4. 選取 [新增步驟]，再選取 [新增動作]。 在中輸入`oracle`toosee hello 可用的動作： 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > 這也是最快方式 toosee hello hello 觸發程序和任何連接器可用動作。 輸入名稱的一部分 hello 連接器， `oracle`。 hello 設計工具會列出任何觸發程序和任何動作。 

5. 選取其中一個 hello 動作，例如**Oracle 資料庫-取得資料列**。 選取 [透過內部部署資料閘道連線]。 輸入 hello Oracle 伺服器名稱、 驗證方法、 使用者名稱、 密碼和選取 hello 閘道：

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. 一旦連接之後，從 [hello] 清單中，選取資料表，然後輸入 hello 資料列識別碼 tooyour 資料表。 您需要 tooknow hello 識別碼 toohello 資料表。 如果您不知道，請連絡您的 Oracle 資料庫管理員，並取得 hello 輸出`select * from yourTableName`。 這讓 hello 需要 tooproceed 的識別資訊。

    在下列範例的 hello 中, 從人力資源資料庫傳回作業資料： 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. 在下一個步驟中，您可以使用任何 hello 其他連接器 toobuild 您的工作流程。 如果您想要從 Oracle、 tootest 取得資料，然後傳送給自己使用其中一種 hello hello Oracle 資料的電子郵件傳送電子郵件連接器，這類的 Office 365 或 Gmail。 使用來自 hello Oracle 資料表 toobuild hello hello 動態權杖`Subject`和`Body`的電子郵件：

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. **儲存**您的邏輯應用程式，接著選取 [執行]。 關閉 hello 設計工具，並查看 hello hello 狀態的執行歷程記錄。 如果失敗，請選取 hello 失敗的訊息資料列。 hello designer 隨即開啟，並顯示您哪個步驟失敗，以及顯示 hello 資訊時發生錯誤。 如果成功，您應該收到含有您所新增的 hello 資訊的電子郵件。


### <a name="workflow-ideas"></a>工作流程想法

* 您想 toomonitor hello #oracle 雜湊標記，並放在資料庫中的 hello 推文，才能查詢，以及其他應用程式中使用。 在邏輯應用程式中，新增 hello`Twitter - When a new tweet is posted`觸發程序，然後輸入 hello **#oracle**雜湊標記。 接著，新增 hello`Oracle Database - Insert row`動作，然後選取您的資料表：

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* Tooa Service Bus 佇列時，會傳送訊息。 您想 tooget 這些訊息，並將它們放在資料庫中。 在邏輯應用程式中，新增 hello`Service Bus - when a message is received in a queue`觸發程序，並選取 hello 佇列。 接著，新增 hello`Oracle Database - Insert row`動作，然後選取您的資料表：

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>常見錯誤

#### <a name="error-cannot-reach-hello-gateway"></a>**錯誤**： 無法連線到閘道 hello

**可能的原因**: hello 在內部部署資料閘道不能 tooconnect toohello 雲端。 

**風險降低**： 請確定您的閘道器正在執行 hello 在內部部署電腦上，您已安裝，它可以連接 toohello 網際網路。  我們建議不要安裝 hello 閘道可能已關閉的電腦或睡眠狀態。 您也可以重新啟動 hello 在內部部署資料閘道器服務 (2147463168 PBIEgwService)。

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**錯誤**: hello 所使用的提供者已過時: ' system.data.oracleclient 需有 Oracle 用戶端軟體 8.1.7 或更新版本。 '。 請瀏覽[https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello 官方提供者。

**可能的原因**: hello Oracle 用戶端在 hello，hello 電腦未安裝 SDK 在內部部署資料閘道正在執行。  

**解析**： 上下載並安裝 Oracle 用戶端 hello SDK hello 與 hello 在內部部署資料閘道相同的電腦。

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**錯誤**：資料表 '[Tablename]' 並未定義任何索引鍵資料行

**可能的原因**: hello 資料表沒有任何主索引鍵。  

**解析**: hello Oracle 資料庫連接器需要有用於具有主索引鍵資料行的資料表。

#### <a name="currently-not-supported"></a>目前不支援

* 檢視和已存程序 
* 包含複合索引鍵的任何資料表
* 資料表中的巢狀物件類型
 
## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/oracle/)。 

## <a name="get-some-help"></a>取得協助

hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)優越放置 tooask 問題、 回答的問題，以及查看其他邏輯應用程式使用者所執行的動作。 

您可以投票並在 [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish) 中提交意見，協助改善 Logic Apps 和連接器。 


## <a name="next-steps"></a>後續步驟
[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)，並瀏覽 hello 在邏輯應用程式中可用的連接器我們[Api 清單](apis-list.md)。
