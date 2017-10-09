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
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="04888-103">解碼 X12 訊息 Azure 邏輯應用程式以 hello 企業版整合套件</span><span class="sxs-lookup"><span data-stu-id="04888-103">Decode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="04888-104">與 hello 解碼 X12 訊息連接器，您可以驗證 hello 信封與交易夥伴協議，驗證 EDI 和夥伴特定的屬性、 分割為交易集的交換或保留整個交換，以及產生已處理的交易的認可。</span><span class="sxs-lookup"><span data-stu-id="04888-104">With hello Decode X12 message connector, you can validate hello envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="04888-105">toouse 此連接器，您必須加入現有的觸發程序邏輯應用程式中的 hello 連接器 tooan。</span><span class="sxs-lookup"><span data-stu-id="04888-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="04888-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="04888-106">Before you start</span></span>

<span data-ttu-id="04888-107">以下是您所需要的 hello 項目：</span><span class="sxs-lookup"><span data-stu-id="04888-107">Here's hello items you need:</span></span>

* <span data-ttu-id="04888-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="04888-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="04888-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="04888-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="04888-110">您必須為整合帳戶 toouse hello 解碼 X12 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="04888-110">You must have an integration account toouse hello Decode X12 message connector.</span></span>
* <span data-ttu-id="04888-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="04888-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="04888-112">已經在整合帳戶中定義的 [X12 合約](logic-apps-enterprise-integration-x12.md)</span><span class="sxs-lookup"><span data-stu-id="04888-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="04888-113">解碼 X12 訊息</span><span class="sxs-lookup"><span data-stu-id="04888-113">Decode X12 messages</span></span>

1. <span data-ttu-id="04888-114">[建立邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="04888-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="04888-115">沒有觸發程序，hello 解碼 X12 訊息連接器，所以您必須新增啟動邏輯應用程式，像是要求觸發程序的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="04888-115">hello Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="04888-116">在 hello 邏輯應用程式的設計工具，加入觸發程序，然後再加入動作 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="04888-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="04888-117">Hello 搜尋方塊中，輸入您的篩選器"x12"。</span><span class="sxs-lookup"><span data-stu-id="04888-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="04888-118">選取 [X12 - 將 X12 訊息]。</span><span class="sxs-lookup"><span data-stu-id="04888-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![搜尋 "x12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="04888-120">如果您先前未建立任何連線 tooyour 整合帳戶，則會提示您 toocreate 現在該連接。</span><span class="sxs-lookup"><span data-stu-id="04888-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="04888-121">命名您的連線，並選取您想 tooconnect hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="04888-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 

    ![提供整合帳戶連線詳細資料](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="04888-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="04888-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="04888-124">屬性</span><span class="sxs-lookup"><span data-stu-id="04888-124">Property</span></span> | <span data-ttu-id="04888-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="04888-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="04888-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="04888-126">Connection Name *</span></span> |<span data-ttu-id="04888-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="04888-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="04888-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="04888-128">Integration Account *</span></span> |<span data-ttu-id="04888-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="04888-129">Enter a name for your integration account.</span></span> <span data-ttu-id="04888-130">請確定應用程式整合帳戶和邏輯位於 hello 相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="04888-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="04888-131">當您完成時，您的連線詳細資料看起來應該類似 toothis 範例。</span><span class="sxs-lookup"><span data-stu-id="04888-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="04888-132">選擇 建立您的連線，toofinish**建立**。</span><span class="sxs-lookup"><span data-stu-id="04888-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![整合帳戶連線詳細資料](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="04888-134">建立您的連線時，此範例中所示之後，請選取 hello X12 一般檔案訊息 toodecode。</span><span class="sxs-lookup"><span data-stu-id="04888-134">After your connection is created, as shown in this example, select hello X12 flat file message toodecode.</span></span>

    ![整合帳戶連線已建立](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="04888-136">例如：</span><span class="sxs-lookup"><span data-stu-id="04888-136">For example:</span></span>

    ![選取 X12 一般檔案訊息進行解碼](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="04888-138">X12 解碼詳細資料</span><span class="sxs-lookup"><span data-stu-id="04888-138">X12 Decode details</span></span>

<span data-ttu-id="04888-139">hello X12 解碼連接器會執行這些工作：</span><span class="sxs-lookup"><span data-stu-id="04888-139">hello X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="04888-140">驗證 hello 信封與交易夥伴協議</span><span class="sxs-lookup"><span data-stu-id="04888-140">Validates hello envelope against trading partner agreement</span></span>
* <span data-ttu-id="04888-141">驗證 EDI 和夥伴特定屬性</span><span class="sxs-lookup"><span data-stu-id="04888-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="04888-142">EDI 結構驗證，以及擴充的結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="04888-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="04888-143">Hello hello 交換信封結構的驗證。</span><span class="sxs-lookup"><span data-stu-id="04888-143">Validation of hello structure of hello interchange envelope.</span></span>
  * <span data-ttu-id="04888-144">針對 hello 控制結構描述的 hello 信封的結構描述驗證。</span><span class="sxs-lookup"><span data-stu-id="04888-144">Schema validation of hello envelope against hello control schema.</span></span>
  * <span data-ttu-id="04888-145">針對 hello 訊息結構描述的 hello 交易集資料元素的結構描述驗證。</span><span class="sxs-lookup"><span data-stu-id="04888-145">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="04888-146">對交易集資料元素執行 EDI 驗證</span><span class="sxs-lookup"><span data-stu-id="04888-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="04888-147">驗證 hello 交換、 群組和交易集控制編號並未重複項目</span><span class="sxs-lookup"><span data-stu-id="04888-147">Verifies that hello interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="04888-148">檢查針對先前已接收交換的 hello 交換控制編號。</span><span class="sxs-lookup"><span data-stu-id="04888-148">Checks hello interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="04888-149">檢查針對 hello 交換中的其他群組控制編號的 hello 群組控制編號。</span><span class="sxs-lookup"><span data-stu-id="04888-149">Checks hello group control number against other group control numbers in hello interchange.</span></span>
  * <span data-ttu-id="04888-150">檢查 hello 交易集控制編號，針對該群組中的其他交易集控制編號。</span><span class="sxs-lookup"><span data-stu-id="04888-150">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="04888-151">分割為交易集，hello 交換或保留 hello 整個交換：</span><span class="sxs-lookup"><span data-stu-id="04888-151">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="04888-152">將交換分割為交易集 - 暫止發生錯誤的交易集︰將交換分割為交易集，並剖析每個交易集。</span><span class="sxs-lookup"><span data-stu-id="04888-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="04888-153">hello X12 解碼動作會輸出太未通過驗證的交易集`badMessages`，並將輸出 hello 剩餘交易設定太`goodMessages`。</span><span class="sxs-lookup"><span data-stu-id="04888-153">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="04888-154">將交換分割為交易集 - 暫止發生錯誤的交換︰將交換分割為交易集，並剖析每個交易集。</span><span class="sxs-lookup"><span data-stu-id="04888-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="04888-155">如果一或多個交易集驗證失敗 hello 交換中，將輸出 hello X12 解碼動作 hello 的所有交易都集在該交換中太`badMessages`。</span><span class="sxs-lookup"><span data-stu-id="04888-155">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="04888-156">保留交換-發生錯誤時暫停交易集： 保留 hello 交換和處理序 hello 整個批次的交換。</span><span class="sxs-lookup"><span data-stu-id="04888-156">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="04888-157">hello X12 解碼動作會輸出太未通過驗證的交易集`badMessages`，並將輸出 hello 剩餘交易設定太`goodMessages`。</span><span class="sxs-lookup"><span data-stu-id="04888-157">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="04888-158">保留交換-發生錯誤時暫停交換： 保留 hello 交換和處理序 hello 整個批次的交換。</span><span class="sxs-lookup"><span data-stu-id="04888-158">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="04888-159">如果一或多個交易集驗證失敗 hello 交換中，將輸出 hello X12 解碼動作 hello 的所有交易都集在該交換中太`badMessages`。</span><span class="sxs-lookup"><span data-stu-id="04888-159">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span> 
* <span data-ttu-id="04888-160">產生技術和/或功能確認 (若已設定)。</span><span class="sxs-lookup"><span data-stu-id="04888-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="04888-161">標頭驗證後會產生技術確認。</span><span class="sxs-lookup"><span data-stu-id="04888-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="04888-162">hello 技術通知會報告對交換標頭和結尾 hello 位址接收者 hello 處理 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="04888-162">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver.</span></span>
  * <span data-ttu-id="04888-163">內文驗證後會產生功能確認。</span><span class="sxs-lookup"><span data-stu-id="04888-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="04888-164">hello 功能通知會報告每個處理 hello 收到文件時所遇到的錯誤</span><span class="sxs-lookup"><span data-stu-id="04888-164">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="04888-165">檢視 hello swagger</span><span class="sxs-lookup"><span data-stu-id="04888-165">View hello swagger</span></span>
<span data-ttu-id="04888-166">請參閱 hello [swagger 詳細資料](/connectors/x12/)。</span><span class="sxs-lookup"><span data-stu-id="04888-166">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="04888-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04888-167">Next steps</span></span>
[<span data-ttu-id="04888-168">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="04888-168">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack") 

