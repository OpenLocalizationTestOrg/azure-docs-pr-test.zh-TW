---
title: "邏輯應用程式連接器的 aaaOverview |Microsoft 文件"
description: "可在邏輯應用程式中使用的連接器概觀"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a>在邏輯應用程式中使用連接器
連接器會提供跨服務、 通訊協定和平台快速存取 tooevents、 資料和動作。  hello 的 Logic Apps 支援的連接器的完整清單可以[在這裡找到](apis-list.md)。  連接器可用來當作觸發程序或邏輯應用程式中的動作，而且可能需要設定*連接*toouse (例如： 授權 Twitter 帳戶 tooaccess 或張貼您的身分)。

## <a name="basics"></a>基本概念
連接器是託管的服務，您可以存取 Dynamics、 Azure、 Salesforce 等其他服務使用邏輯應用程式 toointegrate 一部分[多](apis-list.md)。  連接器是由 Microsoft 所部署和管理，因此您可以建置規模、輸送量和安全性都有人幫您處理的整合工作流程。  您可以藉由搜尋並選取 連接器動作新增連接器 tooa 邏輯應用程式或觸發程序底下**顯示 Microsoft managed Api**。

![可供選取觸發程序的 [動作] 功能表][1]

每個連接器動作或觸發程序會將屬性 tooconfigure 的設定。  您可以按一下 hello 資訊按鈕 toolearn 深入了解動作，或參考其文件[toolearn 詳細](apis-list.md)。

如果您想 toointegrate 與服務或應用程式開發介面不是尚未連接器，您也可以擴充邏輯應用程式透過[自訂連接器](../logic-apps/logic-apps-create-api-app.md)或只需要呼叫直接 toohello 服務透過 HTTP 之類的通訊協定。

## <a name="triggers"></a>觸發程序
某些連接器有觸發程序，這表示從該連接器的事件將引發邏輯應用程式，並傳入 hello 觸發程序的一部分的任何資料。  觸發程序永遠是 hello 邏輯應用程式中的第一個步驟。  受歡迎的觸發程序所包含的作業如下︰

* 循環 - 每小時執行一次
* 收到 HTTP 要求時
* 項目加入 tooa 佇列中時
* 收到電子郵件時

某些觸發程序會引發 hello 即時事件發生時透過通知 toohello 邏輯應用程式和其他人將會需要 hello 邏輯應用程式會檢查的頻率 （向上 tooevery 15 秒) 事件的 hello 服務上設定循環間隔。  

一旦收到事件時，會引發 hello 邏輯應用程式執行，並開始 hello 工作流程中的 hello 動作。  您也會無法 tooaccess 整個 hello 工作流程觸發 hello 中的任何資料 （如範例 hello 'On 新推文' 觸發程序會傳入 hello 推文 hello 執行）。

## <a name="actions"></a>動作
大部分的連接器會有一個或多個可當做 hello 工作流程的一部分執行的動作。  動作是 hello 執行之後，就可能發生的任何步驟已引發觸發程序。  tooadd 動作按一下 hello**新步驟**按鈕並搜尋 hello 想 toouse 連接器。  一旦選取 (和之後設定任何[連線](#connections)可能有必要) 您會看到 hello 動作卡，您可以設定。  您可以按一下任一 hello 語彙基元的輸出，從上一個步驟中選取資料，或視需要輸入中的任何其他設定。

![設定連接器動作][2]

## <a name="connections"></a>連線
大部分的連接器都需要您 tooconfigure*連接*才能夠使用 hello 連接器。  A*連接*是任何登入，或需要 tooaccess hello 連接器的連線設定。  對於使用 OAuth、 建立連接的接點表示登入 hello 服務 （例如 Office 365、 Salesforce 或 GitHub） 可以加密和安全地儲存在 Azure 的密碼存放區存取權杖。  其他連接器 (例如 FTP 和 SQL) 則需要包含伺服器位址、使用者名稱和密碼等組態的連線。  這些連線的組態詳細資料也會加密並安全地儲存。  連線會無法 tooaccess hello 服務只要 hello 服務允許。  Azure Active Directory OAuth 連線 （例如 Office 365 和 Dynamics） 我們可以無限期繼續 toorefresh hello 存取權杖。  其他服務則可能會限制權杖的使用時限，在此時限內，完全不需要重新整理權杖。  一般來說，某些動作 (例如變更密碼) 會導致所有存取權杖失效。  

按一下 [瀏覽]，然後選取 [API 連線]，即可在 Azure 中檢視和管理連線。  從 hello API 連接資源，您可以檢視、 編輯、 更新或重新授權已建立的任何連線。

## <a name="next-steps"></a>後續步驟
* [建立第一個邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)
* [了解邏輯應用程式的常見用法和範例](../logic-apps/logic-apps-examples-and-scenarios.md)
* [開始使用企業整合觸發程序和動作](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
