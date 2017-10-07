---
title: "總為 Azure 邏輯應用程式的 Azure 事件中心的事件監視 aaaSet |Microsoft 文件"
description: "監視資料的資料流 tooreceive 事件和事件傳送為 Azure 事件中心的 Azure 邏輯應用程式"
services: logic-apps
keywords: "資料流、事件監視器、事件中樞"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a>監視、 接收和傳送與 hello 事件中心連接器事件

tooset 總事件監視，因此邏輯應用程式可以偵測事件，會接收事件，且事件，傳送連接 tooan [Azure 事件中心](https://azure.microsoft.com/services/event-hubs)從邏輯應用程式。 深入了解 [Azure 事件中樞](../event-hubs/event-hubs-what-is-event-hubs.md)。

## <a name="requirements"></a>需求

* 您有 toohave[事件中樞命名空間和事件中心](../event-hubs/event-hubs-create.md)在 Azure 中。 深入了解[如何 toocreate 事件中樞命名空間和事件中心](../event-hubs/event-hubs-create.md)。 

* toouse[任何連接器](https://docs.microsoft.com/azure/connectors/apis-list)在邏輯應用程式，您必須 toocreate 邏輯應用程式第一次。 深入了解[如何 toocreate 邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a>檢查事件中樞命名空間的權限，並尋找 hello 連接字串

如您邏輯應用程式 tooaccess 任何服務，您有 toocreate [*連接*](./connectors-overview.md)之間邏輯應用程式與 hello 服務，如果您還沒有這麼做。 此連接會授權您 tooaccess 邏輯應用程式的資料。
您的邏輯應用程式 tooaccess 事件中樞，您必須 toohave**管理**權限和 hello 事件中樞命名空間的連接字串。

toocheck 您權限和 get hello 連接字串，請遵循下列步驟。

1.  登入 toohello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。 

2.  移 tooyour 事件中心*命名空間*，不 hello 特定事件中心。 Hello 命名空間 刀鋒視窗底下**設定**，選擇**共用存取原則**。 在 [宣告] 之下，確認您有該命名空間的 [管理] 權限。

    ![管理事件中樞命名空間的權限](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  toocopy hello 連接字串 hello 事件中樞命名空間中，選擇**RootManageSharedAccessKey**。 下一步 tooyour 主索引鍵的連接字串中，選擇 hello 複製 按鈕。

    ![複製事件中樞命名空間連接字串](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > tooconfirm 與事件中樞命名空間或特定的事件中心，相關聯的連接字串是否檢查 hello 連接字串 hello`EntityPath`參數。 如果您發現此參數，hello 連接字串是特定的事件中心 「 實體 」，而非 hello 正確的字串 toouse 邏輯應用程式。

4.  現在當系統提示您輸入認證加入事件中心觸發程序或動作 tooyour 邏輯應用程式之後，您可以連接 tooyour 事件中樞命名空間。 為您的連線指定名稱，輸入 hello 連接字串，複製，再選擇**建立**。

    ![輸入事件中樞命名空間的連接字串](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    建立您的連線之後，hello 連接名稱應該會出現在 hello 事件中心觸發程序或動作。 
    然後，您可以繼續使用 hello 邏輯應用程式中的其他步驟。

    ![已建立事件中樞命名空間連線](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a>在事件中樞收到新事件時啟動工作流程

[觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)是在邏輯應用程式中啟動工作流程的事件。 新的事件傳送 tooyour 事件中樞時，請啟動的工作流程，請遵循下列步驟來新增 hello 觸發程序偵測到此事件。

1.  在 hello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")、 移 tooyour 現有邏輯應用程式，或建立空白的邏輯應用程式。

2.  在 hello hello 邏輯應用程式的設計工具搜尋方塊中輸入`event hubs`用於您篩選條件。 選取此觸發程序︰**當事件可用於事件中樞時**

    ![選取當事件中樞收到新事件時的觸發程序](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    如果您還沒有連接 tooyour 事件中樞命名空間，則會提示您 toocreate 現在這個連線。 指定的名稱，您的連線，並輸入您的事件中樞命名空間 hello 連接字串。 
    如有必要，了解[如何 toofind 連接字串](#permissions-connection-string)。

    ![輸入事件中樞命名空間的連接字串](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    建立 hello 連線之後，hello 設定 hello**內發生事件時使用事件中心**觸發程序會出現。

    ![當事件中樞收到新事件時的觸發程序設定](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  輸入或選取 hello hello 想 toomonitor 事件中樞的名稱。 選取 hello 頻率和間隔 toocheck hello 事件中心的頻率。

    > [!TIP]
    > toooptionally 選取讀取事件的取用者群組中，選擇  **Show advanced 選項**。 

    ![指定事件中樞或取用者群組](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    您現在設定觸發程序 toostart 工作流程應用程式邏輯。 
    應用程式邏輯會檢查 hello 指定根據您設定的 hello 排程的事件中樞。 
    如果您的應用程式中 hello 事件中心，找到新的事件，hello 觸發程序，則會執行其他動作或觸發程序邏輯應用程式中。

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a>從邏輯應用程式傳送事件 tooyour 事件中樞

[動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)是邏輯應用程式工作流程所執行的工作。 新增觸發程序 tooyour 邏輯應用程式之後，您可以加入動作 tooperform 操作該觸發程序所產生的資料。 toosend 事件 tooyour 事件中心從邏輯應用程式，請遵循下列步驟。

1.  在邏輯應用程式設計工具中，於您的邏輯應用程式觸發程序之下，選擇 [新增步驟] > [新增動作]。

    ![選擇 [新增步驟]，然後選擇 [新增動作]](./media/connectors-create-api-azure-event-hubs/add-action.png)

    現在您可以尋找並選取動作 tooperform。 
    雖然您可以選取任何動作，如這個範例中，我們想要 hello 事件中心動作 toosend 事件。

2.  在 [hello] 搜尋方塊中，輸入`event hubs`用於您篩選條件。
選取此動作︰**傳送事件**

    ![選取「事件中樞 - 傳送事件」動作](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  Hello 事件，例如 hello hello 想 toosend hello 事件的事件中樞的名稱，請輸入所需的 hello 詳細資料。 輸入任何其他選擇性 hello 事件，例如，針對該事件內容的相關詳細資料。

    > [!TIP]
    > toooptionally 指定 hello 事件中心資料分割，其中 toosend hello 事件，選擇**Show advanced 選項**。 

    ![輸入事件中樞名稱和選擇性事件詳細資料](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  儲存您的變更。

    ![儲存您的邏輯應用程式](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    您現在已設定動作 toosend 事件，從應用程式邏輯。 

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/eventhubs/)。 

## <a name="get-help"></a>取得說明

tooask 問題、 解答的問題，以及執行其他 Azure 邏輯應用程式使用者，請參閱瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。

toohelp 改善邏輯應用程式和連接器、 票選或送出意見在 hello [Logic Apps 使用者意見反應網站](http://aka.ms/logicapps-wish)。

## <a name="next-steps"></a>後續步驟

*  [尋找 Azure Logic Apps 的其他連接器](./apis-list.md)