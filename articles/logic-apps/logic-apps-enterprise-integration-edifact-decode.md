---
title: "aaaDecode EDIFACT 訊息-Azure 邏輯應用程式 |Microsoft 文件"
description: "驗證 EDI 並產生通知與 hello EDIFACT 訊息解碼器 hello 企業版整合套件中，Azure 邏輯應用程式"
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
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="b3164-103">Azure 邏輯應用程式的 EDIFACT 訊息解碼以 hello 企業版整合套件</span><span class="sxs-lookup"><span data-stu-id="b3164-103">Decode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="b3164-104">與 hello 解碼 EDIFACT 訊息連接器，您可以驗證 EDI 和夥伴特定的屬性、 分割為交易集的交換或保留整個交換，以及產生通知已處理的交易。</span><span class="sxs-lookup"><span data-stu-id="b3164-104">With hello Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="b3164-105">toouse 此連接器，您必須加入現有的觸發程序邏輯應用程式中的 hello 連接器 tooan。</span><span class="sxs-lookup"><span data-stu-id="b3164-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="b3164-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="b3164-106">Before you start</span></span>

<span data-ttu-id="b3164-107">以下是您所需要的 hello 項目：</span><span class="sxs-lookup"><span data-stu-id="b3164-107">Here's hello items you need:</span></span>

* <span data-ttu-id="b3164-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="b3164-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="b3164-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="b3164-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="b3164-110">您必須為整合帳戶 toouse hello 解碼 EDIFACT 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="b3164-110">You must have an integration account toouse hello Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="b3164-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="b3164-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="b3164-112">已經在整合帳戶中定義的 [EDIFACT 合約](logic-apps-enterprise-integration-edifact.md)</span><span class="sxs-lookup"><span data-stu-id="b3164-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="b3164-113">解碼 EDIFACT 訊息</span><span class="sxs-lookup"><span data-stu-id="b3164-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="b3164-114">[建立邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="b3164-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="b3164-115">沒有觸發程序，hello 解碼 EDIFACT 訊息連接器，所以您必須新增啟動邏輯應用程式，像是要求觸發程序的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="b3164-115">hello Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="b3164-116">在 hello 邏輯應用程式的設計工具，加入觸發程序，然後再加入動作 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3164-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3. <span data-ttu-id="b3164-117">在 hello 搜尋方塊中輸入"EDIFACT"做為您的篩選器。</span><span class="sxs-lookup"><span data-stu-id="b3164-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="b3164-118">選取 [將 EDIFACT 訊息解碼]。</span><span class="sxs-lookup"><span data-stu-id="b3164-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![搜尋 EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="b3164-120">如果您先前未建立任何連線 tooyour 整合帳戶，則會提示您 toocreate 現在該連接。</span><span class="sxs-lookup"><span data-stu-id="b3164-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="b3164-121">命名您的連線，並選取您想 tooconnect hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3164-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![建立整合帳戶](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="b3164-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="b3164-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="b3164-124">屬性</span><span class="sxs-lookup"><span data-stu-id="b3164-124">Property</span></span> | <span data-ttu-id="b3164-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="b3164-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="b3164-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="b3164-126">Connection Name *</span></span> |<span data-ttu-id="b3164-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="b3164-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="b3164-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="b3164-128">Integration Account *</span></span> |<span data-ttu-id="b3164-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="b3164-129">Enter a name for your integration account.</span></span> <span data-ttu-id="b3164-130">請確定應用程式整合帳戶和邏輯位於 hello 相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="b3164-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

4. <span data-ttu-id="b3164-131">當您完成建立您的連線 toofinish 時，選擇 **建立**。</span><span class="sxs-lookup"><span data-stu-id="b3164-131">When you're done toofinish creating your connection, choose **Create**.</span></span> <span data-ttu-id="b3164-132">連接詳細資料，應該看起來類似 toothis 範例：</span><span class="sxs-lookup"><span data-stu-id="b3164-132">Your connection details should look similar toothis example:</span></span>

    ![整合帳戶詳細資料](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="b3164-134">建立您的連線時，此範例中所示之後，請選取 hello EDIFACT 一般檔案訊息 toodecode。</span><span class="sxs-lookup"><span data-stu-id="b3164-134">After your connection is created, as shown in this example, select hello EDIFACT flat file message toodecode.</span></span>

    ![整合帳戶連線已建立](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="b3164-136">例如：</span><span class="sxs-lookup"><span data-stu-id="b3164-136">For example:</span></span>

    ![選取 EDIFACT 一般檔案訊息以便解碼](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="b3164-138">EDIFACT 解碼器詳細資料</span><span class="sxs-lookup"><span data-stu-id="b3164-138">EDIFACT decoder details</span></span>

<span data-ttu-id="b3164-139">hello 解碼 EDIFACT 連接器會執行這些工作：</span><span class="sxs-lookup"><span data-stu-id="b3164-139">hello Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="b3164-140">驗證 hello 信封與交易夥伴協議。</span><span class="sxs-lookup"><span data-stu-id="b3164-140">Validates hello envelope against trading partner agreement.</span></span>
* <span data-ttu-id="b3164-141">比對 hello 傳送者辨識符號 & 識別項以及接收者辨識符號 & 識別項，以解析 hello 協議。</span><span class="sxs-lookup"><span data-stu-id="b3164-141">Resolves hello agreement by matching hello sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="b3164-142">Hello 交換具有多個交易根據 hello 協議的接收設定組態時，會分割成多筆交易的交換。</span><span class="sxs-lookup"><span data-stu-id="b3164-142">Splits an interchange into multiple transactions when hello interchange has more than one transaction based on hello agreement's receive settings configuration.</span></span>
* <span data-ttu-id="b3164-143">反組譯 hello 交換。</span><span class="sxs-lookup"><span data-stu-id="b3164-143">Disassembles hello interchange.</span></span>
* <span data-ttu-id="b3164-144">驗證 EDI 和夥伴特定屬性，包括：</span><span class="sxs-lookup"><span data-stu-id="b3164-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="b3164-145">Hello 交換的信封結構的驗證</span><span class="sxs-lookup"><span data-stu-id="b3164-145">Validation of hello interchange envelope structure</span></span>
  * <span data-ttu-id="b3164-146">針對 hello 控制結構描述的 hello 信封的結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="b3164-146">Schema validation of hello envelope against hello control schema</span></span>
  * <span data-ttu-id="b3164-147">針對 hello 訊息結構描述的 hello 交易集資料元素的結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="b3164-147">Schema validation of hello transaction-set data elements against hello message schema</span></span>
  * <span data-ttu-id="b3164-148">對交易集資料元素執行 EDI 驗證</span><span class="sxs-lookup"><span data-stu-id="b3164-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="b3164-149">驗證 hello 交換、 群組和交易集控制編號並未重複 （若已設定）</span><span class="sxs-lookup"><span data-stu-id="b3164-149">Verifies that hello interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="b3164-150">檢查針對先前已接收交換的 hello 交換控制編號。</span><span class="sxs-lookup"><span data-stu-id="b3164-150">Checks hello interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="b3164-151">檢查針對 hello 交換中的其他群組控制編號的 hello 群組控制編號。</span><span class="sxs-lookup"><span data-stu-id="b3164-151">Checks hello group control number against other group control numbers in hello interchange.</span></span> 
  * <span data-ttu-id="b3164-152">檢查 hello 交易集控制編號，針對該群組中的其他交易集控制編號。</span><span class="sxs-lookup"><span data-stu-id="b3164-152">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="b3164-153">分割為交易集，hello 交換或保留 hello 整個交換：</span><span class="sxs-lookup"><span data-stu-id="b3164-153">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="b3164-154">將交換分割為交易集 - 暫止發生錯誤的交易集︰將交換分割為交易集，並剖析每個交易集。</span><span class="sxs-lookup"><span data-stu-id="b3164-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="b3164-155">hello X12 解碼動作會輸出太未通過驗證的交易集`badMessages`，並將輸出 hello 剩餘交易設定太`goodMessages`。</span><span class="sxs-lookup"><span data-stu-id="b3164-155">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="b3164-156">將交換分割為交易集 - 暫止發生錯誤的交換︰將交換分割為交易集，並剖析每個交易集。</span><span class="sxs-lookup"><span data-stu-id="b3164-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="b3164-157">如果一或多個交易集驗證失敗 hello 交換中，將輸出 hello X12 解碼動作 hello 的所有交易都集在該交換中太`badMessages`。</span><span class="sxs-lookup"><span data-stu-id="b3164-157">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="b3164-158">保留交換-發生錯誤時暫停交易集： 保留 hello 交換和處理序 hello 整個批次的交換。</span><span class="sxs-lookup"><span data-stu-id="b3164-158">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="b3164-159">hello X12 解碼動作會輸出太未通過驗證的交易集`badMessages`，並將輸出 hello 剩餘交易設定太`goodMessages`。</span><span class="sxs-lookup"><span data-stu-id="b3164-159">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="b3164-160">保留交換-發生錯誤時暫停交換： 保留 hello 交換和處理序 hello 整個批次的交換。</span><span class="sxs-lookup"><span data-stu-id="b3164-160">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="b3164-161">如果一或多個交易集驗證失敗 hello 交換中，將輸出 hello X12 解碼動作 hello 的所有交易都集在該交換中太`badMessages`。</span><span class="sxs-lookup"><span data-stu-id="b3164-161">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
* <span data-ttu-id="b3164-162">產生技術 (控制) 和/或功能確認 (若已設定)。</span><span class="sxs-lookup"><span data-stu-id="b3164-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="b3164-163">技術通知或 hello CONTRL 通知會報告 hello 的 hello 完整接收的交換進行語法檢查的結果。</span><span class="sxs-lookup"><span data-stu-id="b3164-163">A Technical Acknowledgment or hello CONTRL ACK reports hello results of a syntactical check of hello complete received interchange.</span></span>
  * <span data-ttu-id="b3164-164">功能確認會確認接受或拒絕已接收的交換或群組</span><span class="sxs-lookup"><span data-stu-id="b3164-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="b3164-165">檢視 Swagger 檔案</span><span class="sxs-lookup"><span data-stu-id="b3164-165">View Swagger file</span></span>
<span data-ttu-id="b3164-166">tooview hello Swagger 詳細資料，hello EDIFACT 連接器，請參閱[EDIFACT](/connectors/edifact/)。</span><span class="sxs-lookup"><span data-stu-id="b3164-166">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3164-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3164-167">Next steps</span></span>
[<span data-ttu-id="b3164-168">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="b3164-168">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack") 

