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
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="05dbe-103">開始使用 hello Twilio 連接器</span><span class="sxs-lookup"><span data-stu-id="05dbe-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="05dbe-104">連線 tooTwilio toosend，並接收全域 SMS、 多媒體和 IP 的訊息。</span><span class="sxs-lookup"><span data-stu-id="05dbe-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="05dbe-105">您可以利用 Twilio 來：</span><span class="sxs-lookup"><span data-stu-id="05dbe-105">With Twilio, you can:</span></span>

* <span data-ttu-id="05dbe-106">建置您的商務流程根據 hello 您 Twilio 從取得的資料。</span><span class="sxs-lookup"><span data-stu-id="05dbe-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="05dbe-107">使用會取得訊息、列出訊息等等的動作。</span><span class="sxs-lookup"><span data-stu-id="05dbe-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="05dbe-108">這些動作取得回應，然後再 hello 輸出適用於其他動作。</span><span class="sxs-lookup"><span data-stu-id="05dbe-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="05dbe-109">舉例來說，當您收到新的 Twilio 訊息時，您可以取得此訊息，並在服務匯流排工作流程中使用。</span><span class="sxs-lookup"><span data-stu-id="05dbe-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="05dbe-110">從建立邏輯應用程式開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="05dbe-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="05dbe-111">建立連接 tooTwilio</span><span class="sxs-lookup"><span data-stu-id="05dbe-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="05dbe-112">當您新增此連接器 tooyour 邏輯應用程式時，請輸入 hello Twilio 值：</span><span class="sxs-lookup"><span data-stu-id="05dbe-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="05dbe-113">屬性</span><span class="sxs-lookup"><span data-stu-id="05dbe-113">Property</span></span> | <span data-ttu-id="05dbe-114">必要</span><span class="sxs-lookup"><span data-stu-id="05dbe-114">Required</span></span> | <span data-ttu-id="05dbe-115">說明</span><span class="sxs-lookup"><span data-stu-id="05dbe-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05dbe-116">帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="05dbe-116">Account ID</span></span> |<span data-ttu-id="05dbe-117">是</span><span class="sxs-lookup"><span data-stu-id="05dbe-117">Yes</span></span> |<span data-ttu-id="05dbe-118">輸入您的 Twilio 帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="05dbe-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="05dbe-119">存取權杖</span><span class="sxs-lookup"><span data-stu-id="05dbe-119">Access Token</span></span> |<span data-ttu-id="05dbe-120">是</span><span class="sxs-lookup"><span data-stu-id="05dbe-120">Yes</span></span> |<span data-ttu-id="05dbe-121">輸入您的 Twilio 存取權杖</span><span class="sxs-lookup"><span data-stu-id="05dbe-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="05dbe-122">如果您沒有 Twilio 存取權杖，請參閱[使用者身分識別和存取權杖](https://www.twilio.com/docs/api/chat/guides/identity)。</span><span class="sxs-lookup"><span data-stu-id="05dbe-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="05dbe-123">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="05dbe-123">Connector-specific details</span></span>

<span data-ttu-id="05dbe-124">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/twilio/)。</span><span class="sxs-lookup"><span data-stu-id="05dbe-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="05dbe-125">其他連接器</span><span class="sxs-lookup"><span data-stu-id="05dbe-125">More connectors</span></span>
<span data-ttu-id="05dbe-126">返回 toohello [Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="05dbe-126">Go back toohello [APIs list](apis-list.md).</span></span>
