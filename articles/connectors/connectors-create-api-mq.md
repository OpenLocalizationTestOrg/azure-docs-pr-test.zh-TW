---
title: "aaaLearn toouse hello Azure 邏輯應用程式中的 MQ 連接器的方式 |Microsoft 文件"
description: "從您的邏輯應用程式工作流程 toobrowse 連接 tooan 內部部署或 Azure MQ 伺服器、 接收和傳送訊息 tooWebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a>從邏輯應用程式使用 hello MQ 連接器連接 tooan IBM MQ 伺服器 

Microsoft Connector for MQ 會傳送並取出儲存在 MQ Server 內部部署或在 Azure 中的訊息。 此連接器包含透過 TCP/IP 網路與遠端 IBM MQ Server 通訊的 Microsoft MQ 用戶端。 這份文件是入門指南 toouse hello MQ 連接器。 我們建議您開始瀏覽到佇列中，單一訊息，然後嘗試 hello 其他動作。    

hello MQ 連接器包括下列動作的 hello。 但不包含觸發程序。

-   瀏覽單一訊息，而不從 hello IBM MQ Server 刪除 hello 訊息
-   瀏覽訊息批次，但不會刪除從 hello IBM MQ 伺服器 hello 訊息
-   接收單一訊息，並從 hello IBM MQ Server 刪除 hello 訊息
-   接收的訊息批次，並從 hello IBM MQ Server 刪除 hello 訊息
-   傳送單一訊息 toohello IBM MQ Server 

## <a name="prerequisites"></a>必要條件

* 如果使用內部部署 MQ server 上，[安裝 hello 在內部部署資料閘道](../logic-apps/logic-apps-gateway-install.md)網路內之伺服器上。 如果 hello MQ Server 上公開使用，或在 Azure 中可用，然後 hello data gateway 已無法使用或所需。

    > [!NOTE]
    > hello 伺服器其中 hello 安裝在內部部署資料閘道也必須有.Net Framework 4.6 安裝 hello MQ 連接器 toofunction。

* 建立 Azure 資源 hello 在內部部署資料閘道-hello [hello 資料閘道連接設定](../logic-apps/logic-apps-gateway-connection.md)。

* 正式支援的 IBM WebSphere MQ 版本：
   * MQ 7.5
   * MQ 8.0

## <a name="create-a-logic-app"></a>建立邏輯應用程式

1. 在 hello **Azure 開始面板**，選取 **+**  （加號） **Web + 行動**，，然後**邏輯應用程式**。 
2. 輸入 hello**名稱**，例如 MQTestApp，**訂用帳戶**，**資源群組**，和**位置**（使用 hello 位置，其中 hello在內部部署資料閘道連線已設定）。 選取**Pin toodashboard**，然後選取**建立**。  
![建立邏輯應用程式](media/connectors-create-api-mq/Create_Logic_App.png)

## <a name="add-a-trigger"></a>新增觸發程序

> [!NOTE]
> hello MQ 連接器並沒有任何觸發程序。 因此，使用另一個觸發程序 toostart 邏輯應用程式，例如 hello**循環**觸發程序。 

1. hello**邏輯應用程式設計師**隨即開啟，選取**循環**hello 一般的觸發程序清單中。
2. 選取**編輯**hello 循環觸發程序內。 
3. 設定 hello**頻率**太**天**，和集合 hello**間隔**太**7**。 

## <a name="browse-a-single-message"></a>瀏覽單一訊息
1. 選取 [+ 新增步驟]，再選取 [新增動作]。
2. 在 [hello] 搜尋方塊中，輸入`mq`，然後選取**MQ-瀏覽訊息**。  
![瀏覽訊息](media/connectors-create-api-mq/Browse_message.png)

3. 如果沒有現有的 MQ 連接，然後建立 hello 連線：  

    1. 選取**連接透過內部部署資料閘道**，然後輸入 hello MQ 伺服器屬性。  
    如**伺服器**，您可以輸入 hello MQ 的伺服器名稱，或輸入 hello IP 位址，後面接著冒號和 hello 的連接埠號碼。 
    2. hello**閘道**下拉式清單中列出的任何現有的閘道連線已設定。 選取您的閘道。
    3. 完成後，請選取 [建立]。 您的連線看起來類似 toohello 下列：   
    ![連線屬性](media/connectors-create-api-mq/Connection_Properties.png)

4. 在 hello 動作屬性，您可以：  

    * 使用 hello**佇列**屬性 tooaccess 比 hello 連接中所定義不同的佇列名稱
    * 使用 hello **MessageId**， **CorrelationId**， **GroupId**，和其他的屬性 toobrowse hello 不同 MQ 訊息屬性為基礎的訊息
    * 設定**IncludeInfo**太**True** tooinclude hello 輸出中的其他訊息資訊。 或者，您也可以設定得**False** toonot hello 輸出中包含額外的訊息資訊。
    * 輸入**逾時**toodetermine 值為空的佇列中訊息 tooarrive 多久 toowait。 如果輸入任何內容，擷取 hello hello 佇列中的第一個訊息，並沒有時間花在等待訊息 tooappear。  
    ![瀏覽訊息屬性](media/connectors-create-api-mq/Browse_message_Props.png)

5. [儲存] 您的變更，然後 [執行] 邏輯應用程式：  
![儲存並執行](media/connectors-create-api-mq/Save_Run.png)

6. 幾秒之後，執行 hello hello 步驟會顯示，而且您可以查看 hello 輸出。 選取每個步驟的 hello 綠色核取記號 toosee 詳細資料。 選取**看到原始輸出**toosee hello 的其他詳細資料輸出資料。  
![瀏覽訊息輸出](media/connectors-create-api-mq/Browse_message_output.png)  

    原始輸出：  
    ![瀏覽訊息原始輸出](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. 當 hello **IncludeInfo** tootrue 設定選項時，會顯示下列輸出的 hello:  
![瀏覽訊息包含資訊](media/connectors-create-api-mq/Browse_message_Include_Info.png)

## <a name="browse-multiple-messages"></a>瀏覽多個訊息
hello**瀏覽訊息**動作包含**BatchSize**選項 tooindicate 應該從 hello 佇列傳回的訊息數量。  如果 **BatchSize** 沒有項目，就會傳回所有的訊息。 hello 傳回輸出的訊息陣列。

1. 當加入 hello**瀏覽訊息**hello 第一個連接所設定的動作，依預設會選取。 選取**變更連接**toocreate 新的連接，或選取不同的連接。

2. 若要瀏覽 hello 輸出訊息所示：  
![瀏覽訊息輸出](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a>接收單一訊息
hello**接收訊息**動作已為 hello hello 相同輸入和輸出**瀏覽訊息**動作。 當使用**接收訊息**，hello 訊息從 hello 佇列中刪除。

## <a name="receive-multiple-messages"></a>接收多個訊息
hello**接收訊息**動作已為 hello hello 相同輸入和輸出**瀏覽訊息**動作。 當使用**接收訊息**，hello 訊息會從 hello 佇列中刪除。

如果有任何訊息 hello 佇列中進行瀏覽 」 或 「 接收時，hello 步驟失敗 hello 下列輸出：  
![MQ 無訊息錯誤](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a>傳送訊息
1. 當加入 hello**傳送訊息**hello 第一個連接所設定的動作，依預設會選取。 選取**變更連接**toocreate 新的連接，或選取不同的連接。 有效的 hello**訊息類型**是**資料包**，**回覆**，或**要求**。  
![傳送訊息屬性](media/connectors-create-api-mq/Send_Msg_Props.png)

2. hello 傳送訊息的輸出看起來像下列 hello:  
![傳送訊息輸出](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/mq/)。

## <a name="next-steps"></a>後續步驟
[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。 瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。
