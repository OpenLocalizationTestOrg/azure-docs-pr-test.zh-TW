---
title: "適用於 B2B 企業整合的 X12 訊息 - Azure Logic Apps | Microsoft Docs"
description: "利用 Azure Logic Apps 交換 EDI 格式的 X12 訊息以進行 B2B 企業整合"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 7422d2d5-b1c7-4a11-8c9b-0d8cfa463164
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1bfaa7b31bfed3ada22c83516839ebd95a351854
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="exchange-x12-messages-for-enterprise-integration-with-logic-apps"></a><span data-ttu-id="2179b-103">利用邏輯應用程式交換適用於企業整合的 X12 訊息</span><span class="sxs-lookup"><span data-stu-id="2179b-103">Exchange X12 messages for enterprise integration with logic apps</span></span>

<span data-ttu-id="2179b-104">您必須先建立 X12 合約並將該合約儲存在您的整合帳戶中，才可以交換 X12 訊息。</span><span class="sxs-lookup"><span data-stu-id="2179b-104">Before you can exchange X12 messages for Azure Logic Apps, you must create an X12 agreement and store that agreement in your integration account.</span></span> <span data-ttu-id="2179b-105">以下是如何建立 X12 合約的步驟。</span><span class="sxs-lookup"><span data-stu-id="2179b-105">Here are the steps for how to create an X12 agreement.</span></span>

> [!NOTE]
> <span data-ttu-id="2179b-106">本頁涵蓋 Azure Logic Apps 的 X12 功能。</span><span class="sxs-lookup"><span data-stu-id="2179b-106">This page covers the X12 features for Azure Logic Apps.</span></span> <span data-ttu-id="2179b-107">如需詳細資訊，請參閱 [EDIFACT](logic-apps-enterprise-integration-edifact.md)。</span><span class="sxs-lookup"><span data-stu-id="2179b-107">For more information, see [EDIFACT](logic-apps-enterprise-integration-edifact.md).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2179b-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="2179b-108">Before you start</span></span>

<span data-ttu-id="2179b-109">以下是您所需的項目︰</span><span class="sxs-lookup"><span data-stu-id="2179b-109">Here's the items you need:</span></span>

* <span data-ttu-id="2179b-110">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)</span><span class="sxs-lookup"><span data-stu-id="2179b-110">An [integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) that's already defined and associated with your Azure subscription</span></span>
* <span data-ttu-id="2179b-111">至少已在整合帳戶中定義兩個[夥伴](../logic-apps/logic-apps-enterprise-integration-partners.md)，以及在 [企業身分識別] 之下設定 X12 識別碼</span><span class="sxs-lookup"><span data-stu-id="2179b-111">At least two [partners](../logic-apps/logic-apps-enterprise-integration-partners.md) that are defined in your integration account and configured with the X12 identifier under **Business Identities**</span></span>    
* <span data-ttu-id="2179b-112">要上傳到[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)的必要[結構描述](../logic-apps/logic-apps-enterprise-integration-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="2179b-112">A required [schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) for uploading to your [integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md)</span></span>

<span data-ttu-id="2179b-113">在您[建立整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)、[新增夥伴](logic-apps-enterprise-integration-partners.md)，以及具有您有使用的[結構描述](../logic-apps/logic-apps-enterprise-integration-schemas.md)之後，您可以依照下列步驟建立 X12 合約。</span><span class="sxs-lookup"><span data-stu-id="2179b-113">After you [create an integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md), [add partners](logic-apps-enterprise-integration-partners.md), and have a [schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) that you want to use, you can create an X12 agreement by following these steps.</span></span>

## <a name="create-an-x12-agreement"></a><span data-ttu-id="2179b-114">建立 X12 合約</span><span class="sxs-lookup"><span data-stu-id="2179b-114">Create an X12 agreement</span></span>

1.  <span data-ttu-id="2179b-115">登入 [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="2179b-115">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="2179b-116">從左側功能表中選取 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="2179b-116">From the left menu, select **More services**.</span></span> 

    > [!TIP]
    > <span data-ttu-id="2179b-117">如果沒有看到 [更多服務]，您可能必須先展開功能表。</span><span class="sxs-lookup"><span data-stu-id="2179b-117">If you don't see **More services**, you might have to expand the menu first.</span></span> <span data-ttu-id="2179b-118">在摺疊功能表的頂端，選取 [顯示功能表]。</span><span class="sxs-lookup"><span data-stu-id="2179b-118">At the top of the collapsed menu, select **Show menu**.</span></span>

    ![在左側功能表上選取 [更多服務]](./media/logic-apps-enterprise-integration-x12/account-1.png)

2.  <span data-ttu-id="2179b-120">在搜尋方塊中，輸入 [整合] 做為篩選條件。</span><span class="sxs-lookup"><span data-stu-id="2179b-120">In the search box, type "integration" as your filter.</span></span> <span data-ttu-id="2179b-121">在結果清單中選取 [整合帳戶]。</span><span class="sxs-lookup"><span data-stu-id="2179b-121">In the results list, select **Integration Accounts**.</span></span>  

    ![依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-x12/account-2.png)

3. <span data-ttu-id="2179b-123">在開啟的 [整合帳戶]  刀鋒視窗中，選取您要在其中新增合約的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="2179b-123">In the **Integration Accounts** blade that opens, select the integration account where you want to add the agreement.</span></span>
<span data-ttu-id="2179b-124">如果沒有看到任何整合帳戶，請[先建立一個](../logic-apps/logic-apps-enterprise-integration-accounts.md "關於整合帳戶的一切")。</span><span class="sxs-lookup"><span data-stu-id="2179b-124">If you don't see any integration accounts, [create one first](../logic-apps/logic-apps-enterprise-integration-accounts.md "All about integration accounts").</span></span>

    ![選取您要在其中建立合約的整合帳戶](./media/logic-apps-enterprise-integration-x12/account-3.png)

4. <span data-ttu-id="2179b-126">選取 [概觀]，然後選取 [合約] 圖格。</span><span class="sxs-lookup"><span data-stu-id="2179b-126">Select **Overview**, then select the **Agreements** tile.</span></span> <span data-ttu-id="2179b-127">如果您沒有 [合約] 圖格，請先新增圖格。</span><span class="sxs-lookup"><span data-stu-id="2179b-127">If you don't have an Agreements tile, add the tile first.</span></span> 

    ![選擇 [合約] 圖格](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. <span data-ttu-id="2179b-129">在開啟的 [合約] 刀鋒視窗中選擇 [新增]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="2179b-129">In the Agreements blade that opens, choose **Add**.</span></span>

    ![選擇 [新增]](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)     

6. <span data-ttu-id="2179b-131">在 [新增] 之下，輸入合約的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="2179b-131">Under **Add**, enter a **Name** for your agreement.</span></span> <span data-ttu-id="2179b-132">針對 [合約類型]，選取 **X12**。</span><span class="sxs-lookup"><span data-stu-id="2179b-132">For the agreement type, select **X12**.</span></span> <span data-ttu-id="2179b-133">選取合約的 [主機夥伴]、[主機身分識別]、[來賓夥伴] 和 [來賓身分識別]。</span><span class="sxs-lookup"><span data-stu-id="2179b-133">Select the **Host Partner**, **Host Identity**, **Guest Partner**, and **Guest Identity** for your agreement.</span></span> <span data-ttu-id="2179b-134">如需更多屬性詳細資訊，請參閱此步驟中的資料表。</span><span class="sxs-lookup"><span data-stu-id="2179b-134">For more property details, see the table in this step.</span></span>

    ![提供合約詳細資料](./media/logic-apps-enterprise-integration-x12/x12-1.png)  

    | <span data-ttu-id="2179b-136">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-136">Property</span></span> | <span data-ttu-id="2179b-137">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-137">Description</span></span> |
    | --- | --- |
    | <span data-ttu-id="2179b-138">名稱</span><span class="sxs-lookup"><span data-stu-id="2179b-138">Name</span></span> |<span data-ttu-id="2179b-139">合約的名稱</span><span class="sxs-lookup"><span data-stu-id="2179b-139">Name of the agreement</span></span> |
    | <span data-ttu-id="2179b-140">合約類型</span><span class="sxs-lookup"><span data-stu-id="2179b-140">Agreement Type</span></span> | <span data-ttu-id="2179b-141">應該是 X12</span><span class="sxs-lookup"><span data-stu-id="2179b-141">Should be X12</span></span> |
    | <span data-ttu-id="2179b-142">主控夥伴</span><span class="sxs-lookup"><span data-stu-id="2179b-142">Host Partner</span></span> |<span data-ttu-id="2179b-143">合約需要主控夥伴和來賓夥伴。</span><span class="sxs-lookup"><span data-stu-id="2179b-143">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="2179b-144">主機夥伴代表設定合約的組織。</span><span class="sxs-lookup"><span data-stu-id="2179b-144">The host partner represents the organization that configures the agreement.</span></span> |
    | <span data-ttu-id="2179b-145">主控身分識別</span><span class="sxs-lookup"><span data-stu-id="2179b-145">Host Identity</span></span> |<span data-ttu-id="2179b-146">主控夥伴的識別碼</span><span class="sxs-lookup"><span data-stu-id="2179b-146">An identifier for the host partner</span></span> |
    | <span data-ttu-id="2179b-147">來賓夥伴</span><span class="sxs-lookup"><span data-stu-id="2179b-147">Guest Partner</span></span> |<span data-ttu-id="2179b-148">合約需要主控夥伴和來賓夥伴。</span><span class="sxs-lookup"><span data-stu-id="2179b-148">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="2179b-149">來賓夥伴代表與主控夥伴有生意往來的組織。</span><span class="sxs-lookup"><span data-stu-id="2179b-149">The guest partner represents the organization that's doing business with the host partner.</span></span> |
    | <span data-ttu-id="2179b-150">來賓身分識別</span><span class="sxs-lookup"><span data-stu-id="2179b-150">Guest Identity</span></span> |<span data-ttu-id="2179b-151">來賓合作夥伴的識別碼</span><span class="sxs-lookup"><span data-stu-id="2179b-151">An identifier for the guest partner</span></span> |
    | <span data-ttu-id="2179b-152">接收設定</span><span class="sxs-lookup"><span data-stu-id="2179b-152">Receive Settings</span></span> |<span data-ttu-id="2179b-153">這些屬性會套用到合約所接收的所有訊息。</span><span class="sxs-lookup"><span data-stu-id="2179b-153">These properties apply to all messages received by an agreement.</span></span> |
    | <span data-ttu-id="2179b-154">傳送設定</span><span class="sxs-lookup"><span data-stu-id="2179b-154">Send Settings</span></span> |<span data-ttu-id="2179b-155">這些屬性會套用到合約所傳送的所有訊息。</span><span class="sxs-lookup"><span data-stu-id="2179b-155">These properties apply to all messages sent by an agreement.</span></span> |  

  > [!NOTE]
  > <span data-ttu-id="2179b-156">X12 合約的解析取決於比對合作夥伴與內送郵件中定義的傳送者辨識符號與識別碼，以及接收者辨識符號與識別碼。</span><span class="sxs-lookup"><span data-stu-id="2179b-156">Resolution of X12 agreement depends on matching the sender qualifier and identifier, and the receiver qualifier and identifier defined in the partner and incoming message.</span></span> <span data-ttu-id="2179b-157">如果您夥伴的這些值變更，請同時更新合約。</span><span class="sxs-lookup"><span data-stu-id="2179b-157">If these values change for your partner, update the agreement too.</span></span>

## <a name="configure-how-your-agreement-handles-received-messages"></a><span data-ttu-id="2179b-158">設定合約處理所收到訊息的方式</span><span class="sxs-lookup"><span data-stu-id="2179b-158">Configure how your agreement handles received messages</span></span>

<span data-ttu-id="2179b-159">您現在已經設定合約屬性，您可以設定此合約如何識別及處理您透過此合約從夥伴接收的內送訊息。</span><span class="sxs-lookup"><span data-stu-id="2179b-159">Now that you've set the agreement properties, you can configure how this agreement identifies and handles incoming messages received from your partner through this agreement.</span></span>

1.  <span data-ttu-id="2179b-160">在 [新增] 之下，選取 [接收設定]。</span><span class="sxs-lookup"><span data-stu-id="2179b-160">Under **Add**, select **Receive Settings**.</span></span>
<span data-ttu-id="2179b-161">根據您與其交換訊息之夥伴所簽署的合約，設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="2179b-161">Configure these properties based on your agreement with the partner that exchanges messages with you.</span></span> <span data-ttu-id="2179b-162">如需屬性說明，請參閱本節中的資料表。</span><span class="sxs-lookup"><span data-stu-id="2179b-162">For property descriptions, see the tables in this section.</span></span>

    <span data-ttu-id="2179b-163">[接收設定] 分成下列各區段：識別碼、通知、結構描述、信封、控制編號、驗證和內部設定。</span><span class="sxs-lookup"><span data-stu-id="2179b-163">**Receive Settings** is organized into these sections: Identifiers, Acknowledgment, Schemas, Envelopes, Control Numbers, Validations, and Internal Settings.</span></span>

2. <span data-ttu-id="2179b-164">完成後，請務必選擇 [確定] 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="2179b-164">After you're done, make sure to save your settings by choosing **OK**.</span></span>

<span data-ttu-id="2179b-165">您的合約現在已準備好處理符合您所選設定的內送訊息。</span><span class="sxs-lookup"><span data-stu-id="2179b-165">Now your agreement is ready to handle incoming messages that conform to your selected settings.</span></span>

### <a name="identifiers"></a><span data-ttu-id="2179b-166">識別項</span><span class="sxs-lookup"><span data-stu-id="2179b-166">Identifiers</span></span>

![設定識別碼屬性](./media/logic-apps-enterprise-integration-x12/x12-2.png)  

| <span data-ttu-id="2179b-168">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-168">Property</span></span> | <span data-ttu-id="2179b-169">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-170">ISA1 (授權辨識符號)</span><span class="sxs-lookup"><span data-stu-id="2179b-170">ISA1 (Authorization Qualifier)</span></span> |<span data-ttu-id="2179b-171">從下拉式清單中選取授權辨識符號值。</span><span class="sxs-lookup"><span data-stu-id="2179b-171">Select the Authorization qualifier value from the drop-down list.</span></span> |
| <span data-ttu-id="2179b-172">ISA2</span><span class="sxs-lookup"><span data-stu-id="2179b-172">ISA2</span></span> |<span data-ttu-id="2179b-173">選用。</span><span class="sxs-lookup"><span data-stu-id="2179b-173">Optional.</span></span> <span data-ttu-id="2179b-174">輸入授權資訊值。</span><span class="sxs-lookup"><span data-stu-id="2179b-174">Enter Authorization information value.</span></span> <span data-ttu-id="2179b-175">如果您為 ISA1 輸入的值是 00 以外的值，請最少輸入 1 個，最多 10 個英數字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-175">If the value you entered for ISA1 is other than 00, enter a minimum of one alphanumeric character and a maximum of 10.</span></span> |
| <span data-ttu-id="2179b-176">ISA3 (安全性辨識符號)</span><span class="sxs-lookup"><span data-stu-id="2179b-176">ISA3 (Security Qualifier)</span></span> |<span data-ttu-id="2179b-177">從下拉式清單中選取安全性辨識符號值。</span><span class="sxs-lookup"><span data-stu-id="2179b-177">Select the Security qualifier value from the drop-down list.</span></span> |
| <span data-ttu-id="2179b-178">ISA4</span><span class="sxs-lookup"><span data-stu-id="2179b-178">ISA4</span></span> |<span data-ttu-id="2179b-179">選用。</span><span class="sxs-lookup"><span data-stu-id="2179b-179">Optional.</span></span> <span data-ttu-id="2179b-180">輸入安全性資訊值。</span><span class="sxs-lookup"><span data-stu-id="2179b-180">Enter the Security information value.</span></span> <span data-ttu-id="2179b-181">如果您為 ISA3 輸入的值是 00 以外的值，請最少輸入 1 個，最多 10 個英數字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-181">If the value you entered for ISA3 is other than 00, enter a minimum of one alphanumeric character and a maximum of 10.</span></span> |

### <a name="acknowledgment"></a><span data-ttu-id="2179b-182">通知</span><span class="sxs-lookup"><span data-stu-id="2179b-182">Acknowledgment</span></span>

![設定通知屬性](./media/logic-apps-enterprise-integration-x12/x12-3.png) 

| <span data-ttu-id="2179b-184">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-184">Property</span></span> | <span data-ttu-id="2179b-185">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-185">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-186">預期 TA1</span><span class="sxs-lookup"><span data-stu-id="2179b-186">TA1 expected</span></span> |<span data-ttu-id="2179b-187">將技術通知傳回給交換傳送者</span><span class="sxs-lookup"><span data-stu-id="2179b-187">Returns a technical acknowledgment to the interchange sender</span></span> |
| <span data-ttu-id="2179b-188">預期 FA</span><span class="sxs-lookup"><span data-stu-id="2179b-188">FA expected</span></span> |<span data-ttu-id="2179b-189">將功能通知傳回給交換傳送者。</span><span class="sxs-lookup"><span data-stu-id="2179b-189">Returns a functional acknowledgment to the interchange sender.</span></span> <span data-ttu-id="2179b-190">接著，根據結構描述版本，選取您想要 997 或 999 通知</span><span class="sxs-lookup"><span data-stu-id="2179b-190">Then select whether you want the 997 or 999 acknowledgments, based on the schema version</span></span> |
| <span data-ttu-id="2179b-191">包含 AK2/IK2 迴圈</span><span class="sxs-lookup"><span data-stu-id="2179b-191">Include AK2/IK2 Loop</span></span> |<span data-ttu-id="2179b-192">在功能通知中針對已接受的交易集啟用 AK2 迴圈的產生</span><span class="sxs-lookup"><span data-stu-id="2179b-192">Enables generation of AK2 loops in functional acknowledgments for accepted transaction sets</span></span> |

### <a name="schemas"></a><span data-ttu-id="2179b-193">結構描述</span><span class="sxs-lookup"><span data-stu-id="2179b-193">Schemas</span></span>

<span data-ttu-id="2179b-194">選取每個交易類型 (ST1) 和傳送者應用程式 (GS2) 的結構描述。</span><span class="sxs-lookup"><span data-stu-id="2179b-194">Select a schema for each transaction type (ST1) and Sender Application (GS2).</span></span> <span data-ttu-id="2179b-195">接收管線會比對內送訊息中 ST1 和 GS2 的值與您在此處設定的值，以及比對內送訊息的結構描述與您在此處設定的結構描述，來解譯內送訊息。</span><span class="sxs-lookup"><span data-stu-id="2179b-195">The receive pipeline disassembles the incoming message by matching the values for ST1 and GS2 in the incoming message with the values you set here, and the schema of the incoming message with the schema you set here.</span></span>

![選取結構描述](./media/logic-apps-enterprise-integration-x12/x12-33.png) 

| <span data-ttu-id="2179b-197">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-197">Property</span></span> | <span data-ttu-id="2179b-198">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-198">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-199">版本</span><span class="sxs-lookup"><span data-stu-id="2179b-199">Version</span></span> |<span data-ttu-id="2179b-200">選取 X12 版本</span><span class="sxs-lookup"><span data-stu-id="2179b-200">Select the X12 version</span></span> |
| <span data-ttu-id="2179b-201">交易類型 (ST01)</span><span class="sxs-lookup"><span data-stu-id="2179b-201">Transaction Type (ST01)</span></span> |<span data-ttu-id="2179b-202">選取交易類型</span><span class="sxs-lookup"><span data-stu-id="2179b-202">Select the transaction type</span></span> |
| <span data-ttu-id="2179b-203">傳送者應用程式 (GS02)</span><span class="sxs-lookup"><span data-stu-id="2179b-203">Sender Application (GS02)</span></span> |<span data-ttu-id="2179b-204">選取傳送者應用程式</span><span class="sxs-lookup"><span data-stu-id="2179b-204">Select the sender application</span></span> |
| <span data-ttu-id="2179b-205">結構描述</span><span class="sxs-lookup"><span data-stu-id="2179b-205">Schema</span></span> |<span data-ttu-id="2179b-206">選取您要使用的結構描述檔案。</span><span class="sxs-lookup"><span data-stu-id="2179b-206">Select the schema file you want to use.</span></span> <span data-ttu-id="2179b-207">結構描述已新增到您的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="2179b-207">Schemas are added to your integration account.</span></span> |

> [!NOTE]
> <span data-ttu-id="2179b-208">設定要上傳到[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)的必要[結構描述](../logic-apps/logic-apps-enterprise-integration-schemas.md)。</span><span class="sxs-lookup"><span data-stu-id="2179b-208">Configure the required [Schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) that is uploaded to your [integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

### <a name="envelopes"></a><span data-ttu-id="2179b-209">信封</span><span class="sxs-lookup"><span data-stu-id="2179b-209">Envelopes</span></span>

![指定交易集中的分隔符號︰選擇 [標準識別碼] 或 [重複分隔符號]](./media/logic-apps-enterprise-integration-x12/x12-34.png)

| <span data-ttu-id="2179b-211">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-211">Property</span></span> | <span data-ttu-id="2179b-212">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-212">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-213">ISA11 使用方法</span><span class="sxs-lookup"><span data-stu-id="2179b-213">ISA11 Usage</span></span> |<span data-ttu-id="2179b-214">指定要用於交易集中的分隔符號︰</span><span class="sxs-lookup"><span data-stu-id="2179b-214">Specifies the separator to use in a transaction set:</span></span> <p><span data-ttu-id="2179b-215">選取 [標準識別碼] 以使用句號 (.) 做為小數點標記，而不是 EDI 接收管線中內送文件的小數點標記。</span><span class="sxs-lookup"><span data-stu-id="2179b-215">Select **Standard identifier** to use a period (.) for decimal notation, rather than the decimal notation of the incoming document in the EDI receive pipeline.</span></span> <p><span data-ttu-id="2179b-216">選取 [重複分隔符號]，以指定重複出現簡單資料元素或重複資料結構的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="2179b-216">Select **Repetition Separator** to specify the separator for repeated occurrences of a simple data element or a repeated data structure.</span></span> <span data-ttu-id="2179b-217">例如，插入號 (^) 通常會做為重複分隔符號。</span><span class="sxs-lookup"><span data-stu-id="2179b-217">For example, usually the carat (^) is used as the repetition separator.</span></span> <span data-ttu-id="2179b-218">針對 HIPAA 結構描述，您只能使用插入號。</span><span class="sxs-lookup"><span data-stu-id="2179b-218">For HIPAA schemas, you can only use the carat.</span></span> |

### <a name="control-numbers"></a><span data-ttu-id="2179b-219">控制編號</span><span class="sxs-lookup"><span data-stu-id="2179b-219">Control Numbers</span></span>

![選取如何處理控制編號重複項目](./media/logic-apps-enterprise-integration-x12/x12-35.png) 

| <span data-ttu-id="2179b-221">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-221">Property</span></span> | <span data-ttu-id="2179b-222">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-222">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-223">不允許交換控制編號重複</span><span class="sxs-lookup"><span data-stu-id="2179b-223">Disallow Interchange Control Number duplicates</span></span> |<span data-ttu-id="2179b-224">封鎖重複的交換。</span><span class="sxs-lookup"><span data-stu-id="2179b-224">Block duplicate interchanges.</span></span> <span data-ttu-id="2179b-225">檢查已接收之交換控制編號的交換控制編號 (ISA13)。</span><span class="sxs-lookup"><span data-stu-id="2179b-225">Checks the interchange control number (ISA13) for the received interchange control number.</span></span> <span data-ttu-id="2179b-226">如果偵測到相符項目，接收管線就不會處理交換。</span><span class="sxs-lookup"><span data-stu-id="2179b-226">If a match is detected, the receive pipeline doesn't process the interchange.</span></span> <span data-ttu-id="2179b-227">您可以提供 [檢查 ISA13 是否重複的天數間隔] 的值，以指定執行檢查的天數。</span><span class="sxs-lookup"><span data-stu-id="2179b-227">You can specify the number of days for performing the check by giving a value for *Check for duplicate ISA13 every (days)*.</span></span> |
| <span data-ttu-id="2179b-228">不允許群組控制編號重複</span><span class="sxs-lookup"><span data-stu-id="2179b-228">Disallow Group control number duplicates</span></span> |<span data-ttu-id="2179b-229">封鎖有重複群組控制編號的交換。</span><span class="sxs-lookup"><span data-stu-id="2179b-229">Block interchanges with duplicate group control numbers.</span></span> |
| <span data-ttu-id="2179b-230">不允許交易集控制編號重複</span><span class="sxs-lookup"><span data-stu-id="2179b-230">Disallow Transaction set control number duplicates</span></span> |<span data-ttu-id="2179b-231">封鎖有重複交易集控制編號的交換。</span><span class="sxs-lookup"><span data-stu-id="2179b-231">Block interchanges with duplicate transaction set control numbers.</span></span> |

### <a name="validations"></a><span data-ttu-id="2179b-232">驗證</span><span class="sxs-lookup"><span data-stu-id="2179b-232">Validations</span></span>

![設定已接收訊息的驗證屬性](./media/logic-apps-enterprise-integration-x12/x12-36.png) 

<span data-ttu-id="2179b-234">當您完成每個驗證資料列時，將會自動新增另一個驗證資料列。</span><span class="sxs-lookup"><span data-stu-id="2179b-234">When you complete each validation row, another is automatically added.</span></span> <span data-ttu-id="2179b-235">如果您未指定任何規則，則驗證會使用「預設」資料列。</span><span class="sxs-lookup"><span data-stu-id="2179b-235">If you don't specify any rules, then validation uses the "Default" row.</span></span>

| <span data-ttu-id="2179b-236">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-236">Property</span></span> | <span data-ttu-id="2179b-237">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-237">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-238">訊息類型</span><span class="sxs-lookup"><span data-stu-id="2179b-238">Message Type</span></span> |<span data-ttu-id="2179b-239">選取 EDI 訊息類型。</span><span class="sxs-lookup"><span data-stu-id="2179b-239">Select the EDI message type.</span></span> |
| <span data-ttu-id="2179b-240">EDI 驗證</span><span class="sxs-lookup"><span data-stu-id="2179b-240">EDI Validation</span></span> |<span data-ttu-id="2179b-241">依照結構描述的 EDI 屬性、長度限制、空白資料元素和尾端分隔符號定義，在資料類型上執行 EDI 驗證。</span><span class="sxs-lookup"><span data-stu-id="2179b-241">Perform EDI validation on data types as defined by the schema's EDI properties, length restrictions, empty data elements, and trailing separators.</span></span> |
| <span data-ttu-id="2179b-242">擴充驗證</span><span class="sxs-lookup"><span data-stu-id="2179b-242">Extended Validation</span></span> |<span data-ttu-id="2179b-243">如果資料類型不是 EDI，則在資料元素要求時才進行驗證，且允許重複、列舉和資料元素長度驗證 (最小/最大)。</span><span class="sxs-lookup"><span data-stu-id="2179b-243">If the data type isn't EDI, validation is on the data element requirement and allowed repetition, enumerations, and data element length validation (min/max).</span></span> |
| <span data-ttu-id="2179b-244">允許前置/尾端零</span><span class="sxs-lookup"><span data-stu-id="2179b-244">Allow Leading/Trailing Zeroes</span></span> |<span data-ttu-id="2179b-245">保留任何額外的前置或尾端零及空格字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-245">Retain any additional leading or trailing zero and space characters.</span></span> <span data-ttu-id="2179b-246">請勿移除這些字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-246">Don't remove these characters.</span></span> |
| <span data-ttu-id="2179b-247">修剪前置/尾端零</span><span class="sxs-lookup"><span data-stu-id="2179b-247">Trim Leading/Trailing Zeroes</span></span> |<span data-ttu-id="2179b-248">移除前置或尾端零及空格字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-248">Remove leading or trailing zero and space characters.</span></span> |
| <span data-ttu-id="2179b-249">尾端分隔符號原則</span><span class="sxs-lookup"><span data-stu-id="2179b-249">Trailing Separator Policy</span></span> |<span data-ttu-id="2179b-250">產生尾端分隔符號。</span><span class="sxs-lookup"><span data-stu-id="2179b-250">Generate trailing separators.</span></span> <p><span data-ttu-id="2179b-251">選取 [不允許]，禁止在已接收的交換中使用尾端分隔符號。</span><span class="sxs-lookup"><span data-stu-id="2179b-251">Select **Not Allowed** to prohibit trailing delimiters and separators in the received interchange.</span></span> <span data-ttu-id="2179b-252">如果交換具有尾端分隔符號，則會被宣告為無效。</span><span class="sxs-lookup"><span data-stu-id="2179b-252">If the interchange has trailing delimiters and separators, the interchange is declared not valid.</span></span> <p><span data-ttu-id="2179b-253">選取 [選擇性]  以接受包含或不含尾端分隔符號的交換。</span><span class="sxs-lookup"><span data-stu-id="2179b-253">Select **Optional** to accept interchanges with or without trailing delimiters and separators.</span></span> <p><span data-ttu-id="2179b-254">如果交換必須具備尾端分隔符號，請選取 [強制性]。</span><span class="sxs-lookup"><span data-stu-id="2179b-254">Select **Mandatory** when the interchange must have trailing delimiters and separators.</span></span> |

### <a name="internal-settings"></a><span data-ttu-id="2179b-255">內部設定</span><span class="sxs-lookup"><span data-stu-id="2179b-255">Internal Settings</span></span>

![選取內部設定](./media/logic-apps-enterprise-integration-x12/x12-37.png) 

| <span data-ttu-id="2179b-257">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-257">Property</span></span> | <span data-ttu-id="2179b-258">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-258">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-259">將隱含的小數格式 "Nn" 轉換為 10 進制數值</span><span class="sxs-lookup"><span data-stu-id="2179b-259">Convert implied decimal format "Nn" to a base 10 numeric value</span></span> |<span data-ttu-id="2179b-260">將使用 "Nn" 格式指定的 EDI 數字轉換為 10 進制數值</span><span class="sxs-lookup"><span data-stu-id="2179b-260">Converts an EDI number that is specified with the format "Nn" into a base-10 numeric value</span></span> |
| <span data-ttu-id="2179b-261">如果允許尾端分隔符號，則建立空的 XML 標籤</span><span class="sxs-lookup"><span data-stu-id="2179b-261">Create empty XML tags if trailing separators are allowed</span></span> |<span data-ttu-id="2179b-262">選取此核取方塊，讓交換傳送者在尾端分隔符號包含空的 XML 標籤。</span><span class="sxs-lookup"><span data-stu-id="2179b-262">Select this check box to have the interchange sender include empty XML tags for trailing separators.</span></span> |
| <span data-ttu-id="2179b-263">將交換分割為交易集 - 發生錯誤時暫停交易集</span><span class="sxs-lookup"><span data-stu-id="2179b-263">Split Interchange as transaction sets - suspend transaction sets on error</span></span>|<span data-ttu-id="2179b-264">套用適當的信封至交易集，將交換中每個交易集剖析為個別的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="2179b-264">Parses each transaction set in an interchange into a separate XML document by applying the appropriate envelope to the transaction set.</span></span> <span data-ttu-id="2179b-265">只暫停驗證失敗的交易。</span><span class="sxs-lookup"><span data-stu-id="2179b-265">Suspends only the transactions where the validation fails.</span></span> |
| <span data-ttu-id="2179b-266">將交換分割為交易集 - 發生錯誤時暫停交換</span><span class="sxs-lookup"><span data-stu-id="2179b-266">Split Interchange as transaction sets - suspend interchange on error</span></span>|<span data-ttu-id="2179b-267">套用適當的信封，將交換中每個交易集剖析為個別的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="2179b-267">Parses each transaction set in an interchange into a separate XML document by applying the appropriate envelope.</span></span> <span data-ttu-id="2179b-268">如果交換中有一或多個交易集無法通過驗證，則會暫停整個交換。</span><span class="sxs-lookup"><span data-stu-id="2179b-268">Suspends entire interchange when one or more transaction sets in the interchange fail validation.</span></span> | 
| <span data-ttu-id="2179b-269">保留交換 - 發生錯誤時暫停交易集</span><span class="sxs-lookup"><span data-stu-id="2179b-269">Preserve Interchange - suspend transaction sets on error</span></span> |<span data-ttu-id="2179b-270">讓交換維持不變，建立整個批次交換的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="2179b-270">Leaves the interchange intact, creates an XML document for the entire batched interchange.</span></span> <span data-ttu-id="2179b-271">只暫停未通過驗證的交易集，而繼續處理所有其他交易集。</span><span class="sxs-lookup"><span data-stu-id="2179b-271">Suspends only the transaction sets that fail validation, while continuing to process all other transaction sets.</span></span> |
| <span data-ttu-id="2179b-272">保留交換 - 發生錯誤時暫停交換</span><span class="sxs-lookup"><span data-stu-id="2179b-272">Preserve Interchange - suspend interchange on error</span></span> |<span data-ttu-id="2179b-273">讓交換維持不變，建立整個批次交換的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="2179b-273">Leaves the interchange intact, creates an XML document for the entire batched interchange.</span></span> <span data-ttu-id="2179b-274">如果交換中有一或多個交易集無法通過驗證，則會暫停整個交換。</span><span class="sxs-lookup"><span data-stu-id="2179b-274">Suspends the entire interchange when one or more transaction sets in the interchange fail validation.</span></span> |

## <a name="configure-how-your-agreement-sends-messages"></a><span data-ttu-id="2179b-275">設定合約傳送訊息的方式</span><span class="sxs-lookup"><span data-stu-id="2179b-275">Configure how your agreement sends messages</span></span>

<span data-ttu-id="2179b-276">您可以設定此合約如何識別及處理您透過此合約傳送給夥伴的外寄訊息。</span><span class="sxs-lookup"><span data-stu-id="2179b-276">You can configure how this agreement identifies and handles outgoing messages that you send to your partner through this agreement.</span></span>

1.  <span data-ttu-id="2179b-277">在 [新增] 之下，選取 [傳送設定]。</span><span class="sxs-lookup"><span data-stu-id="2179b-277">Under **Add**, select **Send Settings**.</span></span>
<span data-ttu-id="2179b-278">根據您與其交換訊息之夥伴所簽署的合約，設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="2179b-278">Configure these properties based on your agreement with your partner who exchanges messages with you.</span></span> <span data-ttu-id="2179b-279">如需屬性說明，請參閱本節中的資料表。</span><span class="sxs-lookup"><span data-stu-id="2179b-279">For property descriptions, see the tables in this section.</span></span>

    <span data-ttu-id="2179b-280">[傳送設定] 分成下列各區段：識別碼、通知、結構描述、信封、字元集和分隔符號、控制編號以及驗證。</span><span class="sxs-lookup"><span data-stu-id="2179b-280">**Send Settings** is organized into these sections: Identifiers, Acknowledgment, Schemas, Envelopes, Character Sets and Separators, Control Numbers, and Validation.</span></span>

2. <span data-ttu-id="2179b-281">完成後，請務必選擇 [確定] 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="2179b-281">After you're done, make sure to save your settings by choosing **OK**.</span></span>

<span data-ttu-id="2179b-282">您的合約現在已準備好處理符合您所選設定的外寄訊息。</span><span class="sxs-lookup"><span data-stu-id="2179b-282">Now your agreement is ready to handle outgoing messages that conform to your selected settings.</span></span>

### <a name="identifiers"></a><span data-ttu-id="2179b-283">識別項</span><span class="sxs-lookup"><span data-stu-id="2179b-283">Identifiers</span></span>

![設定識別碼屬性](./media/logic-apps-enterprise-integration-x12/x12-4.png)  

| <span data-ttu-id="2179b-285">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-285">Property</span></span> | <span data-ttu-id="2179b-286">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-287">授權辨識符號 (ISA1)</span><span class="sxs-lookup"><span data-stu-id="2179b-287">Authorization qualifier (ISA1)</span></span> |<span data-ttu-id="2179b-288">從下拉式清單中選取授權辨識符號值。</span><span class="sxs-lookup"><span data-stu-id="2179b-288">Select the Authorization qualifier value from the drop-down list.</span></span> |
| <span data-ttu-id="2179b-289">ISA2</span><span class="sxs-lookup"><span data-stu-id="2179b-289">ISA2</span></span> |<span data-ttu-id="2179b-290">輸入授權資訊值。</span><span class="sxs-lookup"><span data-stu-id="2179b-290">Enter Authorization information value.</span></span> <span data-ttu-id="2179b-291">如果此值不是 00，則請最少輸入 1 個，最多 10 個英數字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-291">If this value is other than 00, then enter a minimum of one alphanumeric character and a maximum of 10.</span></span> |
| <span data-ttu-id="2179b-292">安全性辨識符號 (ISA3)</span><span class="sxs-lookup"><span data-stu-id="2179b-292">Security qualifier (ISA3)</span></span> |<span data-ttu-id="2179b-293">從下拉式清單中選取安全性辨識符號值。</span><span class="sxs-lookup"><span data-stu-id="2179b-293">Select the Security qualifier value from the drop-down list.</span></span> |
| <span data-ttu-id="2179b-294">ISA4</span><span class="sxs-lookup"><span data-stu-id="2179b-294">ISA4</span></span> |<span data-ttu-id="2179b-295">輸入安全性資訊值。</span><span class="sxs-lookup"><span data-stu-id="2179b-295">Enter the Security information value.</span></span> <span data-ttu-id="2179b-296">如果此值不是 00，則在 [值 (ISA4)] 文字方塊中，請最少輸入 1 個，最多 10 個英數字元值。</span><span class="sxs-lookup"><span data-stu-id="2179b-296">If this value is other than 00, for the Value (ISA4) text box, then enter a minimum of one alphanumeric value and a maximum of 10.</span></span> |

### <a name="acknowledgment"></a><span data-ttu-id="2179b-297">通知</span><span class="sxs-lookup"><span data-stu-id="2179b-297">Acknowledgment</span></span>

![設定通知屬性](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| <span data-ttu-id="2179b-299">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-299">Property</span></span> | <span data-ttu-id="2179b-300">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-300">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-301">預期 TA1</span><span class="sxs-lookup"><span data-stu-id="2179b-301">TA1 expected</span></span> |<span data-ttu-id="2179b-302">將技術通知 (TA1) 傳回給交換傳送者。</span><span class="sxs-lookup"><span data-stu-id="2179b-302">Return a technical acknowledgment (TA1) to the interchange sender.</span></span> <span data-ttu-id="2179b-303">此設定指定傳送訊息的主控夥伴向合約中的來賓合作夥伴要求通知。</span><span class="sxs-lookup"><span data-stu-id="2179b-303">This setting specifies that the host partner who is sending the message requests an acknowledgment from the guest partner in the agreement.</span></span> <span data-ttu-id="2179b-304">主控夥伴根據合約的「接收設定」，預期有這些通知。</span><span class="sxs-lookup"><span data-stu-id="2179b-304">These acknowledgments are expected by the host partner based on the Receive Settings of the agreement.</span></span> |
| <span data-ttu-id="2179b-305">預期 FA</span><span class="sxs-lookup"><span data-stu-id="2179b-305">FA expected</span></span> |<span data-ttu-id="2179b-306">將功能通知 (FA) 傳回給交換傳送者。</span><span class="sxs-lookup"><span data-stu-id="2179b-306">Return a functional acknowledgment (FA) to the interchange sender.</span></span> <span data-ttu-id="2179b-307">根據您正在使用的結構描述版本，選取您想要 997 或 999 通知。</span><span class="sxs-lookup"><span data-stu-id="2179b-307">Select whether you want the 997 or 999 acknowledgements, based on the schema versions you are working with.</span></span> <span data-ttu-id="2179b-308">主控夥伴根據合約的「接收設定」，預期有這些通知。</span><span class="sxs-lookup"><span data-stu-id="2179b-308">These acknowledgments are expected by the host partner based on the Receive Settings of the agreement.</span></span> |
| <span data-ttu-id="2179b-309">FA 版本</span><span class="sxs-lookup"><span data-stu-id="2179b-309">FA Version</span></span> |<span data-ttu-id="2179b-310">選取 FA 版本</span><span class="sxs-lookup"><span data-stu-id="2179b-310">Select the FA version</span></span> |

### <a name="schemas"></a><span data-ttu-id="2179b-311">結構描述</span><span class="sxs-lookup"><span data-stu-id="2179b-311">Schemas</span></span>

![選取要使用的結構描述](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| <span data-ttu-id="2179b-313">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-313">Property</span></span> | <span data-ttu-id="2179b-314">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-314">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-315">版本</span><span class="sxs-lookup"><span data-stu-id="2179b-315">Version</span></span> |<span data-ttu-id="2179b-316">選取 X12 版本</span><span class="sxs-lookup"><span data-stu-id="2179b-316">Select the X12 version</span></span> |
| <span data-ttu-id="2179b-317">交易類型 (ST01)</span><span class="sxs-lookup"><span data-stu-id="2179b-317">Transaction Type (ST01)</span></span> |<span data-ttu-id="2179b-318">選取交易類型</span><span class="sxs-lookup"><span data-stu-id="2179b-318">Select the transaction type</span></span> |
| <span data-ttu-id="2179b-319">結構描述</span><span class="sxs-lookup"><span data-stu-id="2179b-319">SCHEMA</span></span> |<span data-ttu-id="2179b-320">選取要使用的結構描述。</span><span class="sxs-lookup"><span data-stu-id="2179b-320">Select the schema to use.</span></span> <span data-ttu-id="2179b-321">結構描述位於您的整合帳戶中。</span><span class="sxs-lookup"><span data-stu-id="2179b-321">Schemas are located in your integration account.</span></span> <span data-ttu-id="2179b-322">若先選取結構描述，它會自動設定版本與交易類型</span><span class="sxs-lookup"><span data-stu-id="2179b-322">If you select schema first, it automatically configures version and transaction type</span></span>  |

> [!NOTE]
> <span data-ttu-id="2179b-323">設定要上傳到[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)的必要[結構描述](../logic-apps/logic-apps-enterprise-integration-schemas.md)。</span><span class="sxs-lookup"><span data-stu-id="2179b-323">Configure the required [Schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) that is uploaded to your [integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

### <a name="envelopes"></a><span data-ttu-id="2179b-324">信封</span><span class="sxs-lookup"><span data-stu-id="2179b-324">Envelopes</span></span>

![指定交易集中的分隔符號︰選擇 [標準識別碼] 或 [重複分隔符號]](./media/logic-apps-enterprise-integration-x12/x12-6.png) 

| <span data-ttu-id="2179b-326">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-326">Property</span></span> | <span data-ttu-id="2179b-327">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-327">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-328">ISA11 使用方法</span><span class="sxs-lookup"><span data-stu-id="2179b-328">ISA11 Usage</span></span> |<span data-ttu-id="2179b-329">指定要用於交易集中的分隔符號︰</span><span class="sxs-lookup"><span data-stu-id="2179b-329">Specifies the separator to use in a transaction set:</span></span> <p><span data-ttu-id="2179b-330">選取 [標準識別碼] 以使用句號 (.) 做為小數點標記，而不是 EDI 接收管線中內送文件的小數點標記。</span><span class="sxs-lookup"><span data-stu-id="2179b-330">Select **Standard identifier** to use a period (.) for decimal notation, rather than the decimal notation of the incoming document in the EDI receive pipeline.</span></span> <p><span data-ttu-id="2179b-331">選取 [重複分隔符號]，以指定重複出現簡單資料元素或重複資料結構的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="2179b-331">Select **Repetition Separator** to specify the separator for repeated occurrences of a simple data element or a repeated data structure.</span></span> <span data-ttu-id="2179b-332">例如，插入號 (^) 通常會做為重複分隔符號。</span><span class="sxs-lookup"><span data-stu-id="2179b-332">For example, usually the carat (^) is used as the repetition separator.</span></span> <span data-ttu-id="2179b-333">針對 HIPAA 結構描述，您只能使用插入號。</span><span class="sxs-lookup"><span data-stu-id="2179b-333">For HIPAA schemas, you can only use the carat.</span></span> |

### <a name="control-numbers"></a><span data-ttu-id="2179b-334">控制編號</span><span class="sxs-lookup"><span data-stu-id="2179b-334">Control Numbers</span></span>

![指定控制編號屬性](./media/logic-apps-enterprise-integration-x12/x12-8.png) 

| <span data-ttu-id="2179b-336">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-336">Property</span></span> | <span data-ttu-id="2179b-337">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-338">控制版本編號 (ISA12)</span><span class="sxs-lookup"><span data-stu-id="2179b-338">Control Version Number (ISA12)</span></span> |<span data-ttu-id="2179b-339">選取 X12 標準的版本</span><span class="sxs-lookup"><span data-stu-id="2179b-339">Select the version of the X12 standard</span></span> |
| <span data-ttu-id="2179b-340">使用狀況指示符號 (ISA15)</span><span class="sxs-lookup"><span data-stu-id="2179b-340">Usage Indicator (ISA15)</span></span> |<span data-ttu-id="2179b-341">選取交換的內容。</span><span class="sxs-lookup"><span data-stu-id="2179b-341">Select the context of an interchange.</span></span>  <span data-ttu-id="2179b-342">值是資訊、生產資料或測試資料</span><span class="sxs-lookup"><span data-stu-id="2179b-342">The values are information, production data, or test data</span></span> |
| <span data-ttu-id="2179b-343">結構描述</span><span class="sxs-lookup"><span data-stu-id="2179b-343">Schema</span></span> |<span data-ttu-id="2179b-344">產生 X12 編碼交換的 GS 和 ST 區段，它會將這些區段傳送至「傳送管線」</span><span class="sxs-lookup"><span data-stu-id="2179b-344">Generates the GS and ST segments for an X12-encoded interchange that it sends to the Send Pipeline</span></span> |
| <span data-ttu-id="2179b-345">GS1</span><span class="sxs-lookup"><span data-stu-id="2179b-345">GS1</span></span> |<span data-ttu-id="2179b-346">選擇性，請從下拉式清單選取功能代碼的值</span><span class="sxs-lookup"><span data-stu-id="2179b-346">Optional, select a value for the functional code from the drop-down list</span></span> |
| <span data-ttu-id="2179b-347">GS2</span><span class="sxs-lookup"><span data-stu-id="2179b-347">GS2</span></span> |<span data-ttu-id="2179b-348">選擇性，應用程式寄件者</span><span class="sxs-lookup"><span data-stu-id="2179b-348">Optional, application sender</span></span> |
| <span data-ttu-id="2179b-349">GS3</span><span class="sxs-lookup"><span data-stu-id="2179b-349">GS3</span></span> |<span data-ttu-id="2179b-350">選擇性，應用程式接收者</span><span class="sxs-lookup"><span data-stu-id="2179b-350">Optional, application receiver</span></span> |
| <span data-ttu-id="2179b-351">GS4</span><span class="sxs-lookup"><span data-stu-id="2179b-351">GS4</span></span> |<span data-ttu-id="2179b-352">選擇性，請選取 CCYYMMDD 或 YYMMDD</span><span class="sxs-lookup"><span data-stu-id="2179b-352">Optional, select CCYYMMDD or YYMMDD</span></span> |
| <span data-ttu-id="2179b-353">GS5</span><span class="sxs-lookup"><span data-stu-id="2179b-353">GS5</span></span> |<span data-ttu-id="2179b-354">選擇性，請選取 HHMM、HHMMSS 或 HHMMSSdd</span><span class="sxs-lookup"><span data-stu-id="2179b-354">Optional, select HHMM, HHMMSS, or HHMMSSdd</span></span> |
| <span data-ttu-id="2179b-355">GS7</span><span class="sxs-lookup"><span data-stu-id="2179b-355">GS7</span></span> |<span data-ttu-id="2179b-356">選擇性，請從下拉式清單選取負責單位的值</span><span class="sxs-lookup"><span data-stu-id="2179b-356">Optional, select a value for the responsible agency from the drop-down list</span></span> |
| <span data-ttu-id="2179b-357">GS8</span><span class="sxs-lookup"><span data-stu-id="2179b-357">GS8</span></span> |<span data-ttu-id="2179b-358">選擇性，文件的版本</span><span class="sxs-lookup"><span data-stu-id="2179b-358">Optional, version of the document</span></span> |
| <span data-ttu-id="2179b-359">交換控制編號 (ISA13)</span><span class="sxs-lookup"><span data-stu-id="2179b-359">Interchange Control Number (ISA13)</span></span> |<span data-ttu-id="2179b-360">必要，輸入交換控制編號的值範圍。</span><span class="sxs-lookup"><span data-stu-id="2179b-360">Required, enter a range of values for the interchange control number.</span></span> <span data-ttu-id="2179b-361">請輸入最小為 1，最大為 999999999 的數值</span><span class="sxs-lookup"><span data-stu-id="2179b-361">Enter a numeric value with a minimum of 1 and a maximum of 999999999</span></span> |
| <span data-ttu-id="2179b-362">群組控制編號 (GS06)</span><span class="sxs-lookup"><span data-stu-id="2179b-362">Group Control Number (GS06)</span></span> |<span data-ttu-id="2179b-363">必要，請輸入群組控制編號的數字範圍。</span><span class="sxs-lookup"><span data-stu-id="2179b-363">Required, enter a range of numbers for the group control number.</span></span> <span data-ttu-id="2179b-364">請輸入最小為 1，最大為 999999999 的數值</span><span class="sxs-lookup"><span data-stu-id="2179b-364">Enter a numeric value with a minimum of 1 and a maximum of 999999999</span></span> |
| <span data-ttu-id="2179b-365">交易集控制編號 (ST02)</span><span class="sxs-lookup"><span data-stu-id="2179b-365">Transaction Set Control Number (ST02)</span></span> |<span data-ttu-id="2179b-366">必要，請輸入交易集控制編號的數字範圍。</span><span class="sxs-lookup"><span data-stu-id="2179b-366">Required, enter a range of numbers for the Transaction Set Control number.</span></span> <span data-ttu-id="2179b-367">請輸入最小為 1，最大為 999999999 的數值範圍</span><span class="sxs-lookup"><span data-stu-id="2179b-367">Enter a range of numeric values with a minimum of 1 and a maximum of 999999999</span></span> |
| <span data-ttu-id="2179b-368">前置詞</span><span class="sxs-lookup"><span data-stu-id="2179b-368">Prefix</span></span> |<span data-ttu-id="2179b-369">選擇性，針對在通知中使用的交易集控制編號範圍指定。</span><span class="sxs-lookup"><span data-stu-id="2179b-369">Optional, designated for the range of transaction set control numbers used in acknowledgment.</span></span> <span data-ttu-id="2179b-370">在中間的兩個欄位輸入數值，在前置詞和尾碼欄位輸入英數字元值 (如有需要)。</span><span class="sxs-lookup"><span data-stu-id="2179b-370">Enter a numeric value for the middle two fields, and an alphanumeric value (if desired) for the prefix and suffix fields.</span></span> <span data-ttu-id="2179b-371">中間欄位是必要欄位，而且包含控制編號的最小值和最大值</span><span class="sxs-lookup"><span data-stu-id="2179b-371">The middle fields are required and contain the minimum and maximum values for the control number</span></span> |
| <span data-ttu-id="2179b-372">尾碼</span><span class="sxs-lookup"><span data-stu-id="2179b-372">Suffix</span></span> |<span data-ttu-id="2179b-373">選擇性，針對在通知中使用的交易集控制編號範圍指定。</span><span class="sxs-lookup"><span data-stu-id="2179b-373">Optional, designated for the range of transaction set control numbers used in an acknowledgment.</span></span> <span data-ttu-id="2179b-374">在中間的兩個欄位輸入數值，在前置詞和尾碼欄位輸入英數字元值 (如有需要)。</span><span class="sxs-lookup"><span data-stu-id="2179b-374">Enter a numeric value for the middle two fields and an alphanumeric value (if desired) for the prefix and suffix fields.</span></span> <span data-ttu-id="2179b-375">中間欄位是必要欄位，而且包含控制編號的最小值和最大值</span><span class="sxs-lookup"><span data-stu-id="2179b-375">The middle fields are required and contain the minimum and maximum values for the control number</span></span> |

### <a name="character-sets-and-separators"></a><span data-ttu-id="2179b-376">字元集和分隔符號</span><span class="sxs-lookup"><span data-stu-id="2179b-376">Character Sets and Separators</span></span>

<span data-ttu-id="2179b-377">除了字元集，您還可以為每個訊息類型輸入一組不同的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="2179b-377">Other than the character set, you can enter a different set of delimiters for each message type.</span></span> <span data-ttu-id="2179b-378">如果指定的訊息結構描述未指定字元集，則會使用預設字元集。</span><span class="sxs-lookup"><span data-stu-id="2179b-378">If a character set isn't specified for a given message schema, then the default character set is used.</span></span>

![指定不同訊息類型的分隔符號](./media/logic-apps-enterprise-integration-x12/x12-9.png) 

| <span data-ttu-id="2179b-380">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-380">Property</span></span> | <span data-ttu-id="2179b-381">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-381">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-382">要使用的字元集</span><span class="sxs-lookup"><span data-stu-id="2179b-382">Character Set to be used</span></span> |<span data-ttu-id="2179b-383">若要驗證屬性，請選取 X12 字元集。</span><span class="sxs-lookup"><span data-stu-id="2179b-383">To validate the properties, select the X12 character set.</span></span> <span data-ttu-id="2179b-384">選項包括 [基本]、[延伸] 和 [UTF8]。</span><span class="sxs-lookup"><span data-stu-id="2179b-384">The options are Basic, Extended, and UTF8.</span></span> |
| <span data-ttu-id="2179b-385">結構描述</span><span class="sxs-lookup"><span data-stu-id="2179b-385">Schema</span></span> |<span data-ttu-id="2179b-386">從下拉式清單中選取結構描述。</span><span class="sxs-lookup"><span data-stu-id="2179b-386">Select a schema from the drop-down list.</span></span> <span data-ttu-id="2179b-387">在您完成每個資料列時，便會自動新增一個資料列。</span><span class="sxs-lookup"><span data-stu-id="2179b-387">After you complete each row, a new row is automatically added.</span></span> <span data-ttu-id="2179b-388">針對選取的結構描述，根據下列分隔符號說明，選取您要使用的分隔符號集。</span><span class="sxs-lookup"><span data-stu-id="2179b-388">For the selected schema, select the separators set that you want to use, based on the following separator descriptions.</span></span> |
| <span data-ttu-id="2179b-389">輸入類型</span><span class="sxs-lookup"><span data-stu-id="2179b-389">Input Type</span></span> |<span data-ttu-id="2179b-390">從下拉式清單中選取輸入類型。</span><span class="sxs-lookup"><span data-stu-id="2179b-390">Select an input type from the drop-down list.</span></span> |
| <span data-ttu-id="2179b-391">元件分隔符號</span><span class="sxs-lookup"><span data-stu-id="2179b-391">Component Separator</span></span> |<span data-ttu-id="2179b-392">若要分隔複合的資料元素，請輸入單一字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-392">To separate composite data elements, enter a single character.</span></span> |
| <span data-ttu-id="2179b-393">資料元素分隔符號</span><span class="sxs-lookup"><span data-stu-id="2179b-393">Data Element Separator</span></span> |<span data-ttu-id="2179b-394">若要分隔複合資料元素內的簡單資料元素，請輸入單一字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-394">To separate simple data elements within composite data elements, enter a single character.</span></span> |
| <span data-ttu-id="2179b-395">取代字元</span><span class="sxs-lookup"><span data-stu-id="2179b-395">Replacement Character</span></span> |<span data-ttu-id="2179b-396">輸入在產生輸出 X12 訊息時，用於取代承載資料中所有分隔符號字元的取代字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-396">Enter a replacement character used for replacing all separator characters in the payload data when generating the outbound X12 message.</span></span> |
| <span data-ttu-id="2179b-397">區段結束字元</span><span class="sxs-lookup"><span data-stu-id="2179b-397">Segment Terminator</span></span> |<span data-ttu-id="2179b-398">若要指出 EDI 區段的結尾，請輸入單一字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-398">To indicate the end of an EDI segment, enter a single character.</span></span> |
| <span data-ttu-id="2179b-399">尾碼</span><span class="sxs-lookup"><span data-stu-id="2179b-399">Suffix</span></span> |<span data-ttu-id="2179b-400">選取與區段識別項一起使用的字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-400">Select the character that is used with the segment identifier.</span></span> <span data-ttu-id="2179b-401">如果指定尾碼，則區段結束字元資料元素可以空白。</span><span class="sxs-lookup"><span data-stu-id="2179b-401">If you designate a suffix, then the segment terminator data element can be empty.</span></span> <span data-ttu-id="2179b-402">如果區段結束字元留空，則必須指定尾碼。</span><span class="sxs-lookup"><span data-stu-id="2179b-402">If the segment terminator is left empty, then you must designate a suffix.</span></span> |

> [!TIP]
> <span data-ttu-id="2179b-403">若要提供特殊字元值，請將合約編輯為 JSON，並為特殊字元提供 ASCII 值。</span><span class="sxs-lookup"><span data-stu-id="2179b-403">To provide special character values, edit the agreement as JSON and provide the ASCII value for the special character.</span></span>

### <a name="validation"></a><span data-ttu-id="2179b-404">驗證</span><span class="sxs-lookup"><span data-stu-id="2179b-404">Validation</span></span>

![設定驗證屬性以便傳送訊息](./media/logic-apps-enterprise-integration-x12/x12-10.png) 

<span data-ttu-id="2179b-406">當您完成每個驗證資料列時，將會自動新增另一個驗證資料列。</span><span class="sxs-lookup"><span data-stu-id="2179b-406">When you complete each validation row, another is automatically added.</span></span> <span data-ttu-id="2179b-407">如果您未指定任何規則，則驗證會使用「預設」資料列。</span><span class="sxs-lookup"><span data-stu-id="2179b-407">If you don't specify any rules, then validation uses the "Default" row.</span></span>

| <span data-ttu-id="2179b-408">屬性</span><span class="sxs-lookup"><span data-stu-id="2179b-408">Property</span></span> | <span data-ttu-id="2179b-409">說明</span><span class="sxs-lookup"><span data-stu-id="2179b-409">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2179b-410">訊息類型</span><span class="sxs-lookup"><span data-stu-id="2179b-410">Message Type</span></span> |<span data-ttu-id="2179b-411">選取 EDI 訊息類型。</span><span class="sxs-lookup"><span data-stu-id="2179b-411">Select the EDI message type.</span></span> |
| <span data-ttu-id="2179b-412">EDI 驗證</span><span class="sxs-lookup"><span data-stu-id="2179b-412">EDI Validation</span></span> |<span data-ttu-id="2179b-413">依照結構描述的 EDI 屬性、長度限制、空白資料元素和尾端分隔符號定義，在資料類型上執行 EDI 驗證。</span><span class="sxs-lookup"><span data-stu-id="2179b-413">Perform EDI validation on data types as defined by the schema's EDI properties, length restrictions, empty data elements, and trailing separators.</span></span> |
| <span data-ttu-id="2179b-414">擴充驗證</span><span class="sxs-lookup"><span data-stu-id="2179b-414">Extended Validation</span></span> |<span data-ttu-id="2179b-415">如果資料類型不是 EDI，則在資料元素要求時才進行驗證，且允許重複、列舉和資料元素長度驗證 (最小/最大)。</span><span class="sxs-lookup"><span data-stu-id="2179b-415">If the data type isn't EDI, validation is on the data element requirement and allowed repetition, enumerations, and data element length validation (min/max).</span></span> |
| <span data-ttu-id="2179b-416">允許前置/尾端零</span><span class="sxs-lookup"><span data-stu-id="2179b-416">Allow Leading/Trailing Zeroes</span></span> |<span data-ttu-id="2179b-417">保留任何額外的前置或尾端零及空格字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-417">Retain any additional leading or trailing zero and space characters.</span></span> <span data-ttu-id="2179b-418">請勿移除這些字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-418">Don't remove these characters.</span></span> |
| <span data-ttu-id="2179b-419">修剪前置/尾端零</span><span class="sxs-lookup"><span data-stu-id="2179b-419">Trim Leading/Trailing Zeroes</span></span> |<span data-ttu-id="2179b-420">移除前置或尾端零字元。</span><span class="sxs-lookup"><span data-stu-id="2179b-420">Remove leading or trailing zero characters.</span></span> |
| <span data-ttu-id="2179b-421">尾端分隔符號原則</span><span class="sxs-lookup"><span data-stu-id="2179b-421">Trailing Separator Policy</span></span> |<span data-ttu-id="2179b-422">產生尾端分隔符號。</span><span class="sxs-lookup"><span data-stu-id="2179b-422">Generate trailing separators.</span></span> <p><span data-ttu-id="2179b-423">選取 [不允許]，禁止在已傳送的交換中使用尾端分隔符號。</span><span class="sxs-lookup"><span data-stu-id="2179b-423">Select **Not Allowed** to prohibit trailing delimiters and separators in the sent interchange.</span></span> <span data-ttu-id="2179b-424">如果交換具有尾端分隔符號，則會被宣告為無效。</span><span class="sxs-lookup"><span data-stu-id="2179b-424">If the interchange has trailing delimiters and separators, the interchange is declared not valid.</span></span> <p><span data-ttu-id="2179b-425">選取 [選擇性] 以傳送包含或不含尾端分隔符號的交換。</span><span class="sxs-lookup"><span data-stu-id="2179b-425">Select **Optional** to send interchanges with or without trailing delimiters and separators.</span></span> <p><span data-ttu-id="2179b-426">如果傳送的交換必須具備尾端分隔符號，請選取 [強制性]。</span><span class="sxs-lookup"><span data-stu-id="2179b-426">Select **Mandatory** if the sent interchange must have trailing delimiters and separators.</span></span> |

## <a name="find-your-created-agreement"></a><span data-ttu-id="2179b-427">尋找您建立的合約</span><span class="sxs-lookup"><span data-stu-id="2179b-427">Find your created agreement</span></span>

1.  <span data-ttu-id="2179b-428">完成所有合約屬性的設定之後，請在 [新增] 刀鋒視窗中選擇 [確定]，以完成合約建立並回到整合帳戶刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2179b-428">After you finish setting all your agreement properties, on the **Add** blade, choose **OK** to finish creating your agreement and return to your integration account blade.</span></span>

    <span data-ttu-id="2179b-429">您新增的合約現在顯示於您的 [合約] 清單中。</span><span class="sxs-lookup"><span data-stu-id="2179b-429">Your newly added agreement now appears in your **Agreements** list.</span></span>

2.  <span data-ttu-id="2179b-430">您也可以在整合帳戶概觀中檢視您的合約。</span><span class="sxs-lookup"><span data-stu-id="2179b-430">You can also view your agreements in your integration account overview.</span></span> <span data-ttu-id="2179b-431">在整合帳戶刀鋒視窗上，選擇 [概觀]，然後選取 [合約] 圖格。</span><span class="sxs-lookup"><span data-stu-id="2179b-431">On your integration account blade, choose **Overview**, then select the **Agreements** tile.</span></span>

    ![選擇 [合約] 圖格來檢視所有合約](./media/logic-apps-enterprise-integration-x12/x12-1-5.png)   

## <a name="view-the-swagger"></a><span data-ttu-id="2179b-433">檢視 Swagger</span><span class="sxs-lookup"><span data-stu-id="2179b-433">View the swagger</span></span>
<span data-ttu-id="2179b-434">請參閱 [Swagger 詳細資料](/connectors/x12/)。</span><span class="sxs-lookup"><span data-stu-id="2179b-434">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="learn-more"></a><span data-ttu-id="2179b-435">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="2179b-435">Learn more</span></span>
* [<span data-ttu-id="2179b-436">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="2179b-436">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "了解企業整合套件")  

