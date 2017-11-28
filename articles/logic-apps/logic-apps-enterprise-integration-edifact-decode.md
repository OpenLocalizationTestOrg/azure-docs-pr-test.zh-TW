---
title: "將 EDIFACT 訊息解碼 - Azure Logic Apps | Microsoft Docs"
description: "在 Azure Logic Apps 的企業整合套件中使用 EDIFACT 解碼器，針對交易集驗證 EDI 及產生通知"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e3787b48037360bf6066ddce2bacba6842213b2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="c2a64-103">使用企業整合套件將 Azure Logic Apps 的 EDIFACT 訊息解碼</span><span class="sxs-lookup"><span data-stu-id="c2a64-103">Decode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="c2a64-104">使用 Decode EDIFACT 訊息連接器，您可以驗證 EDI 和夥伴特定的屬性、將交換分割為交易集或保留整個交換，並產生已處理交易的通知。</span><span class="sxs-lookup"><span data-stu-id="c2a64-104">With the Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="c2a64-105">若要使用此連接器，您必須將連接器新增至邏輯應用程式中的現有觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c2a64-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c2a64-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="c2a64-106">Before you start</span></span>

<span data-ttu-id="c2a64-107">以下是您所需的項目︰</span><span class="sxs-lookup"><span data-stu-id="c2a64-107">Here's the items you need:</span></span>

* <span data-ttu-id="c2a64-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="c2a64-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="c2a64-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="c2a64-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="c2a64-110">您必須有整合帳戶才能使用解碼 EDIFACT 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="c2a64-110">You must have an integration account to use the Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="c2a64-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="c2a64-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="c2a64-112">已經在整合帳戶中定義的 [EDIFACT 合約](logic-apps-enterprise-integration-edifact.md)</span><span class="sxs-lookup"><span data-stu-id="c2a64-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="c2a64-113">解碼 EDIFACT 訊息</span><span class="sxs-lookup"><span data-stu-id="c2a64-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="c2a64-114">[建立邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="c2a64-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="c2a64-115">解碼 EDIFACT 訊息連接器沒有觸發程序，因此您必須新增觸發程序 (例如要求觸發程序) 來啟動邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2a64-115">The Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="c2a64-116">在 Logic Apps 設計工具中，新增觸發程序，然後將動作新增至您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2a64-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3. <span data-ttu-id="c2a64-117">在搜尋方塊中，輸入 "EDIFACT" 做為篩選條件。</span><span class="sxs-lookup"><span data-stu-id="c2a64-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="c2a64-118">選取 [將 EDIFACT 訊息解碼]。</span><span class="sxs-lookup"><span data-stu-id="c2a64-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![搜尋 EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="c2a64-120">如果您先前未建立與整合帳戶的任何連線，系統將會提示您立即建立該連線。</span><span class="sxs-lookup"><span data-stu-id="c2a64-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="c2a64-121">替連線命名，然後選取您要連線的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="c2a64-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![建立整合帳戶](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="c2a64-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="c2a64-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="c2a64-124">屬性</span><span class="sxs-lookup"><span data-stu-id="c2a64-124">Property</span></span> | <span data-ttu-id="c2a64-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="c2a64-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="c2a64-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="c2a64-126">Connection Name *</span></span> |<span data-ttu-id="c2a64-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="c2a64-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="c2a64-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="c2a64-128">Integration Account *</span></span> |<span data-ttu-id="c2a64-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="c2a64-129">Enter a name for your integration account.</span></span> <span data-ttu-id="c2a64-130">確定您的整合帳戶和邏輯應用程式位於相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="c2a64-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

4. <span data-ttu-id="c2a64-131">當您完成連線建立時，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="c2a64-131">When you're done to finish creating your connection, choose **Create**.</span></span> <span data-ttu-id="c2a64-132">您的連線詳細資料看起來類似此範例：</span><span class="sxs-lookup"><span data-stu-id="c2a64-132">Your connection details should look similar to this example:</span></span>

    ![整合帳戶詳細資料](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="c2a64-134">建立您的連線之後 (如此範例所示)，請選取要解碼的 EDIFACT 一般檔案訊息。</span><span class="sxs-lookup"><span data-stu-id="c2a64-134">After your connection is created, as shown in this example, select the EDIFACT flat file message to decode.</span></span>

    ![整合帳戶連線已建立](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="c2a64-136">例如：</span><span class="sxs-lookup"><span data-stu-id="c2a64-136">For example:</span></span>

    ![選取 EDIFACT 一般檔案訊息以便解碼](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="c2a64-138">EDIFACT 解碼器詳細資料</span><span class="sxs-lookup"><span data-stu-id="c2a64-138">EDIFACT decoder details</span></span>

<span data-ttu-id="c2a64-139">解碼 EDIFACT 連接器會執行下列工作︰</span><span class="sxs-lookup"><span data-stu-id="c2a64-139">The Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="c2a64-140">針對交易夥伴協議驗證信封。</span><span class="sxs-lookup"><span data-stu-id="c2a64-140">Validates the envelope against trading partner agreement.</span></span>
* <span data-ttu-id="c2a64-141">比對傳送者辨識符號和識別項，以及接收者辨識符號和識別項，以解析合約。</span><span class="sxs-lookup"><span data-stu-id="c2a64-141">Resolves the agreement by matching the sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="c2a64-142">在交換具有多個交易時，根據合約的接收設定組態，將交換分割成多筆交易。</span><span class="sxs-lookup"><span data-stu-id="c2a64-142">Splits an interchange into multiple transactions when the interchange has more than one transaction based on the agreement's receive settings configuration.</span></span>
* <span data-ttu-id="c2a64-143">解譯交換。</span><span class="sxs-lookup"><span data-stu-id="c2a64-143">Disassembles the interchange.</span></span>
* <span data-ttu-id="c2a64-144">驗證 EDI 和夥伴特定屬性，包括：</span><span class="sxs-lookup"><span data-stu-id="c2a64-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="c2a64-145">驗證交換信封結構</span><span class="sxs-lookup"><span data-stu-id="c2a64-145">Validation of the interchange envelope structure</span></span>
  * <span data-ttu-id="c2a64-146">針對控制結構描述進行信封的結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="c2a64-146">Schema validation of the envelope against the control schema</span></span>
  * <span data-ttu-id="c2a64-147">針對訊息結構描述進行交易集資料元素的結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="c2a64-147">Schema validation of the transaction-set data elements against the message schema</span></span>
  * <span data-ttu-id="c2a64-148">對交易集資料元素執行 EDI 驗證</span><span class="sxs-lookup"><span data-stu-id="c2a64-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="c2a64-149">驗證交換、群組和交易集控制編號並未重複 (若已設定)</span><span class="sxs-lookup"><span data-stu-id="c2a64-149">Verifies that the interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="c2a64-150">針對先前已接收的交換檢查交換控制編號。</span><span class="sxs-lookup"><span data-stu-id="c2a64-150">Checks the interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="c2a64-151">針對交換中的其他群組控制編號檢查群組控制編號。</span><span class="sxs-lookup"><span data-stu-id="c2a64-151">Checks the group control number against other group control numbers in the interchange.</span></span> 
  * <span data-ttu-id="c2a64-152">針對該群組中其他交易集控制編號檢查交易集控制編號。</span><span class="sxs-lookup"><span data-stu-id="c2a64-152">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="c2a64-153">將交換分割為交易集，或保留整個交換︰</span><span class="sxs-lookup"><span data-stu-id="c2a64-153">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="c2a64-154">將交換分割為交易集 - 暫止發生錯誤的交易集︰將交換分割為交易集，並剖析每個交易集。</span><span class="sxs-lookup"><span data-stu-id="c2a64-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="c2a64-155">X12 Decode 動作只會輸出未通過 `badMessages` 驗證的交易集，並將剩餘的交易輸出到 `goodMessages`。</span><span class="sxs-lookup"><span data-stu-id="c2a64-155">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="c2a64-156">將交換分割為交易集 - 暫止發生錯誤的交換︰將交換分割為交易集，並剖析每個交易集。</span><span class="sxs-lookup"><span data-stu-id="c2a64-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="c2a64-157">如果交換中有一或多個交易集無法通過驗證，X12 Decode 動作會將該交換中的所有交易集輸出到 `badMessages`。</span><span class="sxs-lookup"><span data-stu-id="c2a64-157">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="c2a64-158">保留交換 - 暫止發生錯誤的交易集︰保留交換並處理整個批次交換。</span><span class="sxs-lookup"><span data-stu-id="c2a64-158">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="c2a64-159">X12 Decode 動作只會輸出未通過 `badMessages` 驗證的交易集，並將剩餘的交易輸出到 `goodMessages`。</span><span class="sxs-lookup"><span data-stu-id="c2a64-159">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="c2a64-160">保留交換 - 暫止發生錯誤的交換︰保留交換並處理整個批次交換。</span><span class="sxs-lookup"><span data-stu-id="c2a64-160">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="c2a64-161">如果交換中有一或多個交易集無法通過驗證，X12 Decode 動作會將該交換中的所有交易集輸出到 `badMessages`。</span><span class="sxs-lookup"><span data-stu-id="c2a64-161">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
* <span data-ttu-id="c2a64-162">產生技術 (控制) 和/或功能確認 (若已設定)。</span><span class="sxs-lookup"><span data-stu-id="c2a64-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="c2a64-163">技術確認或 CONTRL ACK 會報告完整接收的交換所進行的語法檢查結果。</span><span class="sxs-lookup"><span data-stu-id="c2a64-163">A Technical Acknowledgment or the CONTRL ACK reports the results of a syntactical check of the complete received interchange.</span></span>
  * <span data-ttu-id="c2a64-164">功能確認會確認接受或拒絕已接收的交換或群組</span><span class="sxs-lookup"><span data-stu-id="c2a64-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="c2a64-165">檢視 Swagger 檔案</span><span class="sxs-lookup"><span data-stu-id="c2a64-165">View Swagger file</span></span>
<span data-ttu-id="c2a64-166">若要檢視 EDIFACT 連接器的 Swagger 詳細資料，請參閱 [EDIFACT](/connectors/edifact/)。</span><span class="sxs-lookup"><span data-stu-id="c2a64-166">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2a64-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2a64-167">Next steps</span></span>
[<span data-ttu-id="c2a64-168">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="c2a64-168">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "了解企業整合套件") 

