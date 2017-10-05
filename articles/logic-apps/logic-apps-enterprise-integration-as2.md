---
title: "適用於 B2B 企業整合的 AS2 訊息 - Azure Logic Apps | Microsoft Docs"
description: "利用 Azure Logic Apps 交換適用於 B2B 企業整合的 AS2 訊息"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 91b2f16611b88aa4b9395ca301d88042065ad9dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a><span data-ttu-id="df0de-103">利用邏輯應用程式交換適用於企業整合的 AS2 訊息</span><span class="sxs-lookup"><span data-stu-id="df0de-103">Exchange AS2 messages for enterprise integration with logic apps</span></span>

<span data-ttu-id="df0de-104">您必須先建立 AS2 合約並將該合約儲存在您的整合帳戶中，才可以交換 AS2 訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-104">Before you can exchange AS2 messages for Azure Logic Apps, you must create an AS2 agreement and store that agreement in your integration account.</span></span> <span data-ttu-id="df0de-105">以下是如何建立 AS2 合約的步驟。</span><span class="sxs-lookup"><span data-stu-id="df0de-105">Here are the steps for how to create an AS2 agreement.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="df0de-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="df0de-106">Before you start</span></span>

<span data-ttu-id="df0de-107">以下是您所需的項目︰</span><span class="sxs-lookup"><span data-stu-id="df0de-107">Here's the items you need:</span></span>

* <span data-ttu-id="df0de-108">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)</span><span class="sxs-lookup"><span data-stu-id="df0de-108">An [integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) that's already defined and associated with your Azure subscription</span></span>
* <span data-ttu-id="df0de-109">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)，以及在 [企業身分識別] 之下設定 AS2 限定詞。</span><span class="sxs-lookup"><span data-stu-id="df0de-109">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account and configured with the AS2 qualifier under **Business Identities**</span></span>

> [!NOTE]
> <span data-ttu-id="df0de-110">當您建立合約時，合約檔案中的內容必須與合約類型相符。</span><span class="sxs-lookup"><span data-stu-id="df0de-110">When you create an agreement, the content in the agreement file must match the agreement type.</span></span>    

<span data-ttu-id="df0de-111">在您[建立整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)並[新增夥伴](logic-apps-enterprise-integration-partners.md)之後，您可以依照下列步驟建立 AS2 合約。</span><span class="sxs-lookup"><span data-stu-id="df0de-111">After you [create an integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) and [add partners](logic-apps-enterprise-integration-partners.md), you can create an AS2 agreement by following these steps.</span></span>

## <a name="create-an-as2-agreement"></a><span data-ttu-id="df0de-112">建立 AS2 合約</span><span class="sxs-lookup"><span data-stu-id="df0de-112">Create an AS2 agreement</span></span>

1.  <span data-ttu-id="df0de-113">登入 [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="df0de-113">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span>  

2.  <span data-ttu-id="df0de-114">從左側功能表中選取 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="df0de-114">From the left menu, select **More services**.</span></span> <span data-ttu-id="df0de-115">在搜尋方塊中，輸入**整合**做為篩選條件。</span><span class="sxs-lookup"><span data-stu-id="df0de-115">In the search box, enter **integration** as your filter.</span></span> <span data-ttu-id="df0de-116">在結果清單中選取 [整合帳戶]。</span><span class="sxs-lookup"><span data-stu-id="df0de-116">In the results list, select **Integration Accounts**.</span></span>

    > [!TIP]
    > <span data-ttu-id="df0de-117">如果沒有看到 [更多服務]，您可能必須先展開功能表。</span><span class="sxs-lookup"><span data-stu-id="df0de-117">If you don't see **More services**, you might have to expand the menu first.</span></span> <span data-ttu-id="df0de-118">在摺疊功能表的頂端，選取 [顯示功能表]。</span><span class="sxs-lookup"><span data-stu-id="df0de-118">At the top of the collapsed menu, select **Show menu**.</span></span>

    ![更多服務，依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. <span data-ttu-id="df0de-120">在開啟的 [整合帳戶]  刀鋒視窗中，選取您要在其中建立合約的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="df0de-120">In the **Integration Accounts** blade that opens, select the integration account where you want to create the agreement.</span></span>
<span data-ttu-id="df0de-121">如果沒有看到任何整合帳戶，請[先建立一個](../logic-apps/logic-apps-enterprise-integration-accounts.md "關於整合帳戶的一切")。</span><span class="sxs-lookup"><span data-stu-id="df0de-121">If you don't see any integration accounts, [create one first](../logic-apps/logic-apps-enterprise-integration-accounts.md "All about integration accounts").</span></span>  

    ![選取您要在其中建立合約的整合帳戶](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="df0de-123">選擇 [合約] 圖格。</span><span class="sxs-lookup"><span data-stu-id="df0de-123">Choose the **Agreements** tile.</span></span> <span data-ttu-id="df0de-124">如果您沒有 [合約] 圖格，請先新增圖格。</span><span class="sxs-lookup"><span data-stu-id="df0de-124">If you don't have an Agreements tile, add the tile first.</span></span>

    ![選擇 [合約] 圖格](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. <span data-ttu-id="df0de-126">在開啟的 [合約] 刀鋒視窗中選擇 [新增]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="df0de-126">In the Agreements blade that opens, choose **Add**.</span></span>

    ![選擇 [新增]](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. <span data-ttu-id="df0de-128">在 [新增] 之下，輸入合約的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="df0de-128">Under **Add**, enter a **Name** for your agreement.</span></span> <span data-ttu-id="df0de-129">針對 [合約類型]，選取 **AS2**。</span><span class="sxs-lookup"><span data-stu-id="df0de-129">For **Agreement type**, select **AS2**.</span></span> <span data-ttu-id="df0de-130">選取合約的 [主機夥伴]、[主機身分識別]、[來賓夥伴] 和 [來賓身分識別]。</span><span class="sxs-lookup"><span data-stu-id="df0de-130">Select the **Host Partner**, **Host Identity**, **Guest Partner**, and **Guest Identity** for your agreement.</span></span>

    ![提供合約詳細資料](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | <span data-ttu-id="df0de-132">屬性</span><span class="sxs-lookup"><span data-stu-id="df0de-132">Property</span></span> | <span data-ttu-id="df0de-133">說明</span><span class="sxs-lookup"><span data-stu-id="df0de-133">Description</span></span> |
    | --- | --- |
    | <span data-ttu-id="df0de-134">名稱</span><span class="sxs-lookup"><span data-stu-id="df0de-134">Name</span></span> |<span data-ttu-id="df0de-135">合約的名稱</span><span class="sxs-lookup"><span data-stu-id="df0de-135">Name of the agreement</span></span> |
    | <span data-ttu-id="df0de-136">合約類型</span><span class="sxs-lookup"><span data-stu-id="df0de-136">Agreement Type</span></span> | <span data-ttu-id="df0de-137">應該是 AS2</span><span class="sxs-lookup"><span data-stu-id="df0de-137">Should be AS2</span></span> |
    | <span data-ttu-id="df0de-138">主控夥伴</span><span class="sxs-lookup"><span data-stu-id="df0de-138">Host Partner</span></span> |<span data-ttu-id="df0de-139">合約需要主控夥伴和來賓夥伴。</span><span class="sxs-lookup"><span data-stu-id="df0de-139">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="df0de-140">主機夥伴代表設定合約的組織。</span><span class="sxs-lookup"><span data-stu-id="df0de-140">The host partner represents the organization that configures the agreement.</span></span> |
    | <span data-ttu-id="df0de-141">主控身分識別</span><span class="sxs-lookup"><span data-stu-id="df0de-141">Host Identity</span></span> |<span data-ttu-id="df0de-142">主控夥伴的識別碼</span><span class="sxs-lookup"><span data-stu-id="df0de-142">An identifier for the host partner</span></span> |
    | <span data-ttu-id="df0de-143">來賓夥伴</span><span class="sxs-lookup"><span data-stu-id="df0de-143">Guest Partner</span></span> |<span data-ttu-id="df0de-144">合約需要主控夥伴和來賓夥伴。</span><span class="sxs-lookup"><span data-stu-id="df0de-144">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="df0de-145">來賓夥伴代表與主控夥伴有生意往來的組織。</span><span class="sxs-lookup"><span data-stu-id="df0de-145">The guest partner represents the organization that's doing business with the host partner.</span></span> |
    | <span data-ttu-id="df0de-146">來賓身分識別</span><span class="sxs-lookup"><span data-stu-id="df0de-146">Guest Identity</span></span> |<span data-ttu-id="df0de-147">來賓合作夥伴的識別碼</span><span class="sxs-lookup"><span data-stu-id="df0de-147">An identifier for the guest partner</span></span> |
    | <span data-ttu-id="df0de-148">接收設定</span><span class="sxs-lookup"><span data-stu-id="df0de-148">Receive Settings</span></span> |<span data-ttu-id="df0de-149">這些屬性會套用到合約所接收的所有訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-149">These properties apply to all messages received by an agreement.</span></span> |
    | <span data-ttu-id="df0de-150">傳送設定</span><span class="sxs-lookup"><span data-stu-id="df0de-150">Send Settings</span></span> |<span data-ttu-id="df0de-151">這些屬性會套用到合約所傳送的所有訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-151">These properties apply to all messages sent by an agreement.</span></span> |

## <a name="configure-how-your-agreement-handles-received-messages"></a><span data-ttu-id="df0de-152">設定合約處理所收到訊息的方式</span><span class="sxs-lookup"><span data-stu-id="df0de-152">Configure how your agreement handles received messages</span></span>

<span data-ttu-id="df0de-153">您現在已經設定合約屬性，您可以設定此合約如何識別及處理您透過此合約從夥伴接收的內送訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-153">Now that you've set the agreement properties, you can configure how this agreement identifies and handles incoming messages received from your partner through this agreement.</span></span>

1.  <span data-ttu-id="df0de-154">在 [新增] 之下，選取 [接收設定]。</span><span class="sxs-lookup"><span data-stu-id="df0de-154">Under **Add**, select **Receive Settings**.</span></span>
<span data-ttu-id="df0de-155">根據您與其交換訊息之夥伴所簽署的合約，設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="df0de-155">Configure these properties based on your agreement with the partner that exchanges messages with you.</span></span> <span data-ttu-id="df0de-156">如需屬性說明，請參閱本節中的資料表。</span><span class="sxs-lookup"><span data-stu-id="df0de-156">For property descriptions, see the table in this section.</span></span>

    ![設定 [接收設定]](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. <span data-ttu-id="df0de-158">您也可以透過選取 [覆寫訊息屬性]，覆寫內送訊息的屬性。</span><span class="sxs-lookup"><span data-stu-id="df0de-158">Optionally, you can override the properties of incoming messages by selecting **Override message properties**.</span></span>

3. <span data-ttu-id="df0de-159">若要要求所有內送訊息都必須經過簽署，請選取 [訊息必須經過簽署]。</span><span class="sxs-lookup"><span data-stu-id="df0de-159">To require all incoming messages to be signed, select **Message should be signed**.</span></span> <span data-ttu-id="df0de-160">從 [憑證] 清單中選取現有的[來賓夥伴公開憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)，以便驗證訊息上的簽章。</span><span class="sxs-lookup"><span data-stu-id="df0de-160">From the **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for validating the signature on the messages.</span></span> <span data-ttu-id="df0de-161">如果您沒有憑證，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="df0de-161">Or create the certificate, if you don't have one.</span></span>

4.  <span data-ttu-id="df0de-162">若要要求加密所有內送訊息，請選取 [訊息必須加密]。</span><span class="sxs-lookup"><span data-stu-id="df0de-162">To require all incoming messages to be encrypted, select **Message should be encrypted**.</span></span> <span data-ttu-id="df0de-163">從 [憑證] 清單，選取現有[主機夥伴私人憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)，以便將內送訊息解密。</span><span class="sxs-lookup"><span data-stu-id="df0de-163">From the **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for decrypting incoming messages.</span></span> <span data-ttu-id="df0de-164">如果您沒有憑證，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="df0de-164">Or create the certificate, if you don't have one.</span></span>

5. <span data-ttu-id="df0de-165">若要要求訊息必須壓縮，請選取 [訊息必須壓縮]。</span><span class="sxs-lookup"><span data-stu-id="df0de-165">To require messages to be compressed, select **Message should be compressed**.</span></span>

6. <span data-ttu-id="df0de-166">若要針對已接收的訊息傳送同步郵件處置通知 (MDN)，請選取 [傳送 MDN]。</span><span class="sxs-lookup"><span data-stu-id="df0de-166">To send a synchronous message disposition notification (MDN) for received messages, select **Send MDN**.</span></span>

7. <span data-ttu-id="df0de-167">若要針對已接收的訊息傳送已簽署的 MDN，請選取 [傳送經過簽署的 MDN]。</span><span class="sxs-lookup"><span data-stu-id="df0de-167">To send signed MDNs for received messages, select **Send signed MDN**.</span></span>

8. <span data-ttu-id="df0de-168">若要針對已接收的訊息傳送非同步 MDN，請選取 [傳送非同步 MDN]。</span><span class="sxs-lookup"><span data-stu-id="df0de-168">To send asynchronous MDNs for received messages, select **Send asynchronous MDN**.</span></span>

9. <span data-ttu-id="df0de-169">完成後，請務必選擇 [確定] 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="df0de-169">After you're done, make sure to save your settings by choosing **OK**.</span></span>

<span data-ttu-id="df0de-170">您的合約現在已準備好處理符合您所選設定的內送訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-170">Now your agreement is ready to handle incoming messages that conform to your selected settings.</span></span>

| <span data-ttu-id="df0de-171">屬性</span><span class="sxs-lookup"><span data-stu-id="df0de-171">Property</span></span> | <span data-ttu-id="df0de-172">說明</span><span class="sxs-lookup"><span data-stu-id="df0de-172">Description</span></span> |
| --- | --- |
| <span data-ttu-id="df0de-173">覆寫訊息屬性</span><span class="sxs-lookup"><span data-stu-id="df0de-173">Override message properties</span></span> |<span data-ttu-id="df0de-174">指出所接收訊息中可被覆寫的屬性。</span><span class="sxs-lookup"><span data-stu-id="df0de-174">Indicates that properties in received messages can be overridden.</span></span> |
| <span data-ttu-id="df0de-175">訊息應該簽署</span><span class="sxs-lookup"><span data-stu-id="df0de-175">Message should be signed</span></span> |<span data-ttu-id="df0de-176">要求訊息必須經過數位簽署。</span><span class="sxs-lookup"><span data-stu-id="df0de-176">Requires messages to be digitally signed.</span></span> <span data-ttu-id="df0de-177">設定來賓合作夥伴公開憑證以進行簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="df0de-177">Configure the guest partner public certificate for signature verification.</span></span>  |
| <span data-ttu-id="df0de-178">訊息應該加密</span><span class="sxs-lookup"><span data-stu-id="df0de-178">Message should be encrypted</span></span> |<span data-ttu-id="df0de-179">要求訊息必須經過加密。</span><span class="sxs-lookup"><span data-stu-id="df0de-179">Requires messages to be encrypted.</span></span> <span data-ttu-id="df0de-180">未加密的訊息會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="df0de-180">Non-encrypted messages are rejected.</span></span> <span data-ttu-id="df0de-181">設定主控夥伴私人憑證以進行訊息解密。</span><span class="sxs-lookup"><span data-stu-id="df0de-181">Configure the host partner private certificate for decrypting the messages.</span></span>  |
| <span data-ttu-id="df0de-182">訊息應該壓縮</span><span class="sxs-lookup"><span data-stu-id="df0de-182">Message should be compressed</span></span> |<span data-ttu-id="df0de-183">要求訊息必須經過壓縮。</span><span class="sxs-lookup"><span data-stu-id="df0de-183">Requires messages to be compressed.</span></span> <span data-ttu-id="df0de-184">未壓縮的訊息會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="df0de-184">Non-compressed messages are rejected.</span></span> |
| <span data-ttu-id="df0de-185">MDN 文字</span><span class="sxs-lookup"><span data-stu-id="df0de-185">MDN Text</span></span> |<span data-ttu-id="df0de-186">要傳送給郵件寄件者的預設郵件處置通知 (MDN)。</span><span class="sxs-lookup"><span data-stu-id="df0de-186">The default message disposition notification (MDN) to be sent to the message sender.</span></span> |
| <span data-ttu-id="df0de-187">傳送 MDN</span><span class="sxs-lookup"><span data-stu-id="df0de-187">Send MDN</span></span> |<span data-ttu-id="df0de-188">要求傳送 MDN。</span><span class="sxs-lookup"><span data-stu-id="df0de-188">Requires MDNs to be sent.</span></span> |
| <span data-ttu-id="df0de-189">傳送簽署的 MDN</span><span class="sxs-lookup"><span data-stu-id="df0de-189">Send signed MDN</span></span> |<span data-ttu-id="df0de-190">要求簽署 MDN。</span><span class="sxs-lookup"><span data-stu-id="df0de-190">Requires MDNs to be signed.</span></span> |
| <span data-ttu-id="df0de-191">MIC 演算法</span><span class="sxs-lookup"><span data-stu-id="df0de-191">MIC Algorithm</span></span> |<span data-ttu-id="df0de-192">選取要用於簽署訊息的演算法。</span><span class="sxs-lookup"><span data-stu-id="df0de-192">Select the algorithm to use for signing messages.</span></span> |
| <span data-ttu-id="df0de-193">傳送非同步 MDN</span><span class="sxs-lookup"><span data-stu-id="df0de-193">Send asynchronous MDN</span></span> | <span data-ttu-id="df0de-194">要求以非同步方式傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-194">Requires messages to be sent asynchronously.</span></span> |
| <span data-ttu-id="df0de-195">URL</span><span class="sxs-lookup"><span data-stu-id="df0de-195">URL</span></span> | <span data-ttu-id="df0de-196">指定要傳送 MDN 的 URL。</span><span class="sxs-lookup"><span data-stu-id="df0de-196">Specify the URL where to send the MDNs.</span></span> |

## <a name="configure-how-your-agreement-sends-messages"></a><span data-ttu-id="df0de-197">設定合約傳送訊息的方式</span><span class="sxs-lookup"><span data-stu-id="df0de-197">Configure how your agreement sends messages</span></span>

<span data-ttu-id="df0de-198">您可以設定此合約如何識別及處理您透過此合約傳送給夥伴的外寄訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-198">You can configure how this agreement identifies and handles outgoing messages that you send to your partners through this agreement.</span></span>

1.  <span data-ttu-id="df0de-199">在 [新增] 之下，選取 [傳送設定]。</span><span class="sxs-lookup"><span data-stu-id="df0de-199">Under **Add**, select **Send Settings**.</span></span>
<span data-ttu-id="df0de-200">根據您與其交換訊息之夥伴所簽署的合約，設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="df0de-200">Configure these properties based on your agreement with the partner that exchanges messages with you.</span></span> <span data-ttu-id="df0de-201">如需屬性說明，請參閱本節中的資料表。</span><span class="sxs-lookup"><span data-stu-id="df0de-201">For property descriptions, see the table in this section.</span></span>

    ![設定 [傳送設定] 屬性](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. <span data-ttu-id="df0de-203">若要將經過簽署的訊息傳送給夥伴，請選取 [啟用訊息簽署]。</span><span class="sxs-lookup"><span data-stu-id="df0de-203">To send signed messages to your partner, select **Enable message signing**.</span></span> <span data-ttu-id="df0de-204">若要簽署訊息，請在 [MIC 演算法] 清單中，選取「主機夥伴私人憑證 MIC 演算法」。</span><span class="sxs-lookup"><span data-stu-id="df0de-204">For signing the messages, in the **MIC Algorithm** list, select the *host partner private certificate MIC Algorithm*.</span></span> <span data-ttu-id="df0de-205">並且在 [憑證] 清單中，選取現有[主機夥伴私人憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="df0de-205">And in the **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span></span>

3. <span data-ttu-id="df0de-206">若要將加密的訊息傳送給夥伴，請選取 [啟用訊息加密]。</span><span class="sxs-lookup"><span data-stu-id="df0de-206">To send encrypted messages to the partner, select **Enable message encryption**.</span></span> <span data-ttu-id="df0de-207">若要加密訊息，請在 [加密演算法] 清單中，選取「來賓夥伴公開憑證演算法」。</span><span class="sxs-lookup"><span data-stu-id="df0de-207">For encrypting the messages, in the **Encryption Algorithm** list, select the *guest partner public certificate algorithm*.</span></span>
<span data-ttu-id="df0de-208">並且在 [憑證] 清單中，選取現有[來賓夥伴公開憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="df0de-208">And in the **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span></span>

4. <span data-ttu-id="df0de-209">若要壓縮訊息，請選取 [啟用訊息壓縮]。</span><span class="sxs-lookup"><span data-stu-id="df0de-209">To compress the message, select **Enable message compression**.</span></span>

5. <span data-ttu-id="df0de-210">若要將 HTTP content-type 標頭展開為單一行，請選取 [展開 HTTP 標頭]。</span><span class="sxs-lookup"><span data-stu-id="df0de-210">To unfold the HTTP content-type header into a single line, select **Unfold HTTP headers**.</span></span>

6. <span data-ttu-id="df0de-211">若要接收所傳送訊息的同步 MDN，請選取 [要求 MDN]。</span><span class="sxs-lookup"><span data-stu-id="df0de-211">To receive synchronous MDNs for the sent messages, select **Request MDN**.</span></span>

7. <span data-ttu-id="df0de-212">若要接收所傳送訊息的已簽署 MDN，請選取 [要求經過簽署的 MDN]。</span><span class="sxs-lookup"><span data-stu-id="df0de-212">To receive signed MDNs for the sent messages, select **Request signed MDN**.</span></span>

8. <span data-ttu-id="df0de-213">若要接收所傳送訊息的同步 MDN，請選取 [要求非同步 MDN]。</span><span class="sxs-lookup"><span data-stu-id="df0de-213">To receive asynchronous MDNs for the sent messages, select **Request asynchronous MDN**.</span></span> <span data-ttu-id="df0de-214">若選取此選項，請輸入 MDN 傳送目標的 URL。</span><span class="sxs-lookup"><span data-stu-id="df0de-214">If you select this option, enter the URL for where to send the MDNs.</span></span>

9. <span data-ttu-id="df0de-215">若要要求接收的不可否認性，請選取 [啟用 NRR]。</span><span class="sxs-lookup"><span data-stu-id="df0de-215">To require non-repudiation of receipt, select **Enable NRR**.</span></span>  

10. <span data-ttu-id="df0de-216">若要指定要用於 MIC 或簽署外寄 AS2 訊息或 MDN 的標題中之演算法格式，選取 **SHA2 演算法格式**。</span><span class="sxs-lookup"><span data-stu-id="df0de-216">To specify algorithm format to use in the MIC or signing in the outgoing headers of the AS2 message or MDN, select **SHA2 Algorithm format**.</span></span>  

11. <span data-ttu-id="df0de-217">完成後，請務必選擇 [確定] 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="df0de-217">After you're done, make sure to save your settings by choosing **OK**.</span></span>

<span data-ttu-id="df0de-218">您的合約現在已準備好處理符合您所選設定的外寄訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-218">Now your agreement is ready to handle outgoing messages that conform to your selected settings.</span></span>

| <span data-ttu-id="df0de-219">屬性</span><span class="sxs-lookup"><span data-stu-id="df0de-219">Property</span></span> | <span data-ttu-id="df0de-220">說明</span><span class="sxs-lookup"><span data-stu-id="df0de-220">Description</span></span> |
| --- | --- |
| <span data-ttu-id="df0de-221">啟用訊息簽署</span><span class="sxs-lookup"><span data-stu-id="df0de-221">Enable message signing</span></span> |<span data-ttu-id="df0de-222">要求傳送自合約的所有訊息都必須經過簽署。</span><span class="sxs-lookup"><span data-stu-id="df0de-222">Requires all messages that are sent from the agreement to be signed.</span></span> |
| <span data-ttu-id="df0de-223">MIC 演算法</span><span class="sxs-lookup"><span data-stu-id="df0de-223">MIC Algorithm</span></span> |<span data-ttu-id="df0de-224">用於簽署訊息的演算法。</span><span class="sxs-lookup"><span data-stu-id="df0de-224">The algorithm to use for signing messages.</span></span> <span data-ttu-id="df0de-225">設定主控夥伴私人憑證 MIC 演算法以簽署訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-225">Configures the host partner private certificate MIC Algorithm for signing the messages.</span></span> |
| <span data-ttu-id="df0de-226">憑證</span><span class="sxs-lookup"><span data-stu-id="df0de-226">Certificate</span></span> |<span data-ttu-id="df0de-227">選取要用於簽署訊息的憑證。</span><span class="sxs-lookup"><span data-stu-id="df0de-227">Select the certificate to use for signing messages.</span></span> <span data-ttu-id="df0de-228">設定主控夥伴私人憑證以簽署訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-228">Configures the host partner private certificate for signing the messages.</span></span> |
| <span data-ttu-id="df0de-229">啟用訊息加密</span><span class="sxs-lookup"><span data-stu-id="df0de-229">Enable message encryption</span></span> |<span data-ttu-id="df0de-230">要求傳送自此合約的所有訊息都必須經過加密。</span><span class="sxs-lookup"><span data-stu-id="df0de-230">Requires encryption of all messages that are sent from this agreement.</span></span> <span data-ttu-id="df0de-231">設定來賓合作夥伴公開憑證演算法以加密訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-231">Configures the guest partner public certificate algorithm for encrypting the messages.</span></span> |
| <span data-ttu-id="df0de-232">加密演算法</span><span class="sxs-lookup"><span data-stu-id="df0de-232">Encryption Algorithm</span></span> |<span data-ttu-id="df0de-233">要用於訊息加密的加密演算法。</span><span class="sxs-lookup"><span data-stu-id="df0de-233">The encryption algorithm to use for message encryption.</span></span> <span data-ttu-id="df0de-234">設定來賓合作夥伴公開憑證以加密訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-234">Configures the guest partner public certificate for encrypting the messages.</span></span> |
| <span data-ttu-id="df0de-235">憑證</span><span class="sxs-lookup"><span data-stu-id="df0de-235">Certificate</span></span> |<span data-ttu-id="df0de-236">要用於加密訊息的憑證。</span><span class="sxs-lookup"><span data-stu-id="df0de-236">The certificate to use to encrypt messages.</span></span> <span data-ttu-id="df0de-237">設定來賓合作夥伴私人憑證以加密訊息。</span><span class="sxs-lookup"><span data-stu-id="df0de-237">Configures the guest partner private certificate for encrypting the messages.</span></span> |
| <span data-ttu-id="df0de-238">啟用訊息壓縮</span><span class="sxs-lookup"><span data-stu-id="df0de-238">Enable message compression</span></span> |<span data-ttu-id="df0de-239">要求傳送自此合約的所有訊息都必須經過壓縮。</span><span class="sxs-lookup"><span data-stu-id="df0de-239">Requires compression of all messages that are sent from this agreement.</span></span> |
| <span data-ttu-id="df0de-240">展開 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="df0de-240">Unfold HTTP headers</span></span> |<span data-ttu-id="df0de-241">請將 HTTP 內容類型標頭放在一行中。</span><span class="sxs-lookup"><span data-stu-id="df0de-241">Places the HTTP content-type header onto a single line.</span></span> |
| <span data-ttu-id="df0de-242">要求 MDN</span><span class="sxs-lookup"><span data-stu-id="df0de-242">Request MDN</span></span> |<span data-ttu-id="df0de-243">針對傳送自此合約的所有訊息要求 MDN。</span><span class="sxs-lookup"><span data-stu-id="df0de-243">Requires an MDN for all messages that are sent from this agreement.</span></span> |
| <span data-ttu-id="df0de-244">要求簽署的 MDN</span><span class="sxs-lookup"><span data-stu-id="df0de-244">Request signed MDN</span></span> |<span data-ttu-id="df0de-245">要求傳送到此合約的所有 MDN 都必須經過簽署。</span><span class="sxs-lookup"><span data-stu-id="df0de-245">Requires all MDNs that are sent to this agreement to be signed.</span></span> |
| <span data-ttu-id="df0de-246">要求非同步 MDN</span><span class="sxs-lookup"><span data-stu-id="df0de-246">Request asynchronous MDN</span></span> |<span data-ttu-id="df0de-247">要求將非同步 MDN 傳送到此合約。</span><span class="sxs-lookup"><span data-stu-id="df0de-247">Requires asynchronous MDNs to be sent to this agreement.</span></span> |
| <span data-ttu-id="df0de-248">URL</span><span class="sxs-lookup"><span data-stu-id="df0de-248">URL</span></span> |<span data-ttu-id="df0de-249">指定要傳送 MDN 的 URL。</span><span class="sxs-lookup"><span data-stu-id="df0de-249">Specify the URL where to send the MDNs.</span></span> |
| <span data-ttu-id="df0de-250">啟用 NRR</span><span class="sxs-lookup"><span data-stu-id="df0de-250">Enable NRR</span></span> |<span data-ttu-id="df0de-251">要求接收的不可否認性 (NRR)，這是一種通訊屬性，它會提供資料已由預訂收件者接收的證據。</span><span class="sxs-lookup"><span data-stu-id="df0de-251">Requires non-repudiation of receipt (NRR), a communication attribute that provides evidence that the data was received as addressed.</span></span> |
| <span data-ttu-id="df0de-252">SHA2 演算法格式</span><span class="sxs-lookup"><span data-stu-id="df0de-252">SHA2 Algorithm format</span></span> |<span data-ttu-id="df0de-253">選取要用於 MIC 或簽署外寄 AS2 訊息或 MDN 的標題中之演算法格式</span><span class="sxs-lookup"><span data-stu-id="df0de-253">Select algorithm format to use in the MIC or signing in the outgoing headers of the AS2 message or MDN</span></span> |

## <a name="find-your-created-agreement"></a><span data-ttu-id="df0de-254">尋找您建立的合約</span><span class="sxs-lookup"><span data-stu-id="df0de-254">Find your created agreement</span></span>

1.  <span data-ttu-id="df0de-255">完成所有合約屬性的設定之後，請在 [新增] 刀鋒視窗中選擇 [確定]，以完成合約建立並回到整合帳戶刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="df0de-255">After you finish setting all your agreement properties, on the **Add** blade, choose **OK** to finish creating your agreement and return to your integration account blade.</span></span>

    <span data-ttu-id="df0de-256">您新增的合約現在顯示於您的 [合約] 清單中。</span><span class="sxs-lookup"><span data-stu-id="df0de-256">Your newly added agreement now appears in your **Agreements** list.</span></span>

2.  <span data-ttu-id="df0de-257">您也可以在整合帳戶概觀中檢視您的合約。</span><span class="sxs-lookup"><span data-stu-id="df0de-257">You can also view your agreements in your integration account overview.</span></span> <span data-ttu-id="df0de-258">在整合帳戶刀鋒視窗上，選擇 [概觀]，然後選取 [合約] 圖格。</span><span class="sxs-lookup"><span data-stu-id="df0de-258">On your integration account blade, choose **Overview**, then select the **Agreements** tile.</span></span> 

    ![選擇 [合約] 圖格來檢視所有合約](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-the-swagger"></a><span data-ttu-id="df0de-260">檢視 Swagger</span><span class="sxs-lookup"><span data-stu-id="df0de-260">View the swagger</span></span>
<span data-ttu-id="df0de-261">請參閱 [Swagger 詳細資料](/connectors/as2/)。</span><span class="sxs-lookup"><span data-stu-id="df0de-261">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="df0de-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df0de-262">Next steps</span></span>
* [<span data-ttu-id="df0de-263">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="df0de-263">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "了解企業整合套件")  
