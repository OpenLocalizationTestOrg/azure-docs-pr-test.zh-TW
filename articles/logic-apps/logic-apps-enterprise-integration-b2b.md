---
title: "aaaCreate B2B 解決方案-Azure 邏輯應用程式 |Microsoft 文件"
description: "邏輯應用程式中接收資料，使用 hello 企業版整合套件 hello B2B 功能"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a>在邏輯與 hello 企業版整合套件中的 hello B2B 功能的應用程式中接收資料

建立具有夥伴和協議的整合帳戶之後，您就準備好 toocreate 商務 toobusiness (B2B) 工作流程應用程式邏輯，以 hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md)。

## <a name="prerequisites"></a>必要條件

toouse hello AS2 與 X12 動作，您必須擁有 Enterprise 整合帳戶。 深入了解[如何 toocreate 企業整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)。

## <a name="create-a-logic-app-with-b2b-connectors"></a>使用 B2B 連接器建立邏輯應用程式

請遵循這些步驟 toocreate B2B 邏輯的應用程式使用 hello AS2 與 X12 動作 tooreceive 資料從交易夥伴：

1. 建立邏輯應用程式，然後[連結您的應用程式 tooyour 整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)。

2. 新增**要求-當 HTTP 要求**觸發程序 tooyour 邏輯應用程式。

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. tooadd hello**解碼的 AS2**動作選取**將動作加入**。

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. toofilter，其中的所有動作 toohello 都輸入 hello 字**as2** hello [搜尋] 方塊中。

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. 選取 hello **AS2 的解碼 AS2 訊息**動作。

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. 新增 hello**主體**想 toouse 做為輸入。 在此範例中，選取 hello hello 觸發程序 hello 邏輯應用程式的 HTTP 要求主體。 或輸入運算式，以輸入 hello 標頭中 hello**標頭**欄位：

    @triggerOutputs()['headers']

7. 新增所需的 hello**標頭**as2，您可以在 hello HTTP 要求標頭中找到。 在此範例中，選取 hello hello HTTP 要求標頭該觸發程序 hello 邏輯應用程式。

8. 現在加入 hello 解碼 X12 訊息的動作。 選取 [新增動作] 。

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. toofilter，其中的所有動作 toohello 都輸入 hello 字**x12** hello [搜尋] 方塊中。

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. 選取 hello **X12-解碼 X12 訊息**動作。

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. 現在，您必須指定 hello 輸入的 toothis 動作。 這項輸入是來自上一個 AS2 動作 hello 的 hello 輸出。

    hello 實際訊息內容的 JSON 物件中，而且是 base64 編碼，因此您必須指定的運算式做為輸入 hello。 
    輸入下列運算式在 hello hello **X12 一般檔案訊息 tooDECODE**輸入的欄位：
    
    @base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])

    現在加入的步驟 toodecode hello X12 資料收到來自交易夥伴的 hello 和輸出的 JSON 物件中的項目。 
    收到 hello 資料 toonotify hello 協力電腦，您可以將回應傳回包含 hello AS2 訊息處理通知 (MDN) 中 HTTP 回應動作。

12. tooadd hello**回應**動作中，選擇**將動作加入**。

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. toofilter，其中的所有動作 toohello 都輸入 hello 字**回應**hello [搜尋] 方塊中。

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. 選取 hello**回應**動作。

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. tooaccess hello hello hello 輸出 MDN**解碼 X12 訊息**動作，集 hello 回應**主體**欄位的這個運算式：

    @base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. 儲存您的工作。

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

您現在已完成 B2B 邏輯應用程式設定。 在真實世界應用程式中，您可能想 toostore hello 解碼 X12 特定業務 (LOB) 應用程式或資料存放區中的資料。 tooconnect 您自己的 LOB 應用程式和應用程式邏輯中使用這些 Api，您可以新增進一步的動作或撰寫自訂應用程式開發介面。

## <a name="features-and-use-cases"></a>功能和使用案例

* hello AS2 與 X12 解碼和編碼動作可讓您在邏輯應用程式中使用業界標準通訊協定交易夥伴間交換資料。
* 與交易夥伴 tooexchange 資料，您可以使用 AS2 與 X12，不論彼此。
* hello B2B 動作可協助您整合帳戶中輕鬆地建立夥伴和協議，及在邏輯應用程式中使用它們。
* 當您使用其他動作延伸您邏輯應用程式的功能時，您可以在其他應用程式與服務 (例如 SalesForce) 之間傳送及接收資料。

## <a name="learn-more"></a>詳細資訊
[深入了解 hello 企業版整合套件](logic-apps-enterprise-integration-overview.md)
