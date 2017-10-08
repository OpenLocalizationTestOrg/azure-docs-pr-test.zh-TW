---
title: "aaaDecode AS2 訊息-Azure 邏輯應用程式 |Microsoft 文件"
description: "Toouse hello hello 企業版整合套件中的 AS2 解碼器 Azure 邏輯應用程式的方式"
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
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Azure 邏輯應用程式的解碼 AS2 訊息，以 hello 企業版整合套件 

tooestablish 安全性和可靠性時傳輸訊息，使用 hello 解碼 AS2 訊息連接器。 此連接器可透過訊息處置通知 (MDN) 提供數位簽章、解密和通知。

## <a name="before-you-start"></a>開始之前

以下是您所需要的 hello 項目：

* Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)
* 已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。 您必須為整合帳戶 toouse hello 解碼 AS2 訊息連接器。
* 至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)
* 已經在整合帳戶中定義的 [AS2 合約](logic-apps-enterprise-integration-as2.md)

## <a name="decode-as2-messages"></a>解碼 AS2 訊息

1. [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

2. 沒有觸發程序，hello 解碼 AS2 訊息連接器，所以您必須新增啟動邏輯應用程式，像是要求觸發程序的觸發程序。 在 hello 邏輯應用程式的設計工具，加入觸發程序，然後再加入動作 tooyour 邏輯應用程式。

3.  Hello 搜尋方塊中，輸入您的篩選器"AS2"。 選取 [AS2 - 解碼 AS2 訊息]。
   
    ![搜尋 "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. 如果您先前未建立任何連線 tooyour 整合帳戶，則會提示您 toocreate 現在該連接。 命名您的連線，並選取您想 tooconnect hello 整合帳戶。
   
    ![建立整合連線](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    具有星號的屬性為必要項目。

    | 屬性 | 詳細資料 |
    | --- | --- |
    | 連線名稱 * |為連接器輸入任何名稱。 |
    | 整合帳戶 * |輸入整合帳戶的名稱。 請確定應用程式整合帳戶和邏輯位於 hello 相同的 Azure 位置。 |

5.  當您完成時，您的連線詳細資料看起來應該類似 toothis 範例。 選擇 建立您的連線，toofinish**建立**。

    ![整合連線詳細資料](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. 建立您的連線時，此範例中所示之後，請選取**主體**和**標頭**hello 從要求的輸出。
   
    ![已建立整合連線](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    例如：

    ![從要求輸出選取內文和標頭](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a>AS2 解碼器詳細資料

hello 解碼的 AS2 連接器會執行這些工作： 

* 處理 AS2/HTTP 標頭
* 確認 hello 簽章 （如果有設定）
* 解密 hello 訊息 （若已設定）
* 將解壓縮 hello 訊息 （若已設定）
* 協調收到的 MDN 與 hello 原始輸出訊息
* 更新，並將 hello 不可否認性資料庫中的記錄相互關聯
* 寫入記錄以便進行 AS2 狀態報告
* hello 裝載內容的輸出是以 base64 編碼
* 判斷是否 MDN 是必要項目，是否 hello MDN 應該是同步或非同步根據設定 AS2 協議中
* 產生同步或非同步 MDN (根據合約組態)
* 設定 hello MDN hello 相互關聯 token 和屬性

## <a name="try-this-sample"></a>嘗試此範例

tootry 部署完全正常運作的邏輯應用程式和範例 AS2 案例，請參閱 hello [AS2 邏輯應用程式範本和案例](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)。

## <a name="view-hello-swagger"></a>檢視 hello swagger
請參閱 hello [swagger 詳細資料](/connectors/as2/)。 

## <a name="next-steps"></a>後續步驟
[深入了解 hello 企業版整合套件](logic-apps-enterprise-integration-overview.md) 

