---
title: "應用程式 B2B edifact 解碼 aaaLogic 解析的 UNH2.5-Azure 邏輯應用程式 |Microsoft 文件"
description: "Azure Logic Apps B2B EDIFACT 解碼解析 UNH2.5"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a>如何 toohandle EDIFACT 文件有 UNH2.5 區段
Hello EDIFACT 文件中有 UNH2.5 時，它用於結構描述查閱。 

範例： hello UNH 欄位是**EAN008** hello EDIFACT 訊息中  
UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'  

步驟 toofollow toohandle hello 訊息 
1. 更新 hello 結構描述
2. 請檢查 hello 協議設定  

## <a name="update-hello-schema"></a>更新 hello 結構描述
tooprocess hello 訊息，您需要 toodeploy 具有 hello UNH2.5 根節點名稱的結構描述。  Hello 結構描述根名稱指定的範例，就是**EFACT_D03B_ORDERS_EAN008**  

針對每個 D03B_ORDERS 以不同的 UNH2.5 區段中，您就必須 toodeploy 個別結構描述。  

## <a name="add-schema-toohello-edifact-agreement"></a>新增結構描述 toohello EDIFACT 協議
### <a name="edifact-decode"></a>EDIFACT 解碼
tooDecode hello 內送訊息，設定 hello 結構描述中 hello EDIFACT 協議接收設定
1. 新增 hello 結構描述 toohello 整合帳戶    
2. 設定 hello 結構描述中 hello EDIFACT 協議接收設定。 
3. 選取 EDIFACT 合約，然後按一下 [編輯為 JSON]。  在 hello 接收協議中加入 UNH2.5 值**schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)

### <a name="edifact-encode"></a>EDIFACT 編碼
tooEncode hello 內送訊息、 在 hello EDIFACT 協議的傳送設定中設定 hello 結構描述
1. 新增 hello 結構描述 toohello 整合帳戶    
2. 在 hello EDIFACT 協議的傳送設定中設定 hello 結構描述。 
3. 選取 EDIFACT 合約，然後按一下 [編輯為 JSON]。  在 hello 傳送協議中加入 UNH2.5 值**schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)

## <a name="next-steps"></a>後續步驟
* [深入了解整合帳戶合約](../logic-apps/logic-apps-enterprise-integration-agreements.md "深入了解企業整合合約")  