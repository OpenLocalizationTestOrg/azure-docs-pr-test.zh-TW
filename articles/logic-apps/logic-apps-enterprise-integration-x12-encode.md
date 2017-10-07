---
title: "aaaEncode X12 訊息-Azure 邏輯應用程式 |Microsoft 文件"
description: "驗證 EDI 和轉換 XML 編碼 Azure 邏輯應用程式訊息編碼器 hello 企業版整合套件中的 x12 訊息"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>將 X12 編碼訊息 Azure 邏輯應用程式以 hello 企業版整合套件

與 hello X12 編碼訊息連接器，您可以驗證 EDI 和夥伴特定的屬性，將 XML 編碼訊息轉換成 hello 交換中的 EDI 交易集和要求技術通知，功能通知，或兩者。
toouse 此連接器，您必須加入現有的觸發程序邏輯應用程式中的 hello 連接器 tooan。

## <a name="before-you-start"></a>開始之前

以下是您所需要的 hello 項目：

* Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)
* 已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。 您必須為整合帳戶 toouse hello X12 編碼訊息連接器。
* 至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)
* 已經在整合帳戶中定義的 [X12 合約](logic-apps-enterprise-integration-x12.md)

## <a name="encode-x12-messages"></a>編碼 X12 訊息

1. [建立邏輯應用程式](logic-apps-create-a-logic-app.md)。

2. 沒有觸發程序，hello X12 編碼訊息連接器，所以您必須新增啟動邏輯應用程式，像是要求觸發程序的觸發程序。 在 hello 邏輯應用程式的設計工具，加入觸發程序，然後再加入動作 tooyour 邏輯應用程式。

3.  Hello 搜尋方塊中，輸入您的篩選器"x12"。 選取  **X12-將 tooX12 訊息編碼協議名稱**或**X12-將編碼識別 tooX12 訊息**。
   
    ![搜尋 "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. 如果您先前未建立任何連線 tooyour 整合帳戶，則會提示您 toocreate 現在該連接。 命名您的連線，並選取您想 tooconnect hello 整合帳戶。 
   
    ![整合帳戶連線](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    具有星號的屬性為必要項目。

    | 屬性 | 詳細資料 |
    | --- | --- |
    | 連線名稱 * |為連接器輸入任何名稱。 |
    | 整合帳戶 * |輸入整合帳戶的名稱。 請確定應用程式整合帳戶和邏輯位於 hello 相同的 Azure 位置。 |

5.  當您完成時，您的連線詳細資料看起來應該類似 toothis 範例。 選擇 建立您的連線，toofinish**建立**。

    ![整合帳戶連線已建立](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    現在已建立您的連線。

    ![整合帳戶連線詳細資料](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>由協議名稱編碼 X12 訊息

如果您選擇 tooencode X12 訊息的協議名稱，開啟 hello**名稱的 X12 協議**清單中，輸入或選取您現有的 X12 協議。 輸入 hello XML 訊息 tooencode。

![輸入 X12 協議名稱和 XML 訊息 tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>由身分識別編碼 X12 訊息

如果您選擇 tooencode X12 訊息的身分識別，輸入 hello 寄件者識別碼、 傳送者辨識符號、 接收者識別碼和接收者辨識符號設定在您的 X12 協議。 選取 hello XML 訊息 tooencode。
   
![提供身分識別傳送者和接收者，選取 XML 訊息 tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>X12 編碼詳細資料

hello X12 編碼連接器會執行這些工作：

* 藉由比對傳送者和接收者內容屬性進行合約解析。
* 序列化 hello EDI 交換，將 XML 編碼訊息轉換成 hello 交換中的 EDI 交易集。
* 套用交易集標頭和結尾區段
* 產生交換控制編號、群組控制編號和每個傳出交換的交易集控制編號
* 取代 hello 裝載資料中的分隔符號
* 驗證 EDI 和夥伴特定屬性
  * Hello 交易集資料元素與 hello 訊息結構描述的結構描述驗證
  * 對交易集資料元素執行 EDI 驗證。
  * 對交易集資料元素執行擴充驗證
* 要求技術和/或功能確認 (若已設定)。
  * 標頭驗證後會產生技術確認。 hello 技術通知會報告對交換標頭和結尾 hello 位址接收者 hello 處理 hello 狀態
  * 內文驗證後會產生功能確認。 hello 功能通知會報告每個處理 hello 收到文件時所遇到的錯誤

## <a name="view-hello-swagger"></a>檢視 hello swagger
請參閱 hello [swagger 詳細資料](/connectors/x12/)。 

## <a name="next-steps"></a>後續步驟
[深入了解 hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack") 

