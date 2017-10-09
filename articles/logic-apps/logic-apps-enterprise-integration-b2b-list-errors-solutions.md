---
title: "Logic Apps B2B 錯誤與解決方案清單：Azure App Service | Microsoft Docs"
description: "Logic Apps B2B 錯誤與解決方案清單"
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
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Logic Apps B2B 錯誤與解決方案清單  
本文協助您針對可能發生在 Logic Apps B2B 案例中的錯誤進行疑難排解，並提出修正這些錯誤的適當動作。


## <a name="agreement-resolution"></a>合約解析

### <a name="no-agreement-found"></a>*找不到合約 

|   |   |  
|---|---|
| 錯誤說明 | 找不到具有合約解析參數的合約|    
| 使用者動作 | hello 協議應加入 toohello 整合帳戶同意的企業身分識別。</br> hello 的商務識別應該符合 toohello 輸入的訊息識別碼|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>* 找不到具有識別身分的合約

|   |   | 
|---|---|
| 錯誤說明 | 找不到具有識別身分的合約：'AS2Identity'::'Partner1' 和 'AS2Identity'::'Partner3'| 
| 使用者動作 | 無效的 AS2-從或針對協議的 AS2 tooconfigured。 </br> 正確的 AS2 訊息 AS2-從或 AS2 tooheaders 或合約 toomatch AS2 id，在 AS2 訊息標頭與協議設定 |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>* 遺漏 AS2 訊息標題  

|   |   |  
|---|---|
| 錯誤說明| 不正確的 AS2 標題。 'AS2-To' 或 'AS2-From' 其中一個標題為空白| 
| 使用者動作 | 收到的 AS2 訊息不包含 hello AS2-從或 AS2 tooor 這兩個標頭。 </br> 檢查 AS2 訊息 AS2-從和 AS2 tooheaders 並更正根據協議設定 |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>* 遺漏 AS2 訊息本文和標題    

|   |   |  
|---|---|
| 錯誤說明| hello 要求內容為 null 或空白 | 
| 使用者動作 | 收到的 AS2 訊息不包含 hello 訊息內文 |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>* AS2 訊息解密失敗

|   |   | 
|---|---|
| 錯誤說明 |  [已處理/錯誤：解密失敗] | 
| 使用者動作 | 新增@base64ToBinarytooAS2Message 傳送 toopartner 之前 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a>* MDN 解密失敗

|   |   | 
|---|---|
| 錯誤說明 |  [已處理/錯誤：解密失敗] | 
| 使用者動作 | 新增@base64ToBinarytooMDN 傳送 toopartner 之前 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a>* 遺漏簽署憑證

|   |   |  
|---|---|
| 錯誤說明| hello 簽署憑證尚未設定 AS2 合作對象。 </br> AS2-From：partner1 AS2-To：partner2 | 
| 使用者動作 | 以正確的簽章憑證設定 AS2 合約設定 |
|  |  | 

## <a name="x12-and-edifact"></a>X12 和 EDIFACT

### <a name="-leading-or-trailing-space-found"></a>* 發現前置或尾端空格    
    
|   |   | 
|---|---|
| 錯誤說明 | 剖析期間發生錯誤。 hello Edifact 交易集與 '（不含群組） 的交換中識別碼為 '987654 包含' id' 123456，為傳送者識別碼 'Partner1'、 接收者識別碼 '夥伴 2' 處於暫停狀態，錯誤如下： 找到前置尾端分隔符號 |
| 使用者動作 | hello 協議設定 toobe 設定 tooallow 開頭與尾端空白字元。 </br> 編輯協議設定 tooallow 開頭與尾端空白字元 |
|   |   |

![允許空格](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a>* 重複檢查已啟用在 hello 協議

|   |   | 
|---|---| 
| 錯誤說明 | 重複控制編號 |
| 使用者動作 | 此錯誤表示收到 hello 訊息有重複的控制編號。 </br> 更正 hello 控制編號，然後再重新傳送 hello 訊息 |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a>* 遺漏 hello 協議中的結構描述

|   |   | 
|---|---| 
| 錯誤說明 | 剖析期間發生錯誤。 識別碼為 '564220001' 包含在功能群組識別碼為 '56422'，在交換傳送者識別碼為' 12345678 id '000056422'，' 接收者識別碼 ' 87654321' hello X12 交易集處於暫停狀態，錯誤如下 「 hello 訊息有不明的文件 type 和未解析 tooany hello hello 協議中設定的現有結構描述的 「 |
| 使用者動作 | 在 hello 協議設定中設定結構描述  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a>* 不正確的結構描述在 hello 協議

|   |   | 
|---|---| 
| 錯誤說明 | hello 訊息具有不明的文件型別，而且未解析 tooany hello hello 協議中設定的現有結構描述。 |
| 使用者動作 | 在 hello 協議設定中設定正確的結構描述  |
|   |   |

## <a name="flat-file"></a>一般檔案

### <a name="-input-message-with-no-body"></a>* 輸入訊息沒有本文

|   |   | 
|---|---|
| 錯誤說明 | InvalidTemplate。 在行 '1' 與欄 '1902' 動作 'Flat_File_Decoding' 輸入中的無法 tooprocess 範本語言運算式: ' 需要 'content' 屬性必須要有值，但卻收到 null。 路徑 ''.'。 |
| 使用者動作 | 此錯誤表示 hello 輸入的訊息不包含主體 |
|   |   | 

## <a name="learn-more"></a>詳細資訊
[深入了解 hello 企業版整合套件](logic-apps-enterprise-integration-overview.md)
