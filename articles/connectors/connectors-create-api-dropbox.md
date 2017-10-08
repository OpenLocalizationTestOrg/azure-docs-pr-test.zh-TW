---
title: "Azure 邏輯應用程式中的 aaaDropbox 連接器 |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 連接 tooDropbox toomanage 您的檔案。 您可以執行各種動作，例如上傳、更新、取得及刪除 Dropbox 中的檔案。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a>開始使用 hello Dropbox 連接器
連接 tooDropbox toomanage 您的檔案。 您可以執行各種動作，例如上傳、更新、取得及刪除 Dropbox 中的檔案。

toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。 您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。

## <a name="connect-toodropbox"></a>連接 tooDropbox
邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。 連線可讓邏輯應用程式與另一個服務連線。 例如，在訂單 tooconnect tooDropbox，您必須先 Dropbox*連接*。 toocreate 連線，您將需要您通常會使用您想要的 tooconnect tooaccess hello 服務 tooprovide hello 認證。 因此，在 hello Dropbox 範例中，您將需要 hello 認證 tooyour 順序 toocreate hello 連接 tooDropbox 的 Dropbox 帳戶。 [深入了解連線]()

### <a name="create-a-connection-toodropbox"></a>建立連接 tooDropbox
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a>使用 Dropbox 觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。 [深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

在此範例中，我們將使用 hello**會建立一個檔案**觸發程序。 這個觸發程序時，我們會呼叫 hello**取得檔案的內容使用路徑**Dropbox 動作。 

1. 輸入*dropbox* hello hello Logic Apps 設計工具上的搜尋方塊，然後選取 hello **Dropbox-建立檔案時**觸發程序。      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. 選取您想在其中 tootrack 檔案建立 hello 資料夾。 選取此項目...（在 hello 紅色方塊識別） 和瀏覽 toohello 資料夾想 tooselect hello 觸發程序的輸入。  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a>使用 Dropbox 動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

既然 hello 已加入觸發程序，請遵循這些步驟 tooadd 執行的動作，會收到 hello 新檔案的內容。

1. 選取**+ 新增步驟**tooadd hello 動作您想要 tootake，建立新檔案時。  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. 選取 [新增動作] 。 此隨即開啟 hello 搜尋方塊中，您可以搜尋的任何動作您希望 tootake。  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. 輸入*dropbox*動作相關 tooDropbox 的 toosearch。  
4. 選取**Dropbox-取得檔案的內容使用路徑**hello 動作 tootake hello 中建立新的檔案時選取的 Dropbox 資料夾。 hello 動作控制區塊會開啟。 您將會提示的 tooauthorize 您邏輯應用程式 tooaccess，如果您還沒有這麼做之前，您的 Dropbox 帳戶。  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. 選取此項目...(位於 hello hello 右邊**檔案路徑**控制項)，並瀏覽您想要 toouse toohello 檔案路徑。 或者，使用 hello**檔案路徑**語彙基元 toospeed 註冊您的邏輯應用程式建立。  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. 儲存您的工作，並在 Dropbox tooactivate 中您的工作流程建立新的檔案。  

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/dropbox/)。

## <a name="more-connectors"></a>其他連接器
返回 toohello [Api 清單](apis-list.md)。
