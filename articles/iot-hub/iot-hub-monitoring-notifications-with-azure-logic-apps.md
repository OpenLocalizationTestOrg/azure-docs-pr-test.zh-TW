---
title: "aaaIoT 遠端監視 Azure 邏輯應用程式使用與通知 |Microsoft 文件"
description: "Azure 邏輯應用程式使用的 IoT 溫度監控您的 IoT 中樞並自動傳送電子郵件通知 tooyour 信箱，偵測到任何異常情況。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 監視、iot 通知、iot 溫度監視"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a>搭配連接 IoT 中樞和信箱的 Azure Logic Apps 進行 IoT 遠端監視和通知

![端對端圖表](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Azure 邏輯應用程式提供方式 tooautomate 處理程序，為一系列的步驟。 邏輯應用程式可以連接多種服務和通訊協定。 一開始會有觸發程序，例如「新增帳戶時」，後面接著一連串動作，例如「傳送推播通知」。 此功能可讓 Logic Apps 成為 IoT 監視的絕佳 IoT 解決方案，例如注意異常行為，以及其他使用情況。

## <a name="what-you-learn"></a>您學到什麼

您了解如何 toocreate 邏輯應用程式連接您的 IoT 中樞和溫度監視和通知的信箱。 當 hello 溫度高於 30 C 時，hello 用戶端應用程式標記`temperatureAlert = "true"`hello 訊息中傳送 tooyour IoT 中樞。 觸發程序 hello 邏輯應用程式 toosend hello 訊息您電子郵件通知。

## <a name="what-you-do"></a>您要做什麼

* 建立服務匯流排命名空間並加入佇列 tooit。
* 加入端點和路由規則 tooyour IoT 中樞。
* 建立、設定和測試邏輯應用程式。

## <a name="what-you-need"></a>您需要什麼

* 教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)完成其中涵蓋了 hello 下列需求：
  * 有效的 Azure 訂用帳戶。
  * 位於您訂用帳戶中的 Azure IoT 中樞。
  * 用戶端應用程式所傳送訊息 tooyour Azure IoT 中樞。

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a>建立服務匯流排命名空間，並加入佇列 tooit

### <a name="create-a-service-bus-namespace"></a>建立服務匯流排命名空間

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增** > **企業整合** > **Service Bus**。
1. 提供下列資訊的 hello:

   **名稱**: hello service bus 的 hello 名稱。

   **定價層**︰ 按一下 [基本] > [選取]。 hello 基本層就足以應付本教學課程。

   **資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。

   **位置**： 使用 hello 相同 IoT 中樞使用的位置。
1. 按一下 [建立] 。

   ![在 hello Azure 入口網站中建立服務匯流排命名空間](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a>新增服務匯流排佇列

1. 開啟 hello 服務匯流排命名空間，然後按一下**+ 佇列**。
1. 輸入 hello 佇列的名稱，然後按一下**建立**。
1. 開啟 hello 服務匯流排佇列，然後按一下**共用存取原則** > **+ 加**。
1. 輸入 hello 原則名稱，核取**管理**，然後按一下**建立**。

   ![在 hello Azure 入口網站中加入服務匯流排佇列](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a>加入端點和路由規則 tooyour IoT 中樞

### <a name="add-an-endpoint"></a>新增端點。

1. 開啟 IoT 中樞，並按一下 [端點] > [+ 新增]。
1. 輸入下列資訊的 hello:

   **名稱**: hello hello 端點名稱。

   **端點類型**：選取**服務匯流排佇列**。

   **服務匯流排命名空間**： 選取您所建立的 hello 命名空間。

   **Service Bus 佇列**: hello 選取您所建立的佇列。
1. 按一下 [確定] 。

   ![在 hello Azure 入口網站中加入端點 tooyour IoT 中樞](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a>新增路由規則

1. 在 IoT 中樞，按一下 [路由] > [+ 新增]。
1. 輸入下列資訊的 hello:

   **名稱**: hello hello 路由規則名稱。

   **資料來源**：選取 [裝置訊息]。

   **端點**： 選取您所建立的 hello 端點。

   **查詢字串**：輸入 `temperatureAlert = "true"`。
1. 按一下 [儲存] 。

   ![在 hello Azure 入口網站中加入的路由規則](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a>建立並設定邏輯應用程式

### <a name="create-a-logic-app"></a>建立邏輯應用程式

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增** > **企業整合** > **邏輯應用程式**。
1. 輸入下列資訊的 hello:

   **名稱**: hello hello 邏輯應用程式名稱。

   **資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。

   **位置**： 使用 hello 相同 IoT 中樞使用的位置。
1. 按一下 [建立] 。

### <a name="configure-hello-logic-app"></a>Hello 邏輯應用程式設定

1. 開啟在 hello 邏輯應用程式的設計工具中開啟檔案的 hello 邏輯應用程式。
1. 在 hello 邏輯應用程式的設計工具中，按一下 **空白邏輯應用程式**。

   ![開頭空白的邏輯中的應用程式 hello Azure 入口網站](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. 按一下 [服務匯流排]。

   ![選取服務匯流排 toostart hello Azure 入口網站中建立邏輯應用程式](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. 按一下 [服務匯流排 – 一個或多個訊息到達佇列時 (自動完成)]。
1. 建立服務匯流排連接。
   1. 輸入連線名稱。
   1. 按一下 hello 服務匯流排命名空間 > hello 服務匯流排原則 >**建立**。

      ![在 hello Azure 入口網站中建立應用程式邏輯的服務匯流排連線](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. 按一下**繼續**hello 服務匯流排連線建立之後。
   1. 選取您建立的 hello 佇列，並輸入`175`如**最大訊息數**

      ![指定在邏輯應用程式中的 hello 服務匯流排連線的 hello 最大訊息計數](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. 按一下 [儲存] 按鈕 toosave hello 變更。

1. 建立 SMTP 服務連接。
   1. 按一下 [新增步驟] > [新增動作]。
   1. 型別`SMTP`，按一下 hello **SMTP**在 hello 搜尋結果中，服務，然後按一下**SMTP-傳送電子郵件**。

      ![在 hello Azure 入口網站中的應用程式邏輯中建立 SMTP 連接](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. 輸入您的信箱，hello SMTP 資訊，然後按一下**建立**。

      ![在 hello Azure 入口網站中的應用程式邏輯中輸入 SMTP 連接資訊](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      取得 hello SMTP 資訊[Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970)， [Gmail](https://support.google.com/a/answer/176600?hl=en)，和[Yahoo 郵件](https://help.yahoo.com/kb/SLN4075.html)。
   1. 輸入**寄件者**和**收件者**的電子郵件地址，並對於**主旨**和**內文**輸入 `High temperature detected`。
   1. 按一下 [儲存] 。

hello 邏輯應用程式時將它儲存為工作順序。

## <a name="test-hello-logic-app"></a>測試 hello 邏輯應用程式

1. 開始部署 tooyour 裝置中的 hello 用戶端應用程式[連接 ESP8266 tooAzure IoT 中樞](iot-hub-arduino-huzzah-esp8266-get-started.md)。
1. 增加 hello 環境溫度周圍 hello SensorTag toobe 上方 30 c。例如，光周圍您 SensorTag k。
1. 您應該會收到 hello 邏輯應用程式所傳送的電子郵件通知。

   > [!NOTE]
   > 您的電子郵件服務提供者可能需要 tooverify hello 寄件者識別 toomake 確定這是您傳送嗨電子郵件的人員。

## <a name="next-steps"></a>後續步驟

您已成功建立連接 IoT 中樞的邏輯應用程式，以及溫度監視和通知的信箱。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
