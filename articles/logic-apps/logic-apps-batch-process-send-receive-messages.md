---
title: "aaaBatch 處理訊息，做為群組或集合-Azure 邏輯應用程式 |Microsoft 文件"
description: "傳送和接收訊息以便在邏輯應用程式中批次處理"
keywords: "批次, 批次程序"
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a>傳送、接收，並在邏輯應用程式中批次處理訊息

tooprocess 訊息群組在一起，您可以傳送資料的項目或訊息，tooa*批次*，然後以批次中處理這些項目。 當您想要確定資料項目 toomake 中以特定方式分組和都會一起處理，則這個方法會很有用。 

您可以建立以批次接收項目，使用 hello 的 logic apps**批次**觸發程序。 然後，您可以建立使用 hello 傳送項目 tooa 批次的 logic apps**批次**動作。

本主題示範如何透過執行這些工作，建置批次解決方案： 

* [建立邏輯應用程式，以批次接收並收集項目](#batch-receiver)。 這個 「 批次接收者 」 邏輯應用程式指定 hello 批次名稱和版本準則 toomeet 之前釋出 hello 接收者邏輯應用程式，並處理項目。 

* [建立邏輯應用程式所傳送的項目 tooa 批次](#batch-sender)。 這個 「 批次傳送者 」 的邏輯應用程式指定的位置 toosend 項目，必須是現有的批次接收者邏輯應用程式。 您可以也指定唯一的索引鍵，例如客戶編號、 太 「 分割 」，或將分割成幾個子集該索引鍵為基礎的 hello 目標批次。 這樣一來，所有具有該索引鍵的項目都會一起收集並處理。 

## <a name="requirements"></a>需求

toofollow 此範例中，您需要這些項目：

* Azure 訂用帳戶。 如果您沒有訂用帳戶，您可以[開始使用免費 Azure 帳戶](https://azure.microsoft.com/free/)。 否則，您可以[註冊隨用隨付訂用帳戶](https://azure.microsoft.com/pricing/purchase-options/)。

* 相關的基本知識[如何 toocreate 邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md) 

* 電子郵件帳戶與任何 [Azure Logic Apps 所支援的電子郵件提供者](../connectors/apis-list.md)

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a>建立以批次接收訊息的邏輯應用程式

您可以傳送訊息 tooa 批次之前，您必須先使用 hello 建立 「 批次接收者 」 邏輯應用程式**批次**觸發程序。 這樣一來，當您建立 hello 寄件者邏輯應用程式時，可以選取這個接收器邏輯應用程式。 Hello 收件者，您可以指定 hello 批次名稱、 釋放準則和其他設定。 

寄件者的 logic apps 需要知道其中 toosend 項目，而接收器邏輯應用程式不需要 tooknow hello 寄件者有關的任何項目。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，建立邏輯應用程式具有此名稱:"BatchReceiver" 

2. 在邏輯應用程式設計師中，新增 hello**批次**觸發程序，用來啟動您的邏輯應用程式工作流程。 在 hello 搜尋方塊中輸入"batch"做為您的篩選器。 選取此觸發程序：**批次 – 批次訊息**

   ![新增批次觸發程序](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. 提供 hello 批次中的名稱，然後指定準則來釋放 hello 批次，例如：

   * **批次名稱**: hello 用名稱 tooidentify hello 批次，也就是在此範例中的"TestBatch"。
   * **訊息計數**： 釋放進行處理，也就是"5"在此範例之前，做為批次 hello 訊息 toohold 數目。

   ![提供批次觸發程序詳細資料](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. 加入另一個 hello 批次觸發程序引發時傳送電子郵件的動作。 每個時間 hello 批次有五個項目，hello 邏輯應用程式傳送電子郵件。

   1. Hello 批次觸發程序，在底下選擇**+ 新增步驟** > **將動作加入**。

   2. 在 hello 搜尋方塊中輸入"email"做為您的篩選器。
   根據您的電子郵件提供者，選取電子郵件連接器。
   
      例如，如果您有工作或學校帳戶時，選取 hello Office 365 Outlook 連接器。 
      如果您有 Gmail 帳戶，請選取 hello Gmail 連接器。

   3. 為您的連接器選取此動作： **{*電子郵件提供者*} - 傳送電子郵件**

      例如：

      ![為您的電子郵件提供者選取「傳送電子郵件」動作](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. 如果您先前未建立電子郵件提供者的連線，請提供您的電子郵件認證，以便當系統提示您時進行驗證。 深入了解[驗證您的電子郵件認證](../logic-apps/logic-apps-create-a-logic-app.md)。

6. 設定您剛才加入的 hello 動作 hello 屬性。

   * 在 hello**至**方塊中，輸入 hello 收件者的電子郵件地址。 
   為了測試用途，您可以使用自己的電子郵件地址。

   * 在 hello**主旨**方塊中，當 hello**動態內容**清單出現時，請選取 hello**資料分割名稱**欄位。

     ![從 hello [動態內容] 清單中，選取 [資料分割名稱]](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     在更新版本的區段中，您可以指定除以 hello 目標批次，邏輯到唯一的資料分割索引鍵設定 toowhere 您可以傳送訊息。 
     每個集合都 hello 寄件者邏輯應用程式所產生的唯一數字。 
     這項功能可讓您使用多個子集的單一批次，並定義您所提供的 hello 名稱與每個子集。

   * 在 hello**主體**方塊中，當 hello**動態內容**清單出現時，請選取 hello**訊息識別碼**欄位。

     ![對於 [內文]，選取 [訊息識別碼]](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     Hello 輸入 hello 傳送電子郵件動作是陣列，因為 hello 設計工具自動加入**每個**圈 hello**傳送電子郵件**動作。 
     此迴圈 hello 內部上執行動作 hello 批次中每個項目。 
     因此，與 hello 批次觸發程序組 toofive 項目，您會取得每個時間 hello 觸發程序引發的五個電子郵件。

7.  既然您建立了批次接收者邏輯應用程式，請儲存您的邏輯應用程式。

    ![儲存您的邏輯應用程式](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a>建立傳送訊息 tooa 批次的 logic apps

現在建立傳送嗨接收者邏輯應用程式所定義的項目 toohello 批次的一或多個邏輯應用程式。 Hello 寄件者，您可以指定 hello 接收者邏輯應用程式和批次名稱、 訊息內容和任何其他設定。 您可以選擇提供唯一的資料分割索引鍵 toodivide hello 批次至子集 toocollect 項目與該索引鍵。

寄件者的 logic apps 需要知道其中 toosend 項目，而接收器邏輯應用程式不需要 tooknow hello 寄件者有關的任何項目。

1. 建立具有名稱 "BatchSender" 的另一個邏輯應用程式

   1. 在 hello 搜尋方塊中輸入"recurrence"做為您的篩選器。 
   選取此觸發程序：**排程 - 重複**

      ![加入 hello"排程 Recurrence"觸發程序](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. 設定每隔一分鐘 hello 頻率和間隔 toorun hello 寄件者邏輯應用程式。

      ![設定重複觸發程序的頻率和間隔](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. 加入新的步驟，以便傳送郵件 tooa 批次。

   1. Hello 循環觸發程序，在底下選擇**+ 新增步驟** > **將動作加入**。

   2. 在 hello 搜尋方塊中輸入"batch"做為您的篩選器。 

   3. 選取此動作：**傳送訊息 toobatch – 選擇批次觸發程序的 Logic Apps 工作流程**

      ![選取 [傳送郵件 toobatch]](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. 現在，選取您先前建立的 "BatchReceiver" 邏輯應用程式，它現在會顯示為動作。

      ![選取「批次接收者」邏輯應用程式](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > hello 清單也會顯示有批次觸發程序的任何其他邏輯應用程式。

3. 設定 hello 批次屬性。

   * **批次名稱**: hello hello 接收者邏輯應用程式，其 「 TestBatch 「 在此範例中，並會在執行階段進行驗證所定義的批次名稱。

     > [!IMPORTANT]
     > 請確定您不要變更 hello 批次名稱必須符合 hello hello 接收者邏輯應用程式所指定的批次名稱。
     > 變更 hello 批次名稱會導致邏輯應用程式 toofail hello 寄件者。

   * **訊息內容**: hello 的 toosend 訊息內容。 
   例如，將此運算式插入到 hello 訊息內容傳送 toohello 批次目前的日期和時間 hello:

     1. 當 hello**動態內容**清單出現時，選擇 **運算式**。 
     2. 輸入 hello 運算式**utcnow()**，然後選擇 **確定**。 

        ![在 [訊息內容] 中，選擇 [運算式]。 輸入"utcnow()"。](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. 現在設定 hello 批次的資料分割。 在 hello"BatchReceiver 」 動作，選擇  **Show advanced 選項**。

   * **分割區名稱**: 選用唯一的資料分割索引鍵 toouse 分配 hello 目標批次。 針對此範例，請新增運算式，產生介於 1 到 5 的隨機數字。
   
     1. 當 hello**動態內容**清單出現時，選擇 **運算式**。
     2. 輸入此運算式：**rand(1,6)**

        ![設定目標批次的資料分割](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        這個 **rand** 函式會產生一到五之間的數字。 
        因此您會將此批次分割成五個有編號的資料分割，此運算式會以動態方式設定。

   * **訊息識別碼**：選擇性的訊息識別碼，空白時是一個產生的 GUID。 
   針對此範例，請將這個方塊保留空白。

5. 儲存您的邏輯應用程式。 寄件者的邏輯應用程式現在看起來類似 toothis 範例：

   ![儲存您的傳送者邏輯應用程式](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a>儲存邏輯應用程式

tootest 您批次處理方案，將保留在幾分鐘後執行邏輯應用程式。 過期，啟動 取得五個群組中的電子郵件時，所有的 hello 相同資料分割索引鍵。

BatchSender 邏輯應用程式會每分鐘執行、 產生隨機數字，介於 1 到 5，並使用這個產生的數字為 hello hello 目標批次的資料分割索引鍵會傳送訊息。 每次 hello 批次有五個項目以 hello 相同的資料分割索引鍵，BatchReceiver 邏輯應用程式就會引發並傳送郵件的每個訊息。

> [!IMPORTANT]
> 當您完成測試，請確定您停用 hello BatchSender 邏輯應用程式 toostop 傳送訊息，並避免超載收件匣。

## <a name="next-steps"></a>後續步驟

* [使用 JSON 建置於邏輯應用程式定義上](../logic-apps/logic-apps-author-definitions.md)
* [在 Visual Studio 中使用 Azure Logic Apps 和 Functions 建置邏輯應用程式](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [適用於邏輯應用程式的例外狀況處理與記錄錯誤](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
