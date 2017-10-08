---
title: "在您的 Logic Apps aaaAdd hello Office 365 Outlook 連接器 |Microsoft 文件"
description: "使用 Office 365 連接器 tooenable 互動與 Office 365 中建立邏輯應用程式。 例如：建立、編輯和更新連絡人及行事曆項目。"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a>開始使用 hello Office 365 Outlook 連接器
hello Office 365 Outlook 連接器可讓 Office 365 中 Outlook 的互動。 使用此連接器 toocreate、 編輯和更新連絡人及行事曆項目，以及取得、 傳送，和回覆 tooemail。

使用 Office 365 Outlook，您可以：

* 建置您的工作流程使用 Office 365 中的 hello 電子郵件和行事曆功能。 
* 當新的電子郵件、 行事曆項目更新時，您的工作流程及其他使用觸發程序 toostart。
* 使用動作 toosend 電子郵件，請建立新的行事曆事件，等等。 例如，當在 Salesforce （觸發程序） 中有新的物件時，傳送電子郵件 tooyour Office 365 Outlook （動作）。 

本主題說明您如何 toouse hello 邏輯應用程式中的 Office 365 Outlook 連接器及清單也 hello 觸發程序和動作。

> [!NOTE]
> 這個版本的 hello 文件適用於 tooLogic 應用程式公開上市 (GA)。
> 
> 

toolearn 進一步了解邏輯應用程式，請參閱[為何的 logic apps](../logic-apps/logic-apps-what-are-logic-apps.md)和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="connect-toooffice-365"></a>連接 tooOffice 365
邏輯應用程式可以存取任何服務之前，您先建立*連接*toohello 服務。 連線可讓邏輯應用程式與另一個服務連線。 例如，tooconnect tooOffice 365 Outlook，您首先需要 Office 365*連接*。 toocreate 連線，請輸入您通常會使用您想要的 tooconnect tooaccess hello 服務的 hello 認證。 因此與 Office 365 Outlook，請輸入 hello 認證 tooyour Office 365 帳戶 toocreate hello 連接。

## <a name="create-hello-connection"></a>建立 hello 連線
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a>使用觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。 觸發程序 「 輪詢"hello 服務以間隔和您想要的頻率。 [深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

1. Hello 邏輯應用程式中，輸入 「 office 365"tooget hello 觸發程序的清單：  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. 選取 [Office 365 Outlook - 即將來臨的事件快要開始時]。 如果連接已存在，然後從 hello 下拉式清單選取行事曆。
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    如果您在提示的 toosign，然後輸入 hello 登詳細資料 toocreate hello 連接中。 [建立 hello 連接](connectors-create-api-office365-outlook.md#create-the-connection)本主題列出 hello 步驟。 
   
   > [!NOTE]
   > 在此範例中，行事曆事件更新時，會執行 hello 邏輯應用程式。 這個觸發程序，toosee hello 結果加入另一個傳送一則簡訊給您的動作。 例如，新增 hello Twilio*傳送訊息*時 hello 行事曆事件的文字會在 15 分鐘內啟動的動作。 
   > 
   > 
3. 選取 hello**編輯**按鈕，然後設定 hello**頻率**和**間隔**值。 例如，如果您想 hello 觸發程序 toopoll 每隔 15 分鐘，然後設定 hello**頻率**太**分鐘**，並設定 hello**間隔**太**15**. 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. **儲存**您的變更 （hello 工具列的左上的角）。 邏輯應用程式將會儲存，而且可能會自動啟用。

## <a name="use-an-action"></a>使用動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

1. 選取加號 hello。 您會看到幾個選擇：**將動作加入**，**加入條件**，或其中一個 hello**詳細**選項。
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. 選擇 [新增動作] 。
3. 在 [hello] 文字方塊中，輸入 「 office 365"tooget 所有 hello 可用動作的清單。
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. 在本例中，選擇 [Office 365 Outlook - 建立連絡人]。 如果連接已存在，然後選擇 hello**資料夾識別碼**，**名字**，和其他屬性：  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    如果系統提示您輸入 hello 連接資訊，然後輸入 hello 詳細資料 toocreate hello 連接。 [建立 hello 連接](connectors-create-api-office365-outlook.md#create-the-connection)本主題說明這些屬性。 
   
   > [!NOTE]
   > 在此範例中，我們會在 Office 365 Outlook 中建立新連絡人。 您可以使用另一個觸發程序 toocreate hello 連絡人的輸出。 例如，新增 hello SalesForce*當建立物件*觸發程序。 然後新增 Office 365 Outlook hello*建立連絡人*動作若使用 hello SalesForce 欄位 toocreate hello 新增新的連絡人 Office 365 中。 
   > 
   > 
5. **儲存**您的變更 （hello 工具列的左上的角）。 邏輯應用程式將會儲存，而且可能會自動啟用。

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/office365connector/)。 

## <a name="next-steps"></a>後續步驟
[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。 瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。

