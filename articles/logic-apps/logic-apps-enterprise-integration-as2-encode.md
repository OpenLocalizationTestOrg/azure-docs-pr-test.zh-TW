---
title: "aaaEncode AS2 訊息-Azure 邏輯應用程式 |Microsoft 文件"
description: "Toouse hello hello 企業版整合套件中的 AS2 編碼器 Azure 邏輯應用程式的方式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="5df5a-103">Azure 邏輯應用程式的編碼 AS2 訊息，以 hello 企業版整合套件</span><span class="sxs-lookup"><span data-stu-id="5df5a-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="5df5a-104">tooestablish 安全性和可靠性時傳輸訊息，使用 hello 編碼的 AS2 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="5df5a-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="5df5a-105">此連接器提供數位簽章、 加密及通知透過訊息處理通知 (MDN)，這也會 toosupport 使用於不可否認性。</span><span class="sxs-lookup"><span data-stu-id="5df5a-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5df5a-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="5df5a-106">Before you start</span></span>

<span data-ttu-id="5df5a-107">以下是您所需要的 hello 項目：</span><span class="sxs-lookup"><span data-stu-id="5df5a-107">Here's hello items you need:</span></span>

* <span data-ttu-id="5df5a-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="5df5a-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="5df5a-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="5df5a-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="5df5a-110">您必須為整合帳戶 toouse hello 編碼的 AS2 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="5df5a-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="5df5a-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="5df5a-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="5df5a-112">已經在整合帳戶中定義的 [AS2 合約](logic-apps-enterprise-integration-as2.md)</span><span class="sxs-lookup"><span data-stu-id="5df5a-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="5df5a-113">編碼 AS2 訊息</span><span class="sxs-lookup"><span data-stu-id="5df5a-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="5df5a-114">[建立邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="5df5a-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="5df5a-115">沒有觸發程序，hello 編碼的 AS2 訊息連接器，所以您必須新增啟動邏輯應用程式，像是要求觸發程序的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5df5a-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="5df5a-116">在 hello 邏輯應用程式的設計工具，加入觸發程序，然後再加入動作 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="5df5a-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="5df5a-117">Hello 搜尋方塊中，輸入您的篩選器"AS2"。</span><span class="sxs-lookup"><span data-stu-id="5df5a-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="5df5a-118">選取 [AS2 - 編碼 AS2 訊息]。</span><span class="sxs-lookup"><span data-stu-id="5df5a-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![搜尋 "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="5df5a-120">如果您先前未建立任何連線 tooyour 整合帳戶，則會提示您 toocreate 現在該連接。</span><span class="sxs-lookup"><span data-stu-id="5df5a-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="5df5a-121">命名您的連線，並選取您想 tooconnect hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="5df5a-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![建立連線 toointegration 帳戶](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="5df5a-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="5df5a-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="5df5a-124">屬性</span><span class="sxs-lookup"><span data-stu-id="5df5a-124">Property</span></span> | <span data-ttu-id="5df5a-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="5df5a-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="5df5a-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="5df5a-126">Connection Name *</span></span> |<span data-ttu-id="5df5a-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="5df5a-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="5df5a-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="5df5a-128">Integration Account *</span></span> |<span data-ttu-id="5df5a-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="5df5a-129">Enter a name for your integration account.</span></span> <span data-ttu-id="5df5a-130">請確定應用程式整合帳戶和邏輯位於 hello 相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="5df5a-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="5df5a-131">當您完成時，您的連線詳細資料看起來應該類似 toothis 範例。</span><span class="sxs-lookup"><span data-stu-id="5df5a-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="5df5a-132">選擇 建立您的連線，toofinish**建立**。</span><span class="sxs-lookup"><span data-stu-id="5df5a-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![整合連線詳細資料](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="5df5a-134">建立您的連線時，此範例中所示之後，提供詳細資料**AS2-從**， **AS2 tooidentifiers**為您的合約中設定和**主體**，也就是hello 訊息裝載。</span><span class="sxs-lookup"><span data-stu-id="5df5a-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![提供必要欄位](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="5df5a-136">AS2 編碼器詳細資料</span><span class="sxs-lookup"><span data-stu-id="5df5a-136">AS2 encoder details</span></span>

<span data-ttu-id="5df5a-137">hello 編碼的 AS2 連接器會執行這些工作：</span><span class="sxs-lookup"><span data-stu-id="5df5a-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="5df5a-138">套用 AS2/HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="5df5a-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="5df5a-139">簽署外寄訊息 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="5df5a-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="5df5a-140">加密外寄訊息 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="5df5a-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="5df5a-141">壓縮 hello 訊息 （若已設定）</span><span class="sxs-lookup"><span data-stu-id="5df5a-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="5df5a-142">嘗試此範例</span><span class="sxs-lookup"><span data-stu-id="5df5a-142">Try this sample</span></span>

<span data-ttu-id="5df5a-143">tootry 部署完全正常運作的邏輯應用程式和範例 AS2 案例，請參閱 hello [AS2 邏輯應用程式範本和案例](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)。</span><span class="sxs-lookup"><span data-stu-id="5df5a-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="5df5a-144">檢視 hello swagger</span><span class="sxs-lookup"><span data-stu-id="5df5a-144">View hello swagger</span></span>
<span data-ttu-id="5df5a-145">請參閱 hello [swagger 詳細資料](/connectors/as2/)。</span><span class="sxs-lookup"><span data-stu-id="5df5a-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5df5a-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5df5a-146">Next steps</span></span>
[<span data-ttu-id="5df5a-147">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="5df5a-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack") 

