---
title: "aaaLearn toouse hello 邏輯應用程式中的 Twitter 連接器的方式 |Microsoft 文件"
description: "搭配 REST API 參數來使用 Twitter 連接器的概觀"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a>開始使用 hello Twitter 連接器
您可以使用 hello Twitter 連接器：

* 張貼推文並取得推文
* 存取時間軸、好友和追隨者
* 執行中的 hello 任何其他動作，如下所述的觸發程序  

toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。 您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。  

## <a name="connect-tootwitter"></a>連接 tooTwitter
邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。 [連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。  

### <a name="create-a-connection-tootwitter"></a>建立連接 tooTwitter
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a>使用 Twitter 觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。 [深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

在此範例中，我將示範如何 toouse hello**新推文回傳時**觸發 #Seattle 的 toosearch，而如果找到 #Seattle，更新的檔案中 Dropbox hello 推文中的 hello 文字。 在企業範例中，您無法搜尋 hello 您的公司名稱，並更新 hello 推文中的 hello 文字的 SQL 資料庫。

1. 輸入*twitter* hello hello 邏輯應用程式的設計工具上的搜尋方塊中然後選取 hello **Twitter-張貼新推文時**觸發程序   
   ![Twitter 觸發程序圖 1](./media/connectors-create-api-twitter/trigger-1.png)  
2. 輸入*#Seattle*在 hello**搜尋文字**控制項  
   ![Twitter 觸發程序圖 2](./media/connectors-create-api-twitter/trigger-2.png) 

此時，應用程式邏輯已與其他觸發程序和 hello 工作流程中的動作會開始執行的 hello 的觸發程序設定。 

> [!NOTE]
> 功能的邏輯應用程式 toobe，它必須包含至少一個觸發程序與一個動作。 請遵循下一個區段 tooadd hello 動作中的 hello 步驟。  
> 
> 

## <a name="add-a-condition"></a>新增條件
因為我們只感興趣的使用者與 50 個以上的使用者推文，條件，以確認 hello 實行項目數目必須先新增 toohello 邏輯應用程式。  

1. 選取**+ 新增步驟**tooadd hello 動作您希望 tootake #Seattle 新推文中發現時  
   ![Twitter 動作圖 1](../../includes/media/connectors-create-api-twitter/action-1.png)  
2. 選取 hello**加入條件**連結。  
   ![Twitter 條件圖 1](../../includes/media/connectors-create-api-twitter/condition-1.png)   
   這會開啟 hello**條件**控制項，例如檢查條件*等於*，*是小於*，*大於*， *包含*等等。  
   ![Twitter 條件圖 2](../../includes/media/connectors-create-api-twitter/condition-2.png)   
3. 選取 hello**選擇值**控制項。  
   在此控制項中，您可以選取一或多個 hello 屬性從任何先前的動作或觸發程序做為其條件會評估的 tootrue 或 false 的 hello 值。
   ![Twitter 條件圖 3](../../includes/media/connectors-create-api-twitter/condition-3.png)   
4. 選取 hello **...** tooexpand hello 清單的內容，讓您可以查看所有可用的 hello 屬性。        
   ![Twitter 條件圖 4](../../includes/media/connectors-create-api-twitter/condition-4.png)   
5. 選取 hello**實行項目計數**屬性。    
   ![Twitter 條件圖 5](../../includes/media/connectors-create-api-twitter/condition-5.png)   
6. 請注意 hello 實行項目計數屬性現在位於 hello 值控制項。    
   ![Twitter 條件影像 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. 選取**大於**從 hello 運算子清單。    
   ![Twitter 條件圖 7](../../includes/media/connectors-create-api-twitter/condition-7.png)   
8. 輸入 50 hello 運算元 hello*大於*運算子。  
   現在加入 hello 條件。 儲存工作使用 hello**儲存**上述 hello 功能表上的連結。    
   ![Twitter 條件圖 8](../../includes/media/connectors-create-api-twitter/condition-8.png)   

## <a name="use-a-twitter-action"></a>使用 Twitter 動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。  

既然您已加入觸發程序，請遵循這些步驟 tooadd 會公佈新推文中的 hello 推文 hello 觸發程序所找到的 hello 內容的動作。 基於本逐步解說的 hello 將公佈使用者與 50 個以上的實行項目從的推文。  

在 hello 下一個步驟中，您將會公佈推文中使用某些 hello 屬性的每個推文中已有 50 個以上的實行項目之使用者所張貼在 Twitter 動作。  

1. 選取 [新增動作] 。 這會開啟 hello 搜尋控制項，您可以搜尋其他動作和觸發程序。  
   ![Twitter 條件圖 9](../../includes/media/connectors-create-api-twitter/condition-9.png)   
2. 輸入*twitter* hello 搜尋方塊中然後選取 hello **Twitter-張貼推文**動作。 這會開啟 hello**張貼推文**控制您將在其中輸入 hello 推文中公佈的所有詳細資料。      
   ![Twitter 動作圖 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)   
3. 選取 hello**推文提供文字**控制項。 從上一個動作和 hello 邏輯應用程式中的觸發程序的所有輸出現在都是可見的。 您可以選取其中任何，並將它們當做 hello 新推文中的 hello 推文中文字的一部分使用。     
   ![Twitter 動作圖 2](../../includes/media/connectors-create-api-twitter/action-2.png)   
4. 選取 [使用者名稱]   
5. 輸入*指出：* hello 推文中的文字控制項中。 在使用者名稱之後執行此動作。  
6. 選取「推文文字」。       
   ![Twitter 動作圖 3](../../includes/media/connectors-create-api-twitter/action-3.png)   
7. 儲存您的工作，並傳送推文中的 hello #Seattle 雜湊標記 tooactivate 與您的工作流程。  


## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/twitterconnector/)。 

## <a name="next-steps"></a>後續步驟
[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)

