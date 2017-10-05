---
title: "將 AS2 訊息解碼 - Azure Logic Apps | Microsoft Docs"
description: "如何在 Azure Logic Apps 的企業整合套件中使用 AS2 解碼器"
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
ms.openlocfilehash: a7920b2509fe368c6f7d55e17fe0bf0020c4562c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="2e13d-103">使用企業整合套件將 Azure Logic Apps 的 AS2 訊息解碼</span><span class="sxs-lookup"><span data-stu-id="2e13d-103">Decode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span> 

<span data-ttu-id="2e13d-104">若要在傳輸訊息時建立安全性和可靠性，請使用解碼 AS2 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="2e13d-104">To establish security and reliability while transmitting messages, use the Decode AS2 message connector.</span></span> <span data-ttu-id="2e13d-105">此連接器可透過訊息處置通知 (MDN) 提供數位簽章、解密和通知。</span><span class="sxs-lookup"><span data-stu-id="2e13d-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2e13d-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="2e13d-106">Before you start</span></span>

<span data-ttu-id="2e13d-107">以下是您所需的項目︰</span><span class="sxs-lookup"><span data-stu-id="2e13d-107">Here's the items you need:</span></span>

* <span data-ttu-id="2e13d-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="2e13d-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="2e13d-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="2e13d-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="2e13d-110">您必須有整合帳戶才能使用解碼 AS2 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="2e13d-110">You must have an integration account to use the Decode AS2 message connector.</span></span>
* <span data-ttu-id="2e13d-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="2e13d-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="2e13d-112">已經在整合帳戶中定義的 [AS2 合約](logic-apps-enterprise-integration-as2.md)</span><span class="sxs-lookup"><span data-stu-id="2e13d-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="2e13d-113">解碼 AS2 訊息</span><span class="sxs-lookup"><span data-stu-id="2e13d-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="2e13d-114">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="2e13d-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="2e13d-115">解碼 AS2 訊息連接器沒有觸發程序，因此您必須新增觸發程序 (例如要求觸發程序) 來啟動邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e13d-115">The Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="2e13d-116">在 Logic Apps 設計工具中，新增觸發程序，然後將動作新增至您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e13d-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="2e13d-117">在搜尋方塊中，輸入 "AS2" 做為篩選條件。</span><span class="sxs-lookup"><span data-stu-id="2e13d-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="2e13d-118">選取 [AS2 - 解碼 AS2 訊息]。</span><span class="sxs-lookup"><span data-stu-id="2e13d-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![搜尋 "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="2e13d-120">如果您先前未建立與整合帳戶的任何連線，系統將會提示您立即建立該連線。</span><span class="sxs-lookup"><span data-stu-id="2e13d-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="2e13d-121">替連線命名，然後選取您要連線的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e13d-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![建立整合連線](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="2e13d-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="2e13d-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="2e13d-124">屬性</span><span class="sxs-lookup"><span data-stu-id="2e13d-124">Property</span></span> | <span data-ttu-id="2e13d-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="2e13d-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="2e13d-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="2e13d-126">Connection Name *</span></span> |<span data-ttu-id="2e13d-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="2e13d-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="2e13d-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="2e13d-128">Integration Account *</span></span> |<span data-ttu-id="2e13d-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="2e13d-129">Enter a name for your integration account.</span></span> <span data-ttu-id="2e13d-130">確定您的整合帳戶和邏輯應用程式位於相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="2e13d-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="2e13d-131">當您完成時，連線詳細資料看起來類似此範例。</span><span class="sxs-lookup"><span data-stu-id="2e13d-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="2e13d-132">若要完成連線建立，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="2e13d-132">To finish creating your connection, choose **Create**.</span></span>

    ![整合連線詳細資料](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="2e13d-134">建立您的連線之後 (如此範例所示)，請選取從 [要求] 輸出中的 [內文] 和 [標頭]。</span><span class="sxs-lookup"><span data-stu-id="2e13d-134">After your connection is created, as shown in this example, select **Body** and **Headers** from the Request outputs.</span></span>
   
    ![已建立整合連線](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="2e13d-136">例如：</span><span class="sxs-lookup"><span data-stu-id="2e13d-136">For example:</span></span>

    ![從要求輸出選取內文和標頭](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="2e13d-138">AS2 解碼器詳細資料</span><span class="sxs-lookup"><span data-stu-id="2e13d-138">AS2 decoder details</span></span>

<span data-ttu-id="2e13d-139">解碼 AS2 連接器會執行下列工作︰</span><span class="sxs-lookup"><span data-stu-id="2e13d-139">The Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="2e13d-140">處理 AS2/HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="2e13d-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="2e13d-141">驗證簽章 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="2e13d-141">Verifies the signature (if configured)</span></span>
* <span data-ttu-id="2e13d-142">將訊息解密 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="2e13d-142">Decrypts the messages (if configured)</span></span>
* <span data-ttu-id="2e13d-143">將訊息解壓縮 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="2e13d-143">Decompresses the message (if configured)</span></span>
* <span data-ttu-id="2e13d-144">協調收到的 MDN 與原始輸出訊息</span><span class="sxs-lookup"><span data-stu-id="2e13d-144">Reconciles a received MDN with the original outbound message</span></span>
* <span data-ttu-id="2e13d-145">更新不可否認性資料庫中的記錄並使其相互關聯</span><span class="sxs-lookup"><span data-stu-id="2e13d-145">Updates and correlates records in the non-repudiation database</span></span>
* <span data-ttu-id="2e13d-146">寫入記錄以便進行 AS2 狀態報告</span><span class="sxs-lookup"><span data-stu-id="2e13d-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="2e13d-147">輸出承載內容是以 base64 編碼</span><span class="sxs-lookup"><span data-stu-id="2e13d-147">The output payload contents are base64 encoded</span></span>
* <span data-ttu-id="2e13d-148">決定是否需要 MDN，以及根據 AS2 合約中的組態決定 MDN 應為同步或非同步</span><span class="sxs-lookup"><span data-stu-id="2e13d-148">Determines whether an MDN is required, and whether the MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="2e13d-149">產生同步或非同步 MDN (根據合約組態)</span><span class="sxs-lookup"><span data-stu-id="2e13d-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="2e13d-150">在 MDN 上設定相互關聯權杖和屬性</span><span class="sxs-lookup"><span data-stu-id="2e13d-150">Sets the correlation tokens and properties on the MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="2e13d-151">嘗試此範例</span><span class="sxs-lookup"><span data-stu-id="2e13d-151">Try this sample</span></span>

<span data-ttu-id="2e13d-152">若要嘗試部署可完整運作的邏輯應用程式和範例 AS2 案例，請參閱 [AS2 邏輯應用程式範本和案例](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)。</span><span class="sxs-lookup"><span data-stu-id="2e13d-152">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="2e13d-153">檢視 Swagger</span><span class="sxs-lookup"><span data-stu-id="2e13d-153">View the swagger</span></span>
<span data-ttu-id="2e13d-154">請參閱 [Swagger 詳細資料](/connectors/as2/)。</span><span class="sxs-lookup"><span data-stu-id="2e13d-154">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2e13d-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e13d-155">Next steps</span></span>
[<span data-ttu-id="2e13d-156">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="2e13d-156">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

