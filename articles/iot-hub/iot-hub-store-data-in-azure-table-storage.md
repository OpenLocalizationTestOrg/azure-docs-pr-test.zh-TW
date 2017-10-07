---
title: "aaaSave IoT 中樞訊息 tooAzure 資料存放區 |Microsoft 文件"
description: "使用 Azure 的函式應用程式 toosave 您的 IoT 中樞訊息 tooyour Azure 資料表儲存體。 hello IoT 中樞訊息包含的資訊，例如傳送從 IoT 裝置感應器資料。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 資料儲存體, iot 感應器資料存儲存體"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a>儲存包含感應器資料 tooyour Azure 資料表儲存體的 IoT 中樞訊息

![端對端圖表](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>您學到什麼

您了解如何 toocreate Azure 儲存體帳戶和 Azure 函式應用程式在您的資料表儲存體 toostore IoT 中樞訊息。

## <a name="what-you-do"></a>您要做什麼

- 建立 Azure 儲存體帳戶。
- 準備您的 IoT 中樞連接 tooread 訊息。
- 建立並部署 Azure 函式應用程式。

## <a name="what-you-need"></a>您需要什麼

- [將裝置設定](iot-hub-raspberry-pi-kit-node-get-started.md)toocover hello 下列需求：
  - 作用中的 Azure 訂用帳戶
  - 您訂用帳戶下的 IoT 中樞 
  - 執行的應用程式所傳送訊息 tooyour IoT 中樞

## <a name="create-an-azure-storage-account"></a>建立 Azure 儲存體帳戶

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增** > **儲存體** > **儲存體帳戶** >  **建立**。

2. 輸入 hello hello 儲存體帳戶的必要資訊：

   ![在 hello Azure 入口網站中建立儲存體帳戶](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **名稱**: hello hello 儲存體帳戶名稱。 hello 名稱必須是全域唯一的。

   * **資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。

   * **Pin toodashboard**： 選取此選項，讓您輕鬆存取 tooyour IoT 中樞從 hello 儀表板。

3. 按一下 [建立] 。

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a>準備您的 IoT 中樞連接 tooread 訊息

IoT 中樞公開內建事件中樞相容端點 tooenable 應用程式 tooread IoT 中樞訊息。 同時，應用程式使用 IoT 中樞取用者群組 tooread 資料。 從您的 IoT 中樞建立 Azure 的函式應用程式 tooread 資料之前，請勿 hello 遵循：

- 收到 hello 的 IoT 中心端點的連接字串。
- 為 IoT 中樞建立取用者群組。

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a>取得 hello 的 IoT 中心端點的連接字串

1. 開啟 IoT 中樞。

2. 在 hello **IoT 中樞**窗格下**傳訊**，按一下**端點**。

3. 在 hello 右窗格中，在**內建端點**，按一下 **事件**。

4. 在 hello**屬性**窗格中，注意 hello 下列值：
   - 事件中樞相容端點
   - 事件中樞相容名稱

   ![取得在 hello Azure 入口網站中的 hello 的 IoT 中心端點的連接字串](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. 在 hello **IoT 中樞**窗格下**設定**，按一下 **共用存取原則**。

6. 按一下 [iothubowner]。

7. 請注意 hello**主索引鍵**值。

8. 建立 IoT 中心端點 hello 連接字串，如下所示：

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > 取代`<Event Hub-compatible endpoint>`和`<Primary key>`與您先前記下的 hello 值。

### <a name="create-a-consumer-group-for-your-iot-hub"></a>為 IoT 中樞建立取用者群組

1. 開啟 IoT 中樞。

2. 在 hello **IoT 中樞**窗格下**傳訊**，按一下**端點**。

3. 在 hello 右窗格中，在**內建端點**，按一下 **事件**。

4. 在 hello**屬性**窗格下**取用者群組**，輸入名稱，然後記下它。

5. 按一下 [儲存] 。

## <a name="create-and-deploy-an-azure-function-app"></a>建立並部署 Azure 函式應用程式

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增** > **計算** > **函式應用程式** >  **建立**。

2. 輸入 hello 的 hello 函式應用程式的必要資訊。

   ![在 hello Azure 入口網站中建立函式應用程式](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **應用程式名稱**: hello 的 hello 函式應用程式的名稱。 hello 名稱必須是全域唯一的。

   * **資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。

   * **儲存體帳戶**: hello 您所建立的儲存體帳戶。

   * **Pin toodashboard**： 核取此選項，讓您輕鬆存取 toohello 函式應用程式從 hello 儀表板。

3. 按一下 [建立] 。

4. 建立 hello 函式應用程式之後，請開啟它。

5. 在 hello 函式應用程式，建立新的函式執行 hello 下列：

   a. 按一下 [新函式]。

   b.這是另一個 C# 主控台應用程式。 選取 [JavaScript] 作為 [語言]，選取 [資料處理] 作為 [案例]。

   c. 按一下 建立此函式，然後按一下新增函式。

   d. 選取**JavaScript** hello 語言和**資料處理**hello 案例。

   e. 按一下 hello **EventHubTrigger JavaScript**範本。

   f. 輸入 hello hello 範本所需的資訊。

      * **命名您的函式**: hello hello 函式名稱。

      * **事件中樞名稱**: hello 您先前記下事件中樞相容名稱。

      * **事件中樞連線**: tooadd hello 連接字串 hello 您建立 IoT 中心端點按一下**新增**。

   g. 按一下 [建立] 。

6. 藉由 hello 下列設定 hello 函式的輸出：

   a. 按一下 [整合] > [新增輸出] > [Azure 資料表儲存體] > [選取]。

      ![在 hello Azure 入口網站中加入資料表儲存體 tooyour 函式應用程式](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. 輸入 hello 的必要資訊。

      * **資料表參數名稱**： 使用`outputTable`，用來在 Azure 的 hello 函式的程式碼。
      
      * **資料表名稱**：使用 `deviceData`。

      * **儲存體帳戶連線**︰按一下 [新增]，然後選取或輸入儲存體帳戶。 如果未顯示 hello 儲存體帳戶，請參閱[儲存體帳戶的需求](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements)。
      
   c. 按一下 [儲存] 。

7. 在 [觸發程序] 底下，按一下 [Azure 事件中樞 (eventHubMessages)]。

8. 在下**事件中樞取用者群組**，輸入 hello 取用者群組，您建立，然後按一下 hello 名稱**儲存**。

9. 按一下您已建立剩餘的 hello 的 hello 函式，然後按一下**檢視檔案**hello 右上。

10. 中的 hello 程式碼取代`index.js`hello 下列：

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. 按一下 [儲存] 。

您現在已建立 hello 函式應用程式。 它會將 IoT 中樞收到的訊息儲存在您的表格儲存體中。

> [!NOTE]
> 您可以使用 hello**執行**按鈕 tootest hello 函式應用程式。 當您按一下**執行**，tooyour IoT 中樞傳送 hello 測試訊息。 hello 抵達的 hello 訊息應該 hello 函式應用程式 toostart 觸發程序，然後再儲存 hello 訊息 tooyour 資料表儲存體。 hello**記錄**窗格記錄 hello hello 程序的詳細資料。

## <a name="verify-your-message-in-your-table-storage"></a>確認訊息位於資料表儲存體中

1. 在您裝置 toosend 訊息 tooyour IoT 中樞執行 hello 範例應用程式。

2. [下載並安裝 Azure 儲存體總管](http://storageexplorer.com/)。

3. 開啟 [儲存體總管] 中，按一下**新增 Azure 帳戶** > **登入**，再於 tooyour Azure 帳戶登入。

4. 按一下您的 Azure 訂用帳戶 > [儲存體帳戶] > 您的儲存體帳戶 > [資料表] > [deviceData]。

   您應該會看到從登入 hello 您裝置 tooyour IoT 中樞傳送的訊息`deviceData`資料表。

## <a name="next-steps"></a>後續步驟

您已成功建立 Azure 儲存體帳戶和 Azure 函式應用程式，以將您的 IoT 中樞收到的訊息儲存在表格儲存體中。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
