---
title: "aaaAdd hello Azure 邏輯應用程式中的 Twilio 連接器 |Microsoft 文件"
description: "使用 REST API 參數 hello Twilio 連接器的概觀"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a>開始使用 hello Twilio 連接器
連線 tooTwilio toosend，並接收全域 SMS、 多媒體和 IP 的訊息。 您可以利用 Twilio 來：

* 建置您的商務流程根據 hello 您 Twilio 從取得的資料。 
* 使用會取得訊息、列出訊息等等的動作。 這些動作取得回應，然後再 hello 輸出適用於其他動作。 舉例來說，當您收到新的 Twilio 訊息時，您可以取得此訊息，並在服務匯流排工作流程中使用。 

從建立邏輯應用程式開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="create-a-connection-tootwilio"></a>建立連接 tooTwilio
當您新增此連接器 tooyour 邏輯應用程式時，請輸入 hello Twilio 值：

| 屬性 | 必要 | 說明 |
| --- | --- | --- |
| 帳戶識別碼 |是 |輸入您的 Twilio 帳戶識別碼 |
| 存取權杖 |是 |輸入您的 Twilio 存取權杖 |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

如果您沒有 Twilio 存取權杖，請參閱[使用者身分識別和存取權杖](https://www.twilio.com/docs/api/chat/guides/identity)。

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/twilio/)。

## <a name="more-connectors"></a>其他連接器
返回 toohello [Api 清單](apis-list.md)。
