---
title: "aaaDecode X12 訊息-Azure 邏輯應用程式 |Microsoft 文件"
description: "驗證 EDI 並產生通知與 hello X12 訊息解碼器 hello 企業版整合套件中，Azure 邏輯應用程式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>解碼 X12 訊息 Azure 邏輯應用程式以 hello 企業版整合套件

與 hello 解碼 X12 訊息連接器，您可以驗證 hello 信封與交易夥伴協議，驗證 EDI 和夥伴特定的屬性、 分割為交易集的交換或保留整個交換，以及產生已處理的交易的認可。 toouse 此連接器，您必須加入現有的觸發程序邏輯應用程式中的 hello 連接器 tooan。

## <a name="before-you-start"></a>開始之前

以下是您所需要的 hello 項目：

* Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)
* 已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。 您必須為整合帳戶 toouse hello 解碼 X12 訊息連接器。
* 至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)
* 已經在整合帳戶中定義的 [X12 合約](logic-apps-enterprise-integration-x12.md)

## <a name="decode-x12-messages"></a>解碼 X12 訊息

1. [建立邏輯應用程式](logic-apps-create-a-logic-app.md)。

2. 沒有觸發程序，hello 解碼 X12 訊息連接器，所以您必須新增啟動邏輯應用程式，像是要求觸發程序的觸發程序。 在 hello 邏輯應用程式的設計工具，加入觸發程序，然後再加入動作 tooyour 邏輯應用程式。

3.  Hello 搜尋方塊中，輸入您的篩選器"x12"。 選取 [X12 - 將 X12 訊息]。
   
    ![搜尋 "x12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. 如果您先前未建立任何連線 tooyour 整合帳戶，則會提示您 toocreate 現在該連接。 命名您的連線，並選取您想 tooconnect hello 整合帳戶。 

    ![提供整合帳戶連線詳細資料](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    具有星號的屬性為必要項目。

    | 屬性 | 詳細資料 |
    | --- | --- |
    | 連線名稱 * |為連接器輸入任何名稱。 |
    | 整合帳戶 * |輸入整合帳戶的名稱。 請確定應用程式整合帳戶和邏輯位於 hello 相同的 Azure 位置。 |

5.  當您完成時，您的連線詳細資料看起來應該類似 toothis 範例。 選擇 建立您的連線，toofinish**建立**。
   
    ![整合帳戶連線詳細資料](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. 建立您的連線時，此範例中所示之後，請選取 hello X12 一般檔案訊息 toodecode。

    ![整合帳戶連線已建立](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    例如：

    ![選取 X12 一般檔案訊息進行解碼](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a>X12 解碼詳細資料

hello X12 解碼連接器會執行這些工作：

* 驗證 hello 信封與交易夥伴協議
* 驗證 EDI 和夥伴特定屬性
  * EDI 結構驗證，以及擴充的結構描述驗證
  * Hello hello 交換信封結構的驗證。
  * 針對 hello 控制結構描述的 hello 信封的結構描述驗證。
  * 針對 hello 訊息結構描述的 hello 交易集資料元素的結構描述驗證。
  * 對交易集資料元素執行 EDI 驗證 
* 驗證 hello 交換、 群組和交易集控制編號並未重複項目
  * 檢查針對先前已接收交換的 hello 交換控制編號。
  * 檢查針對 hello 交換中的其他群組控制編號的 hello 群組控制編號。
  * 檢查 hello 交易集控制編號，針對該群組中的其他交易集控制編號。
* 分割為交易集，hello 交換或保留 hello 整個交換：
  * 將交換分割為交易集 - 暫止發生錯誤的交易集︰將交換分割為交易集，並剖析每個交易集。 
  hello X12 解碼動作會輸出太未通過驗證的交易集`badMessages`，並將輸出 hello 剩餘交易設定太`goodMessages`。
  * 將交換分割為交易集 - 暫止發生錯誤的交換︰將交換分割為交易集，並剖析每個交易集。 
  如果一或多個交易集驗證失敗 hello 交換中，將輸出 hello X12 解碼動作 hello 的所有交易都集在該交換中太`badMessages`。
  * 保留交換-發生錯誤時暫停交易集： 保留 hello 交換和處理序 hello 整個批次的交換。 
  hello X12 解碼動作會輸出太未通過驗證的交易集`badMessages`，並將輸出 hello 剩餘交易設定太`goodMessages`。
  * 保留交換-發生錯誤時暫停交換： 保留 hello 交換和處理序 hello 整個批次的交換。 
  如果一或多個交易集驗證失敗 hello 交換中，將輸出 hello X12 解碼動作 hello 的所有交易都集在該交換中太`badMessages`。 
* 產生技術和/或功能確認 (若已設定)。
  * 標頭驗證後會產生技術確認。 hello 技術通知會報告對交換標頭和結尾 hello 位址接收者 hello 處理 hello 狀態。
  * 內文驗證後會產生功能確認。 hello 功能通知會報告每個處理 hello 收到文件時所遇到的錯誤

## <a name="view-hello-swagger"></a>檢視 hello swagger
請參閱 hello [swagger 詳細資料](/connectors/x12/)。 

## <a name="next-steps"></a>後續步驟
[深入了解 hello Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack") 

