---
title: "aaaEncode EDIFACT 訊息-Azure 邏輯應用程式 |Microsoft 文件"
description: "驗證 EDI 並產生 Azure 邏輯應用程式與 EDIFACT 訊息編碼器 hello 企業版整合套件中的 XML"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Azure 邏輯應用程式的 EDIFACT 訊息編碼以 hello 企業版整合套件

與 hello 編碼 EDIFACT 訊息連接器，您可以驗證 EDI 和夥伴特定的屬性，產生 XML 文件的每個交易集，並要求技術通知，功能通知，或兩者。
toouse 此連接器，您必須加入現有的觸發程序邏輯應用程式中的 hello 連接器 tooan。

## <a name="before-you-start"></a>開始之前

以下是您所需要的 hello 項目：

* Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)
* 已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。 您必須為整合帳戶 toouse hello 編碼 EDIFACT 訊息連接器。 
* 至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)
* 已經在整合帳戶中定義的 [EDIFACT 合約](logic-apps-enterprise-integration-edifact.md)

## <a name="encode-edifact-messages"></a>編碼 EDIFACT 訊息

1. [建立邏輯應用程式](logic-apps-create-a-logic-app.md)。

2. 沒有觸發程序，hello 編碼 EDIFACT 訊息連接器，所以您必須新增啟動邏輯應用程式，像是要求觸發程序的觸發程序。 在 hello 邏輯應用程式的設計工具，加入觸發程序，然後再加入動作 tooyour 邏輯應用程式。

3.  在 hello 搜尋方塊中輸入"EDIFACT"做為您的篩選器。 選取  **EDIFACT 訊息編碼協議名稱**或**識別編碼 tooEDIFACT 訊息**。
   
    ![搜尋 EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. 如果您先前未建立任何連線 tooyour 整合帳戶，則會提示您 toocreate 現在該連接。 命名您的連線，並選取您想 tooconnect hello 整合帳戶。

    ![建立整合帳戶連線](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    具有星號的屬性為必要項目。

    | 屬性 | 詳細資料 |
    | --- | --- |
    | 連線名稱 * |為連接器輸入任何名稱。 |
    | 整合帳戶 * |輸入整合帳戶的名稱。 請確定應用程式整合帳戶和邏輯位於 hello 相同的 Azure 位置。 |

5.  當您完成時，您的連線詳細資料看起來應該類似 toothis 範例。 選擇 建立您的連線，toofinish**建立**。

    ![整合帳戶連線詳細資料](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    現在已建立您的連線。

    ![整合帳戶連線已建立](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a>依協議名稱將 EDIFACT 訊息編碼

如果您選擇 tooencode EDIFACT 訊息的協議名稱，開啟 hello**名稱的 EDIFACT 協議**清單中，輸入或選取您 EDIFACT 協議的名稱。 輸入 hello XML 訊息 tooencode。

![輸入 EDIFACT 協議名稱和 XML 訊息 tooencode](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a>由身分識別編碼 EDIFACT 訊息

如果您選擇 tooencode EDIFACT 訊息的身分識別，請輸入 hello 寄件者識別碼、 傳送者辨識符號、 接收者識別碼和接收者辨識符號為您的 EDIFACT 協議中設定。 選取 hello XML 訊息 tooencode。

![提供身分識別傳送者和接收者，選取 XML 訊息 tooencode](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a>EDIFACT 編碼詳細資料

hello 編碼 EDIFACT 連接器會執行這些工作： 

* 比對 hello 傳送者辨識符號和識別項和接收者辨識符號和識別項，以解析 hello 協議
* 序列化 hello EDI 交換，將 XML 編碼訊息轉換成 hello 交換中的 EDI 交易集。
* 套用交易集標頭和結尾區段
* 產生交換控制編號、群組控制編號和每個傳出交換的交易集控制編號
* 取代 hello 裝載資料中的分隔符號
* 驗證 EDI 和夥伴特定屬性
  * 針對 hello 訊息結構描述的 hello 交易集資料元素的結構描述驗證。
  * 對交易集資料元素執行 EDI 驗證。
  * 對交易集資料元素執行擴充驗證
* 產生每個交易集的 XML 文件。
* 要求技術和/或功能確認 (若已設定)。
  * 做為技術通知，hello CONTRL 訊息會指示接收交換。
  * 做為功能通知，hello CONTRL 訊息會指示接受或拒絕的錯誤或不支援的功能清單 hello 收到交換、 群組或訊息，

## <a name="view-swagger-file"></a>檢視 Swagger 檔案
tooview hello Swagger 詳細資料，hello EDIFACT 連接器，請參閱[EDIFACT](/connectors/edifact/)。

## <a name="next-steps"></a>後續步驟
[深入了解 hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack") 

