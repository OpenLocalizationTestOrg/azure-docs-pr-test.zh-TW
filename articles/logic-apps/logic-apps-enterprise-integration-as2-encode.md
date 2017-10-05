---
title: "將 AS2 訊息編碼 - Azure Logic Apps | Microsoft Docs"
description: "如何在 Azure Logic Apps 的企業整合套件中使用 AS2 編碼器"
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
ms.openlocfilehash: 7889bf9e4e02143b6bb4c797531afa54f8647ce5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="95ae4-103">使用企業整合套件將 Azure Logic Apps 的 AS2 訊息編碼</span><span class="sxs-lookup"><span data-stu-id="95ae4-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="95ae4-104">若要在傳輸訊息時建立安全性和可靠性，請使用編碼 AS2 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="95ae4-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span></span> <span data-ttu-id="95ae4-105">此連接器可透過訊息處置通知 (MDN) 提供數位簽章、加密和通知，這也可能導致支援不可否認性。</span><span class="sxs-lookup"><span data-stu-id="95ae4-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="95ae4-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="95ae4-106">Before you start</span></span>

<span data-ttu-id="95ae4-107">以下是您所需的項目︰</span><span class="sxs-lookup"><span data-stu-id="95ae4-107">Here's the items you need:</span></span>

* <span data-ttu-id="95ae4-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="95ae4-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="95ae4-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="95ae4-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="95ae4-110">您必須有整合帳戶才能使用編碼 AS2 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="95ae4-110">You must have an integration account to use the Encode AS2 message connector.</span></span>
* <span data-ttu-id="95ae4-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="95ae4-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="95ae4-112">已經在整合帳戶中定義的 [AS2 合約](logic-apps-enterprise-integration-as2.md)</span><span class="sxs-lookup"><span data-stu-id="95ae4-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="95ae4-113">編碼 AS2 訊息</span><span class="sxs-lookup"><span data-stu-id="95ae4-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="95ae4-114">[建立邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="95ae4-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="95ae4-115">編碼 AS2 訊息連接器沒有觸發程序，因此您必須新增觸發程序 (例如要求觸發程序) 來啟動邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="95ae4-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="95ae4-116">在 Logic Apps 設計工具中，新增觸發程序，然後將動作新增至您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="95ae4-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="95ae4-117">在搜尋方塊中，輸入 "AS2" 做為篩選條件。</span><span class="sxs-lookup"><span data-stu-id="95ae4-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="95ae4-118">選取 [AS2 - 編碼 AS2 訊息]。</span><span class="sxs-lookup"><span data-stu-id="95ae4-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    ![搜尋 "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="95ae4-120">如果您先前未建立與整合帳戶的任何連線，系統將會提示您立即建立該連線。</span><span class="sxs-lookup"><span data-stu-id="95ae4-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="95ae4-121">替連線命名，然後選取您要連線的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="95ae4-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![建立整合帳戶連線](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="95ae4-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="95ae4-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="95ae4-124">屬性</span><span class="sxs-lookup"><span data-stu-id="95ae4-124">Property</span></span> | <span data-ttu-id="95ae4-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="95ae4-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="95ae4-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="95ae4-126">Connection Name *</span></span> |<span data-ttu-id="95ae4-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="95ae4-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="95ae4-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="95ae4-128">Integration Account *</span></span> |<span data-ttu-id="95ae4-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="95ae4-129">Enter a name for your integration account.</span></span> <span data-ttu-id="95ae4-130">確定您的整合帳戶和邏輯應用程式位於相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="95ae4-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="95ae4-131">當您完成時，連線詳細資料看起來類似此範例。</span><span class="sxs-lookup"><span data-stu-id="95ae4-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="95ae4-132">若要完成連線建立，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="95ae4-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![整合連線詳細資料](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="95ae4-134">建立您的連線之後 (如此範例所示)，提供您合約中設定的 **[AS2-From]** 、**[AS2-To]** 識別碼詳細資訊，以及 **[內文]** \(這是訊息承載)。</span><span class="sxs-lookup"><span data-stu-id="95ae4-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span></span>
   
    ![提供必要欄位](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="95ae4-136">AS2 編碼器詳細資料</span><span class="sxs-lookup"><span data-stu-id="95ae4-136">AS2 encoder details</span></span>

<span data-ttu-id="95ae4-137">編碼 AS2 連接器會執行下列工作︰</span><span class="sxs-lookup"><span data-stu-id="95ae4-137">The Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="95ae4-138">套用 AS2/HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="95ae4-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="95ae4-139">簽署外寄訊息 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="95ae4-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="95ae4-140">加密外寄訊息 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="95ae4-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="95ae4-141">壓縮訊息 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="95ae4-141">Compresses the message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="95ae4-142">嘗試此範例</span><span class="sxs-lookup"><span data-stu-id="95ae4-142">Try this sample</span></span>

<span data-ttu-id="95ae4-143">若要嘗試部署可完整運作的邏輯應用程式和範例 AS2 案例，請參閱 [AS2 邏輯應用程式範本和案例](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)。</span><span class="sxs-lookup"><span data-stu-id="95ae4-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="95ae4-144">檢視 Swagger</span><span class="sxs-lookup"><span data-stu-id="95ae4-144">View the swagger</span></span>
<span data-ttu-id="95ae4-145">請參閱 [Swagger 詳細資料](/connectors/as2/)。</span><span class="sxs-lookup"><span data-stu-id="95ae4-145">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="95ae4-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="95ae4-146">Next steps</span></span>
[<span data-ttu-id="95ae4-147">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="95ae4-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "了解企業整合套件") 

