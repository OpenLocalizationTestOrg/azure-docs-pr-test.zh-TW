---
title: "將 X12 訊息編碼 - Azure Logic Apps | Microsoft Docs"
description: "在 Azure Logic Apps 的企業整合套件中使用 X12 訊息編碼器來驗證 EDI 及轉換 XML 編碼的訊息"
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
ms.openlocfilehash: 29d19364b9a98e351c95f13e68a2e63b9f6439f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="7a134-103">使用企業整合套件將 Azure Logic Apps 的 X12 訊息編碼</span><span class="sxs-lookup"><span data-stu-id="7a134-103">Encode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="7a134-104">使用編碼 X12 訊息連接器，可以驗證 EDI 和夥伴特定屬性，交換時將 XML 編碼的訊息轉換成 EDI 交易集，以及要求技術通知、功能通知或兩者。</span><span class="sxs-lookup"><span data-stu-id="7a134-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="7a134-105">若要使用此連接器，您必須將連接器新增至邏輯應用程式中的現有觸發程序。</span><span class="sxs-lookup"><span data-stu-id="7a134-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7a134-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="7a134-106">Before you start</span></span>

<span data-ttu-id="7a134-107">以下是您所需的項目︰</span><span class="sxs-lookup"><span data-stu-id="7a134-107">Here's the items you need:</span></span>

* <span data-ttu-id="7a134-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="7a134-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="7a134-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="7a134-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="7a134-110">您必須有整合帳戶才能使用編碼 X12 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="7a134-110">You must have an integration account to use the Encode X12 message connector.</span></span>
* <span data-ttu-id="7a134-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="7a134-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="7a134-112">已經在整合帳戶中定義的 [X12 合約](logic-apps-enterprise-integration-x12.md)</span><span class="sxs-lookup"><span data-stu-id="7a134-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="7a134-113">編碼 X12 訊息</span><span class="sxs-lookup"><span data-stu-id="7a134-113">Encode X12 messages</span></span>

1. <span data-ttu-id="7a134-114">[建立邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="7a134-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="7a134-115">編碼 X12 訊息連接器沒有觸發程序，因此您必須新增觸發程序 (例如要求觸發程序) 來啟動邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a134-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="7a134-116">在 Logic Apps 設計工具中，新增觸發程序，然後將動作新增至您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a134-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="7a134-117">在搜尋方塊中，輸入 "X12" 做為篩選條件。</span><span class="sxs-lookup"><span data-stu-id="7a134-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="7a134-118">選取 [X12 - 依照合約名稱編碼為 X12 訊息] 或是 [X12 - 依照身分識別編碼為 X12 訊息]。</span><span class="sxs-lookup"><span data-stu-id="7a134-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span></span>
   
    ![搜尋 "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="7a134-120">如果您先前未建立與整合帳戶的任何連線，系統將會提示您立即建立該連線。</span><span class="sxs-lookup"><span data-stu-id="7a134-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="7a134-121">替連線命名，然後選取您要連線的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a134-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![整合帳戶連線](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="7a134-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="7a134-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="7a134-124">屬性</span><span class="sxs-lookup"><span data-stu-id="7a134-124">Property</span></span> | <span data-ttu-id="7a134-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7a134-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="7a134-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="7a134-126">Connection Name *</span></span> |<span data-ttu-id="7a134-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="7a134-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="7a134-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="7a134-128">Integration Account *</span></span> |<span data-ttu-id="7a134-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="7a134-129">Enter a name for your integration account.</span></span> <span data-ttu-id="7a134-130">確定您的整合帳戶和邏輯應用程式位於相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="7a134-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="7a134-131">當您完成時，連線詳細資料看起來類似此範例。</span><span class="sxs-lookup"><span data-stu-id="7a134-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="7a134-132">若要完成連線建立，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="7a134-132">To finish creating your connection, choose **Create**.</span></span>

    ![整合帳戶連線已建立](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="7a134-134">現在已建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="7a134-134">Your connection is now created.</span></span>

    ![整合帳戶連線詳細資料](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="7a134-136">由協議名稱編碼 X12 訊息</span><span class="sxs-lookup"><span data-stu-id="7a134-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="7a134-137">如果您選擇依照合約名稱將 X12 訊息編碼，請開啟 [X12 合約名稱] 清單，輸入或選取現有的 X12 合約。</span><span class="sxs-lookup"><span data-stu-id="7a134-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="7a134-138">輸入 XML 訊息進行編碼。</span><span class="sxs-lookup"><span data-stu-id="7a134-138">Enter the XML message to encode.</span></span>

![輸入 X12 合約名稱和 XML 訊息進行編碼](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="7a134-140">由身分識別編碼 X12 訊息</span><span class="sxs-lookup"><span data-stu-id="7a134-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="7a134-141">如果您選擇依照身分識別將 X12 訊息編碼，請輸入傳送者識別碼、傳送者限定詞、接收者識別碼和接收者限定詞，如 X12 合約中所設定。</span><span class="sxs-lookup"><span data-stu-id="7a134-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="7a134-142">選取要編碼的 XML 訊息。</span><span class="sxs-lookup"><span data-stu-id="7a134-142">Select the XML message to encode.</span></span>
   
![提供傳送者與收件者的身分識別，選取要編碼的 XML 訊息](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="7a134-144">X12 編碼詳細資料</span><span class="sxs-lookup"><span data-stu-id="7a134-144">X12 Encode details</span></span>

<span data-ttu-id="7a134-145">X12 編碼連接器會執行下列工作︰</span><span class="sxs-lookup"><span data-stu-id="7a134-145">The X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="7a134-146">藉由比對傳送者和接收者內容屬性進行合約解析。</span><span class="sxs-lookup"><span data-stu-id="7a134-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="7a134-147">序列化 EDI 交換，將 XML 編碼訊息轉換為交換中的 EDI 交易集。</span><span class="sxs-lookup"><span data-stu-id="7a134-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="7a134-148">套用交易集標頭和結尾區段</span><span class="sxs-lookup"><span data-stu-id="7a134-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="7a134-149">產生交換控制編號、群組控制編號和每個傳出交換的交易集控制編號</span><span class="sxs-lookup"><span data-stu-id="7a134-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="7a134-150">取代承載資料中的分隔符號</span><span class="sxs-lookup"><span data-stu-id="7a134-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="7a134-151">驗證 EDI 和夥伴特定屬性</span><span class="sxs-lookup"><span data-stu-id="7a134-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="7a134-152">針對訊息結構描述進行交易集資料元素的結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="7a134-152">Schema validation of the transaction-set data elements against the message Schema</span></span>
  * <span data-ttu-id="7a134-153">對交易集資料元素執行 EDI 驗證。</span><span class="sxs-lookup"><span data-stu-id="7a134-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="7a134-154">對交易集資料元素執行擴充驗證</span><span class="sxs-lookup"><span data-stu-id="7a134-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="7a134-155">要求技術和/或功能確認 (若已設定)。</span><span class="sxs-lookup"><span data-stu-id="7a134-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="7a134-156">標頭驗證後會產生技術確認。</span><span class="sxs-lookup"><span data-stu-id="7a134-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="7a134-157">技術確認會報告位址接收者處理交換標頭和結尾的狀態</span><span class="sxs-lookup"><span data-stu-id="7a134-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span></span>
  * <span data-ttu-id="7a134-158">內文驗證後會產生功能確認。</span><span class="sxs-lookup"><span data-stu-id="7a134-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="7a134-159">功能確認會報告處理接收的文件時遇到的每個錯誤</span><span class="sxs-lookup"><span data-stu-id="7a134-159">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="7a134-160">檢視 Swagger</span><span class="sxs-lookup"><span data-stu-id="7a134-160">View the swagger</span></span>
<span data-ttu-id="7a134-161">請參閱 [Swagger 詳細資料](/connectors/x12/)。</span><span class="sxs-lookup"><span data-stu-id="7a134-161">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7a134-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a134-162">Next steps</span></span>
[<span data-ttu-id="7a134-163">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="7a134-163">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "了解企業整合套件") 

