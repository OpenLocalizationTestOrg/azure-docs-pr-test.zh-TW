---
title: "在您的 Logic Apps aaaAdd hello OneDrive 連接器 |Microsoft 文件"
description: "使用 REST API 參數 hello OneDrive 連接器概觀"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a>開始使用 hello OneDrive 連接器
連接 tooOneDrive toomanage 檔案，包括上傳、 get、 刪除檔案等等。 

使用 OneDrive，您會︰ 

* 將檔案儲存在 OneDrive 中或更新 OneDrive 中的現有檔案以建置您的工作流程。 
* 建立或更新您的 OneDrive 中的檔案時使用觸發程序 toostart 您的工作流程。
* 使用動作 toocreate 檔案，請刪除檔案，等等。 例如，當收到有附件的新 Office 365 電子郵件時 (觸發程序)，在 OneDrive 建立新的檔案 (動作)。

本主題說明您如何 toouse hello 邏輯應用程式中的 OneDrive 連接器及清單也 hello 觸發程序和動作。

toolearn 進一步了解邏輯應用程式，請參閱[為何的 logic apps](../logic-apps/logic-apps-what-are-logic-apps.md)和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="connect-tooonedrive"></a>連接 tooOneDrive
邏輯應用程式可以存取任何服務之前，您先建立*連接*toohello 服務。 連線可讓邏輯應用程式與另一個服務連線。 例如，tooconnect tooOneDrive，您必須先 OneDrive*連接*。 toocreate 連線，請輸入您通常會使用您想要的 tooconnect tooaccess hello 服務的 hello 認證。 因此，使用 OneDrive，請輸入 hello 認證 tooyour OneDrive 帳戶 toocreate hello 連接。

### <a name="create-hello-connection"></a>建立 hello 連線
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a>使用觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。 觸發程序 「 輪詢"hello 服務以間隔和您想要的頻率。 [深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

1. Hello 邏輯應用程式中，輸入 「 onedrive"tooget hello 觸發程序的清單：  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. 選取 [當檔案遭到修改時]。 如果連接已存在，請選取 hello 顯示選擇器 按鈕 tooselect 資料夾。
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    如果您在提示的 toosign，然後輸入 hello 登詳細資料 toocreate hello 連接中。 [建立 hello 連接](connectors-create-api-onedrive.md#create-the-connection)本主題列出 hello 步驟。 
   
   > [!NOTE]
   > 在此範例中，hello 邏輯應用程式時執行的檔案會更新您所選擇的 hello 資料夾中。 這個觸發程序，toosee hello 結果加入另一個傳送一封電子郵件給您的動作。 例如，新增 hello Office 365 Outlook*傳送電子郵件*電子郵件寄給您更新檔案時的動作。 

3. 選取 hello**編輯**按鈕，然後設定 hello**頻率**和**間隔**值。 例如，如果您想 hello 觸發程序 toopoll 每隔 15 分鐘，然後設定 hello**頻率**太**分鐘**，並設定 hello**間隔**太**15**. 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. **儲存**您的變更 （hello 工具列的左上的角）。 邏輯應用程式將會儲存，而且可能會自動啟用。

## <a name="use-an-action"></a>使用動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

1. 選取加號 hello。 您會看到幾個選擇：**將動作加入**，**加入條件**，或其中一個 hello**詳細**選項。
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. 選擇 [新增動作] 。
3. 在 [hello] 文字方塊中，輸入 「 onedrive"tooget 所有 hello 可用動作的清單。
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. 在我們的範例中，選擇 [OneDrive - 建立檔案]。 如果連接已存在，然後選取 hello**資料夾路徑**tooput hello 檔案中，輸入 hello**檔案名稱**，然後選擇 hello**檔案內容**您想要：  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    如果系統提示您輸入 hello 連接資訊，然後輸入 hello 詳細資料 toocreate hello 連接。 [建立 hello 連接](connectors-create-api-onedrive.md#create-the-connection)本主題說明這些屬性。 
   
   > [!NOTE]
   > 在此範例中，我們會在 OneDrive 資料夾建立新檔案。 您可以使用輸出從另一個觸發程序 toocreate hello OneDrive 檔案。 例如，新增 hello Office 365 Outlook*新的電子郵件送達時*觸發程序。 然後新增 hello OneDrive*建立檔案*使用 ForEach toocreate hello 新的檔案在 OneDrive 中的 hello 附件和內容類型欄位的動作。 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. **儲存**您的變更 （hello 工具列的左上的角）。 邏輯應用程式將會儲存，而且可能會自動啟用。


## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/onedriveconnector/)。

## <a name="more-connectors"></a>其他連接器
返回 toohello [Api 清單](apis-list.md)。
