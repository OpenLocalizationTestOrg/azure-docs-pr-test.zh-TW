---
title: "Azure 邏輯應用程式中的 aaaUse hello Slack 連接器 |Microsoft 文件"
description: "連接 tooSlack 邏輯應用程式中"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a>開始使用 hello Slack 連接器
Slack 是團隊通訊工具，能把您團隊的通訊都集中在一個地方，讓您不但在何處都可使用，還能搜尋各項記錄。 

立即開始建立邏輯應用程式，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="create-a-connection-tooslack"></a>建立連接 tooSlack
toouse hello Slack 連接器，您先建立**連接**然後提供這些屬性中的 hello 詳細資料： 

| 屬性 | 必要 | 說明 |
| --- | --- | --- |
| 權杖 |是 |提供 Slack 的認證 |

遵循這些步驟 toosign 到 Slack 和完整 hello hello Slack 設定**連接**邏輯應用程式中：

1. 選取 [週期] 
2. 選取 [頻率] 並輸入 [間隔]
3. 選取 [新增動作]  
   ![設定 Slack][1]  
4. Hello [搜尋] 方塊中輸入 Slack，並等候 hello 搜尋 tooreturn hello 名稱中在與 Slack 的所有項目
5. 選取 [Slack - 張貼訊息] 
6. 選取**登入 tooSlack**:  
   ![設定 Slack][2]
7. 提供您的 Slack 認證 toosign tooauthorize hello 應用程式中    
   ![設定 Slack][3]  
8. 您將會重新導向的 tooyour 組織的登入頁面。 **授權**Slack toointeract 邏輯應用程式：      
   ![設定 Slack][5] 
9. Hello 授權完成後，您應該重新導向的 tooyour 邏輯應用程式 toocomplete 它藉由設定 hello**延-取得所有訊息**> 一節。 加入其他所需的觸發和動作。  
   ![設定 Slack][6]
10. 儲存您的工作，藉由選取**儲存**hello 上方的功能表列上。

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/slack/)。

## <a name="more-connectors"></a>其他連接器
返回 toohello [Api 清單](apis-list.md)。

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
