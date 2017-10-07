---
title: "aaaAS2 B2B 企業整合 Azure 邏輯應用程式訊息 |Microsoft 文件"
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
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a><span data-ttu-id="2a04d-103">利用邏輯應用程式交換適用於企業整合的 AS2 訊息</span><span class="sxs-lookup"><span data-stu-id="2a04d-103">Exchange AS2 messages for enterprise integration with logic apps</span></span>

<span data-ttu-id="2a04d-104">您必須先建立 AS2 合約並將該合約儲存在您的整合帳戶中，才可以交換 AS2 訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-104">Before you can exchange AS2 messages for Azure Logic Apps, you must create an AS2 agreement and store that agreement in your integration account.</span></span> <span data-ttu-id="2a04d-105">以下是如何 hello 步驟 toocreate AS2 協議。</span><span class="sxs-lookup"><span data-stu-id="2a04d-105">Here are hello steps for how toocreate an AS2 agreement.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2a04d-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="2a04d-106">Before you start</span></span>

<span data-ttu-id="2a04d-107">以下是您所需要的 hello 項目：</span><span class="sxs-lookup"><span data-stu-id="2a04d-107">Here's hello items you need:</span></span>

* <span data-ttu-id="2a04d-108">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)</span><span class="sxs-lookup"><span data-stu-id="2a04d-108">An [integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) that's already defined and associated with your Azure subscription</span></span>
* <span data-ttu-id="2a04d-109">在至少兩個[夥伴](logic-apps-enterprise-integration-partners.md)，已經定義在整合帳戶並且使用 hello AS2 限定詞下設定**商務識別**</span><span class="sxs-lookup"><span data-stu-id="2a04d-109">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account and configured with hello AS2 qualifier under **Business Identities**</span></span>

> [!NOTE]
> <span data-ttu-id="2a04d-110">當您建立協議時，hello 合約檔案中的 hello 內容必須符合 hello 合約類型。</span><span class="sxs-lookup"><span data-stu-id="2a04d-110">When you create an agreement, hello content in hello agreement file must match hello agreement type.</span></span>    

<span data-ttu-id="2a04d-111">在您[建立整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)並[新增夥伴](logic-apps-enterprise-integration-partners.md)之後，您可以依照下列步驟建立 AS2 合約。</span><span class="sxs-lookup"><span data-stu-id="2a04d-111">After you [create an integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) and [add partners](logic-apps-enterprise-integration-partners.md), you can create an AS2 agreement by following these steps.</span></span>

## <a name="create-an-as2-agreement"></a><span data-ttu-id="2a04d-112">建立 AS2 合約</span><span class="sxs-lookup"><span data-stu-id="2a04d-112">Create an AS2 agreement</span></span>

1.  <span data-ttu-id="2a04d-113">登入 toohello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="2a04d-113">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span>  

2.  <span data-ttu-id="2a04d-114">從 hello 左窗格中，選取**更多服務**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-114">From hello left menu, select **More services**.</span></span> <span data-ttu-id="2a04d-115">在 [hello] 搜尋方塊中，輸入**整合**做為您的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="2a04d-115">In hello search box, enter **integration** as your filter.</span></span> <span data-ttu-id="2a04d-116">在 hello 結果清單中，選取 **整合帳戶**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-116">In hello results list, select **Integration Accounts**.</span></span>

    > [!TIP]
    > <span data-ttu-id="2a04d-117">如果您沒有看到**更多服務**，您可能必須 tooexpand hello 功能表第一次。</span><span class="sxs-lookup"><span data-stu-id="2a04d-117">If you don't see **More services**, you might have tooexpand hello menu first.</span></span> <span data-ttu-id="2a04d-118">在 hello hello 摺疊功能表頂端，選取**顯示功能表**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-118">At hello top of hello collapsed menu, select **Show menu**.</span></span>

    ![更多服務，依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. <span data-ttu-id="2a04d-120">在 hello**整合帳戶**刀鋒視窗中開啟，您想要 toocreate hello 協議選取 hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="2a04d-120">In hello **Integration Accounts** blade that opens, select hello integration account where you want toocreate hello agreement.</span></span>
<span data-ttu-id="2a04d-121">如果沒有看到任何整合帳戶，請[先建立一個](../logic-apps/logic-apps-enterprise-integration-accounts.md "關於整合帳戶的一切")。</span><span class="sxs-lookup"><span data-stu-id="2a04d-121">If you don't see any integration accounts, [create one first](../logic-apps/logic-apps-enterprise-integration-accounts.md "All about integration accounts").</span></span>  

    ![選取其中 toocreate hello 協議的 hello 整合帳戶](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="2a04d-123">選擇 hello**協議**磚。</span><span class="sxs-lookup"><span data-stu-id="2a04d-123">Choose hello **Agreements** tile.</span></span> <span data-ttu-id="2a04d-124">如果您還沒有合約磚，請先新增 hello 磚。</span><span class="sxs-lookup"><span data-stu-id="2a04d-124">If you don't have an Agreements tile, add hello tile first.</span></span>

    ![選擇 [合約] 圖格](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. <span data-ttu-id="2a04d-126">在 hello 協議刀鋒視窗中開啟，選擇 **新增**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-126">In hello Agreements blade that opens, choose **Add**.</span></span>

    ![選擇 [新增]](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. <span data-ttu-id="2a04d-128">在 [新增] 之下，輸入合約的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="2a04d-128">Under **Add**, enter a **Name** for your agreement.</span></span> <span data-ttu-id="2a04d-129">針對 [合約類型]，選取 **AS2**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-129">For **Agreement type**, select **AS2**.</span></span> <span data-ttu-id="2a04d-130">選取 hello**主控合作夥伴**，**主機識別**，**來賓夥伴**，和**客體身分識別**協議。</span><span class="sxs-lookup"><span data-stu-id="2a04d-130">Select hello **Host Partner**, **Host Identity**, **Guest Partner**, and **Guest Identity** for your agreement.</span></span>

    ![提供合約詳細資料](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | <span data-ttu-id="2a04d-132">屬性</span><span class="sxs-lookup"><span data-stu-id="2a04d-132">Property</span></span> | <span data-ttu-id="2a04d-133">說明</span><span class="sxs-lookup"><span data-stu-id="2a04d-133">Description</span></span> |
    | --- | --- |
    | <span data-ttu-id="2a04d-134">名稱</span><span class="sxs-lookup"><span data-stu-id="2a04d-134">Name</span></span> |<span data-ttu-id="2a04d-135">Hello 協議的名稱</span><span class="sxs-lookup"><span data-stu-id="2a04d-135">Name of hello agreement</span></span> |
    | <span data-ttu-id="2a04d-136">合約類型</span><span class="sxs-lookup"><span data-stu-id="2a04d-136">Agreement Type</span></span> | <span data-ttu-id="2a04d-137">應該是 AS2</span><span class="sxs-lookup"><span data-stu-id="2a04d-137">Should be AS2</span></span> |
    | <span data-ttu-id="2a04d-138">主控夥伴</span><span class="sxs-lookup"><span data-stu-id="2a04d-138">Host Partner</span></span> |<span data-ttu-id="2a04d-139">合約需要主控夥伴和來賓夥伴。</span><span class="sxs-lookup"><span data-stu-id="2a04d-139">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="2a04d-140">hello 主控合作夥伴代表 hello 組織設定 hello 協議。</span><span class="sxs-lookup"><span data-stu-id="2a04d-140">hello host partner represents hello organization that configures hello agreement.</span></span> |
    | <span data-ttu-id="2a04d-141">主控身分識別</span><span class="sxs-lookup"><span data-stu-id="2a04d-141">Host Identity</span></span> |<span data-ttu-id="2a04d-142">Hello 主控合作夥伴的的識別項</span><span class="sxs-lookup"><span data-stu-id="2a04d-142">An identifier for hello host partner</span></span> |
    | <span data-ttu-id="2a04d-143">來賓夥伴</span><span class="sxs-lookup"><span data-stu-id="2a04d-143">Guest Partner</span></span> |<span data-ttu-id="2a04d-144">合約需要主控夥伴和來賓夥伴。</span><span class="sxs-lookup"><span data-stu-id="2a04d-144">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="2a04d-145">hello 來賓夥伴代表正在進行 hello 主控合作夥伴與商務的 hello 組織。</span><span class="sxs-lookup"><span data-stu-id="2a04d-145">hello guest partner represents hello organization that's doing business with hello host partner.</span></span> |
    | <span data-ttu-id="2a04d-146">來賓身分識別</span><span class="sxs-lookup"><span data-stu-id="2a04d-146">Guest Identity</span></span> |<span data-ttu-id="2a04d-147">Hello 來賓夥伴的的識別項</span><span class="sxs-lookup"><span data-stu-id="2a04d-147">An identifier for hello guest partner</span></span> |
    | <span data-ttu-id="2a04d-148">接收設定</span><span class="sxs-lookup"><span data-stu-id="2a04d-148">Receive Settings</span></span> |<span data-ttu-id="2a04d-149">這些屬性會套用 tooall 的協議所收到的訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-149">These properties apply tooall messages received by an agreement.</span></span> |
    | <span data-ttu-id="2a04d-150">傳送設定</span><span class="sxs-lookup"><span data-stu-id="2a04d-150">Send Settings</span></span> |<span data-ttu-id="2a04d-151">這些屬性會套用 tooall 的協議所傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-151">These properties apply tooall messages sent by an agreement.</span></span> |

## <a name="configure-how-your-agreement-handles-received-messages"></a><span data-ttu-id="2a04d-152">設定合約處理所收到訊息的方式</span><span class="sxs-lookup"><span data-stu-id="2a04d-152">Configure how your agreement handles received messages</span></span>

<span data-ttu-id="2a04d-153">既然您已經設定 hello 協議屬性，您可以設定如何識別本合約，以及處理從夥伴透過此協議接收內送訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-153">Now that you've set hello agreement properties, you can configure how this agreement identifies and handles incoming messages received from your partner through this agreement.</span></span>

1.  <span data-ttu-id="2a04d-154">在 [新增] 之下，選取 [接收設定]。</span><span class="sxs-lookup"><span data-stu-id="2a04d-154">Under **Add**, select **Receive Settings**.</span></span>
<span data-ttu-id="2a04d-155">設定這些屬性，根據您的合約與 hello 夥伴與您交換訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-155">Configure these properties based on your agreement with hello partner that exchanges messages with you.</span></span> <span data-ttu-id="2a04d-156">如屬性描述，請參閱本節中的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="2a04d-156">For property descriptions, see hello table in this section.</span></span>

    ![設定 [接收設定]](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. <span data-ttu-id="2a04d-158">（選擇性） 您可以覆寫內送訊息的 hello 屬性選取**覆寫訊息屬性**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-158">Optionally, you can override hello properties of incoming messages by selecting **Override message properties**.</span></span>

3. <span data-ttu-id="2a04d-159">toorequire 所有內送訊息 toobe 簽署，請選取**訊息應該簽署**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-159">toorequire all incoming messages toobe signed, select **Message should be signed**.</span></span> <span data-ttu-id="2a04d-160">從 hello**憑證**清單中，選取現有[來賓夥伴公開憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)驗證 hello hello 訊息上的簽章。</span><span class="sxs-lookup"><span data-stu-id="2a04d-160">From hello **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for validating hello signature on hello messages.</span></span> <span data-ttu-id="2a04d-161">或如果您沒有建立 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="2a04d-161">Or create hello certificate, if you don't have one.</span></span>

4.  <span data-ttu-id="2a04d-162">選取 toorequire 加密，所有內送訊息 toobe**訊息應該加密**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-162">toorequire all incoming messages toobe encrypted, select **Message should be encrypted**.</span></span> <span data-ttu-id="2a04d-163">從 hello**憑證**清單中，選取現有[主機夥伴私人憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)解密內送訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-163">From hello **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for decrypting incoming messages.</span></span> <span data-ttu-id="2a04d-164">或如果您沒有建立 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="2a04d-164">Or create hello certificate, if you don't have one.</span></span>

5. <span data-ttu-id="2a04d-165">toorequire 訊息 toobe 壓縮，選取**訊息應該壓縮**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-165">toorequire messages toobe compressed, select **Message should be compressed**.</span></span>

6. <span data-ttu-id="2a04d-166">toosend 接收的訊息，同步訊息處理通知 (MDN) 選取**傳送 MDN**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-166">toosend a synchronous message disposition notification (MDN) for received messages, select **Send MDN**.</span></span>

7. <span data-ttu-id="2a04d-167">toosend 簽署 Mdn 的接收的訊息，選取**傳送簽署的 MDN**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-167">toosend signed MDNs for received messages, select **Send signed MDN**.</span></span>

8. <span data-ttu-id="2a04d-168">非同步的 Mdn 接收之訊息，選取 toosend**傳送非同步 MDN**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-168">toosend asynchronous MDNs for received messages, select **Send asynchronous MDN**.</span></span>

9. <span data-ttu-id="2a04d-169">瀏覽完畢之後，請確定 toosave 您的設定選擇**確定**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-169">After you're done, make sure toosave your settings by choosing **OK**.</span></span>

<span data-ttu-id="2a04d-170">現在您的合約已準備好 toohandle 內送訊息符合 tooyour 選取的設定。</span><span class="sxs-lookup"><span data-stu-id="2a04d-170">Now your agreement is ready toohandle incoming messages that conform tooyour selected settings.</span></span>

| <span data-ttu-id="2a04d-171">屬性</span><span class="sxs-lookup"><span data-stu-id="2a04d-171">Property</span></span> | <span data-ttu-id="2a04d-172">說明</span><span class="sxs-lookup"><span data-stu-id="2a04d-172">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a04d-173">覆寫訊息屬性</span><span class="sxs-lookup"><span data-stu-id="2a04d-173">Override message properties</span></span> |<span data-ttu-id="2a04d-174">指出所接收訊息中可被覆寫的屬性。</span><span class="sxs-lookup"><span data-stu-id="2a04d-174">Indicates that properties in received messages can be overridden.</span></span> |
| <span data-ttu-id="2a04d-175">訊息應該簽署</span><span class="sxs-lookup"><span data-stu-id="2a04d-175">Message should be signed</span></span> |<span data-ttu-id="2a04d-176">需要訊息 toobe 數位簽章。</span><span class="sxs-lookup"><span data-stu-id="2a04d-176">Requires messages toobe digitally signed.</span></span> <span data-ttu-id="2a04d-177">設定用於簽章驗證的 hello 來賓夥伴公開憑證。</span><span class="sxs-lookup"><span data-stu-id="2a04d-177">Configure hello guest partner public certificate for signature verification.</span></span>  |
| <span data-ttu-id="2a04d-178">訊息應該加密</span><span class="sxs-lookup"><span data-stu-id="2a04d-178">Message should be encrypted</span></span> |<span data-ttu-id="2a04d-179">需要加密的訊息 toobe。</span><span class="sxs-lookup"><span data-stu-id="2a04d-179">Requires messages toobe encrypted.</span></span> <span data-ttu-id="2a04d-180">未加密的訊息會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="2a04d-180">Non-encrypted messages are rejected.</span></span> <span data-ttu-id="2a04d-181">設定用於解密 hello 訊息的 hello 主機夥伴私人憑證。</span><span class="sxs-lookup"><span data-stu-id="2a04d-181">Configure hello host partner private certificate for decrypting hello messages.</span></span>  |
| <span data-ttu-id="2a04d-182">訊息應該壓縮</span><span class="sxs-lookup"><span data-stu-id="2a04d-182">Message should be compressed</span></span> |<span data-ttu-id="2a04d-183">需要訊息 toobe 壓縮。</span><span class="sxs-lookup"><span data-stu-id="2a04d-183">Requires messages toobe compressed.</span></span> <span data-ttu-id="2a04d-184">未壓縮的訊息會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="2a04d-184">Non-compressed messages are rejected.</span></span> |
| <span data-ttu-id="2a04d-185">MDN 文字</span><span class="sxs-lookup"><span data-stu-id="2a04d-185">MDN Text</span></span> |<span data-ttu-id="2a04d-186">hello 預設訊息處置通知 (MDN) toobe 傳送 toohello 訊息寄件者。</span><span class="sxs-lookup"><span data-stu-id="2a04d-186">hello default message disposition notification (MDN) toobe sent toohello message sender.</span></span> |
| <span data-ttu-id="2a04d-187">傳送 MDN</span><span class="sxs-lookup"><span data-stu-id="2a04d-187">Send MDN</span></span> |<span data-ttu-id="2a04d-188">需要傳送 Mdn toobe。</span><span class="sxs-lookup"><span data-stu-id="2a04d-188">Requires MDNs toobe sent.</span></span> |
| <span data-ttu-id="2a04d-189">傳送簽署的 MDN</span><span class="sxs-lookup"><span data-stu-id="2a04d-189">Send signed MDN</span></span> |<span data-ttu-id="2a04d-190">需要已簽署的 Mdn toobe。</span><span class="sxs-lookup"><span data-stu-id="2a04d-190">Requires MDNs toobe signed.</span></span> |
| <span data-ttu-id="2a04d-191">MIC 演算法</span><span class="sxs-lookup"><span data-stu-id="2a04d-191">MIC Algorithm</span></span> |<span data-ttu-id="2a04d-192">選取 hello 演算法 toouse 簽署訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-192">Select hello algorithm toouse for signing messages.</span></span> |
| <span data-ttu-id="2a04d-193">傳送非同步 MDN</span><span class="sxs-lookup"><span data-stu-id="2a04d-193">Send asynchronous MDN</span></span> | <span data-ttu-id="2a04d-194">需要訊息 toobe 以非同步方式傳送。</span><span class="sxs-lookup"><span data-stu-id="2a04d-194">Requires messages toobe sent asynchronously.</span></span> |
| <span data-ttu-id="2a04d-195">URL</span><span class="sxs-lookup"><span data-stu-id="2a04d-195">URL</span></span> | <span data-ttu-id="2a04d-196">指定 hello toosend 其中 hello Mdn 的 URL。</span><span class="sxs-lookup"><span data-stu-id="2a04d-196">Specify hello URL where toosend hello MDNs.</span></span> |

## <a name="configure-how-your-agreement-sends-messages"></a><span data-ttu-id="2a04d-197">設定合約傳送訊息的方式</span><span class="sxs-lookup"><span data-stu-id="2a04d-197">Configure how your agreement sends messages</span></span>

<span data-ttu-id="2a04d-198">您可以設定此協議如何識別及處理外寄傳送 tooyour 夥伴透過此合約的訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-198">You can configure how this agreement identifies and handles outgoing messages that you send tooyour partners through this agreement.</span></span>

1.  <span data-ttu-id="2a04d-199">在 [新增] 之下，選取 [傳送設定]。</span><span class="sxs-lookup"><span data-stu-id="2a04d-199">Under **Add**, select **Send Settings**.</span></span>
<span data-ttu-id="2a04d-200">設定這些屬性，根據您的合約與 hello 夥伴與您交換訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-200">Configure these properties based on your agreement with hello partner that exchanges messages with you.</span></span> <span data-ttu-id="2a04d-201">如屬性描述，請參閱本節中的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="2a04d-201">For property descriptions, see hello table in this section.</span></span>

    ![設定 hello [傳送設定] 屬性](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. <span data-ttu-id="2a04d-203">toosend 簽章的訊息 tooyour 夥伴、 選取**啟用訊息簽署**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-203">toosend signed messages tooyour partner, select **Enable message signing**.</span></span> <span data-ttu-id="2a04d-204">用於簽章 hello 訊息，請在 hello **MIC 演算法**清單中，選取 hello*主機夥伴私人憑證 MIC 演算法*。</span><span class="sxs-lookup"><span data-stu-id="2a04d-204">For signing hello messages, in hello **MIC Algorithm** list, select hello *host partner private certificate MIC Algorithm*.</span></span> <span data-ttu-id="2a04d-205">在 hello**憑證**清單中，選取現有[主機夥伴私人憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="2a04d-205">And in hello **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span></span>

3. <span data-ttu-id="2a04d-206">toosend 加密的訊息 toohello 夥伴、 選取**啟用訊息加密**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-206">toosend encrypted messages toohello partner, select **Enable message encryption**.</span></span> <span data-ttu-id="2a04d-207">加密 hello 訊息，請在 hello**加密演算法**清單中，選取 hello*來賓夥伴公開憑證演算法*。</span><span class="sxs-lookup"><span data-stu-id="2a04d-207">For encrypting hello messages, in hello **Encryption Algorithm** list, select hello *guest partner public certificate algorithm*.</span></span>
<span data-ttu-id="2a04d-208">在 hello**憑證**清單中，選取現有[來賓夥伴公開憑證](../logic-apps/logic-apps-enterprise-integration-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="2a04d-208">And in hello **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span></span>

4. <span data-ttu-id="2a04d-209">toocompress hello 訊息，選取**啟用訊息壓縮**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-209">toocompress hello message, select **Enable message compression**.</span></span>

5. <span data-ttu-id="2a04d-210">單一資料行，選取 toounfold hello HTTP content-type 標頭**展開 HTTP 標頭**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-210">toounfold hello HTTP content-type header into a single line, select **Unfold HTTP headers**.</span></span>

6. <span data-ttu-id="2a04d-211">tooreceive hello 同步 Mdn 傳送訊息，選取**要求 MDN**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-211">tooreceive synchronous MDNs for hello sent messages, select **Request MDN**.</span></span>

7. <span data-ttu-id="2a04d-212">tooreceive 簽署 Mdn 之傳送 hello 訊息，選取**要求簽署的 MDN**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-212">tooreceive signed MDNs for hello sent messages, select **Request signed MDN**.</span></span>

8. <span data-ttu-id="2a04d-213">tooreceive hello 非同步 Mdn 傳送訊息，選取**要求非同步 MDN**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-213">tooreceive asynchronous MDNs for hello sent messages, select **Request asynchronous MDN**.</span></span> <span data-ttu-id="2a04d-214">如果您選取此選項，輸入 hello URL toosend hello Mdn 的位置。</span><span class="sxs-lookup"><span data-stu-id="2a04d-214">If you select this option, enter hello URL for where toosend hello MDNs.</span></span>

9. <span data-ttu-id="2a04d-215">選取 toorequire 不可否認性回條、**啟用 NRR**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-215">toorequire non-repudiation of receipt, select **Enable NRR**.</span></span>  

10. <span data-ttu-id="2a04d-216">選取在 hello MIC toospecify 演算法格式 toouse 或登入 hello 傳出標頭的 hello AS2 訊息或 MDN， **SHA2 演算法格式**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-216">toospecify algorithm format toouse in hello MIC or signing in hello outgoing headers of hello AS2 message or MDN, select **SHA2 Algorithm format**.</span></span>  

11. <span data-ttu-id="2a04d-217">瀏覽完畢之後，請確定 toosave 您的設定選擇**確定**。</span><span class="sxs-lookup"><span data-stu-id="2a04d-217">After you're done, make sure toosave your settings by choosing **OK**.</span></span>

<span data-ttu-id="2a04d-218">現在您的合約是準備 toohandle 外寄訊息符合 tooyour 選取的設定。</span><span class="sxs-lookup"><span data-stu-id="2a04d-218">Now your agreement is ready toohandle outgoing messages that conform tooyour selected settings.</span></span>

| <span data-ttu-id="2a04d-219">屬性</span><span class="sxs-lookup"><span data-stu-id="2a04d-219">Property</span></span> | <span data-ttu-id="2a04d-220">說明</span><span class="sxs-lookup"><span data-stu-id="2a04d-220">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a04d-221">啟用訊息簽署</span><span class="sxs-lookup"><span data-stu-id="2a04d-221">Enable message signing</span></span> |<span data-ttu-id="2a04d-222">需要從帶正負號的 hello 協議 toobe 傳送的所有訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-222">Requires all messages that are sent from hello agreement toobe signed.</span></span> |
| <span data-ttu-id="2a04d-223">MIC 演算法</span><span class="sxs-lookup"><span data-stu-id="2a04d-223">MIC Algorithm</span></span> |<span data-ttu-id="2a04d-224">hello 演算法 toouse 簽署訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-224">hello algorithm toouse for signing messages.</span></span> <span data-ttu-id="2a04d-225">設定 hello 主機夥伴私人憑證 MIC 演算法來簽署 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-225">Configures hello host partner private certificate MIC Algorithm for signing hello messages.</span></span> |
| <span data-ttu-id="2a04d-226">憑證</span><span class="sxs-lookup"><span data-stu-id="2a04d-226">Certificate</span></span> |<span data-ttu-id="2a04d-227">選取 hello 憑證 toouse 簽署訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-227">Select hello certificate toouse for signing messages.</span></span> <span data-ttu-id="2a04d-228">設定 hello 主機夥伴私人憑證來簽署 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-228">Configures hello host partner private certificate for signing hello messages.</span></span> |
| <span data-ttu-id="2a04d-229">啟用訊息加密</span><span class="sxs-lookup"><span data-stu-id="2a04d-229">Enable message encryption</span></span> |<span data-ttu-id="2a04d-230">要求傳送自此合約的所有訊息都必須經過加密。</span><span class="sxs-lookup"><span data-stu-id="2a04d-230">Requires encryption of all messages that are sent from this agreement.</span></span> <span data-ttu-id="2a04d-231">設定 hello 來賓夥伴公開憑證演算法來加密 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-231">Configures hello guest partner public certificate algorithm for encrypting hello messages.</span></span> |
| <span data-ttu-id="2a04d-232">加密演算法</span><span class="sxs-lookup"><span data-stu-id="2a04d-232">Encryption Algorithm</span></span> |<span data-ttu-id="2a04d-233">hello 訊息加密的加密演算法 toouse。</span><span class="sxs-lookup"><span data-stu-id="2a04d-233">hello encryption algorithm toouse for message encryption.</span></span> <span data-ttu-id="2a04d-234">設定加密 hello 訊息的 hello 來賓夥伴公開憑證。</span><span class="sxs-lookup"><span data-stu-id="2a04d-234">Configures hello guest partner public certificate for encrypting hello messages.</span></span> |
| <span data-ttu-id="2a04d-235">憑證</span><span class="sxs-lookup"><span data-stu-id="2a04d-235">Certificate</span></span> |<span data-ttu-id="2a04d-236">hello 憑證 toouse tooencrypt 訊息。</span><span class="sxs-lookup"><span data-stu-id="2a04d-236">hello certificate toouse tooencrypt messages.</span></span> <span data-ttu-id="2a04d-237">設定加密 hello 訊息的 hello 來賓夥伴私人憑證。</span><span class="sxs-lookup"><span data-stu-id="2a04d-237">Configures hello guest partner private certificate for encrypting hello messages.</span></span> |
| <span data-ttu-id="2a04d-238">啟用訊息壓縮</span><span class="sxs-lookup"><span data-stu-id="2a04d-238">Enable message compression</span></span> |<span data-ttu-id="2a04d-239">要求傳送自此合約的所有訊息都必須經過壓縮。</span><span class="sxs-lookup"><span data-stu-id="2a04d-239">Requires compression of all messages that are sent from this agreement.</span></span> |
| <span data-ttu-id="2a04d-240">展開 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="2a04d-240">Unfold HTTP headers</span></span> |<span data-ttu-id="2a04d-241">會放置到單一行 hello HTTP content-type 標頭。</span><span class="sxs-lookup"><span data-stu-id="2a04d-241">Places hello HTTP content-type header onto a single line.</span></span> |
| <span data-ttu-id="2a04d-242">要求 MDN</span><span class="sxs-lookup"><span data-stu-id="2a04d-242">Request MDN</span></span> |<span data-ttu-id="2a04d-243">針對傳送自此合約的所有訊息要求 MDN。</span><span class="sxs-lookup"><span data-stu-id="2a04d-243">Requires an MDN for all messages that are sent from this agreement.</span></span> |
| <span data-ttu-id="2a04d-244">要求簽署的 MDN</span><span class="sxs-lookup"><span data-stu-id="2a04d-244">Request signed MDN</span></span> |<span data-ttu-id="2a04d-245">需要所有傳送 toothis 協議 toobe 簽署的 Mdn。</span><span class="sxs-lookup"><span data-stu-id="2a04d-245">Requires all MDNs that are sent toothis agreement toobe signed.</span></span> |
| <span data-ttu-id="2a04d-246">要求非同步 MDN</span><span class="sxs-lookup"><span data-stu-id="2a04d-246">Request asynchronous MDN</span></span> |<span data-ttu-id="2a04d-247">要求非同步 Mdn 傳送 toobe toothis 協議。</span><span class="sxs-lookup"><span data-stu-id="2a04d-247">Requires asynchronous MDNs toobe sent toothis agreement.</span></span> |
| <span data-ttu-id="2a04d-248">URL</span><span class="sxs-lookup"><span data-stu-id="2a04d-248">URL</span></span> |<span data-ttu-id="2a04d-249">指定 hello toosend 其中 hello Mdn 的 URL。</span><span class="sxs-lookup"><span data-stu-id="2a04d-249">Specify hello URL where toosend hello MDNs.</span></span> |
| <span data-ttu-id="2a04d-250">啟用 NRR</span><span class="sxs-lookup"><span data-stu-id="2a04d-250">Enable NRR</span></span> |<span data-ttu-id="2a04d-251">需要不可否認性回條 (NRR)，提供辨識項 hello 資料通訊屬性收到因為收件者。</span><span class="sxs-lookup"><span data-stu-id="2a04d-251">Requires non-repudiation of receipt (NRR), a communication attribute that provides evidence that hello data was received as addressed.</span></span> |
| <span data-ttu-id="2a04d-252">SHA2 演算法格式</span><span class="sxs-lookup"><span data-stu-id="2a04d-252">SHA2 Algorithm format</span></span> |<span data-ttu-id="2a04d-253">選取演算法格式 toouse hello MIC 或登入 hello 傳出 hello AS2 訊息或 MDN 的標頭中</span><span class="sxs-lookup"><span data-stu-id="2a04d-253">Select algorithm format toouse in hello MIC or signing in hello outgoing headers of hello AS2 message or MDN</span></span> |

## <a name="find-your-created-agreement"></a><span data-ttu-id="2a04d-254">尋找您建立的合約</span><span class="sxs-lookup"><span data-stu-id="2a04d-254">Find your created agreement</span></span>

1.  <span data-ttu-id="2a04d-255">完成設定您協議屬性，在 hello 之後**新增**刀鋒視窗中，選擇**確定**toofinish 建立您的合約和傳回 tooyour 整合帳戶 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2a04d-255">After you finish setting all your agreement properties, on hello **Add** blade, choose **OK** toofinish creating your agreement and return tooyour integration account blade.</span></span>

    <span data-ttu-id="2a04d-256">您新增的合約現在顯示於您的 [合約] 清單中。</span><span class="sxs-lookup"><span data-stu-id="2a04d-256">Your newly added agreement now appears in your **Agreements** list.</span></span>

2.  <span data-ttu-id="2a04d-257">您也可以在整合帳戶概觀中檢視您的合約。</span><span class="sxs-lookup"><span data-stu-id="2a04d-257">You can also view your agreements in your integration account overview.</span></span> <span data-ttu-id="2a04d-258">在您整合帳戶] 刀鋒視窗中，選擇 [**概觀**，然後選取 hello**協議**磚。</span><span class="sxs-lookup"><span data-stu-id="2a04d-258">On your integration account blade, choose **Overview**, then select hello **Agreements** tile.</span></span> 

    ![選擇 「 合約 」 磚 tooview 所有協議](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a><span data-ttu-id="2a04d-260">檢視 hello swagger</span><span class="sxs-lookup"><span data-stu-id="2a04d-260">View hello swagger</span></span>
<span data-ttu-id="2a04d-261">請參閱 hello [swagger 詳細資料](/connectors/as2/)。</span><span class="sxs-lookup"><span data-stu-id="2a04d-261">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2a04d-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a04d-262">Next steps</span></span>
* [<span data-ttu-id="2a04d-263">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="2a04d-263">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")  
